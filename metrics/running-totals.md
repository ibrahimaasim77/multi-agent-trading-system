# Running Totals

Auto-updated by the post-mortem agent at end of each trading day.

```yaml
system_start: 2026-06-22       # first live trading day (post-Juneteenth)
last_updated: 2026-09-02
trading_days_elapsed: 52

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
  guardrail_aborts: 96             # 94 through 9/1; +2 today (9/2 morning #95 + intraday #96) = 96 total
  # note (updated 2026-09-02): Day 52 elapsed (Day 49 of $0 streak since 6/25), still $0.00.
  # +2 guardrail aborts (9/2 morning + intraday) → 96 total. SPY closed $765.14 (+0.44%
  # from $761.78). RISK-ON relief rally: S&P +0.46% (7,666.60), Dow +0.56% (+295 pts),
  # Nasdaq +0.45% (26,217.83). Major events: AVGO Q3 earnings MISS AH (-4.1% AH to $352.50
  # from $367.77 close) — chip gate will fire NEGATIVE 9/3. DELL +15.81% on blowout earnings
  # (missed — capital failure). CRM gap-and-fade: +10.53% PM → -0.36% close (correct stand).
  # CRWD -5.42% (avoided — investor briefing catalyst failed). Five stand-aside candidates:
  # CRM correct (-0.36%); DELL MISSED (+15.81%); AMD correct (-0.72%, structural block);
  # CRWD avoided (-5.42%); HPE correct (+1.89%, binary event block). 4/5 correct/avoided.
  # Stand-aside: 52/95 = 54.74% — NEW ALL-TIME HIGH (+1.41 ppts). Daily score: 70.
  # Next binary event: September 16 FOMC (40% probability 25bp rate hike; 10 trading days).
  # Call Robinhood Support: 1-800-279-1969. Account ●●●●9602. Day 50 — escalate to supervisor.

decision_quality:
  win_rate_pct: null           # set after first trade
  stand_aside_correctness_pct: 54.74   # 52/95 — NEW ALL-TIME HIGH; 4/5 correct/avoided today
  stand_aside_count: 95
  stand_aside_correct: 52
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
  #   stand_aside: 52/95 = 54.74%. NEW ALL-TIME HIGH (+1.41 ppts). 4/5 sweep.

benchmark:
  spy_close_at_system_start: 744.37
  spy_close_today: 765.14             # EOD 2026-09-02; SPY +0.44% (risk-ON relief rally)
  spy_pct_change_since_start: +2.79   # (765.14 - 744.37) / 744.37 * 100
  system_alpha_vs_spy_pct: -102.79  # UNCONFIRMED — mechanical result of the unexplained $0 balance
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
