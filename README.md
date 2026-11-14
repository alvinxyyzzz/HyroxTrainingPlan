# HYROX PERFORMANCE LAB · v1.2

**Published:** 2026-11-14. **Training data verified through 2026-11-13.** This release changes programming, not the Garmin sync timestamp.

**App:** https://alvinxyyzzz.github.io/HyroxTrainingPlan/  
**Central database:** https://docs.google.com/spreadsheets/d/1o48IfYCb14lNhEYOX8cgBFSrbD0CscJocKCYXgef8M0/edit

## New fixed constraints

- **Petra WOD is ONLY on Wednesday**, optional, expected roughly once every two weeks. Actual attendance requires confirmation; a whiteboard photograph alone does not mean Alvin attended.
- **Petra Interval Running is on Thursday every week** (except race-week/taper adjustments). **NO World Gym on Thursday.**
- **Wednesday hard WOD + Thursday hard running interval must not both be full intensity**. If Wed WOD is hard, still attend Thursday class if appropriate but ask the coach to adapt to Easy / Technique at ~RPE4–5 or reduce the work to ~30–50% as tolerated. If Thu class cannot be adjusted, prioritize Thu quality running and skip Wed hard WOD.
- World Gym foundational **strength A on Monday and strength B on Tuesday**, with Tuesday primarily upper body and a flexible/light hinge if Wednesday hard WOD is possible. Friday is recovery / mobility. Saturday World Gym Ski/Row WOD is **optional only if no hard Petra WOD Wed and adequately recovered from Thursday**.
- Running remains a separate track: Thursday Petra class + 1–2 flexible Easy/Long Easy runs, with deload/symptoms controlling volume. Ski/Row may replace treadmill in World Gym WOD but do not count erg distance as run distance. Do not impose fixed 3 hard cardio days.

### Two-week flexible template

| Day | A: no Wednesday WOD | B: Wednesday Petra WOD |
| --- | --- | --- |
| Sun | Easy/Long run or easy Erg, flexible | Easy/Long run or easy Erg, recovery permitting |
| Mon | World Gym Strength A (legs/back) | World Gym Strength A |
| Tue | World Gym Strength B (upper/hinge) | World Gym Strength B, lighter legs |
| Wed | Rest or easy Ski/Row | Optional Petra WOD (Wednesday only) |
| Thu | Petra Running Interval (quality) **no World Gym** | Petra running class EASY/Technique after Wed hard WOD; full quality only if Wed was skipped |
| Fri | Recovery | Recovery |
| Sat | Optional World Gym Ski/Row WOD only if recovered | No second hard World Gym WOD after hard Petra Wednesday |

These are readiness-dependent templates, not a requirement to attend Wednesday WOD in particular numbered weeks. If user attends on a different Wednesday, classify according to actual attendance.

## Exceptions / periodization

- W01 post-11/12 calf recovery: Thu class can be adapted or skipped if symptomatic; no forced intervals.
- W04/W08/W12 deload weeks: no mandatory hard WOD, Thursday reduced to Easy/Technique.
- W14 special rehearsal: Wednesday preferably no hard WOD; **Thursday Petra Easy**, **Friday shortened 8-station simulation**, **Saturday Day-2 recovery test**. If Wed hard WOD occurs, Friday simulation must be removed or downgraded.
- W16 taper: Thursday easy or skip, no hard station WOD.
- W17 March 7–13 race week: **skip Thursday running interval**, Friday March 12 Mixed Doubles, Saturday March 13 Men Open (race entries/timing subject to official confirmation).

## Files and implementation

- Primary data: `data/report.json`, top-level `version: 1.2.0`, `planRelease.label: v1.2`, `scheduleRevision` fixed weekdays.
- Daily App cards: `seasonPlan.weeks[].dailyPlan`. Fixed Thursday card is marked `PETRA`/running and will not contain a World Gym prescription; Wednesday is optional Petra WOD or rest; Tuesday moved to WorldGym Strength B.
- Running track: `seasonPlan.weeks[].runningTrack` includes fixed Petra Thursday and conditional quality intensity; race week exception is clearly displayed. `sessions[id=interval]` is Thursday Petra running, `sessions[id=pull]` maps to Tuesday strength, `sessions[id=wod]` is conditional World Gym Saturday except W14 Friday simulation.
- Google Sheet tabs: `Training_Plan_v1_2_CURRENT` is the new active schedule, `Schedule_2Week_v1_2` contains A/B rules and exceptions, `Coaching_Rules_v1_2` contains decision policies. Previous v1.1 tabs remain for history; `WOD_Library_v1_1` is still valid exercise library since only WOD scheduling changed.
- Feedback: `Weekly_Review` has hard session count, Session RPE, calf/knee pain, Ski/Row volume, station quality and next-week adjustment. Future coaching review must use **v1.2** rather than deprecated v1.1.

## Privacy and freshness

The app is a **public GitHub Pages training program**, not a live Garmin or Google Sheets viewer. Never put private Garmin credentials, raw FIT/GPS, individual private whiteboard photos or sensitive personal notes into public repository. Garmin private sync code lives in `alvinxyyzzz/hyrox-garmin-sync`; v1.2 did not modify its schedule. A successful GitHub commit must be followed by Pages deployment verification. PWA cache bumped to `hyrox-v1-2-20261114-v26`.

## Prior release preservation

The v1.0/v1.1 17-week Sunday–Saturday calendar, strength phase emphasis, Garmin/Petra evidence and pre-race foundations are preserved where compatible. This update changes the **weekday placement and conditional intensity**, not the baseline measurements or verified workout history.
