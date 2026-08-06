# Running Totals

Auto-updated by the post-mortem agent at end of each trading day.

```yaml
system_start: 2026-06-22       # first live trading day (post-Juneteenth)
last_updated: 2026-08-06
trading_days_elapsed: 33

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
  guardrail_aborts: 58             # 6/25 m+i, 6/26 m+i, 6/29 m+i, 6/30 m+i, 7/1 m+i, 7/2 m+i, 7/6 m+i, 7/7 m+pm, 7/8 m+i, 7/9 m+i, 7/10 m+i, 7/13 m+i, 7/14 m+i, 7/15 m+i, 7/16 m+i, 7/17 m+i, 7/21 m+i, 7/22 m+i, 7/23 m+i, 7/24 m+i, 7/27 m+i, 7/28 m+i, 7/29 m+i, 7/30 m+i, 7/31 m+i, 8/3 m+i, 8/4 m+i, 8/5 m+i, 8/6 m+i
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
  # note (updated 2026-08-06): Day 33 elapsed (Day 29 of $0 streak), still $0.00.
  # +2 guardrail_aborts (8/6 morning + intraday). Flat-to-slightly-negative tape:
  # SPY -0.16% ($769.79→$768.56), QQQ -0.38% ($717.30→$714.56). Individual earnings
  # names outperformed the broad market: DIS +2.87% ($101.76→$104.68) on Q2 FY2026
  # beat (EPS $1.57 vs $1.50 est; streaming income +88% to $582M); SHOP +2.29%
  # ($144.24→$147.54) on Q2 2026 beat (EPS $0.42 vs $0.39 est; revenue +34% YoY).
  # Both names eliminated in premarket: DIS (+0.64% pm, below 2% threshold + >$100
  # budget); SHOP (-0.37% pm, negative premarket + 1.44× cap). Web search premarket
  # data again substantially incorrect (3rd consecutive session): INTC claimed +10.84%
  # (actual -1.67%), COHR +12.35% (actual -1.83%), PANW +5.53% (actual -1.31%),
  # AMD +7.00% (actual -1.12%). All four correctly eliminated by Robinhood quotes.
  # AMD rule fired (Day 4 of cycle): -1.12% premarket; AMD closed +1.50% from prior
  # close (flat zone, "correct"). Morning macro call "stand aside on mixed day" →
  # correct (SPY -0.16%). Macro accuracy: 26/29 = 89.7% (from 25/28 = 89.3%).
  # +3 stand_aside candidates: DIS "missed" (+2.87%), SHOP "missed" (+2.29%),
  # AMD "correct" (+1.50%). stand_aside: 17/45 = 37.78% (from 16/42 = 38.10%).
  # 58 total guardrail aborts. SPY +3.25% since system start (was +3.41% on 8/5;
  # SPY now $768.56 vs start $744.37).
  # Day 29 — URGENT. CALL ROBINHOOD SUPPORT: 1-800-279-1969. Account ●●●●9602.

decision_quality:
  win_rate_pct: null           # set after first trade
  stand_aside_correctness_pct: 37.78   # 17/45
  stand_aside_count: 45
  stand_aside_correct: 17
  stand_aside_missed: 28
  # 2026-08-06: +3 candidates (morning opportunistic scan before cash-gate abort):
  #   DIS (+0.64% premarket, $102.41 vs $101.76 prior close): EVALUATED — Q2 FY2026
  #     beat (EPS $1.57 vs $1.50 est; streaming income +88% to $582M). Eliminated by:
  #     (1) premarket +0.64% < 2% threshold; (2) $102.41 > $100 per-trade cap (0 whole
  #     shares on limit order). Close: $104.68 (+2.87% vs prior close). Structurally
  #     untradeable even with cash restored due to cap constraint. Scored "missed" per
  #     mechanical rule. stand_aside_missed: +1.
  #   SHOP (-0.37% premarket, $143.70 vs $144.24 prior close): EVALUATED — Q2 2026
  #     beat (EPS $0.42 vs $0.39 est; revenue +34% YoY; GMV +30%+). Eliminated by:
  #     (1) negative premarket (-0.37%); (2) 1.44× cap ($143.70 >> $100). Close:
  #     $147.54 (+2.29% vs prior close). V-bottom: negative premarket → +2.29% close.
  #     Rule applied correctly at evaluation time. Scored "missed." stand_aside_missed: +1.
  #   AMD (-1.12% premarket, $476.67 vs $482.05 prior close): EVALUATED — Q2 2026
  #     miss continuing (AH -8.5% on 8/4; session -7.33% on 8/5). AMD rule fires:
  #     negative premarket + confirmed negative catalyst. Close: $489.29 (+1.50% vs
  #     prior close). Relief bounce; AMD closed in flat zone. Scored "correct."
  #     stand_aside_correct: +1.
  #   stand_aside: 17/45 = 37.78% (from 16/42 = 38.10%).

benchmark:
  spy_close_at_system_start: 744.37   # captured EOD 2026-06-22 (system's first tracked day)
  spy_close_today: 768.56             # EOD 2026-08-06 (official market close from Robinhood)
  spy_pct_change_since_start: +3.25   # (768.56 - 744.37) / 744.37 * 100
  system_alpha_vs_spy_pct: -103.25  # UNCONFIRMED — mechanical result of the unexplained $0 balance, not a skill signal. See financial note above.
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
