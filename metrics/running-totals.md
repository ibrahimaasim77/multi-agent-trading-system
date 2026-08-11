# Running Totals

Auto-updated by the post-mortem agent at end of each trading day.

```yaml
system_start: 2026-06-22       # first live trading day (post-Juneteenth)
last_updated: 2026-08-11
trading_days_elapsed: 36

trades:
  total: 0
  wins: 0
  losses: 0
  scratches: 0
  unfilled: 0

financial:
  starting_cash_usd: 217.19
  current_account_value_usd: 0.00   # UNCONFIRMED — see note below, not a confirmed trading loss
  total_pnl_dollars: -217.19        # UNCONFIRMED — see note below
  total_pnl_pct: -100.00           # UNCONFIRMED — see note below
  avg_daily_deploy_usd: 0.00
  guardrail_aborts: 64             # 6/25 m+i, 6/26 m+i, 6/29 m+i, 6/30 m+i, 7/1 m+i, 7/2 m+i, 7/6 m+i, 7/7 m+pm, 7/8 m+i, 7/9 m+i, 7/10 m+i, 7/13 m+i, 7/14 m+i, 7/15 m+i, 7/16 m+i, 7/17 m+i, 7/21 m+i, 7/22 m+i, 7/23 m+i, 7/24 m+i, 7/27 m+i, 7/28 m+i, 7/29 m+i, 7/30 m+i, 7/31 m+i, 8/3 m+i, 8/4 m+i, 8/5 m+i, 8/6 m+i, 8/7 m+i, 8/10 m+i, 8/11 m+i
  # note (updated 2026-07-02): account 912269602 (Agentic, ●●●●9602) has now
  # shown $0.00 total_value / $0.00 cash for SIX consecutive trading days
  # (6/25, 6/26, 6/29, 6/30, 7/1, 7/2), down from $217.19 cash_close recorded
  # in the 2026-06-24 journal, with ZERO trades placed and ZERO orders ever
  # recorded on this account (checked across all time). Twelve independent live
  # get_portfolio queries across six trading days (morning + intraday each
  # day) and three full weekends have all returned identically $0.00.
  # No order, transfer, or withdrawal record is visible to any agent that
  # explains the drop from $217.19 to $0.00. This is a CONFIRMED, PERSISTENT
  # capital-layer failure — not a provisional anomaly. Could be an unauthorized
  # withdrawal, an ACH sweep, or a portfolio-endpoint data bug — cannot be
  # determined from inside this system. The pnl/account-value fields above are
  # computed mechanically from the reported $0.00 and should be treated as
  # UNCONFIRMED until the user verifies actual transfer/balance history in the
  # Robinhood app directly. Do not treat -100% as a performance verdict on the
  # trading logic — no trades have ever been placed on this account
  # (trades.total: 0 throughout).
  # note (updated 2026-08-11): Day 36 elapsed (Day 33 of $0 streak since 6/25), still $0.00.
  # +2 guardrail_aborts (8/11 morning + intraday). SPY closed $770.45 (-0.33% from $773.03).
  # Pre-CPI caution; US-Iran/Strait of Hormuz drag. PERFECT STAND-ASIDE DAY: 4/4 correct
  # (INTC +0.19%, COHR +1.05%, PANW -0.29%, TTD +1.19% — all within flat zone).
  # Stand-aside correctness: 27/59 = 45.76% (new system high, from 41.82%).
  # INTC in second consecutive sub-$100 session ($97.705 close). CPI releases 8/12 8:30 AM ET.
  # 64 total guardrail aborts. Call Robinhood Support: 1-800-279-1969. Account ●●●●9602.

decision_quality:
  win_rate_pct: null           # set after first trade
  stand_aside_correctness_pct: 45.76   # 27/59
  stand_aside_count: 59
  stand_aside_correct: 27
  stand_aside_missed: 32
  # 2026-08-11: +4 candidates (morning evaluation before cash-gate abort):
  #   INTC (premarket -0.51%, $97.02; no named catalyst last 24h; AMD-rule-adjacent):
  #     Negative premarket → hard elimination. Cap $97.02 < $100 (technically eligible by
  #     price but eliminated on premarket gate). Close $97.705 = +0.19% from prior $97.52.
  #     Scored "correct." +1 correct.
  #   COHR (premarket -0.20%, $324.50; cap 3.25×; do-not-evaluate flag):
  #     Negative premarket + cap + flag → triple elimination. Close $328.58 = +1.05% from
  #     prior $325.15 (dead-cat bounce after 8/10 -14.24%). Scored "correct." +1 correct.
  #   PANW (premarket -0.12%, $384.57; cap 3.85×):
  #     Negative premarket + cap → eliminated. Close $383.93 = -0.29% from prior $385.04.
  #     Scored "correct." +1 correct.
  #   TTD (premarket -0.82%, $13.28; post-earnings Day 2; AMD-rule-analog):
  #     Negative premarket + consolidation window Day 2 → eliminated. Close $13.55 =
  #     +1.19% from prior $13.39. Scored "correct." +1 correct.
  #   stand_aside: 27/59 = 45.76% (from 23/55 = 41.82%). NEW SYSTEM HIGH. 4/4 correct.

benchmark:
  spy_close_at_system_start: 744.37   # captured EOD 2026-06-22 (system's first tracked day)
  spy_close_today: 770.45             # EOD 2026-08-11 (Robinhood last_trade_price at 19:59:59Z)
  spy_pct_change_since_start: +3.50   # (770.45 - 744.37) / 744.37 * 100
  system_alpha_vs_spy_pct: -103.50  # UNCONFIRMED — mechanical result of the unexplained $0 balance, not a skill signal. See financial note above.
```

## Reading the table

- **win_rate_pct** = wins / (wins + losses). Null until first non-scratch trade.
- **stand_aside_correctness_pct** = stand_aside_correct / stand_aside_count. Skipping a flat ticker = correct. Skipping a +5% ticker = missed.
- **system_alpha_vs_spy_pct** = total system return − SPY return over the same window. Positive means the system is beating buy-and-hold SPY.
- **guardrail_aborts** counts the number of times a hard rule (cap exceeded, blacklist, halt detected) prevented a trade. These are protective wins, not losses.

## How the post-mortem updates this

After computing today's numbers, the post-mortem agent:
1. Reads this file
2. Updates each numeric field
3. Commits the change with the daily journal

No history is kept here — only running totals. For per-day detail, see `../trades/`
