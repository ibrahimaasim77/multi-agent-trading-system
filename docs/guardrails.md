# Guardrails

The trading agents are LLMs. LLMs reason fluently and occasionally rationalize away their own rules. Every safety design choice here assumes this and adds layers that don't depend on the LLM's judgment.

## The hierarchy of trust

1. **Anything the LLM produces** — *least trusted.* Can drift, can be wrong, can rationalize.
2. **State the LLM reads from external sources** — *medium trusted.* The data itself is correct, but the LLM might misinterpret it.
3. **State the broker validates server-side** — *most trusted.* If Robinhood rejects the order, the order does not exist.

Every guardrail is anchored at the lowest trust level it can be.

## Hard caps (enforced via state derivation)

| Rule | Enforcement |
|---|---|
| Max $100 deployed per day | Compute `available_budget = $100 − sum(today's orders)` at the start of every run. Trade size = `min(tier_cap, available_budget)`. |
| Max one trade per routine | Each agent's prompt explicitly forbids a second order. Combined with the daily cap, this is double-bound. |
| Limit orders only | Prompt forbids `type=market`. Robinhood will accept market orders if the agent rebels, but the cap prevents catastrophic loss. |
| No buying after 3:30 PM ET (intraday agent) | Time check in prompt. Reading current time is a deterministic operation. |
| No trading on market holidays | First step of every routine is a web search confirming the market is open today. Juneteenth, Memorial Day, etc. are listed explicitly. |

## Whitelist (positive list)

A trade can only happen on a ticker in this set:

**Core whitelist (always eligible):**
`IWM, SPY, QQQ, NVDA, AMD, AVGO, META`

**Opportunistic whitelist (eligible IF all filters pass):**
Any stock that satisfies ALL of:
- S&P 500 OR Nasdaq 100 member
- Market cap > $5B
- Share price > $15
- Avg daily volume > 3M shares
- Up >2% pre-market (or >2% intraday for the intraday agent)
- Catalyst named, concrete, from last 24h
- Catalyst language is NOT "rumor", "speculation", "reportedly", "WSB", "short squeeze"

## Blacklist (negative list, absolute)

A trade can never happen on a ticker in any of these categories — regardless of catalyst strength, regardless of agent confidence:

- **Meme history:** GME, AMC, BBBY, MULN, NKLA, any historical short-squeeze name
- **Fresh IPOs:** anything IPO'd in the last 6 months (illiquidity + post-lockup risk)
- **Sub-$15 stocks:** penny-stock-adjacent volatility
- **Biotech under $20B market cap:** binary FDA risk
- **Recently halted sectors:** anything with circuit-breaker history this week
- **Crypto proxies on volatile days:** MSTR, COIN on days BTC moves >5%

## Abort triggers (in addition to the above)

Even on a whitelisted ticker with a passing catalyst, an agent will abort if:

| Condition | Why |
|---|---|
| VIX > 28 (morning) / >30 (intraday) | Regime uncertainty; rules calibrated for normal vol |
| Account cash < $50 | Cap precision degrades; not worth deploying |
| Pre-market move > 15% on the chosen ticker | Chasing blow-off tops kills small accounts |
| Intraday move > 12% on the chosen ticker | Same reason, later in day |
| Any "unconfirmed" / "rumor" / "reportedly" in primary catalyst | Catalyst is not actually known |
| Routine ambiguity ("if you find yourself arguing for an exception") | Meta-rule: argumentation = signal to stop |

## Tone calibration

The agents are explicitly instructed to be **moderately aggressive, not maximally cautious**. A 60–70% confidence trade with a named catalyst and passing filters is worth taking at this position size. Standing aside from every uncertainty defeats the purpose of the system.

The $100 daily cap is what makes "edgy" safe. With strict caps in place, false positives cost at most $100. Without strict caps, you'd want a more cautious agent. We chose the former.

## What is deliberately NOT a guardrail

- **No stop-losses.** Stops can fire on a flash dip then never recover. Hard daily cap is simpler and bounds losses better at this size.
- **No fundamental analysis required.** Agents don't read 10-Ks. Catalysts are surfaced by web search; valuation is implicit in the whitelist's bias toward large-cap quality.
- **No portfolio rebalancing.** This system places single tickets. Existing positions are tracked but not actively managed by these agents.
- **No selling.** Agents are buy-only. Exits are manual or via a future agent.

## Failure of guardrails: what would have to happen

For the system to lose more than $100 in a day, every layer would have to fail simultaneously:

1. The LLM ignores all "NEVER >$100" instructions in the prompt
2. The LLM ignores the `available_budget` it computed from `get_equity_orders`
3. Robinhood accepts an order that should be rejected
4. The user fails to cancel the order in the ~5.5 hours between fill and market close

This is implausible but not zero. It's why we say the system is "safe-enough" for $100/day stakes, not "safe" for unlimited stakes. The dollar cap is the actual floor.
