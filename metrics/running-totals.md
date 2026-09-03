# Running Totals

Auto-updated by the post-mortem agent at end of each trading day.

```yaml
system_start: 2026-06-22       # first live trading day (post-Juneteenth)
last_updated: 2026-09-03
trading_days_elapsed: 53

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
  guardrail_aborts: 98             # 96 through 9/2; +2 estimated today (9/3 morning #97 + intraday #98) = 98 total
  # note (updated 2026-09-03): Day 53 elapsed (Day 50 of $0 streak — ROUND-NUMBER MILESTONE).
  # +2 guardrail aborts (estimated — no Gmail drafts found, 4th no-draft anomaly). SPY closed
  # $773.16 (+1.05% from $765.16). Strong RISK-ON: QQQ +1.18% ($717.61). AVGO chip gate NEGATIVE:
  # AVGO closed $357.24 (-2.72%) after Q3 earnings MISS AH on 9/2. AMD -0.18% (structural block,
  # 7+ sessions, CORRECT). SMCI +2.35% (chip gate override applied but SMCI diverged — MISSED;
  # second SMCI divergence from AVGO gate, 8/31 +0.54% was first). No draft found (4th anomaly:
  # 8/18, 8/26, 8/27, 9/3). 2 reconstructed stand-aside candidates: AMD correct (-0.18%); SMCI
  # missed (+2.35%). Stand-aside: 53/97 = 54.64% (slight pullback from 54.74% peak). Daily score: 60.
  # Next binary event: September 16 FOMC (40% probability 25bp rate hike; 9 trading days).
  # Call Robinhood Support: 1-800-279-1969. Account ●●●●9602. Day 50 — DAY 50 LANDMARK.

decision_quality:
  win_rate_pct: null           # set after first trade
  stand_aside_correctness_pct: 54.64   # 53/97; slight pullback from 54.74% peak (9/2)
  stand_aside_count: 97
  stand_aside_correct: 53
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
  spy_close_today: 773.16             # EOD 2026-09-03; SPY +1.05% (strong risk-ON; AVGO chip drag isolated)
  spy_pct_change_since_start: +3.87   # (773.16 - 744.37) / 744.37 * 100
  system_alpha_vs_spy_pct: -103.87  # UNCONFIRMED — mechanical result of the unexplained $0 balance
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
