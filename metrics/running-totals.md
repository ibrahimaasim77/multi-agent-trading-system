# Running Totals

Auto-updated by the post-mortem agent at end of each trading day.

```yaml
system_start: 2026-06-22       # first live trading day (post-Juneteenth)
last_updated: 2026-09-16
trading_days_elapsed: 61

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
  guardrail_aborts: 114            # 112 through 9/15; +2 est (9/16 morning #113 + intraday #114)
  # note (updated 2026-09-16): Day 61 elapsed (Day 59 of $0 streak). 114 GUARDRAIL ABORTS (EST).
  # DRAFT COMPLIANCE UNKNOWN — no Stand Aside drafts found in Gmail for 9/16 (streak may be broken at Day 10).
  # FOMC RATE HIKE DAY: Fed hiked +25bps (first hike in 3 years). Warsh: 1 more hike in 2026, hold 2027.
  # Macro: Dow -1.21%; SPY -0.44% → $754.09; QQQ +0.03% → $704.75. Tech flat — "priced in" hike narrative.
  #   META +0.46% ($670.24 → $673.33): Muse Day 6. Stand-aside — CORRECT (< +2% threshold).
  #   AMD +1.72% ($504.20 → $512.89): Post-FOMC normal eval. Gate 5 FAIL (< +2%). Stand-aside — CORRECT.
  #   AMD divergence pattern MODERATED: no PM-to-close > +2% today. Standard Gate 5 restored.
  # Stand-aside: 64/117 = 54.70% (from 53.91%; +2 correct; +0.79 ppts). Daily score: 70.
  # POST-FOMC REGIME NOW OPEN. Call Robinhood: 1-800-279-1969. Account ●●●●9602.
  # note (updated 2026-09-15): Day 60 elapsed (Day 58 of $0 streak). 112 GUARDRAIL ABORTS.
  # Two drafts confirmed — 10th consecutive compliant day. No-draft anomaly resolved.
  # Macro: FOMC eve — bifurcated (SPY -0.46% → $757.38; QQQ -0.65% → $704.59). Oil $107+/bbl (9th+ elevated session).
  #   FOMC rate hike probability >90%. 10-yr yield above 5%. Individual AI names diverged: META +0.73%, AMD +2.21%, NVDA +0.57%.
  # META +0.73% ($665.60 → $670.49): Gate 5 FAIL (-0.47% PM, < +2%). Muse Day 5. No fresh catalyst. Close +0.73% — CORRECT.
  # AMD +2.21% ($493.41 → $504.30): FOMC eve protocol (DO NOT EVALUATE) + Gate 5 FAIL (+1.20% PM < +2%). Close +2.21% — MISSED.
  #   AMD divergence pattern 3rd consecutive session: PM +1.20% → close +2.21% (+101bps intraday outperformance).
  # Stand-aside: 62/115 = 53.91% (from 53.98%; META correct, AMD missed). Daily score: 55.
  # FOMC September 16 IS TOMORROW. Call Robinhood: 1-800-279-1969. Account ●●●●9602.
  # note (updated 2026-09-14): Day 59 elapsed (Day 57 of $0 streak). 110 GUARDRAIL ABORTS.
  # Two drafts confirmed — 8th consecutive compliant day. No-draft anomaly resolved.
  # Macro: severe risk-off (SPY -0.46% → $760.77; QQQ -0.80% → $709.16). Saudi pipeline shutdown (Brent +3% → $107.65/bbl).
  #   Anthropic/OpenAI AI slowdown calls. FOMC Sep 16 ONE SESSION AWAY. Rate hike probability 85.5%.
  # META +2.73% ($648.03 → $665.71): Gate 5 FAIL (+1.74% PM, < +2%). Muse Day 4 (JPMorgan OW/$820, GS reiteration). Close surpassed threshold — MISSED.
  # AMD -4.43% ($516.13 → $493.26): CHIP GATE NEGATIVE (AVGO -4.16% PM) + Gate 5 FAIL (-5.80% PM). Largest AMD PM decline in system history. AVOIDED.
  # Stand-aside: 61/113 = 53.98% (from 54.05%; META missed, AMD avoided). Daily score: 60.
  # FOMC September 16 is ONE TRADING SESSION AWAY. Call Robinhood: 1-800-279-1969. Account ●●●●9602.
  # note (updated 2026-09-11): Day 58 elapsed (Day 55 of $0 streak). 108 GUARDRAIL ABORTS.
  # Two drafts confirmed — 7th consecutive compliant day. No-draft anomaly resolved.
  # Macro: relief bounce (SPY +0.84% → $764.20; QQQ +0.87% → $714.85). Oracle earnings drove tech bid.
  #   Oil $102.59/bbl (7th daily gain). PPI +5.4% YoY (slightly above consensus). FOMC Sep 16 (2 sessions away). Rate hike 59%.
  # AMD +2.52% ($503.60 → $516.28): Gate 5 FAIL (+1.34% PM, < +2%). No catalyst. Close surpassed threshold — 2nd session AMD PM-to-close divergence. MISSED.
  # META +0.60% ($644.38 → $648.23): Gate 5 FAIL (+1.60% PM). Muse Day 3 (TechCrunch adoption data ✓ but PM below threshold). CORRECT.
  # SMCI +7.28% ($37.38 → $40.10): AVGO carve-out activates (+1.09% PM). Gate 5 PASS (+2.16% PM). FOMC override (59% hike, SMCI maximally sensitive). MISSED (largest miss of week).
  # ORCL -1.76% ($152.94 → $150.26): Opportunistic; earnings beat; Gate 5 PASS (+7% PM). Capital guardrail fires. Gap-and-fade validated. CORRECT.
  # Stand-aside: 60/111 = 54.05% (from 54.21%; AMD missed, META correct, SMCI missed, ORCL correct). Daily score: 40.
  # FOMC September 16 now 2 trading sessions away. Call Robinhood: 1-800-279-1969. Account ●●●●9602.

decision_quality:
  win_rate_pct: null           # set after first trade
  stand_aside_correctness_pct: 54.70   # 64/117; META correct (+0.46%), AMD correct (+1.72%) — FOMC day
  stand_aside_count: 117
  stand_aside_correct: 64
  # 2026-09-16: +2 candidates (FOMC DAY; +25bps hike as expected; tech flat QQQ +0.03%; Dow -1.21%):
  #   META: close $673.33 = +0.46%. Scored "correct." Muse Day 6. Cash guardrail ($0, Day 59).
  #         Close +0.46% in (-1% to +2%) correct band. Gate 5 unverified (no draft found).
  #         Muse arc moderating (Day 6: +0.46% vs Day 1: +6.51%). Fresh catalyst needed for Day 7.
  #   AMD: close $512.89 = +1.72%. Scored "correct." Post-FOMC normal eval reinstated.
  #         Gate 5 FAIL (< +2%). Divergence pattern moderated — close did NOT exceed +2% today.
  #         AMD recovering from $493.26 rout (9/14): now $512.89, +3.97% above rout low.
  #   stand_aside: 64/117 = 54.70% (from 62/115 = 53.91%; +2 candidates, +2 correct; +0.79 ppts.)
  # 2026-09-15: +2 candidates (FOMC eve; bifurcated tape; META Muse Day 5; AMD FOMC block):
  #   META: close $670.49 = +0.73%. Scored "correct." Gate 5 FAIL (-0.47% PM < +2%). Muse Day 5.
  #         No confirmed fresh catalyst within 24h. FOMC eve protocol also fires (>90% hike prob).
  #         Close +0.73% validates stand-aside — within correct band (-1% to +2%). Gate correctly applied.
  #   AMD: close $504.30 = +2.21%. Scored "missed." FOMC eve protocol (DO NOT EVALUATE per 9/14 journal).
  #         Gate 5 FAIL also fires (+1.20% PM < +2%). Close +2.21% — 3rd consecutive AMD PM-to-close
  #         divergence session: 9/9 (PM -1.11% → +3.03%), 9/11 (PM +1.34% → +2.52%), 9/15 (PM +1.20% → +2.21%).
  #         FOMC eve block was protocol-correct. AMD divergence pattern now confirmed structural (3 of 3).
  #   stand_aside: 62/115 = 53.91% (from 61/113 = 53.98%; +2 candidates, +1 correct; -0.07 ppts.)
  # 2026-09-14: +2 candidates (severe risk-off; AI/chip rout; pre-FOMC; Saudi oil shock; AI slowdown narrative):
  #   META: close $665.71 = +2.73%. Scored "MISSED." Muse Day 4 (JPMorgan OW/$820, GS reiteration, #3 App Store).
  #         Gate 5 FAIL (+1.74% PM < +2% threshold) — 26bps below. FOMC probability 85.5%. Cash guardrail fires.
  #         First session where Gate 5 FAILED at evaluation but META closed ABOVE +2% threshold. Gate correctly applied.
  #   AMD: close $493.26 = -4.43%. Scored "avoided." CHIP GATE NEGATIVE (AVGO -4.16% PM, far below -1% threshold).
  #         Gate 5 FAIL (-5.80% PM — largest single-day AMD PM decline in system history). Doubly blocked.
  #         AMD premarket-to-close divergence pattern does NOT apply at -5.80% PM. Both gates validated.
  #   stand_aside: 61/113 = 53.98% (from 60/111 = 54.05%; +2 candidates, +1 correct; -0.07 ppts.)
  # 2026-09-11: +4 candidates (relief bounce; Oracle earnings; pre-FOMC Friday; oil $102.59/bbl):
  #   AMD: close $516.28 = +2.52%. Scored "missed." Gate 5 FAIL (+1.34% PM < +2%). No catalyst.
  #         AVGO carve-out active (+1.09% PM). Close exceeded threshold — 2nd AMD PM-to-close divergence.
  #   META: close $648.23 = +0.60%. Scored "correct." Gate 5 FAIL (+1.60% PM). Muse Day 3 TechCrunch
  #         adoption catalyst ✓ but PM below +2%. +0.60% close validates stand-aside.
  #   SMCI: close $40.10 = +7.28%. Scored "missed." AVGO carve-out: Gate 5 PASS (+2.16% PM).
  #         GS conf catalyst ($60B backlog, FY2027 guidance). FOMC override (59% hike). Largest miss of week.
  #   ORCL: close $150.26 = -1.76%. Scored "correct." Opportunistic: earnings beat (+30% rev, EPS beat).
  #         Gate 5 PASS (+7% PM). Capital guardrail fires (abort #107). Gap-and-fade validated.
  #   stand_aside: 60/111 = 54.05% (from 58/107 = 54.21%; +4 candidates, +2 correct. -0.16 ppts.)
  # 2026-09-10: +3 candidates (broad risk-off; oil at $100/bbl; FOMC 3 sessions away):
  #   META: close $644.37 = -1.43%. Scored "correct." Gate 5 FAIL (premarket -0.33% < +2%). Muse
  #         catalyst Day 2 — stale, no continuation news. -1.43% close validates evaluation.
  #   AMD: close $503.47 = -3.38%. Scored "avoided." Gate 5 FAIL (-2.46% PM) + AVGO chip gate
  #         NEGATIVE (-1.70% PM). Double-blocked. FOMC-sensitive reversal. Both gates validated.
  #   SMCI: close $37.39 = -3.96%. Scored "avoided." AVGO chip gate NEGATIVE (-1.70% PM). Carve-out
  #         NOT activated. Chip gate 4/4 accuracy. $2.97 avoided on $75 theoretical.
  #   stand_aside: 58/107 = 54.21% (from 55/104 = 52.88%; +3 candidates, +3 correct. +1.33 ppts.)
  # 2026-09-09: +3 candidates (continuing risk-off; stock-picker's market; FOMC 4 sessions away):
  #   META: close $653.39 = +6.51%. Scored "MISSED." Muse AI agent launch (Sep 8 PM). Premarket
  #         +5.17% ($645.18). ALL eligibility gates pass; VIX 16.60 (safe). Tier 1 setup — best
  #         since DELL +15.81% on 9/2. ONLY fail: cash <$50 guardrail (Day 53 anomaly). Capital
  #         failure, not decision failure. Hypothetical entry ~$645.22 → close $653.39 = +1.27% on pos.
  #   AMD: close $521.08 = +3.03%. Scored "MISSED." Structural block LIFTED (per 9/8 journal).
  #         Evaluated fresh: premarket -1.11% → Gate 5 FAIL (< +2%). Gate application correct given
  #         available information at 8:42 AM. AMD is now 3 consecutive sessions +3-5%. Post-block
  #         momentum pattern: AMD trending positive regardless of premarket signal. Gate-structure
  #         limitation, not decision error. Monitor for Gate 5 threshold revision discussion.
  #   SMCI: close $38.92 = -3.33%. Scored "avoided." AVGO premarket -1.04% → chip gate FIRES
  #         (< -1% threshold). Carve-out protocol correctly NOT activated (carve-out requires
  #         AVGO ≥ -1%). SMCI blocked. -3.33% close validates the gate. Protocol working perfectly.
  #   stand_aside: 55/104 = 52.88% (from 54/101 = 53.47%; +3 candidates, +1 correct).
  # 2026-09-08: +2 candidates (geopolitical shock: Iran/Saudi oil strikes; split market day):
  #   AMD: close $505.53 = +5.85%. Scored "MISSED." Structural block carried forward from 9/4 per
  #         protocol. Cumulative 2-session surge: +10.74% (9/4 +4.67%, 9/8 +5.85%). Block now formally
  #         invalid — original premise (7+ sessions underperforming QQQ) broken decisively. LIFT for 9/9.
  #         No-draft anomaly (5th) means catalyst evaluation unverifiable. Decision error + process failure.
  #   SMCI: close $40.25 = +1.67%. Scored "correct." AVGO gate POSITIVE (+2.97%). Carve-out protocol
  #         applied: evaluate SMCI independently when AVGO gate NEUTRAL/POSITIVE. +1.67% in correct zone.
  #         Protocol verified — first post-carve-out correct evaluation.
  #   stand_aside: 54/101 = 53.47% (from 53.54%; AMD miss -0.07 ppts; SMCI correct partially offsets).
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

benchmark:
  spy_close_at_system_start: 744.37
  spy_close_today: 754.09             # EOD 2026-09-16; SPY -0.44% (FOMC hike day; Dow -1.21%, QQQ +0.03%, tech flat)
  spy_pct_change_since_start: +1.31   # (754.09 - 744.37) / 744.37 * 100
  system_alpha_vs_spy_pct: -101.31  # UNCONFIRMED — mechanical result of the unexplained $0 balance
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
