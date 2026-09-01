# Running Totals

Auto-updated by the post-mortem agent at end of each trading day.

```yaml
system_start: 2026-06-22       # first live trading day (post-Juneteenth)
last_updated: 2026-09-01
trading_days_elapsed: 51

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
  guardrail_aborts: 94             # 92 through 8/31; +2 today (9/1 morning #93 + intraday #94) = 94 total
  # note (updated 2026-09-01): Day 51 elapsed (Day 48 of $0 streak since 6/25), still $0.00.
  # +2 guardrail aborts (9/1 morning + intraday) → 94 total. SPY closed $761.65 (-0.70%
  # from $767.05). RISK-OFF: Inflation worries + elevated oil (Brent >$90/bbl; Iran-Hormuz
  # ongoing) lifting bond yields; FOMC September 16 overhang (40% probability 25bp hike per
  # Warsh hawkish Jackson Hole signal). Dow -0.79%; S&P -0.71%; Nasdaq -1.03%; QQQ -1.27%.
  # Both routines ran and produced Gmail drafts. Two stand-aside candidates:
  # SMCI correct (-1.50%, premarket -2.44% Gate 5 fail; AVGO -1.47% PM chip gate FAIL;
  # no SMCI-specific catalyst; September risk-off tape);
  # AMD avoided (-2.33%, premarket -2.07% Gate 5 fail; structural block — 5-session
  # underperformance streak; Raymond James upgrade 5 trading days old/stale). Even with
  # capital restored, no valid trade existed today — no Gate-5 pass, chip gate negative.
  # Stand-aside: 48/90 = 53.33% — NEW ALL-TIME HIGH (+1.06 ppts). Daily score: 70.
  # Next binary event: September 16 FOMC (40% probability 25bp rate hike; 10 trading days).
  # Call Robinhood Support: 1-800-279-1969. Account ●●●●9602. September 2 is a business day.

decision_quality:
  win_rate_pct: null           # set after first trade
  stand_aside_correctness_pct: 53.33   # 48/90 — NEW ALL-TIME HIGH; SMCI correct -1.50%, AMD avoided -2.33%
  stand_aside_count: 90
  stand_aside_correct: 48
  # 2026-09-01: +2 candidates (September risk-off; inflation+oil+yields; FOMC overhang):
  #   SMCI: close $36.72 = -1.50%. Scored "correct." +1/+1. Premarket -2.44% Gate 5 fail;
  #         AVGO -1.47% PM chip gate FAIL; no new SMCI catalyst; September risk-off tape.
  #   AMD: close $459.75 = -2.33%. Scored "avoided." +1/+1. Premarket -2.07% Gate 5 fail;
  #         structural 5-session underperformance block; stale catalyst (5 trading days old).
  #         AMD led the tape lower today, down -2.33% vs QQQ -1.27%. Pattern accelerating.
  #   stand_aside: 48/90 = 53.33%. NEW ALL-TIME HIGH (+1.06 ppts). Clean 2/2 sweep.

benchmark:
  spy_close_at_system_start: 744.37
  spy_close_today: 761.65             # EOD 2026-09-01; SPY -0.70% (inflation + oil + yields; risk-off)
  spy_pct_change_since_start: +2.32   # (761.65 - 744.37) / 744.37 * 100
  system_alpha_vs_spy_pct: -102.32  # UNCONFIRMED — mechanical result of the unexplained $0 balance
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
