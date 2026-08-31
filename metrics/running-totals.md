# Running Totals

Auto-updated by the post-mortem agent at end of each trading day.

```yaml
system_start: 2026-06-22       # first live trading day (post-Juneteenth)
last_updated: 2026-08-31
trading_days_elapsed: 50

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
  guardrail_aborts: 92             # 90 confirmed through 8/28; +2 today (8/31 morning + intraday) = 92 total
  # note (updated 2026-08-31): Day 50 elapsed (Day 47 of $0 streak since 6/25), still $0.00.
  # +2 guardrail aborts (8/31 morning + intraday) → 92 total. SPY closed $766.95 (-0.31%
  # from $769.35). RISK-OFF: Iran-Hormuz escalation (US struck Iranian rocket launchers on
  # Larak Island, Sunday 8/30; Iran retaliated). Brent >$90/bbl. Dow -0.9%; S&P -0.33%;
  # QQQ +0.06% (tech resilient). Both routines ran and produced Gmail drafts.
  # Two stand-aside candidates: SMCI correct (+0.54%, premarket -1.67% Gate 5 fail; AVGO
  # -0.93% PM chip gate FAIL; no SMCI-specific catalyst; post-Warsh consolidation; flat zone);
  # AMD correct (+0.94%, premarket -0.19% Gate 5 fail; structural block — 3-session
  # underperformance streak; Raymond James upgrade 5 trading days old/stale). Even with
  # capital restored, no valid trade existed today — no Gate-5 pass, chip gate negative.
  # END OF AUGUST: SPY +3.03% since system start. 0 trades placed in 50 trading days.
  # Stand-aside: 46/88 = 52.27% — NEW ALL-TIME HIGH (+1.11 ppts). Daily score: 65.
  # Next binary event: September 16 FOMC (40% probability 25bp rate hike).
  # Call Robinhood Support: 1-800-279-1969. Account ●●●●9602. September 1 is a business day.

decision_quality:
  win_rate_pct: null           # set after first trade
  stand_aside_correctness_pct: 52.27   # 46/88 — NEW ALL-TIME HIGH; SMCI correct +0.54%, AMD correct +0.94%
  stand_aside_count: 88
  stand_aside_correct: 46
  # 2026-08-31: +2 candidates (Iran-Hormuz escalation; post-Warsh consolidation; risk-off):
  #   SMCI: close $37.28 = +0.54%. Scored "correct." +1/+1. Premarket -1.67% Gate 5 fail;
  #         AVGO -0.93% PM chip gate FAIL; no new SMCI catalyst; flat zone.
  #   AMD: close $469.95 = +0.94%. Scored "correct." +1/+1. Premarket -0.19% Gate 5 fail;
  #         structural 3-session underperformance block; stale catalyst (5 trading days old).
  #   stand_aside: 46/88 = 52.27%. NEW ALL-TIME HIGH (+1.11 ppts). Clean 2/2 sweep.

benchmark:
  spy_close_at_system_start: 744.37
  spy_close_today: 766.95             # EOD 2026-08-31; SPY -0.31% (Iran-Hormuz escalation; risk-off)
  spy_pct_change_since_start: +3.03   # (766.95 - 744.37) / 744.37 * 100; END OF AUGUST
  system_alpha_vs_spy_pct: -103.03  # UNCONFIRMED — mechanical result of the unexplained $0 balance
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
