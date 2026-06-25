# Running Totals

Auto-updated by the post-mortem agent at end of each trading day.

```yaml
system_start: 2026-06-22       # first live trading day (post-Juneteenth)
last_updated: 2026-06-25
trading_days_elapsed: 4

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
  guardrail_aborts: 2              # both 6/25 routines (morning + intraday) hard-aborted on cash < $50
  # note (added 2026-06-25): account 912269602 (Agentic, ••••9602) showed
  # $0.00 total_value / $0.00 cash on 2026-06-25, down from $217.19 cash_close
  # recorded in the 2026-06-24 journal, with ZERO trades placed in between and
  # ZERO orders ever recorded on this account (checked across all time). Both
  # today's morning and intraday routines independently hit this and stood
  # aside. Re-queried get_portfolio twice — not a transient glitch. No order,
  # transfer, or withdrawal record is visible to any agent that explains the
  # gap. This could be an unauthorized withdrawal, an ACH sweep, or a
  # portfolio-endpoint data bug — cannot be determined from inside this
  # system. The pnl/account-value fields above are computed mechanically from
  # the reported $0.00 and should be treated as UNCONFIRMED until the user
  # verifies actual transfer/balance history in the Robinhood app directly.
  # Do not treat -100% as a performance verdict on the trading logic — no
  # trades have ever been placed on this account (trades.total: 0 throughout).

decision_quality:
  win_rate_pct: null           # set after first trade
  stand_aside_correctness_pct: 41.18
  stand_aside_count: 17
  stand_aside_correct: 7
  stand_aside_missed: 10
  # note (corrected 2026-06-24): the 2026-06-23 journal claimed zero stand-aside
  # records existed due to a Gmail search bug (search_threads excludes drafts by
  # default; both routines deliver via create_draft per ADR-005). list_drafts on
  # 2026-06-24 confirmed 2026-06-23 DID produce full morning + intraday writeups
  # (IBM, SMCI, VRNS, VKTX, QNT, INFQ, MU/SNDK/WDC premarket-data conflict).
  # NOT yet backfilled into the counts above pending a full re-score of that
  # day's candidates against settle prices — still flagged as a follow-up for
  # a future post-mortem run. Counts above include 2026-06-22 (9, 2 correct) +
  # 2026-06-24 (7, 5 correct) + 2026-06-25 (1, 0 correct: MU +15.74%, scored
  # "missed" by the close-change rule, but it was a forced miss caused by the
  # $0 cash gate blocking trade selection before catalyst screening — not a
  # judgment failure. See trades/2026-06-25.md for full context.

benchmark:
  spy_close_at_system_start: 744.37   # captured EOD 2026-06-22 (system's first tracked day)
  spy_close_today: 733.26
  spy_pct_change_since_start: -1.49
  system_alpha_vs_spy_pct: -98.51    # UNCONFIRMED — mechanical result of the unexplained $0 balance, not a skill signal. See financial note above.
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
