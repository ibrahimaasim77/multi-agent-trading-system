# Running Totals

Auto-updated by the post-mortem agent at end of each trading day.

```yaml
system_start: 2026-06-22       # first live trading day (post-Juneteenth)
last_updated: 2026-09-04
trading_days_elapsed: 54

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
  guardrail_aborts: 100            # 98 through 9/3; +2 today (9/4 morning #99 + intraday #100) = 100 ROUND-NUMBER MILESTONE
  # note (updated 2026-09-04): Day 54 elapsed (Day 51 of $0 streak). 100 GUARDRAIL ABORTS — landmark.
  # Two Gmail drafts found (draft anomaly resolved; no 5th no-draft anomaly). NFP day (first Friday
  # of September — employment report at 8:30 AM ET). Morning routine incorrectly noted "No major US
  # data scheduled." Protocol gap identified: add NFP/CPI/FOMC calendar check to morning routine.
  # SPY -0.38% ($770.23 vs $773.17). QQQ +0.19%. AI infrastructure surged: AMD +4.67% ($477.45),
  # SMCI +4.55% ($39.59). DDOG +6.08% premarket → -0.84% close (gap-and-fade, no catalyst).
  # AMD: Gate 5 FAIL (+0.86% PM) + structural block → MISSED (+4.67%). NFP macro rotation.
  # SMCI: AVGO gate NEUTRAL (+0.20%); premarket not checked → MISSED (+4.55%). Protocol gap.
  # DDOG: opportunistic, no catalyst → correct (-0.84%). Stand-aside: 53/99 = 53.54%.
  # Daily score: 50. Call Robinhood Support: 1-800-279-1969. Account ●●●●9602. 100 ABORTS.
  # FOMC September 16 now 8 trading days away. Labor Day Monday 9/7 — market CLOSED.
  # Next trading day: Tuesday September 8, 2026.

decision_quality:
  win_rate_pct: null           # set after first trade
  stand_aside_correctness_pct: 53.54   # 53/99; pullback from 54.64% (9/3); two misses today (AMD, SMCI)
  stand_aside_count: 99
  stand_aside_correct: 53
  # 2026-09-04: +3 candidates (NFP day; AI infrastructure surge; jobs-report rotation):
  #   AMD: close $477.45 = +4.67%. Scored "MISSED." Gate 5 FAIL (+0.86% PM < +2%) + structural
  #         block (7+ sessions underperforming QQQ). NFP macro rotation drove intraday surge.
  #         Block remains active — one macro-driven day does not reset structural underperformance.
  #   SMCI: close $39.59 = +4.55%. Scored "MISSED." AVGO gate NEUTRAL; morning routine did not
  #         check SMCI premarket (protocol gap). Third consecutive week of SMCI miss. Gate carve-out
  #         protocol revision now urgent: always check SMCI premarket when AVGO gate ≥ -1%.
  #   DDOG: close $212.95 = -0.84%. Scored "correct." PM +6.08% with no named catalyst → faded.
  #         Consistent with CRWD (9/2: -5.42%) and CRM (9/2: -0.36%) gap-and-fade pattern.
  #   stand_aside: 53/99 = 53.54% (pullback; two misses AMD+SMCI; DDOG correct partially offsets).
  # 2026-09-03: +2 reconstructed candidates (no Gmail draft found — 4th no-draft anomaly):
  #   AMD: close $456.24 = -0.18%. Scored "correct." Structural block; 7th consecutive session
  #         underperforming chip complex. AMD -0.18% vs QQQ +1.18% (-136bps vs tape).
  #   SMCI: close $37.87 = +2.35%. Scored "MISSED." AVGO chip gate override applied (AVGO -2.72%).
  #         SMCI diverged from AVGO — server manufacturer vs chip designer decoupling.
  #         Second SMCI positive divergence on negative chip gate day (prior: 8/31 +0.54%).
  #         Protocol gap identified: SMCI gate carve-out recommended. Rule-based miss, not judgment.
  #   stand_aside: 53/97 = 54.64% (pullback from 54.74% peak; SMCI miss is the driver).
  # 2026-09-02: +5 candidates (risk-ON day; AVGO earnings AH; earnings-driven movers):
  #   CRM: close $257.19 = -0.36%. Scored "correct." PM +10.53% gap-and-fade. Anthropic
  #         partnership announced; market sold the news. Agent flagged: "not a same-day chaser."
  #   DELL: close $492.18 = +15.81%. Scored "MISSED." PM +9.11% on blowout Q2 earnings.
  #         Capital failure (not decision error) — this was the correct pick, $0 prevented entry.
  #   AMD: close $456.30 = -0.72%. Scored "correct." Structural block holds: 6th consecutive
  #         session underperforming chip complex. AMD -0.72% vs QQQ +0.23% (-95bps vs tape).
  #   CRWD: close $203.42 = -5.42%. Scored "avoided." PM +9.23% investor briefing → reversed
  #         hard. Ambiguous catalyst correctly identified as lower-tier. Saved ~5.4% loss.
  #   HPE: close $51.83 = +1.89%. Scored "correct." Binary event block (earnings day).
  #   stand_aside: 52/95 = 54.74%. WAS ALL-TIME HIGH (+1.41 ppts). 4/5 sweep.

benchmark:
  spy_close_at_system_start: 744.37
  spy_close_today: 770.23             # EOD 2026-09-04; SPY -0.38% (NFP jobs surprise; yields jumped; mixed market)
  spy_pct_change_since_start: +3.47   # (770.23 - 744.37) / 744.37 * 100
  system_alpha_vs_spy_pct: -103.47  # UNCONFIRMED — mechanical result of the unexplained $0 balance
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