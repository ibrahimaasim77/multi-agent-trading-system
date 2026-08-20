# Running Totals

Auto-updated by the post-mortem agent at end of each trading day.

```yaml
system_start: 2026-06-22       # first live trading day (post-Juneteenth)
last_updated: 2026-08-20
trading_days_elapsed: 43

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
  guardrail_aborts: 78             # 76 confirmed through 8/19; +2 today (8/20 morning + intraday) = 78 total
                                   # prior: 6/25 m+i, 6/26 m+i, 6/29 m+i, 6/30 m+i, 7/1 m+i, 7/2 m+i, 7/6 m+i, 7/7 m+pm, 7/8 m+i, 7/9 m+i, 7/10 m+i, 7/13 m+i, 7/14 m+i, 7/15 m+i, 7/16 m+i, 7/17 m+i, 7/21 m+i, 7/22 m+i, 7/23 m+i, 7/24 m+i, 7/27 m+i, 7/28 m+i, 7/29 m+i, 7/30 m+i, 7/31 m+i, 8/3 m+i, 8/4 m+i, 8/5 m+i, 8/6 m+i, 8/7 m+i, 8/10 m+i, 8/11 m+i, 8/12 m+i, 8/13 m+i, 8/14 m+i, 8/17 m+i (inferred), 8/18 m+i, 8/19 m+i, 8/20 m+i
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
  # history (S&P 500 member, mcap >$5B, price $34.45 ≤ $100 cap, Q4 FY26 earnings beat
  # as named catalyst, premarket +9.49% within 2-14.99%). Sole block: $0 cash. SMCI
  # closed +18.86% ($31.60 → $37.56). First concrete, non-structural opportunity cost.
  # Hypothetical P&L: 2 shares × ($37.56 - $34.45) = +$6.22 on $68.90 deployed (+9.03%).
  # CRWV also missed (+19.20%): correctly blocked by >15% premarket abort rule (structural).
  # Stand-aside correctness: 27/61 = 44.26% (from 45.76%). INTC bounced back above $100
  # cap (+3.32% to $100.95) — sub-$100 window (8/10–8/11) now closed. 66 total guardrail
  # aborts. Call Robinhood Support: 1-800-279-1969. Account ●●●●9602.
  # note (updated 2026-08-13): Day 38 elapsed (Day 35 of $0 streak since 6/25), still $0.00.
  # +2 guardrail_aborts (8/13 morning + intraday) → 68 total. SPY closed $777.77 (+0.68%
  # from $772.49). S&P 500 index hit all-time high 7,798.99 — first-ever close above 7,800.
  # SMCI Day 2: opened at prior close $37.61 (flat premarket); analyst upgrades intraday
  # (Rosenblatt $51 PT, Wedbush $40 PT, Citigroup $39 PT); Gate 5 failed at evaluation time
  # (premarket <2%); close $39.16 (+4.12%); scored "missed" (mechanical). Evaluation logic
  # CORRECT — no premarket signal = no limit order warranted. TTD Day 4 post-earnings:
  # +7.86% on ATH short-covering/no named catalyst; scored "missed." Stand-aside correct.
  # Stand-aside correctness: 27/63 = 42.86% (from 44.26%). Call 1-800-279-1969.
  # note (updated 2026-08-14): Day 39 elapsed (Day 36 of $0 streak since 6/25), still $0.00.
  # +2 guardrail_aborts (8/14 morning + intraday) → 70 total. SPY closed $776.31 (-0.20%
  # from $777.88). Russell 2000 fresh all-time high (IWM +0.52%). No valid trade even
  # hypothetically. Five stand-aside candidates: SMCI correct (+1.74% flat zone, Day 3);
  # TTD avoided (-2.98%, AMD-rule-analog Day 5 fired correctly — final application);
  # RDDT missed (+12.56%, Gate 1 structural — not S&P 500 member until 8/18); AMD missed
  # (+6.48%, structural price cap 5.14× on Technology Leadership Forum catalyst);
  # WDAY avoided (-3.74%, abort threshold fired on +17-25% Silver Lake M&A rumor that
  # was subsequently denied — most dramatic abort threshold validation in system history,
  # entry at open would have been -19 to -23% loss by close). Stand-aside: 30/68 = 44.12%
  # (+1.26 pts). Call 1-800-279-1969. Week 8 of anomaly begins Monday 8/17 (Day 37).
  # note: 2026-08-17 — NO JOURNAL WRITTEN. Reconstructed closes: SPY $772.67 (-0.47%),
  # SMCI $38.28 (-3.92% from 8/14), TTD $13.40 (-5.17%), RDDT $164.50 (-7.57%),
  # AMD $506.00 (-1.61%). Day 40 elapsed, Day 37 of $0 streak. +2 guardrail aborts
  # (8/17 morning + intraday) inferred → 72 estimated. Stand-aside candidates unknown.
  # note (updated 2026-08-18): Day 41 elapsed (Day 38 of $0 streak since 6/25), still $0.00.
  # +2 guardrail aborts (8/18 morning + intraday) → 74 estimated total. SPY closed $767.42
  # (-0.68% from $772.67). Semiconductor sector -5.5%; Nasdaq -1.33%; chip selloff drove
  # AMD -4.22%, NVDA -2.31%, SMCI -2.27%. No valid trade even hypothetically. Two
  # stand-aside candidates: SMCI avoided (-2.27%, Gate 5 fail — negative premarket in chip
  # selloff environment); TTD correct (+0.11%, flat zone, no named catalyst, normal eval mode
  # Day 2). RDDT (S&P 500 inclusion Day 1) declined -3.80% — post-inclusion fading as
  # predicted, Gate 3 structural block ($158.24 > $100 cap). No Gmail drafts found for today.
  # Stand-aside: 32/70 = 45.71% (+1.59 pts). Call 1-800-279-1969. Week 9 of anomaly.
  # note (updated 2026-08-19): Day 42 elapsed (Day 39 of $0 streak since 6/25), still $0.00.
  # +2 guardrail aborts (8/19 morning + intraday) → 76 total. SPY closed $769.06 (+0.21%
  # from $767.45). Sector-rotation day: IWM +0.50%, META +0.46%; but semis continued lower
  # (AVGO -4.60% on earnings miss Day 2, AMD -3.63%, NVDA -0.93%). QQQ -0.19%. Both routines
  # ran and produced Gmail drafts (draft-absence anomaly from 8/18 resolved). Two stand-aside
  # candidates: SMCI avoided (-2.23%, Gate 5 fail — AVGO earnings miss Day 2 chip headwind;
  # third consecutive correct SMCI block; prior close $37.41); TTD correct (+0.89%, flat zone,
  # no named catalyst, normal eval mode Day 3; prior close $13.42). KEYS +2.6% PM on record
  # Q3 — above $100 cap, not evaluated. No valid trade even hypothetically.
  # Stand-aside: 34/72 = 47.22% (+1.51 pts) — NEW ALL-TIME HIGH. Call 1-800-279-1969.
  # note (updated 2026-08-20): Day 43 elapsed (Day 40 of $0 streak since 6/25), still $0.00.
  # +2 guardrail aborts (8/20 morning + intraday) → 78 total. SPY closed $762.65 (-0.83%
  # from $769.06). Risk-off session: WMT -9.7% (disappointing sales); Treasury yields reversed
  # from prior day's sharp decline (Treasury Dept announced doubled long-dated buybacks);
  # oil ~$88 (Trump "Operation Economic Fury" Iran sanctions). Both routines ran and produced
  # Gmail drafts. Two stand-aside candidates: SMCI correct (-0.25%, premarket -0.38% Gate 5
  # fail, AVGO stabilizing -0.15% but not recovering, no SMCI company-specific catalyst;
  # fourth consecutive correct SMCI block since 8/14 peak); TTD correct (-1.70%, premarket
  # -0.30% Gate 5 fail, no named catalyst, normal eval mode Day 4). No valid trade even
  # hypothetically. COHR +12.35% per web search — price unverified, likely above $100 cap.
  # Stand-aside: 36/74 = 48.65% (+1.43 pts) — NEW ALL-TIME HIGH. Call 1-800-279-1969.

decision_quality:
  win_rate_pct: null           # set after first trade
  stand_aside_correctness_pct: 48.65   # 36/74
  stand_aside_count: 74
  stand_aside_correct: 36
  stand_aside_missed: 38
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
  # 2026-08-14: +5 candidates (morning + intraday evaluation before cash-gate abort):
  #   SMCI (Day 3 post-earnings; premarket -0.50%; Gate 5 fail; close +1.74%): correct. +1/+1.
  #   TTD (Day 5 AMD-rule-analog; premarket -0.55%; hard block; close -2.98%): avoided. +1/+1.
  #   RDDT (S&P 500 inclusion 8/18; Gate 1 fail — not a member today; close +12.56%): missed. +0/+1.
  #   AMD (Technology Leadership Forum +6.48% catalyst; structural price cap 5.14×; close +6.48%): missed. +0/+1.
  #   WDAY (Silver Lake M&A rumor +17-25% spike, then denied; abort threshold >12%; close -3.74%): avoided. +1/+1.
  #   stand_aside: 30/68 = 44.12% (from 27/63 = 42.86%). Three correct/avoided, two missed (both structural).
  # 2026-08-17: NO JOURNAL — stand-aside candidates unknown; +2 guardrail aborts inferred.
  # 2026-08-18: +2 candidates (morning evaluation before cash-gate abort):
  #   SMCI (Gate 5 fail — semiconductor sector -5.5% selloff; premarket negative inferred;
  #         no company-specific catalyst; prior close $38.28 [8/17 confirmed]):
  #     Close $37.41 = -2.27% from prior $38.28. Scored "avoided." +1/+1.
  #   TTD (normal evaluation mode Day 2; no named catalyst; flat +0.11%):
  #     Close $13.42 = +0.11% from prior $13.40. Scored "correct." +1/+1.
  #   stand_aside: 32/70 = 45.71% (from 30/68 = 44.12%). Two correct/avoided, zero missed.
  # 2026-08-19: +2 candidates (morning evaluation before cash-gate abort):
  #   SMCI (Gate 5 fail — AVGO earnings miss extends chip headwind Day 2; premarket -0.72%;
  #         no SMCI company-specific catalyst; prior close $37.41):
  #     Close $36.58 = -2.23% from prior $37.41. Scored "avoided." +1/+1.
  #   TTD (normal evaluation mode Day 3; no named catalyst; premarket +0.22% below Gate 5;
  #        prior close $13.42):
  #     Close $13.54 = +0.89% from prior $13.42. Scored "correct." +1/+1.
  #   stand_aside: 34/72 = 47.22% (from 32/70 = 45.71%). Two correct/avoided. NEW ALL-TIME HIGH.
  # 2026-08-20: +2 candidates (morning evaluation before cash-gate abort):
  #   SMCI (premarket -0.38% Gate 5 fail; AVGO stabilizing -0.15% but not recovering;
  #         no SMCI company-specific catalyst; prior close $36.58):
  #     Close $36.49 = -0.25% from prior. Scored "correct." +1/+1.
  #   TTD (premarket -0.30% Gate 5 fail; no named catalyst; normal eval mode Day 4;
  #        prior close $13.54):
  #     Close $13.31 = -1.70% from prior. Scored "correct." +1/+1.
  #   stand_aside: 36/74 = 48.65% (from 34/72 = 47.22%). Two correct. NEW ALL-TIME HIGH.

benchmark:
  spy_close_at_system_start: 744.37   # captured EOD 2026-06-22 (system's first tracked day)
  spy_close_today: 762.65             # EOD 2026-08-20 (Robinhood last_trade_price at 19:59:59Z); SPY -0.83% on risk-off/WMT/Treasury yield reversal day
  spy_pct_change_since_start: +2.46   # (762.65 - 744.37) / 744.37 * 100
  system_alpha_vs_spy_pct: -102.46  # UNCONFIRMED — mechanical result of the unexplained $0 balance, not a skill signal. See financial note above.
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
