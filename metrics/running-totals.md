# Running Totals

Auto-updated by the post-mortem agent at end of each trading day.

```yaml
system_start: 2026-06-22       # first live trading day (post-Juneteenth)
last_updated: 2026-07-08
trading_days_elapsed: 12

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
  guardrail_aborts: 18             # 6/25 m+i, 6/26 m+i, 6/29 m+i, 6/30 m+i, 7/1 m+i, 7/2 m+i, 7/6 m+i, 7/7 m+pm, 7/8 m+i
  # note (updated 2026-07-02): account 912269602 (Agentic, ••••9602) has now
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
  # note (updated 2026-07-06): Day 10 elapsed, still $0.00. +2 guardrail_aborts
  # (7/6 morning + intraday). No new stand-aside candidates — both routines
  # aborted at Step 1 before any ticker evaluation.
  # note (updated 2026-07-07): Day 11 elapsed (Day 8 of $0 streak), still $0.00.
  # +2 guardrail_aborts (7/7 morning + post-mortem). Global semi rout today:
  # SMH -3.84%, AMD -6.43% (Samsung quarterly miss + DeepSeek AI-chip narrative).
  # Correct stand-aside even hypothetically — no CORE long setup premarket.
  # META +2.55%, NVDA +0.71% bucked the rout. No new stand-aside candidates —
  # cash gate aborted before any ticker evaluation. Stand-aside stats unchanged.
  # note (updated 2026-07-08): Day 12 elapsed (Day 9 of $0 streak), still $0.00.
  # +2 guardrail_aborts (7/8 morning hard-abort + intraday cash-gate block).
  # Intraday agent ran full watchlist scan and identified AVGO as Tier 1
  # candidate (Apple-Broadcom $30B+ multiyear partnership announced at open;
  # AVGO closed +4.82% vs prior close $370.78 → $388.67). Trade doubly blocked:
  # no cash AND AVGO price ($387+) > $100 per-trade cap. Counted as 1 new
  # "missed" stand-aside candidate. Email escalation at Day 9 — direct user
  # phone call to Robinhood Support required.

decision_quality:
  win_rate_pct: null           # set after first trade
  stand_aside_correctness_pct: 36.84
  stand_aside_count: 19
  stand_aside_correct: 7
  stand_aside_missed: 12
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
  # judgment failure. See trades/2026-06-25.md for full context.)
  # 6/26, 6/29, and 6/30 added no stand-aside candidates (cash gate aborted
  # before any ticker was evaluated on all three days).
  # 2026-07-01 added 1: META (morning + intraday) → closed +8.81%, scored
  # "missed." NOTE: META at $627/share exceeds the $100 single-trade cap for
  # whole shares — this was doubly structural (no cash AND price > cap); even
  # with cash restored, META cannot be traded under current rules. Counted as
  # "missed" per the close-change rule for completeness; not a judgment error.
  # 2026-07-06: no new candidates — both routines aborted at cash gate before
  # any ticker was evaluated. stand_aside_count unchanged at 18.
  # 2026-07-07: no new formal candidates — cash gate aborted before any ticker
  # evaluation. META ended +2.55% (above "missed" threshold) but only showed
  # +0.44% premarket and never cleared the 2% premarket trigger that initiates
  # formal candidate creation. Not counted. Metrics unchanged at 18/7/11.
  # 2026-07-08: +1 candidate: AVGO (intraday). Apple-Broadcom $30B+ partnership
  # announced at open; AVGO closed +4.82% vs prior close of $370.78 → $388.67.
  # Scored "missed" (>+2% threshold). Doubly structural blocker: no cash AND
  # AVGO price ($387+) > $100 per-trade cap. stand_aside_count: 19,
  # stand_aside_missed: 12, stand_aside_correctness_pct: 7/19 = 36.84.

benchmark:
  spy_close_at_system_start: 744.37   # captured EOD 2026-06-22 (system's first tracked day)
  spy_close_today: 745.34             # EOD 2026-07-08
  spy_pct_change_since_start: +0.13   # (745.34 - 744.37) / 744.37 * 100
  system_alpha_vs_spy_pct: -100.13   # UNCONFIRMED — mechanical result of the unexplained $0 balance, not a skill signal. See financial note above.
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
