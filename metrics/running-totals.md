# Running Totals

Auto-updated by the post-mortem agent at end of each trading day.

```yaml
system_start: 2026-06-22       # first live trading day (post-Juneteenth)
last_updated: 2026-08-07
trading_days_elapsed: 34

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
  guardrail_aborts: 60             # 6/25 m+i, 6/26 m+i, 6/29 m+i, 6/30 m+i, 7/1 m+i, 7/2 m+i, 7/6 m+i, 7/7 m+pm, 7/8 m+i, 7/9 m+i, 7/10 m+i, 7/13 m+i, 7/14 m+i, 7/15 m+i, 7/16 m+i, 7/17 m+i, 7/21 m+i, 7/22 m+i, 7/23 m+i, 7/24 m+i, 7/27 m+i, 7/28 m+i, 7/29 m+i, 7/30 m+i, 7/31 m+i, 8/3 m+i, 8/4 m+i, 8/5 m+i, 8/6 m+i, 8/7 m+i
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
  # note (updated 2026-08-07): Day 34 elapsed (Day 30 of $0 streak), still $0.00.
  # +2 guardrail_aborts (8/7 morning + intraday). "Bad news is good news" tape:
  # July NFP miss (-23K vs +80K expected) → rate-cut expectations → risk-on rally.
  # SPY +0.60% ($768.56→$773.20), QQQ +1.17% ($714.65→$723.04). Gold miners
  # outperformed: NEM +7.17% ($105.43→$112.99) on jobs-miss → gold catalyst;
  # COHR +13.42% ($334.22→$379.05) on unknown catalyst + AI/rate-cut halo.
  # Both NEM and COHR eliminated by price > $100 cap. Four stand-aside candidates
  # ended flat: AMD -1.18%, ANET -1.92%, INTC +1.83%, PANW +1.22% (all correct).
  # Web search premarket data incorrect for 4th consecutive session (INTC claimed
  # +10.84%, actual +2.99%; COHR claimed +12.35%, actual +7.25%; PANW claimed
  # +5.53%, actual +2.35%). Morning macro call "bad news is good news" → correct
  # (SPY +0.60%, QQQ +1.17%). Macro accuracy: 27/30 = 90.0% (from 26/29 = 89.7%).
  # +6 stand_aside candidates today: COHR "missed" (+13.42%), NEM "missed" (+7.17%),
  # AMD "correct" (-1.18%), ANET "correct" (-1.92%), INTC "correct" (+1.83%),
  # PANW "correct" (+1.22%). stand_aside: 21/51 = 41.18% (from 17/45 = 37.78%).
  # 60 total guardrail aborts. SPY +3.87% since system start (was +3.25% on 8/6;
  # SPY now $773.20 vs start $744.37).
  # Day 30 MILESTONE — URGENT. CALL ROBINHOOD SUPPORT: 1-800-279-1969. Account ●●●●9602.

decision_quality:
  win_rate_pct: null           # set after first trade
  stand_aside_correctness_pct: 41.18   # 21/51
  stand_aside_count: 51
  stand_aside_correct: 21
  stand_aside_missed: 30
  # 2026-08-07: +6 candidates (morning opportunistic scan before cash-gate abort):
  #   COHR (+7.25% premarket, $358.43 vs $334.22 prior close): EVALUATED — no named
  #     catalyst identified (possible AI data center optical/photonics re-rating on
  #     rate-cut expectations). Eliminated by cap (3.58×). Close: $379.05 (+13.42%).
  #     COHR accelerated premarket-to-close — unusual. Scored "missed." +1 missed.
  #   NEM (+5.69% premarket, $111.43 vs $105.43 prior close): EVALUATED — named
  #     catalyst: July NFP miss (-23K) → Fed rate cut → gold rally → gold miners.
  #     Eliminated by price > $100 cap ($111.43 = 1.11×). Close: $112.99 (+7.17%).
  #     Cleanest catalyst-correct stand-aside miss in recent sessions. +1 missed.
  #   AMD (+2.79% premarket, $502.91 vs $489.28 prior close): EVALUATED — no named
  #     catalyst last 24h (AMD rule does NOT fire; positive premarket). Eliminated by
  #     cap (5.03×). Close: $483.50 (-1.18%). Reversed from premarket gains.
  #     Scored "correct." +1 correct.
  #   ANET (+3.19% premarket, $198.46 vs $192.32 prior close): EVALUATED — no named
  #     catalyst. Eliminated by cap (1.98×). Close: $188.64 (-1.92%). Gave back all
  #     premarket gains despite broad QQQ +1.17% tape. Scored "correct." +1 correct.
  #   INTC (+2.99% premarket, $102.79 vs $99.81 prior close): EVALUATED — no named
  #     catalyst. Eliminated by price > $100 (0 whole shares on limit order). Close:
  #     $101.64 (+1.83%). Flat zone. Scored "correct." +1 correct.
  #   PANW (+2.35% premarket, $368.10 vs $359.49 prior close): EVALUATED — no named
  #     catalyst. Eliminated by cap (3.68×). Close: $363.86 (+1.22%). Flat zone.
  #     Scored "correct." +1 correct.
  #   stand_aside: 21/51 = 41.18% (from 17/45 = 37.78%).

benchmark:
  spy_close_at_system_start: 744.37   # captured EOD 2026-06-22 (system's first tracked day)
  spy_close_today: 773.20             # EOD 2026-08-07 (official market close from Robinhood)
  spy_pct_change_since_start: +3.87   # (773.20 - 744.37) / 744.37 * 100
  system_alpha_vs_spy_pct: -103.87  # UNCONFIRMED — mechanical result of the unexplained $0 balance, not a skill signal. See financial note above.
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
