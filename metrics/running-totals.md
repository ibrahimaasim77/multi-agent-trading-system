# Running Totals

Auto-updated by the post-mortem agent at end of each trading day.

```yaml
system_start: 2026-06-22       # first live trading day (post-Juneteenth)
last_updated: 2026-08-13
trading_days_elapsed: 38

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
  guardrail_aborts: 68             # 6/25 m+i, 6/26 m+i, 6/29 m+i, 6/30 m+i, 7/1 m+i, 7/2 m+i, 7/6 m+i, 7/7 m+pm, 7/8 m+i, 7/9 m+i, 7/10 m+i, 7/13 m+i, 7/14 m+i, 7/15 m+i, 7/16 m+i, 7/17 m+i, 7/21 m+i, 7/22 m+i, 7/23 m+i, 7/24 m+i, 7/27 m+i, 7/28 m+i, 7/29 m+i, 7/30 m+i, 7/31 m+i, 8/3 m+i, 8/4 m+i, 8/5 m+i, 8/6 m+i, 8/7 m+i, 8/10 m+i, 8/11 m+i, 8/12 m+i, 8/13 m+i
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
  # note (updated 2026-08-12): Day 37 elapsed (Day 34 of $0 streak since 6/25), still $0.00.
  # +2 guardrail_aborts (8/12 morning + intraday). SPY closed $772.54 (+0.26% from $770.56).
  # CPI in-line (3.4% YoY, 2.5% core) — modest relief rally.
  # WATERSHED EVENT: SMCI passed ALL FIVE EVALUATION GATES for the first time in system
  # history (S&P 500 member, mcap >$5B, price $34.45 <= $100 cap, Q4 FY26 earnings beat
  # as named catalyst, premarket +9.49% within 2-14.99%). Sole block: $0 cash. SMCI
  # closed +18.86% ($31.60 -> $37.56). First concrete, non-structural opportunity cost.
  # Hypothetical P&L: 2 shares x ($37.56 - $34.45) = +$6.22 on $68.90 deployed (+9.03%).
  # CRWV also missed (+19.20%): correctly blocked by >15% premarket abort rule (structural).
  # Stand-aside correctness: 27/61 = 44.26% (from 45.76%). INTC bounced back above $100
  # cap (+3.32% to $100.95) — sub-$100 window (8/10–8/11) now closed. 66 total guardrail
  # aborts. Call Robinhood Support: 1-800-279-1969. Account ●●●●9602.
  # note (updated 2026-08-13): Day 38 elapsed (Day 35 of $0 streak since 6/25), still $0.00.
  # +2 guardrail_aborts (8/13 morning + intraday) -> 68 total. SPY closed $777.77 (+0.68%
  # from $772.49). S&P 500 index hit all-time high 7,798.99 — first-ever close above 7,800.
  # SMCI Day 2: opened at prior close $37.61 (flat premarket); analyst upgrades intraday
  # (Rosenblatt $51 PT, Wedbush $40 PT, Citigroup $39 PT); Gate 5 failed at evaluation time
  # (premarket <2%); close $39.16 (+4.12%); scored "missed" (mechanical). Evaluation logic
  # CORRECT — no premarket signal = no limit order warranted. TTD Day 4 post-earnings:
  # +7.86% on ATH short-covering/no named catalyst; scored "missed." Stand-aside correct.
  # Stand-aside correctness: 27/63 = 42.86% (from 44.26%). Call 1-800-279-1969.

decision_quality:
  win_rate_pct: null           # set after first trade
  stand_aside_correctness_pct: 42.86   # 27/63
  stand_aside_count: 63
  stand_aside_correct: 27
  stand_aside_missed: 36
  # 2026-08-12: +2 candidates (morning evaluation before cash-gate abort):
  #   SMCI (premarket +9.49%, ~$34.45; Q4 FY2026 earnings blowout — gross margin 17.6%,
  #         guidance $65-72B vs $52.5B consensus, $60B+ new orders; S&P 500 member;
  #         ALL FIVE GATES CLEARED; sole block: $0 cash guardrail):
  #     Close $37.56 = +18.86% from prior $31.60. Scored "missed." +1 missed.
  #   CRWV (premarket +18%; Q2 2026 earnings beat — $104B backlog, revenue +112% YoY;
  #         >15% abort rule fires before cap/cash/S&P check; structural hard abort):
  #     Close $107.67 = +19.20% from prior $90.32. Scored "missed." +1 missed (structural).
  #   stand_aside: 27/61 = 44.26% (from 27/59 = 45.76%). Two misses, zero correct.
  # 2026-08-13: +2 candidates (morning evaluation before cash-gate abort):
  #   SMCI (Day 2 post-earnings; analyst upgrades intraday — Rosenblatt $51 PT, Wedbush $40 PT,
  #         Citigroup $39 PT; premarket flat/opened at $37.61 prior close; Gate 5 <2% fail;
  #         evaluation logic CORRECT — no premarket signal = no entry warranted):
  #     Close $39.16 = +4.12% from prior $37.61. Scored "missed." +1 missed (evaluation correct).
  #   TTD (Day 4 post-earnings consolidation; AMD-rule-analog active; no named company catalyst;
  #        +7.86% driven by S&P 500 ATH short-covering; named catalyst requirement unsatisfied):
  #     Close $14.55 = +7.86% from prior $13.49. Scored "missed." +1 missed (evaluation correct).
  #   stand_aside: 27/63 = 42.86% (from 27/61 = 44.26%). Two misses, zero correct.

benchmark:
  spy_close_at_system_start: 744.37   # captured EOD 2026-06-22 (system's first tracked day)
  spy_close_today: 777.77             # EOD 2026-08-13 (Robinhood last_trade_price at 19:59:59Z)
  spy_pct_change_since_start: +4.49   # (777.77 - 744.37) / 744.37 * 100; S&P 500 index hit ATH 7,798.99
  system_alpha_vs_spy_pct: -104.49  # UNCONFIRMED — mechanical result of the unexplained $0 balance, not a skill signal. See financial note above.
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
