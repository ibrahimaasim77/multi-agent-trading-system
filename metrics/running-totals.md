# Running Totals

Auto-updated by the post-mortem agent at end of each trading day.

```yaml
system_start: 2026-06-22       # first live trading day (post-Juneteenth)
last_updated: 2026-08-10
trading_days_elapsed: 35

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
  guardrail_aborts: 62             # 6/25 m+i, 6/26 m+i, 6/29 m+i, 6/30 m+i, 7/1 m+i, 7/2 m+i, 7/6 m+i, 7/7 m+pm, 7/8 m+i, 7/9 m+i, 7/10 m+i, 7/13 m+i, 7/14 m+i, 7/15 m+i, 7/16 m+i, 7/17 m+i, 7/21 m+i, 7/22 m+i, 7/23 m+i, 7/24 m+i, 7/27 m+i, 7/28 m+i, 7/29 m+i, 7/30 m+i, 7/31 m+i, 8/3 m+i, 8/4 m+i, 8/5 m+i, 8/6 m+i, 8/7 m+i, 8/10 m+i
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
  # note (updated 2026-08-10): Day 35 elapsed (Day 31 of $0 streak since 6/25), still $0.00.
  # +2 guardrail_aborts (8/10 morning + intraday). Flat tape: SPY -0.03% ($773.26→$773.06),
  # QQQ -0.31% ($723.03→$720.81). Markets digesting 8/7 jobs-miss rally; awaiting CPI this week.
  # KEY DEVELOPMENT: INTC closed $97.54 (-4.04% from $101.65) — FIRST CLOSE BELOW $100 CAP
  # IN SYSTEM HISTORY. INTC now cap-eligible by price. TTD closed $13.38 (-3.04% from $13.80) —
  # second cap-priced evaluation candidate. COHR collapsed -14.24% ($379.13→$325.18),
  # retroactively validating the 8/7 structural stand-aside (cap 3.58×).
  # 4 stand_aside candidates today: ABNB "missed" (+3.71%; earnings beat, 1.78×cap + >15%abort),
  # TTD "avoided" (-3.04%; earnings miss, AMD-rule-analog), VRTX "missed" (+5.62%; 4.96×cap),
  # HON "correct" (-1.33%; 2.46×cap). stand_aside: 23/55 = 41.82% (from 21/51 = 41.18%).
  # 62 total guardrail aborts. SPY +3.86% since system start ($773.06 vs $744.37).
  # Day 31 MILESTONE. INTC BELOW $100. CALL ROBINHOOD SUPPORT: 1-800-279-1969. Account ●●●●9602.

decision_quality:
  win_rate_pct: null           # set after first trade
  stand_aside_correctness_pct: 41.82   # 23/55
  stand_aside_count: 55
  stand_aside_correct: 23
  stand_aside_missed: 32
  # 2026-08-10: +4 candidates (morning opportunistic scan before cash-gate abort):
  #   ABNB (est. +15%+ premarket, $178.07 prior close = 1.78× cap): EVALUATED —
  #     Q2 2026 earnings beat. >15% premarket abort rule fires. Cap 1.78× eliminates
  #     independently. Intraday peak +17.4%, close +3.71%. Scored "missed." +1 missed.
  #   TTD (est. -15%+ premarket, $13.80 prior close = within $100 cap by price):
  #     EVALUATED — Q2 2026 earnings miss (inferred from -21.9% intraday trough).
  #     AMD-rule-analog fires: negative premarket on own negative catalyst. Within cap
  #     by price but eliminated at first gate. Close -3.04%. Scored "avoided." +1 correct.
  #   VRTX (est. +5-7% premarket, $496.07 prior close = 4.96× cap): EVALUATED —
  #     biotech catalyst (FDA approval or clinical data). Cap 4.96× eliminates.
  #     Close +5.62%. Scored "missed." +1 missed.
  #   HON (est. +5-8% premarket, $246.21 prior close = 2.46× cap): EVALUATED —
  #     possible earnings or energy/industrial catalyst. Cap 2.46× eliminates.
  #     Reversed from +7.5% intraday to -1.33% close. Scored "correct." +1 correct.
  #   stand_aside: 23/55 = 41.82% (from 21/51 = 41.18%).
  # 2026-08-07: +6 candidates: COHR "missed" (+13.42%), NEM "missed" (+7.17%),
  #   AMD "correct" (-1.18%), ANET "correct" (-1.92%), INTC "correct" (+1.83%),
  #   PANW "correct" (+1.22%). stand_aside: 21/51 = 41.18% (from 17/45 = 37.78%).

benchmark:
  spy_close_at_system_start: 744.37   # captured EOD 2026-06-22 (system's first tracked day)
  spy_close_today: 773.06             # EOD 2026-08-10 (Robinhood last_trade_price at 19:59:59Z)
  spy_pct_change_since_start: +3.86   # (773.06 - 744.37) / 744.37 * 100
  system_alpha_vs_spy_pct: -103.86  # UNCONFIRMED — mechanical result of the unexplained $0 balance, not a skill signal. See financial note above.
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
