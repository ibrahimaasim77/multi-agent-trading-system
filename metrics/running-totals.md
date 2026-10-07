# Running Totals

Auto-updated by the post-mortem agent at end of each trading day.

```yaml
system_start: 2026-06-22       # first live trading day (post-Juneteenth)
last_updated: 2026-10-07
trading_days_elapsed: 76

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
  guardrail_aborts: 144            # est. 144 by 10/7 (142 through 10/6 + Abort #143 morning + Abort #144 intraday)
  # note (updated 2026-10-07): Day 76 elapsed (Day 74 of $0 streak). 144 GUARDRAIL ABORTS (EST).
  # RISK-OFF DAY — compliance restart Day 1 confirmed. Two Stand Aside drafts in Gmail:
  #   Morning: 12:40 UTC (~8:40 AM ET). Intraday: 15:17 UTC (~11:17 AM ET). Streak Day 1.
  # SPY -0.25% → $777.17; QQQ -0.26% → $757.71. Risk-off: 10-yr yield 5.35%, VIX 15.81, all futures red PM.
  #   AMD -0.55% ($649.42 → $645.83): Gate 5 FAIL (-1.91% PM). Chip gate NEGATIVE (AVGO -1.28% PM).
  #     Cash guardrail fires ($0, Day 74 — Abort #143 morning + Abort #144 intraday).
  #     Close -0.55% = CORRECT stand-aside (within -1% to +2% band). AMD intraday recovered +1.39% from PM lows.
  #     AMD cumulative post-FOMC (9/16 → 10/7): $512.89 → $645.83 = +25.91%. $0 deployed.
  #   META -2.40% ($738.88 → $721.15): Gate 5 FAIL (-0.42% PM). No fresh Muse catalyst.
  #     Cash guardrail fires ($0, Day 74 — Abort #143). Intraday: additional -2.00% sell from PM level.
  #     Close -2.40% = AVOIDED (< -2%). Muse arc (9/21 relaunch) fully reversing from $741.13 peak.
  #     Good stand-aside. Dodged a -2.40% decline. Post-arc trajectory: $741.13 → $721.15 = -2.70%.
  #   AVGO +0.12% ($375.81 → $376.27): Reversed from -1.28% PM to close slightly positive. Chip sector resilient.
  #   Draft compliance: ✅ Day 1 restart. Two drafts confirmed. Target: Day 10 by 10/21.
  #   Stand-aside: 71/129 = 55.04% (+0.71 ppts from 54.33%; +2 candidates, +2 correct [AMD ✓, META avoided]).
  #   Daily score: 75. AMD correct +10, META avoided +10, drafts Day 1 +5; base 50.
  #   Even with capital, today's system would NOT have traded — both candidates Gate 5 FAIL at evaluation time.
  # note (updated 2026-10-06): Day 75 elapsed (Day 73 of $0 streak). ~142 GUARDRAIL ABORTS (EST).
  # ⚠️ 10-DAY ROUTINE GAP: No journals or Stand Aside drafts filed 9/23–10/5 (10 consecutive sessions).
  # Post-mortem and morning routine failed to document evaluations. Cause unknown. Resumed 10/6.
  # Today (10/6): SPY +0.56% → $779.14; QQQ +0.45% → $759.61. Mildly risk-on. Chip sector led.
  #   AMD +2.82% ($631.75 → $649.55): EVALUATION UNKNOWN — no morning draft. Close above Gate 5 +2% threshold.
  #     AVGO chip gate STRONGLY POSITIVE (+3.70% → $375.92). Capital blocked (~Abort #143 est.).
  #     Probable missed entry (Gate 5 likely PASS; Gate 4 catalyst status unknown). AMD now +26.65% from 9/16 close.
  #   META -0.37% ($741.90 → $739.19): Below Gate 5 threshold. Would have been correct stand-aside.
  #   SMCI +0.60% ($43.19 → $43.45): Below Gate 5 threshold. Would have been correct stand-aside.
  #   No drafts found in Gmail since 9/22. Draft compliance: ❌ 10-day break. Streak Day 0. Restart required 10/7.
  #   Daily score: 35. No formal stand-aside candidates (no draft). AMD probable unverified miss.
  #   AMD cumulative post-FOMC (9/16 → 10/6): $512.89 → $649.55 = +26.65% across 14 sessions. $0 deployed.
  # note (updated 2026-09-22): Day 65 elapsed (Day 63 of $0 streak). 122 GUARDRAIL ABORTS (EST).
  # POST-FOMC DAY 4: SPY -0.01% → $773.40; QQQ +0.81% → $747.47 (FIRST NASDAQ RECORD SINCE JUNE). Chipmakers rally.
  #   AMD +1.38% ($615.52 → $624.00): Gate 5 FAIL (-1.40% PM). Post-3-session exhaustion/digestion.
  #     AVGO chip gate borderline (-0.18% PM; technically active >-1%). Cash guardrail fires ($0, Day 63 — Abort #121).
  #     Close +1.38% = CORRECT stand-aside (within -1% to +2% band). First AMD correct in post-FOMC regime.
  #     AMD now +21.67% across 4 post-FOMC sessions ($512.89 → $624.00). $0 deployed.
  #   META -0.62% ($741.245 → $736.68): Gate 5 FAIL (-0.37% PM). Muse arc Day 2 consolidation.
  #     Close -0.62% = CORRECT stand-aside. Day 2 profit-taking (prior arc Day 2 was -1.43%; pattern confirmed).
  #     Cash guardrail fires ($0, Day 63 — Abort #121 morning).
  #   AVGO chip gate: +0.54% close ($362.66 → $364.61). Chip gate active; no core candidate reached Gate 5.
  #   DRAFT COMPLIANCE: ✅ RESTORED. Day 1 of new streak. Two drafts confirmed (morning 8:41 AM ET, intraday 11:12 AM ET).
  #     Streak broken 9/21 (Day 3); restarted today. Target Day 10 by 10/5.
  #   Stand-aside: 69/127 = 54.33% (+0.73 ppts from 53.60%; +2 candidates, +2 correct [AMD ✓, META ✓]).
  #   Daily score: 75 (AMD correct +10, META correct +10, drafts Day 1 +5; base 50).
  # note (updated 2026-09-21): Day 64 elapsed (Day 62 of $0 streak). 120 GUARDRAIL ABORTS (EST).
  # POST-FOMC DAY 3 — WORST SINGLE-SESSION MISS IN SYSTEM HISTORY:
  #   SPY +1.55% ($761.69 → $773.53); QQQ +2.77% ($721.45 → $741.45). Explosive risk-on.
  #   AMD +9.92% ($559.82 → $615.36): Capital blocked (Abort #119). Gate 5 PASS probable (PM likely ≥+2%).
  #     AVGO chip gate POSITIVE (+1.38%). AMD now +19.98% across 3 post-FOMC sessions ($512.89→$615.36).
  #     No morning draft found — evaluation unverified. Capital failure, 3rd consecutive post-FOMC session.
  #   META +11.33% ($665.75 → $741.13): Capital blocked. Fresh catalyst suspected (Muse arc RELAUNCH Day 9+).
  #     9/18 arc declared exhausted (D8 -2.48%); +11.33% move implies weekend catalyst (quant adoption
  #     data, enterprise news, or large analyst upgrade). Largest single-session META miss in system history.
  #     No morning draft found — gate evaluation unverifiable.
  #   SMCI +5.36% ($39.09 → $41.19): Capital blocked (core watchlist Day 2). AVGO chip gate POSITIVE.
  #     Recovery from 9/18 reversal (-3.07%). Gate 5 PASS probable. AI backlog thesis ($60B GS) intact.
  #   DRAFT COMPLIANCE FAILURE: No Stand Aside drafts found in Gmail for 9/21. Day 3 streak BROKEN (was Day 2).
  #   Hypothetical total if $217.19 deployed (equal weight): +$19.16 = +8.82% portfolio in ONE session.
  #   Daily score: 20 (lowest in system history). Stand-aside: 67/125 = 53.60% (−1.32 ppts; worst drop).
  #   CALL ROBINHOOD: 1-800-279-1969. Account ●●●●9602. AMD $615.36 (+19.98% post-FOMC). $0 deployed.
  # note (updated 2026-09-18): Day 63 elapsed (Day 61 of $0 streak). 118 GUARDRAIL ABORTS (EST).
  # POST-FOMC DAY 2: SPY -0.13% → $761.64; QQQ +0.62% → $721.36. Tech/AI outperforms; broad market digests.
  #   AMD +2.70% ($545.09 → $559.80): Gate 5 FAIL (+0.002% PM — flat after +6.31% surge). AMD DIVERGENCE PATTERN
  #     RETURNS (4th instance): flat PM → +2.70% intraday close. Gate correctly blocked on data; structural pattern
  #     unaddressed. Stand-aside: MISSED. Gate design limitation now requires formal protocol discussion.
  #   META -2.48% ($682.31 → $665.38): Muse Day 8. Gate 5 FAIL (+1.21% PM < +2%). No fresh catalyst. Close -2.48%
  #     = worst Muse arc session since D2 (-1.43%). Muse arc exhaustion confirmed. Stand-aside: AVOIDED. ✓ Skill.
  #   SMCI -3.07% ($40.35 → $39.11): Gate 5 FAIL (-0.15% PM). FIRST session SMCI properly on core watchlist
  #     (9/17 process gap corrected). Chip gate positive (AVGO +0.44%); SMCI's own PM negative → correctly blocked.
  #     Stand-aside: AVOIDED. ✓ Process correction validated on Day 1.
  #   AVGO +2.88% ($347.30 → $357.30): 2nd consecutive post-FOMC strong session. Chip gate strongly positive.
  # Draft compliance: Day 2 of new streak (morning 08:41 ET + intraday 11:11 ET confirmed). Target Day 10 by 10/1.
  # Daily score: 70. META avoided +10, SMCI avoided +10, drafts Day 2 +5, SMCI fix validated +5; AMD missed -5.
  # Stand-aside: 67/122 = 54.92% (+0.30 ppts from 54.62%; +3 candidates, +2 correct [META avoided, SMCI avoided]).
  # CALL ROBINHOOD: 1-800-279-1969. Account ●●●●9602. AMD +9.20% across 2 post-FOMC sessions. $0 deployed. Day 61.
  # note (updated 2026-09-17): Day 62 elapsed (Day 60 of $0 streak). 116 GUARDRAIL ABORTS (EST).
  # DRAFT COMPLIANCE: Day 1 of new streak. Two drafts confirmed — morning 08:42 ET, intraday 11:12 ET.
  # POST-FOMC DAY 1: SPY +1.14% → $762.64; QQQ +1.72% → $716.87. Risk-on. Oil -0.99% to $104.78.
  #   AMD +6.31% ($512.50 → $544.83): ALL GATES PASS. Gate 5 PASS (+3.55% PM). Chip gate STRONGLY POSITIVE
  #     (AVGO +2.52% PM). Gate 4 PASS (Piper Sandler OW/$600 PT). VIX 17.20. Capital blocked — Abort #115.
  #     LARGEST AMD SINGLE-DAY GAIN IN SYSTEM HISTORY. BIGGEST CAPITAL FAILURE. Stand-aside: MISSED.
  #   META +1.40% ($673.31 → $682.70): Muse Day 7. Gate 5 FAIL (+1.26% PM < +2%). Stand-aside: CORRECT.
  #     Muse arc Day 7 uptick: D6 +0.46% → D7 +1.40% — possible post-FOMC re-energization.
  #   SMCI +9.49% ($36.85 → $40.345): NOT EVALUATED — process gap (4th occurrence). Must add to core watchlist.
  #     AVGO chip gate was strongly positive; 9/16 journal recommended SMCI evaluation. Not acted upon.
  # Stand-aside: 65/119 = 54.62% (from 64/117 = 54.70%; AMD missed [+1/+0], META correct [+1/+1]; -0.08 ppts.)
  # Daily score: 40. AMD capital failure (-15), SMCI process gap (-10), META correct (+5), drafts OK (+5), macro correct (+5).
  # CALL ROBINHOOD: 1-800-279-1969. Account ●●●●9602. AMD +6.31% TODAY UNDEPLOYED.
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
  stand_aside_correctness_pct: 55.04   # 71/129; 2026-10-07: AMD correct (-0.55%), META avoided (-2.40%)
  stand_aside_count: 129
  stand_aside_correct: 71
  # 2026-10-07: +2 candidates (RISK-OFF; SPY -0.25%; QQQ -0.26%; 10-yr yield 5.35%; VIX 15.81; all futures red PM):
  #   AMD: close $645.83 = -0.55% ($649.42 → $645.83). Scored "correct." Gate 5 FAIL (-1.91% PM).
  #         AVGO chip gate NEGATIVE (-1.28% PM) — chip gate fires, no carve-out active.
  #         Cash guardrail ($0, Day 74 — Abort #143). Close -0.55% within (-1% to +2%) correct band.
  #         AMD intraday recovered +1.39% from PM low ($637.00). AMD now +25.91% post-FOMC ($512.89 → $645.83). $0 deployed.
  #   META: close $721.15 = -2.40% ($738.88 → $721.15). Scored "avoided." Gate 5 FAIL (-0.42% PM).
  #         No fresh Muse catalyst. Cash guardrail ($0, Day 74 — Abort #143).
  #         Intraday continued sell: -$14.66/-2.00% from PM level ($735.81 → $721.15).
  #         Muse arc (9/21 relaunch) reversing: $741.13 (9/21 peak) → $721.15 today = -2.70%.
  #         Close -2.40% < -2% = avoided. Good stand-aside. High-yield / sticky inflation headwind for META.
  #   DRAFT COMPLIANCE: ✅ Day 1 streak restart. Two drafts confirmed (morning 8:40 AM ET, intraday 11:17 AM ET).
  #   Stand-aside: 71/129 = 55.04% (from 69/127 = 54.33%; +2 candidates, +2 correct; +0.71 ppts — first time >55%).
  #   Daily score: 75. Even with capital, system would not have traded — both Gate 5 FAIL at evaluation.
  # 2026-09-22: +2 candidates (POST-FOMC DAY 4; SPY -0.01% → $773.40; QQQ +0.81% → $747.47; FIRST NASDAQ RECORD SINCE JUNE; chipmakers rally):
  #   AMD: close $624.00 = +1.38% ($615.52 → $624.00). Scored "correct." Gate 5 FAIL (-1.40% PM).
  #         AVGO chip gate borderline (-0.18% PM; technically active >-1%). Cash guardrail ($0, Day 63 — Abort #121).
  #         Close +1.38% within (-1% to +2%) correct band. First AMD correct in post-FOMC 4-session run.
  #         AMD now +21.67% across post-FOMC sessions ($512.89 → $624.00). $0 deployed entire run.
  #   META: close $736.68 = -0.62% ($741.245 → $736.68). Scored "correct." Gate 5 FAIL (-0.37% PM).
  #         Muse arc Day 2 consolidation. Day 2 profit-taking confirmed (prior arc Day 2: -1.43%; pattern holds).
  #         Cash guardrail ($0, Day 63). Close -0.62% within correct band. Gate correctly applied.
  #   DRAFT COMPLIANCE: ✅ Day 1 streak restart. Both drafts confirmed after 9/21 failure.
  #   stand_aside: 69/127 = 54.33% (from 67/125 = 53.60%; +2 candidates, +2 correct; +0.73 ppts recovery.)
  # 2026-09-21: +3 candidates (POST-FOMC DAY 3; SPY +1.55% → $773.53; QQQ +2.77% → $741.45; MOST EXPLOSIVE SESSION IN SYSTEM HISTORY):
  #   AMD: close $615.36 = +9.92% ($559.82 → $615.36). Scored "MISSED." Evaluation unknown (no morning draft).
  #         AVGO chip gate POSITIVE (close +1.38%). Cash guardrail fires ($0, Day 62 — Abort #119).
  #         AMD now +19.98% across 3 post-FOMC sessions ($512.89 → $615.36). Capital failure, 3rd consecutive.
  #         Gate 5 PASS probable (close magnitude implies strong premarket). No gate error. Infrastructure failure.
  #   META: close $741.13 = +11.33% ($665.75 → $741.13). Scored "MISSED." Evaluation unknown (no morning draft).
  #         9/18 Muse arc declared exhausted (D8 -2.48%). +11.33% today implies Muse arc RELAUNCH (fresh catalyst).
  #         Cash guardrail fires ($0, Day 62). Largest single-session META miss in system history (prior: D1 +6.51%).
  #         Gate status unknown. Hypothetical +$11.33 on $100 notional. Capital failure.
  #   SMCI: close $41.19 = +5.36% ($39.09 → $41.19). Scored "MISSED." Evaluation unknown (no morning draft).
  #         Core watchlist Day 2 (corrected protocol active). AVGO chip gate POSITIVE. Cash guardrail fires ($0, Day 62).
  #         Recovery from 9/18 reversal (-3.07%). Gate 5 PASS probable. Capital failure.
  #   DRAFT COMPLIANCE FAILURE: No Stand Aside drafts found in Gmail for 9/21. Day 3 streak BROKEN (stayed at Day 2).
  #   Hypothetical portfolio gain if $217.19 deployed equal-weight: ~+$19.16 = +8.82% in ONE session (system record).
  #   stand_aside: 67/125 = 53.60% (from 67/122 = 54.92%; +3 candidates, +0 correct; −1.32 ppts — WORST single-day drop.)
  # 2026-09-18: +3 candidates (POST-FOMC DAY 2; SPY -0.13% → $761.64; QQQ +0.62% → $721.36; tech outperforms; digestion):
  #   AMD: close $559.80 = +2.70% ($545.09 → $559.80). Scored "missed." Gate 5 FAIL (+0.002% PM — flat after +6.31%).
  #         AVGO chip gate POSITIVE (+0.44% PM) → carve-out active. Gate 5 terminal fail at +0.002%.
  #         Close +2.70% = AMD DIVERGENCE PATTERN (4th confirmed instance): flat PM → +2.70% intraday surge.
  #         Gate correctly blocked on available data; structural AMD pattern remains unaddressed by gate design.
  #         AMD now +9.20% across two post-FOMC sessions ($512.89 → $559.80). Capital anomaly: $0 deployed.
  #   META: close $665.38 = -2.48% ($682.31 → $665.38). Scored "avoided." Muse Day 8.
  #         Gate 5 FAIL (+1.21% PM < +2%). No fresh Muse catalyst at evaluation time.
  #         Close -2.48% = worst Muse arc day since D2 (-1.43%). Muse arc exhaustion confirmed.
  #         Full arc record: D1 +6.51% miss, D2-D3-D5-D6-D7-D8 correct (5 of 6), D4 missed.
  #   SMCI: close $39.11 = -3.07% ($40.35 → $39.11). Scored "avoided."
  #         FIRST SESSION on core watchlist (9/17 process gap corrected). Gate 5 FAIL (-0.15% PM).
  #         Chip gate positive (AVGO +0.44%) but SMCI own PM negative → correctly blocked.
  #         Process correction validated immediately: -3.07% avoided on post-surge reversal day.
  #   stand_aside: 67/122 = 54.92% (from 65/119 = 54.62%; +3 candidates, +2 correct; +0.30 ppts.)
  # 2026-09-17: +2 candidates (POST-FOMC DAY 1; SPY +1.14%; QQQ +1.72%; oil -0.99%; peak-rates regime):
  #   AMD: close $544.83 = +6.31% ($512.50 → $544.83). Scored "MISSED." ALL GATES PASSED at 8:39 AM ET.
  #         Gate 5 PASS (+3.55% PM $530.69). Chip gate STRONGLY POSITIVE (AVGO +2.52% PM). Gate 4 PASS
  #         (Piper Sandler OW/$600 PT, David O'Connor, 'ramp-ups on track'). VIX 17.20. Oil -0.99% tailwind.
  #         Post-FOMC protocol CLEAR. Every single gate cleared. Cash guardrail fires ($0, Day 60 — Abort #115).
  #         LARGEST AMD DAILY RETURN IN SYSTEM HISTORY. HIGHEST-CONVICTION CAPITAL FAILURE IN SYSTEM HISTORY.
  #         This is NOT a gate error. It is the most expensive manifestation of the capital anomaly to date.
  #   META: close $682.70 = +1.40% ($673.31 → $682.70). Scored "correct." Muse Day 7.
  #         Gate 5 FAIL (+1.26% PM < +2%). No confirmed fresh Muse catalyst within 24h. Terminal fail.
  #         Close +1.40% validates: within (-1% to +2%) correct band. Notable: D7 (+1.40%) > D6 (+0.46%) —
  #         possible post-FOMC re-energization of Muse arc. Watch D8 for ≥+2% PM AND fresh catalyst.
  #   SMCI: close $40.345 = +9.49% ($36.85 → $40.345). NOT a formal stand-aside candidate today (not evaluated).
  #         Process failure: 9/16 journal recommended SMCI evaluation if chip gate positive. AVGO +2.52% PM
  #         (chip gate strongly positive); SMCI absent from morning watchlist. 4th SMCI process failure.
  #         MANDATORY FIX: add SMCI to core watchlist permanently when chip gate ≥ -1% PM.
  #   stand_aside: 65/119 = 54.62% (from 64/117 = 54.70%; +2 candidates, +1 correct; -0.08 ppts.)
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
  spy_close_today: 777.17             # EOD 2026-10-07; SPY -0.25% (risk-off; 10-yr yield 5.35%; VIX 15.81)
  spy_pct_change_since_start: +4.41   # (777.17 - 744.37) / 744.37 * 100
  system_alpha_vs_spy_pct: -104.41  # UNCONFIRMED — mechanical result of the unexplained $0 balance
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
