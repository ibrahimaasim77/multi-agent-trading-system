# Running Totals

Auto-updated by the post-mortem agent at end of each trading day.

```yaml
system_start: 2026-06-22       # first live trading day (post-Juneteenth)
last_updated: 2026-07-24
trading_days_elapsed: 24

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
  guardrail_aborts: 40             # 6/25 m+i, 6/26 m+i, 6/29 m+i, 6/30 m+i, 7/1 m+i, 7/2 m+i, 7/6 m+i, 7/7 m+pm, 7/8 m+i, 7/9 m+i, 7/10 m+i, 7/13 m+i, 7/14 m+i, 7/15 m+i, 7/16 m+i, 7/17 m+i, 7/21 m+i, 7/22 m+i, 7/23 m+i, 7/24 m+i
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
  # note (updated 2026-07-09): Day 13 elapsed (Day 10 of $0 streak), still $0.00.
  # +2 guardrail_aborts (7/9 morning + intraday). Market risk-on: QQQ +1.65%,
  # SPY +0.84%. AI chip rally (SK Hynix US debut). AMD +5.65% (DeepSeek bounce),
  # AVGO +3.20% (Apple-Broadcom Day 2 continuation; cumulative 2-day +8.18%
  # from 7/7 close of $370.78 → today $401.12), META +4.67%, NVDA -0.67%
  # (negative divergence, first in 2 sessions). No formal stand-aside candidates
  # evaluated — both routines aborted at cash gate before any ticker screening.
  # Morning draft escalated to include Robinhood Support phone number
  # (1-800-279-1969) in subject. Email escalation chain exhausted at Day 10.
  # note (updated 2026-07-10): Day 14 elapsed (Day 11 of $0 streak), still $0.00.
  # +2 guardrail_aborts (7/10 morning + intraday). Mixed/mild risk-on: SPY +0.42%,
  # QQQ +0.31%, IWM -0.43% (small-cap diverging negative). META +5.99% (dominant
  # mover, no named catalyst found by either routine — noted but not formally
  # scored per standing methodology). NVDA +4.03% (resumed AI-infra outperformance
  # after 1-session interruption). AMD +2.06% (surpassed pre-DeepSeek-rout close
  # of $552.05; recovery largely complete). AVGO -0.28% (Apple-Broadcom catalyst
  # fully exhausted Day 3, exactly as predicted). No formal stand-aside candidates
  # evaluated — both routines aborted at cash gate. Metrics unchanged.
  # note (updated 2026-07-13): Day 15 elapsed (Day 12 of $0 streak), still $0.00.
  # +2 guardrail_aborts (7/13 morning + intraday). Risk-off on Iran weekend
  # escalation: US strikes on Iranian targets, Iran retaliated on Gulf facilities,
  # container ship struck in Strait of Hormuz. SPY -0.78%, QQQ -1.90%, IWM -0.86%.
  # Semis worsened intraday vs premarket: NVDA -3.54% (vs -1.57% pm), AMD -4.21%
  # (vs -2.81% pm), AVBO -4.03% (vs -1.77% pm). META -1.86% (marginal outperformance
  # vs QQQ; Meta Compute thesis intact). TMUS +0.44% (BofA upgrade absorbed;
  # first live analyst-upgrade data point — no 2%+ same-day trigger on risk-off day).
  # No formal stand-aside candidates — cash gate aborted before evaluation.
  # META catalyst now confirmed: Meta Compute AI cloud + Iris chip (Broadcom/TSMC).
  # AMD reverted below pre-DeepSeek close ($552.05) — memory sector contagion
  # (SNDK/WDC/MU -5% premarket) remains the primary driver. Macro accuracy: 15/15.
  # note (updated 2026-07-14): Day 16 elapsed (Day 13 of $0 streak), still $0.00.
  # +2 guardrail_aborts (7/14 morning + intraday). Risk-on: CPI June 3.5% vs 3.8%
  # expected (cooler) drove tech rally: QQQ +1.11%, NVDA +4.06% (AI-infra resumed),
  # AMD +2.48% (faded from +4.72% premarket — catalyst-less gapper, validates freshness
  # filter). AVGO +1.30% (exhausted catalyst, correct call). SPY +0.36%. Bank earnings
  # day (JPM/WFC/C/GS): mixed but non-disruptive. XLE +0.37% at close (intraday Iran
  # spike to +3.2% fully reversed — 2nd consecutive intraday fade on Iran oil premium).
  # Morning routine formally evaluated AMD (failed freshness) and AVGO (exhausted catalyst)
  # before cash-gate abort. +2 stand_aside_candidates: AMD "missed" (+2.48% > 2%
  # threshold, though filter correctly applied), AVGO "correct" (+1.30%). 
  # stand_aside: 8/21 = 38.10%. Macro accuracy: 16/16.
  # CRITICAL: Day 13 of $0 balance. Call Robinhood Support 1-800-279-1969.
  # note (updated 2026-07-15): Day 17 elapsed (Day 14 of $0 streak), still $0.00.
  # +2 guardrail_aborts (7/15 morning + intraday). Mixed session, NOT the clean
  # tech-led risk-on day the premarket suggested: SPY +0.39%, QQQ -0.28% (tech
  # underperformed despite ASML Q2 beat). SpaceX fell below its IPO price for the
  # first time — weighed on growth/Nasdaq sentiment. NVDA +0.33% (muted ASML halo).
  # AMD -3.43% (dramatic reversal from +1.42% premarket — 3rd consecutive session
  # validating catalyst-freshness filter; would have been a significant loss).
  # ASML itself +3.00% (best CORE watchlist performer, untradeable at $1,818 price).
  # PYPL +17.21% from prior close (Stripe/Advent unconfirmed M&A), but CLOSED
  # at $55.52 vs premarket $56.51 — giving back nearly $1/share from the premarket
  # peak; >15% premarket abort correctly applied. +2 stand-aside candidates both
  # scored "missed" mechanically (ASML +3.00%, PYPL +17.21%), but neither
  # represents a genuine judgment failure (hard structural ineligibility in both
  # cases). stand_aside: 8/23 = 34.78%. Macro accuracy: 16/17 (94%) — first
  # QQQ directional miss (predicted tech-led but QQQ -0.28%). CRITICAL: Day 14
  # of $0 balance. Call Robinhood Support 1-800-279-1969. 28 total guardrail aborts.
  # note (updated 2026-07-16): Day 18 elapsed (Day 15 of $0 streak), still $0.00.
  # +2 guardrail_aborts (7/16 morning + intraday). Risk-off for chips; rotation into
  # software/healthcare. TSM "sell the news" (77% EPS beat → shares -4%+) combined
  # with Kospi -7% chip contagion (echo of 7/13 pattern): SPY -0.53%, QQQ -1.63%.
  # Software/SaaS rotated INTO favor: CRM +3.40%, WDAY +2.55%, CTSH +3.17%,
  # INTU +5.38% (morning agent dismissed as "data unreliable" — EOD confirmed real).
  # ABT (Abbott Labs) +10.70% on confirmed Q2 earnings beat + raised FY2026 guidance
  # — best within-cap opportunity in system history (close $98.82 < $100 cap; named
  # catalyst; all eligibility filters passed; ONLY blocked by $0 buying power).
  # +5 stand-aside candidates: INTU (missed +5.38%), CRM (missed +3.40%),
  # WDAY (missed +2.55%), CTSH (missed +3.17%), ABT (missed +10.70%).
  # All 5 missed → stand_aside: 8/28 = 28.57% (down from 34.78%).
  # Structural misses: INTU (cap 2.95×), CRM (cap 1.67× + stale catalyst),
  # WDAY (cap 1.42× + no catalyst). CTSH (no catalyst; cap-eligible; possible
  # scan-depth gap). ABT: 100% cash-blocked, not a judgment failure.
  # CRITICAL: Day 15 of $0 balance. 30 total guardrail aborts.
  # CALL ROBINHOOD SUPPORT NOW: 1-800-279-1969. Ref account ●●●●9602.
  # note (updated 2026-07-17): Day 19 elapsed (Day 16 of $0 streak), still $0.00.
  # +2 guardrail_aborts (7/17 morning + intraday). Broad risk-off: SPY -1.00%,
  # QQQ ~-1.81%. Three converging bearish themes: (1) NFLX -7.39% on Q3 revenue
  # guidance miss (reported after 7/15 close; -11% intraday low); (2) TSM -2.82%
  # (Day 2 sell-the-news on 77% EPS beat; 2-day post-earnings total: -5.5%);
  # (3) UAL -2.87% on Q2 earnings miss. Energy outperformed (oil spike on Middle
  # East tensions). ABT +1.86% close (Day 2 of 7/16 earnings continuation; peaked
  # +4% intraday at ~$102.78 at 11am then faded 54% by close; any 11am entry
  # would have been a loss of ~$2.11/share by EOD). +4 stand-aside candidates
  # today, all correct: NFLX (avoided, -7.39%), TSM (avoided, -2.82%), UAL
  # (avoided, -2.87%), ABT (correct, +1.86%). First perfect-score stand-aside day.
  # stand_aside: 12/32 = 37.50%. 2-session alpha window confirmed for earnings
  # catalysts: ABT Day 1 +10.70%, Day 2 peak +4% fading to +1.86% close.
  # CRITICAL: Day 16 of $0 balance. 32 total guardrail aborts.
  # CALL ROBINHOOD SUPPORT NOW: 1-800-279-1969. Ref account ●●●●9602.
  # note (updated 2026-07-21): Day 21 elapsed (Day 17 of $0 streak), still $0.00.
  # +2 guardrail_aborts (7/21 morning + intraday). Chip-led risk-on day: MU +10.1%
  # (Morgan Stanley memory price recovery note; named, same-day, confirmed), NVDA
  # +~2% (Nebius stake). SMH +4.0%, QQQ +1.85%, SPY +0.83%, IWM +1.43%.
  # MU at ~$93-95 was within the $100 per-trade cap and passed all eligibility
  # filters — second consecutive within-cap, >10% catalyst win blocked only by $0
  # buying power (ABT 7/16 +10.70%, MU 7/21 +10.1%). No formal stand-aside
  # candidates evaluated — both routines aborted at cash gate. trading_days_elapsed
  # corrected to 21 (+1 for the 7/20 Monday that was incorrectly stubbed as
  # "Market closed - no activity (Sunday)" in the 7/20 post-mortem).
  # 34 total guardrail aborts. Stand-aside stats unchanged: 12/32 = 37.50%.
  # GOOGL/TSLA earnings scheduled for after-close 7/22 — key macro event.
  # CALL ROBINHOOD SUPPORT NOW: 1-800-279-1969. Ref account ●●●●9602.
  # note (updated 2026-07-23): Day 23 elapsed (Day 19 of $0 streak), still $0.00.
  # +2 guardrail_aborts (7/23 morning + intraday). Sharp risk-off: GOOGL -7.15%
  # (Q2 revenue beat but FY capex raised to $195-205B + negative quarterly FCF for
  # first time since IPO → "show-me AI ROI" sell-off); TSLA -14.62% (EPS miss);
  # SPY -1.23%, QQQ -1.89%. Chips followed lower on AI ROI uncertainty despite
  # GOOGL capex being structurally bullish: NVDA -1.58%, AMD -2.27%. XLE +0.33%
  # (only positive; Iran/oil theme session 11; WTI +3.8% premarket on Houthi
  # tanker attacks). NOW (ServiceNow) was formal stand-aside candidate: Q2 beat+raise
  # (+4.76% premarket) but structural blocker (share price ~$100.25 > $75 tier cap
  # = 0 whole shares). NOW closed -3.68% ($95.46 → $91.95) — "avoided" (risk-off
  # tape overwhelmed the earnings catalyst). +1 stand_aside candidate (avoided):
  # stand_aside: 13/33 = 39.39%. 38 total guardrail aborts.
  # SPY now -0.82% since system start (744.37 → 738.24).
  # CALL ROBINHOOD SUPPORT NOW: 1-800-279-1969. Ref account ●●●●9602. Day 19.
  # note (updated 2026-07-22): Day 22 elapsed (Day 18 of $0 streak), still $0.00.
  # +2 guardrail_aborts (7/22 morning + intraday). Mild risk-off pre-GOOGL/TSLA
  # earnings: SPY -0.13%, QQQ -0.52%, IWM -0.94%. GOOGL -1.46% during session
  # (pre-earnings de-risking; reports after close tonight). Chip sector diverged
  # positive: NVDA +2.30% (Nebius Day 2), AMD +1.42% (premarket -2.36% → full
  # intraday reversal, no fresh catalyst identified). XLE +1.17% on Iran/oil.
  # No formal stand-aside candidates — no S&P 500/Nasdaq 100 member cleared
  # 2%+ premarket threshold with named catalyst within $100 cap. Both routines
  # aborted at cash gate before eligibility screening. Stand-aside stats unchanged:
  # 12/32 = 37.50%. GOOGL after-hours $340.26 at 4:37 PM ET (ambiguous — possible
  # early post-print or pre-call after-hours drift). 36 total guardrail aborts.
  # CALL ROBINHOOD SUPPORT NOW: 1-800-279-1969. Ref account ●●●●9602.
  # note (updated 2026-07-24): Day 24 elapsed (Day 20 of $0 streak), still $0.00.
  # +2 guardrail_aborts estimated (7/24 morning + intraday — no Gmail Stand Aside
  # drafts found for today's routines; aborts presumed per established 20-day pattern).
  # Bifurcated tape: SPY +0.09% ($738.18 → $738.85; blue chips stabilized; Dow +0.5%),
  # QQQ -1.12% ($691.96 → $684.22; Nasdaq 100 extended decline, Day 2 of GOOGL
  # AI-capex sell-off; now -3.01% in 2 sessions from pre-GOOGL close of $705.35).
  # IWM -0.31% ($292.09 → $291.19). XLE +0.38% ($59.38 → $59.605) — positive
  # despite headline oil price plunge on Friday; possible geopolitical premium
  # embedding or value-rotation bid (first documented XLE-positive/oil-down session).
  # No formal stand-aside candidates — cash gate presumed to have fired before
  # any ticker evaluation. No Gmail drafts confirming routine runs found (anomalous
  # relative to 7/21–7/23 pattern; may indicate silent abort or non-standard subjects).
  # Stand-aside stats unchanged: 13/33 = 39.39%. 40 total guardrail aborts.
  # SPY -0.74% since system start (744.37 → 738.85). QQQ -3.01% in 2 sessions
  # post-GOOGL earnings — most sustained tech drawdown in monitoring window.
  # META earnings next pivotal binary event (expected late July).
  # CALL ROBINHOOD SUPPORT NOW: 1-800-279-1969. Ref account ●●●●9602. Day 20.

decision_quality:
  win_rate_pct: null           # set after first trade
  stand_aside_correctness_pct: 39.39   # 13/33
  stand_aside_count: 33
  stand_aside_correct: 13
  stand_aside_missed: 20
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
  # 2026-07-09 through 2026-07-13: no new formal candidates — cash gate aborted
  # before checklist reached on all days. Metrics frozen at 7/19 = 36.84%.
  # 2026-07-14: +2 candidates (morning routine ran eligibility checks before abort):
  #   AMD (+4.72% premarket) — INELIGIBLE (no fresh 24h catalyst); closed +2.48% →
  #     "missed" mechanically (>+2%), but catalyst-freshness screen correctly applied;
  #     AMD faded 47% of premarket gain by EOD, consistent with no-catalyst profile.
  #   AVGO (+2.66% premarket) — INELIGIBLE (Apple-Broadcom 6 days old, exhausted);
  #     closed +1.30% → "correct" (within -1% to +2% flat band). stand_aside: 8/21 = 38.10%.
  # 2026-07-15: +2 candidates (morning routine):
  #   ASML (+2.39% premarket) — INELIGIBLE (price $1,818 >> $100 cap, mandatory hard abort);
  #     closed +3.00% → "missed" mechanically, but not a judgment failure. Untradeable by rule.
  #   PYPL (+19.3% premarket) — INELIGIBLE (>15% premarket hard abort + unconfirmed catalyst);
  #     closed +17.21% from prior close but actually DECLINED from premarket ($56.51 → $55.52).
  #     Scored "missed" for consistency; >15% abort correctly applied — any premarket entry
  #     would have lost money by close. stand_aside: 8/23 = 34.78%.
  # 2026-07-16: +5 candidates (morning opportunistic scan + intraday identification):
  #   INTU (+5.38% premarket, flagged as data-unreliable) — cap 2.95× ($295); EOD
  #     confirmed +5.38% — morning "data unreliable" call was a methodology gap;
  #     structurally untradeable regardless. Scored "missed."
  #   CRM (+4.84% premarket) — cap 1.67× ($167) + catalyst 3 days old; closed
  #     +3.40% → "missed." Both disqualifiers structural; not a judgment failure.
  #   WDAY (+4.26% premarket) — cap 1.42× ($142) + no named catalyst; closed
  #     +2.55% (faded 40% of premarket move) → "missed." No-catalyst fade pattern.
  #   CTSH (+3.74% premarket) — no named catalyst; cap-ELIGIBLE ($43); closed
  #     +3.17% (held 85% of premarket move) → "missed." Possible scan-depth gap:
  #     a catalyst may have been missed; requires CTSH-specific follow-up search.
  #   ABT (intraday, +10.70% close) — FULLY ACTIONABLE (Q2 beat + raised guidance,
  #     same-day catalyst, close $98.82 within $100 cap, Tier 3 eligible). Blocked
  #     ONLY by $0 buying power. System's best opportunity in 18 days. "missed."
  #   stand_aside: 8/28 = 28.57%.
  # 2026-07-17: +4 candidates (morning negative scan + intraday identification):
  #   NFLX (-7.39% close) — Q3 revenue guidance miss; negative premarket; not a
  #     long candidate at any point; "avoided" → correct. Any long entry on NFLX
  #     today would have been a major loss.
  #   TSM (-2.82% close) — Day 2 sell-the-news continuation from 7/16 (-4%);
  #     not a long candidate; "avoided" → correct. 2-day post-earnings total: -5.5%.
  #   UAL (-2.87% close) — Q2 earnings miss; negative result + $118 above cap;
  #     not a long candidate; "avoided" → correct.
  #   ABT (+1.86% close) — intraday, Day 2 earnings continuation; peaked +4% at
  #     11am (~$102.78) then faded 54% to $100.67 close. Only blocker: $0 cash.
  #     Entry at 11am scan price would have been a loss of ~$2.11/share by EOD.
  #     "correct" (within -1% to +2% flat band). 2-session alpha window for
  #     earnings confirmed: ABT Day 1 +10.70%, Day 2 faded to +1.86%.
  #   All 4 today correct → stand_aside: 12/32 = 37.50%.
  #   First perfect-score stand-aside day in system history (4/4 correct/avoided).
  # 2026-07-21: no new formal stand-aside candidates — both routines aborted at cash
  #   gate before any ticker eligibility screening. MU (+10.1%) and NVDA (+~2%) noted
  #   informally but not formally scored (MU: cash gate fired before evaluation; NVDA:
  #   >cap at ~$212). stand_aside: 12/32 = 37.50% (unchanged).
  # 2026-07-22: no new formal stand-aside candidates — no S&P 500/Nasdaq 100 member
  #   cleared 2%+ premarket threshold with a named catalyst within $100 cap on this
  #   session. AMD (-2.36% premarket) and XLE (+0.97% premarket) noted but did not
  #   meet formal evaluation criteria. stand_aside: 12/32 = 37.50% (unchanged).
  # 2026-07-23: +1 candidate (morning opportunistic scan after cash-gate abort):
  #   NOW (ServiceNow, +4.76% premarket): EVALUATED — Q2 beat+raise (revenue +24%
  #   YoY, op margin 29.5% above guidance, FY guide raised). Named catalyst, last 24h,
  #   all eligibility filters passed EXCEPT trade size math (~$100.25 share price >
  #   $75 single-name tier cap = 0 whole shares for premarket limit order). Primary
  #   block: $0 cash. NOW closed -3.68% ($95.46 → $91.95) → "avoided" (risk-off
  #   tape overwhelmed strong earnings; bullet dodged). stand_aside: 13/33 = 39.39%.
  #   XLE (+1.72% premarket on WTI +3.8%/Houthi attacks): noted, NOT a formal
  #   candidate (below 2% premarket threshold). Closed +0.33% — threshold rule
  #   protective (buying at $60.22 premarket vs $59.40 close = -0.87% loss).
  # 2026-07-24: no new formal stand-aside candidates — no Gmail drafts found for
  #   today's routines (anomalous vs prior days). Both routines presumed to have
  #   aborted at cash gate before eligibility screening per 20-day pattern. Market:
  #   SPY +0.09%, QQQ -1.12%, IWM -0.31%, XLE +0.38%. No documented premarket
  #   movers above 2% with named catalyst. stand_aside: 13/33 = 39.39% (unchanged).

benchmark:
  spy_close_at_system_start: 744.37   # captured EOD 2026-06-22 (system's first tracked day)
  spy_close_today: 738.85             # EOD 2026-07-24
  spy_pct_change_since_start: -0.74   # (738.85 - 744.37) / 744.37 * 100
  system_alpha_vs_spy_pct: -99.26  # UNCONFIRMED — mechanical result of the unexplained $0 balance, not a skill signal. See financial note above.
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
