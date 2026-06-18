# Architecture Decision Records

Each entry documents a non-obvious design choice and why it was made.

## ADR-001: Three agents instead of one

**Decision:** Split the trading workflow into three separate scheduled agents (pre-market, intraday, post-mortem) rather than a single long-running agent.

**Context:** A single agent would need to handle pre-market analysis, mid-day re-evaluation, end-of-day post-mortem, and overnight state persistence — all in one prompt or one long session.

**Why split:**
- Each agent has a focused success criterion, easier to evaluate
- Failure of one agent doesn't take down the others
- Schedule-driven invocation maps cleanly to discrete decisions (open vs. mid-day vs. close)
- Each prompt is small enough to iterate on without breaking the others
- LLM context-window pressure is lower per agent

**Tradeoff accepted:** Coordination becomes a real engineering problem (handled via the brokerage's order log as a shared bus).

---

## ADR-002: GitHub repo as state, not a database

**Decision:** Persistent state (daily journals, running metrics) lives as Markdown files in this repo, not in Postgres / Supabase / DynamoDB.

**Context:** Standard advice is "use a real database for structured data."

**Why GitHub:**
- Zero ops cost — no provisioning, no migrations, no credentials
- Version-controlled by default — every state change is auditable
- Human-readable — debugging means opening a `.md` file, not a SQL client
- Already attached to every routine as a source — no new MCP needed
- Obsidian / any Markdown editor reads it natively for a "dashboard"

**Tradeoff accepted:** No queries. To compute "average return on QQQ trades over last 6 weeks," you read all the files and reduce. At current volume (one entry per trading day), this is irrelevant. At scale it would matter.

**When this stops being right:** If the journal grows past ~500 files (~2 years), the next-morning agent's context window starts to feel it. At that point, summarize into a rolling 90-day window.

---

## ADR-003: Limit orders only, no market orders

**Decision:** All orders are limit. Market orders are forbidden.

**Context:** Market orders fill faster and more reliably. Limit orders can sit unfilled if the price moves away.

**Why limit only:**
- Small accounts are slippage-sensitive. A $0.05 slippage on a $100 trade is 0.05% of the position — material.
- Market orders during news events can fill at wildly off-quote prices
- Limit orders at the current ask are still highly fillable for our liquid whitelist
- GFD (good-for-day) means an unfilled limit cancels at close — no overnight surprise

**Tradeoff accepted:** Some real catalysts will go un-traded because the price runs away. At small position sizes this is preferable to chasing.

---

## ADR-004: Hard daily cap instead of per-trade stops

**Decision:** Risk is bounded by a $100/day total deploy cap, not by per-trade stop-loss orders.

**Context:** Most retail trading advice mandates stop-losses.

**Why cap:**
- Stops can fire on flash dips then never re-enter — pure cost
- Stops are themselves orders; in CCR's scheduled-fire model, managing stops means adding another agent
- A hard cap upstream of the trade is enforced before any order is placed — fundamentally simpler
- At $100/day, worst case is $100/day. The math is clean.

**Tradeoff accepted:** A single trade *can* lose up to its full size. We accept this and bound the total.

---

## ADR-005: Calendar push notifications, not email or Slack

**Decision:** Primary user notification is a Google Calendar event with a popup reminder. Email is secondary (draft only). Slack was considered and skipped.

**Context:** Three channels evaluated:
1. Gmail send — would push but the available connector only exposes `create_draft`
2. Slack — would push reliably but requires adding a new connector
3. Google Calendar event with reminder — already authorized, pushes natively

**Why Calendar:**
- Already-authorized connector. Zero new setup.
- Phone Calendar app push notifications are reliable across iOS/Android
- Event title carries the decision summary — readable at-a-glance from lock screen
- Event description carries the full reasoning for when the user wants depth
- AVAILABILITY_FREE means it doesn't pollute the calendar visually

**Tradeoff accepted:** Calendar isn't designed for transient notifications, so events accumulate. Mitigated by setting them to AVAILABILITY_FREE and accepting visual clutter.

---

## ADR-006: Cloud-only execution, no local components

**Decision:** Every part of the system runs on Anthropic infrastructure (CCR). No local servers, no daemons on the user's machine.

**Context:** Could have built this as a local Python service with cron, or hybrid (local for sensitive ops, cloud for orchestration).

**Why cloud-only:**
- Runs whether the user's laptop is on, off, or in a different timezone
- No local credentials to leak — Robinhood/Gmail/Calendar auth is in the user's claude.ai account
- Recoverable from anywhere — open https://claude.ai/code on any device
- Zero infra cost for a project of this scope
- Forces the design to be stateless and idempotent, which is good discipline

**Tradeoff accepted:** Bound to Anthropic's roadmap and pricing. If CCR pricing changes materially, this becomes a different system.

---

## ADR-007: Loosened filters for "edginess"

**Decision:** Filter thresholds (market cap, share price, premarket move, VIX abort) were deliberately loosened from initial conservative values.

**Context:** The first version of the prompt was tuned to almost always stand aside.

**Why loosen:**
- The $100 cap makes false positives cheap
- Standing aside every day is the same as not running the system
- A 60–70% confidence trade is the actual sweet spot for active equity trading
- Tightening can come later if results show too many false positives

**Tradeoff accepted:** Higher absolute number of trades, higher absolute number of small losses. Net P&L is the only thing that matters; trade count is a process metric.
