# Architecture

## Execution model

All three agents run on **Claude Code Remote (CCR)** — Anthropic's managed environment for scheduled Claude agents. Each fire spawns a fresh, isolated session that:

1. Receives the prompt stored in the routine config
2. Clones the source repository (this one)
3. Connects to attached MCP servers (Robinhood, Gmail, Google Calendar)
4. Executes the prompt to completion
5. Terminates — no persistent process

There is **no shared memory between runs**. Coordination happens through observable state: the brokerage's order history and the journal files in this repository.

## Why no shared memory was a feature, not a bug

A naive design would have a long-running orchestrator process that holds state in memory and dispatches sub-agents. Instead, each agent rehydrates state from external sources every run. Benefits:

- **Crash-safe** — if a run dies mid-execution, the next scheduled run sees the same state and proceeds correctly
- **Idempotent** — re-running a routine for a given day produces the same decision given the same inputs
- **Auditable** — every state transition is visible in Robinhood's order log + this repo's git history
- **No infra** — no servers, no Redis, no message bus

## The three agents

### Morning agent (`agents/morning.md`)

- Fires 8:30 AM ET weekdays (1 hour before market open)
- Inputs: account state, last 14 days of journal entries, overnight news, futures, watchlist quotes
- Output: one trade decision (placed limit order) or stand-aside, written to today's journal stub
- Time budget: ~3–8 minutes per fire

### Intraday agent (`agents/intraday.md`)

- Fires 11:00 AM ET weekdays (90 minutes after open)
- Inputs: morning agent's decision and any resulting fills, post-open price action, intraday news
- Output: a second decision if a *new* catalyst has emerged since open; otherwise stand aside
- Key coordination point: reads `get_equity_orders` to compute remaining daily budget AND avoid duplicating a morning ticker
- Time budget: ~3–6 minutes

### Post-mortem agent (`agents/postmortem.md`)

- Fires 4:30 PM ET weekdays (30 minutes after close)
- Inputs: today's orders + fills, end-of-day prices, what each "stand aside" candidate actually did
- Output: a structured journal entry committed to `trades/YYYY-MM-DD.md` and an update to `metrics/running-totals.md`
- This is the learning loop — tomorrow's morning agent reads these

## Coordination protocol

The two morning-time agents coordinate through `get_equity_orders`, not by talking to each other.

```
[Morning fires at 8:30 ET]
  → reads get_equity_orders(today)
  → sees empty list
  → decides + places trade ($24 of QQQ)

[Intraday fires at 11:00 ET]
  → reads get_equity_orders(today)
  → sees morning's order ($24 QQQ)
  → computes available_budget = $100 - $24 = $76
  → tier_cap for new trade reduced to min(tier_cap, $76)
  → if intraday picks QQQ also: refuses (same ticker rule)

[Post-mortem fires at 16:30 ET]
  → reads all orders + final prices
  → writes journal
```

This works because the brokerage's order log is the source of truth — both agents read the same thing, and neither can "miss" the other's actions.

## Safety architecture

Safety is enforced at three independent layers. An LLM drift that bypasses layer 1 still hits layers 2 and 3.

**Layer 1 — Prompt-level rules**
- Explicit "NEVER" non-negotiables in the prompt
- Whitelist + blacklist with hard semantics ("regardless of catalyst")
- Meta-rule: "if you find yourself arguing for an exception, stand aside"

**Layer 2 — State-derived checks**
- Read account state before every trade decision
- Compute available budget from actual order history (not from a counter the LLM tracks)
- Compare proposed trade size against current cash + already-committed dollar exposure

**Layer 3 — Brokerage-side validation**
- `review_equity_order` returns alerts (PDT, halts, insufficient buying power, restricted instruments)
- Robinhood's server rejects orders that violate account rules (no margin trading, no options on this account level)
- `agentic_allowed=false` accounts physically cannot be traded by any agent, regardless of prompt

Layer 3 is the only one that's truly bulletproof — it's outside the LLM. Layers 1 and 2 are defense in depth.

## Notification path

Email cannot be the primary notification channel because the available Gmail MCP only exposes `create_draft`, not `send`. Drafts sit in Drafts folder and do not push.

**Solution:** Google Calendar create_event with a popup reminder at 0 minutes before event start. Phone Calendar app fires a native push notification reliably across iOS and Android. Title carries the decision summary; description carries the full reasoning.

```
[Agent decides BUY $24 QQQ]
  → Gmail create_draft (full reasoning, lives in Drafts)
  → Calendar create_event (title: "Trade Placed - BUY $24 QQQ", time: 9:25 AM ET, reminder: 0 min)
  → Phone buzzes at 9:25 AM
  → User taps notification, sees summary, opens Gmail Drafts for full reasoning
```

## Schedule timezone strategy

Cron expressions are **fixed UTC**. The local fire time drifts by one hour at DST transitions. This is intentional — the alternative (re-coding the cron twice a year) is error-prone. The DST drift is logged in the project notes and is acceptable for this use case since the market also follows local clock changes.

## Failure modes and recovery

| Failure | What happens | Recovery |
|---|---|---|
| LLM API rate limit | Routine fails, no trade placed | Next scheduled fire proceeds normally |
| Robinhood MCP unreachable | Routine reports the error in email | Manual trade in app if catalyst still valid |
| Gmail MCP fails | Calendar notification still fires | User checks routine page on claude.ai |
| Calendar MCP fails | Email draft still created | User checks email inbox |
| Order rejected by Robinhood | Agent emails the rejection reason | User adjusts (e.g., wait for market hours) |
| Cron infrastructure outage | Run is missed entirely | Next day proceeds normally; no catch-up |

The system is designed to fail-soft. A missed day is better than an incorrect day.
