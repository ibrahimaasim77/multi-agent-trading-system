# Running Totals

Auto-updated by the post-mortem agent at end of each trading day.

```yaml
system_start: 2026-06-22       # first live trading day (post-Juneteenth)
last_updated: 2026-06-24
trading_days_elapsed: 3

trades:
  total: 0
  wins: 0
  losses: 0
  scratches: 0
  unfilled: 0

financial:
  starting_cash_usd: 217.19
  current_account_value_usd: 217.19
  total_pnl_dollars: 0.00
  total_pnl_pct: 0.00
  avg_daily_deploy_usd: 0.00
  guardrail_aborts: 0

decision_quality:
  win_rate_pct: null           # set after first trade
  stand_aside_correctness_pct: 43.75
  stand_aside_count: 16
  stand_aside_correct: 7
  stand_aside_missed: 9
  # note (corrected 2026-06-24): the 2026-06-23 journal claimed zero stand-aside
  # records existed due to a Gmail search bug (search_threads excludes drafts by
  # default; both routines deliver via create_draft per ADR-005). list_drafts on
  # 2026-06-24 confirmed 2026-06-23 DID produce full morning + intraday writeups
  # (IBM, SMCI, VRNS, VKTX, QNT, INFQ, MU/SNDK/WDC premarket-data conflict).
  # NOT yet backfilled into the counts above pending a full re-score of that
  # day's candidates against settle prices — flagged as a follow-up for the next
  # post-mortem run. Counts above include only 2026-06-22 (9, 2 correct) +
  # 2026-06-24 (7, 5 correct).

benchmark:
  spy_close_at_system_start: 744.37   # captured EOD 2026-06-22 (system's first tracked day)
  spy_close_today: 733.07
  spy_pct_change_since_start: -1.52
  system_alpha_vs_spy_pct: 1.52      # system_pct - spy_pct (flat account vs down SPY; not a skill signal — no trades were made to compare)
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

No history is kept here — only running totals. For per-day detail, see `../trades/`.
