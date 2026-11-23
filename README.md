# 2026-11-23 · Garmin × Petra 全歷史復盤｜Alvin coach plan v1.5.6 (PWA v39)

- **Current coaching source of truth:** private native Sheet [Training_Plan_v1_5_6_CURRENT](https://docs.google.com/spreadsheets/d/1o48IfYCb14lNhEYOX8cgBFSrbD0CscJocKCYXgef8M0/edit#gid=2115407852). New private [Coaching_Review_v1_5_6](https://docs.google.com/spreadsheets/d/1o48IfYCb14lNhEYOX8cgBFSrbD0CscJocKCYXgef8M0/edit#gid=1472542332) gives evidence, source reliability, and coaching rationale. Historical v1.5.1 preserved.
- **Public app prospective-plan overlay:** `data/coaching-v156.json`, W03–W16 only. `index.html` fetches it network-first and substitutes those weeks' 7-day prescriptions and running targets; `sw.js` v39 offline-caches this file, `data/latest-garmin.json`, and `data/report.json` with normalized cache keys. If overlay unavailable, original report plan remains readable.
- **Actual activity coverage:** Garmin Personal API year-by-year 2009–2026 returned 82 activities, all Sep24–Nov23 2026, 38 running sessions; last full history re-read 2026-11-23 13:38:43 UTC re-fetched all 82, zero new or changed summaries. Existing Garmin CSV overlaps and must NOT be added blindly.
- **Evidence integrity:** 38/38 runs have FIT Lap and minute-HR records, 14/14 Strength have FIT sets with weights/reps; team WOD scores NEVER individual performance, Petra photos (38 registered, 36 documented audit entries) cannot by themselves prove attendance. 18 historical Petra source-index rows were upgraded from stale missing-photo status to grounded photo classifications.
- **Restored training structure:** no regular Saturday Petra WOD; only Wednesday Petra WOD optional, Tuesday Strength optional, Thursday Interval optional. Athlete A/B/C whiteboards are educational reference, not Alvin attendance or training full-volume. 11/25 WOD unavailable due childcare; 11/28 one-off PFT; W03 after-PFT recovery 6–12km; W04 12–16km; W05 14–18km; W06 16–20km; W07 deload 12–16km; W08 15–19km. Dynamic option: Wednesday hard WOD -> Thursday Easy/Rest and Saturday no hard Station. Low-volume unilateral strength and calf stability replace, not add to, existing accessory work.
- **Privacy:** All historical daily wellness/HRV/sleep/BB/individual FIT data lives ONLY in private Google Sheet. Public Pages contains coaching prescriptions and previously authorized aggregate training count only. No personally identifying Garmin FIT/GPS or raw wellness records are pushed to GitHub.

---

# 2026-11-23 · Garmin full-source clarification / UI v38

The official Garmin Personal API does record real FIT strength repetition counts AND weights. Alvin private database: 14 strength sessions, 108 active sets, 107 containing weight, 4–70kg FIT-recorded values. Later edited exercise names in Garmin Connect are **not** available via current Garmin Personal API authorization (`exerciseSets` HTTP404 on two verified IDs), but do NOT say weights were missing. Original FIT first-ranked exercise candidates can be wrong.

Private database has 82 Garmin activity `summaryDTO` rows (including training loads) and 28-day recovery records (sleep, HRV, Body Battery, stress, RHR, VO₂max) and Garmin configured HR zones. Public app must NOT expose personally identifying biometric raw rows. Garmin current (2026-11-23) configured Z2 118–136 bpm, Z3 137–156; this is Garmin HR_MAX model, not validated LT1. 11/23 Easy Run avg149 was Garmin Z3, so use conversational/RPE assessment and avoid assuming prior HR135–145 is true Z2.

11/23 five recorded sessions: 5.897km run + 1.005km Ski + two strength activities (12 active FIT sets/109 reps, recorded kg) + 1.003km Row. Combined activityTrainingLoad ≈199.5. Recovery sleep score55, HRV38 Unbalanced, RHR53, stress41, BB latest14 => priority recovery Tue 11/24, no Wed WOD due to childcare, Thu easy only if recovered, Fri rest, Nov28 one-time PFT. Keep strength session-specific kg PRIVATE until exercises actually reconciled with user's Garmin Connect edits. Private source of truth: https://docs.google.com/spreadsheets/d/1o48IfYCb14lNhEYOX8cgBFSrbD0CscJocKCYXgef8M0/edit

---

# 2026-11-23 · Garmin 365-day reconciliation + W02 actual / PFT taper (UI v37)

- Central private spreadsheet: https://docs.google.com/spreadsheets/d/1o48IfYCb14lNhEYOX8cgBFSrbD0CscJocKCYXgef8M0/edit
- Private sync pipeline: `alvinxyyzzz/hyrox-garmin-sync` now calls `src.sync_reconcile`, upserts by Garmin Activity ID, hourly 3-day and weekly 365-day reconciliation.
- Verified private data: **82 Garmin activities / 38 running activities / 162.7743 km actual runs**, 2026-11-23 20:36 Taipei first full backfill added 4 afternoon sessions and refreshed 4 historic summaries. Second optimized 20:46 Taipei pass found 0 new/0 revised. Private audit log showed **14 optional detail warnings**; corrected Garmin Connect strength exercise sets were **not confirmed** (new optional table exists but is empty). Original FIT strength sets remain provisional estimates, never treat as actual edited exercise names/weights.
- Public aggregate snapshot: `data/latest-garmin.json` is a safe no-GPS/no-FIT summary. UI only overlays it when its `dataThrough` is at least as fresh as `data/report.json`, so a future automation can supersede old data. Do not publish raw Garmin personal records.
- **2026-11-23 actual:** 07:41 run 5.897km/38:24/HR149; 16:56 XC Ski Indoor 1.005km/5:22/HR149; 17:06 Strength 16:57/HR129; 17:28 Strength 3:48/HR147; 17:33 Indoor Rowing 1.003km/5:09/HR159. These are five Garmin IDs, not one workout; Ski/Row metres are not running kilometres.
- **W02 11/22–28:** Tue REST/recovery primary, optional light Petra Strength only if fully recovered. Wed **not attending WOD because childcare**. Thu optional short Easy/activation, no full hard Interval. Fri REST, Sat 11/28 **one-off PFT** (1km run / 50 BBJ / 100 stationary lunges / 1km row / 30 HR push-ups / 100 6kg WB). No recurring Saturday WOD.
- Keep today's special lower-body capacity card from previous conversation and user preference for long-term single-leg / calf stability, but **do not** mislabel suggested sets as Garmin-verified completed weights/reps. Replace, not stack, when fatigue is elevated.

---

# HYROX PERFORMANCE LAB · UI v37 / 2026-11-23 (data and training baseline retained)

**Live App:** https://alvinxyyzzz.github.io/HyroxTrainingPlan/

## 2026-11-23 · special recovery legs + persistent unilateral/calf microcycles (UI v37)

- Updated **existing GitHub Pages app**, keeping `data/report.json` and the existing 17-week training structure intact. This is not a new app.
- On **Monday 2026-11-23 only**, the weekly card displays a 60-minute low-fatigue lower-body session before optional Petra Strength Tuesday and the one-off Nov 28 PFT: Ski warm-up; barbell squat warm-ups 20 kg × 8 and 30 kg × 6, then up to 40 kg × 6 × 2 at RPE 4–5; bodyweight reverse lunges 2 × 6/side; low step-down 1 × 5/side; supported single-leg calf raise 2 × 8–10/side plus tibialis raises 2 × 12; SkiErg 6 minutes + RowErg 3 minutes easy; cooldown. No heavy sled/Wall Ball or jumps that day. Warm-up decision gate scales down to recovery cardio or stops as appropriate.
- **Normal later Monday sessions** expose a progressive unilateral strength / calf / ankle-reactivity accessory module, instead of stacking a new workout. If the underlying training prescription already includes unilateral work, the module does not add a duplicate unilateral exercise. Uses lower volume on W04/W08/W12/W16 deloads, and is suppressed in the Nov 28 PFT week and race week.
- Future loads should be calibrated to confirmed same-movement Garmin sets, with RPE as a second gate. The UI does not claim a new automated Garmin strength-weight model; private Garmin raw data and symptoms are not stored in public code.
- PWA cache key updated to `hyrox-weekly-board-20261123-v37`; existing plan, Petra Wed WOD optional status, one-time PFT, and Fri/Sat Taipei race details retained.


## Important scheduling correction · 2026-11-22

- **Petra WOD is a Wednesday class only.** A Friday or Saturday workout containing HYROX stations is **self-directed optional Station**, never labeled Petra WOD and never assumed attended.
- **Saturday has no recurring Petra class or recurring HYROX WOD.** Optional Station/Easy/Recovery is contingent on workload and actual Wednesday participation.
- **Saturday 2026-11-28 HYROX PFT** is a **one-time test**, goal 25 minutes. The app renders this on that exact date only; it should not propagate to subsequent Saturdays.
- The athlete program/whiteboard photos supplied on Nov 21 are for the coach to learn exercise progressions (Ski+Run, Lunge+Wall Ball+Run, Row+Run), **not Alvin's attendance, class booking, or a schedule to copy**.
- Petra Tuesday Strength and Thursday Interval are optional classes; the app is for **Alvin only**, not Stacy's schedule.
- The app's weekly UI is the default landing view, with a per-week Wednesday WOD attendance choice persisted locally, seven-day cards, PFT callout and a phone-friendly layout. This is an **interface/interpretation correction**; the existing 17-week plan and private training data were not overwritten. Any future data update must preserve these principles.
- Cache and installed PWA launch version advanced to v36.

---

# HYROX PERFORMANCE LAB · v1.5.5 (training plan base v1.5.1, cardio transfer v1.5.5)

**App data updated:** 2026-11-18 (Petra WOD + Garmin FIT-minute HR analysis and six-week WB/Ski/Row transition v1.5.5); 74 Garmin activities / 36 runs / 150.25 km actual running / 231 FIT laps, 38 audited Petra photos.

**Live Web App:** https://alvinxyyzzz.github.io/HyroxTrainingPlan/  
**Google Sheets central training database:** https://docs.google.com/spreadsheets/d/1o48IfYCb14lNhEYOX8cgBFSrbD0CscJocKCYXgef8M0/edit

## 2026-11-18 · v1.5.5 Petra WOD and 6-week cardio transfer

- Petra photo IMG_1755.HEIC audited: Nov18 AMRAP30 Ski/HR Push-up/Row/15 Wall Balls/350m run/90s rest, Alvin 3R+45. Three full rounds suggest 45 WB and ~1.05km internal running (photo-based, NOT Garmin run km); +45 is total score units, not 45 more Wall Balls. WB weight unknown.
- Garmin HIIT 25117883969 30:04 avgHR170, max211 possibly isolated wrist artefact, TE aerobic3.6/anaerobic3.2. Private minute HR shows early ramp, later resting valleys around 141/145/152. WOD after-run 25118351864 5.0583km/30:51 avgHR162, 5km HR153→168. Weekly actual Garmin run 16.7587km from Nov16/17/18, NOT counting WOD internal distance.
- Week01 Thu hard Petra running and Sat main Station cancelled; avoid extra Long Easy, as hard Wed WOD and run completed. Private Sheet Cardio_Transition_v1_5_5 defines Weeks01–06 controlled Ski→WB→Row moderate transfer replacing original Sat main, only when Wed hard Petra WOD absent; WB reps 18→24→12 deload→24→32 (6kg) included in the main station, not stacked.
- Garmin GitHub Actions hourly UTC minute23, scheduled short three-day backfill, manual backfill available. Private Garmin_API_HR_Minute contains FIT 60-second HR summaries (no GPS/tracks), and on-demand workflow + minute backfill both succeeded. GitHub schedule may be delayed.

## 2026-11-17 · v1.5.3 all-data refresh and Petra audit reconciliation

- Manually triggered existing private Garmin sync via `sync-now.request` at 05:17 Taipei; GitHub Actions success, final sync `2026-11-16T21:20:55Z` (05:20 Asia/Taipei). The retry checked 70 activities and added 0 new; compared with prior App snapshot, 2 extra Garmin activities / 2 FIT laps on 2026-11-16 are now represented.
- Verified totals: **70 unique Garmin activities**, **34 running activities**, **139.34 km** genuine running and **218 FIT laps**. Newest two records are Nov 16 Strength 12:27 (36:04 elapsed, HR avg102/max147) and XC Ski Indoor 13:04 (10:44 elapsed, HR avg165/max178); Ski distance/watts were unavailable and are not invented. Nov 16 morning Easy Run 5.8532km / avgHR141 remains counted once.
- Petra photo folder unchanged: **37 audited/registered photos**, most recent IMG_1702.HEIC from Nov 10 session, uploaded Nov 13. No newly modified photo as of Nov 17. **13 stale historical `Petra_Whiteboard` pending rows** were aligned to `Petra_Photo_Audit_v5`; preserve score caveats, team-only scores and uncertain individual attendance.
- Updated public `data/report.json` to v1.5.3, including accurate dashboard totals, coaching analysis cards in the `{title,body}` shape expected by `index.html`, and W01 Tue Nov 17 optional Easy Run/Ski being skipped after Nov 16 combined training. Wed is recovery; Thu Petra run is scaled to physical readiness. **No structural changes to the 17-week periodization or future Long Easy progression.**
- Private `Athlete_Notes!A6:I6` records source IDs and unknown fields; do not infer World Gym/Petra attendance, Ski distance or symptom resolution from the Garmin activity name or HR. The public app holds summary only, no raw Garmin FIT tracks or private Petra images.

## 2026-11-16 · v1.5.2 Garmin Easy running review

- Private Garmin sync succeeded: new running activity 25092581863 / 5.8532km / 39:02 / avg HR141 / max HR157 / aerobic TE2.6, +6 FIT laps.
- Overall through 11/16: 68 unique Garmin activities, 34 running activities, 139.34km actual run distance, 216 FIT laps; 11/09 week revised to 19.95km, 11/16 partial 5.85km.
- HR zones based on %Max HR, %HRR or %LTHR are **not yet verified** for this athlete. **135–145bpm is only a preliminary Easy observation band**, not an established Z2 border. Flat Easy pace starts around 6:40–7:20/km, slower/run-walk as needed; prioritize conversational RPE2–4.
- W01 Nov 16 easy 5.85km is already this week's Long Easy. Conditional long-run progression W02 6.5–7km, W03 7–7.5, W04 6–6.5 deload, W05 7.5–8, W06 8–8.5, W07 8.5–9, W08 7–7.5 deload, W09 9–10km if recovered. Flex scheduling, keep 1 Petra quality run and optional short Easy.
- Public App `data/report.json` updated with today's 6 laps (summaries only) and a compact running-tab coaching guide. `Running_10K_v1_5_1` central Sheet Long_Easy_1x rows W01–W09 updated. No changes to strength/station workouts.

## 2026-11-15 · v1.5.1: World Gym available equipment

**High intensity Station = RowErg + SkiErg**. The athlete's cycling-machine example was illustrative, not equipment available in World Gym.

- **W05**: 3 × (RowErg **5 min RPE6–7** → SkiErg **1,000 m RPE7.5**); rest **2:30** each round.
- **W10**: 3 × (RowErg **5 min RPE6–7** → SkiErg **1,500 m RPE8**); rest **3:00** each round.
- **W15**: 2 × (RowErg **4 min RPE6–7** → SkiErg **800 m RPE7**); rest **2:30**; taper/sharpen.
- Longer Ski 2 km × 3–4 is a later optional advanced benchmark; not a current compulsory workout.
- One hard engine session **replaces** a regular Station main, never stacks atop Wed hard Petra WOD or Thu hard run when recovery is insufficient. The 10K 50:00 / 5:00km independent running goal is unchanged.
- App still shows short actionable menu in Strength/Station and flexible running milestones under Running; device-level loading updated to v34.


## 2026-11-15 · v1.5 | 10K 50:00 + RowErg × SkiErg

**Standalone running goal:** 10 km in **50:00 (5:00/km)**, aspirational rather than guaranteed; HYROX doubles and single remain separate race goals. Train using real Garmin running, not a blanket 5:00/km pace for Easy runs. Keep one run quality stimulus (usually Petra Thu), one movable Long Easy, and an optional short Easy. W01–04: easy base; W05–08: 6–8km comfortable / selective 800m repeats only at current fitness; W09–12: work toward 8–10km Easy + controlled 1km intervals; W13–15: optional longer repeats at ~5:05–5:15/km if ready; W16–17 taper and HYROX racing. Verify the full 10K 50:00 ability independently after recovery if needed. Erg metres are not running kilometres.

**High-intensity Station main replacements — NOT extra workouts:**
- **W05** 3 × (RowErg **5min** → SkiErg **1000m**), ~RPE7, 150 sec between rounds
- **W10** 3 × (RowErg **5min** → SkiErg **1500m**), ~RPE7–8, 180 sec between rounds
- **W15** 2 × (RowErg **5min** → SkiErg **1000m**), ~RPE6–7, 180 sec between rounds, sharpening not maximal

The original advanced workout of **3–4 × (5min Fan Bike + SkiErg 2000m)** is a **future benchmark**, not imposed immediately. This keeps the original Row/Sled/Carry/Lunge/BBJ and run-station work in other weeks. If Wed hard Petra WOD was actually attended it substitutes for Sat main, and Petra Thu running must be scaled. If calf/knee symptoms persist, defer high-intensity work.

**Equipment check:** the World Gym fan bike/RowErg presence is **NOT VERIFIED**. The App prescribes a simple alternative when unavailable: **RowErg 5min → SkiErg** (same round count and RPE), and the private equipment inventory is marked unverified.

**Data:** current source is `data/report.json` v1.5.0, with `tenKPerformanceGoal`, 17 individual `runningTrack.tenK50` entries, and `rowSkiSkiWorkout` in W05/W10/W15. Native Sheet tabs: `Training_Plan_v1_5_CURRENT`, `Running_10K_v1_5`, `RowErg_Ski_v1_5`. Old tabs kept for history. Plan updates do not constitute new Garmin/photo sync.

## UI correction · 2026-11-15 · Full seven days + flexible running (v32)

At the athlete's request, the **力量／Station** screen once again shows **all seven day cards (Sunday–Saturday)**. Do NOT filter out Sunday or Thursday merely because there is also a separate running page. **Station sessions, such as SkiErg, RowErg, Sled Push/Pull, Farmer Carry, Wall Ball, BBJ, Sandbag Lunges and Run→Station, must have their actual rounds/distances/reps visible here**; the running page is not a replacement for Station prescriptions. W07/W09/W11/W13 Run→Station and W14 shortened rehearsal are rendered from their structured `stationPrescription` / `runStationTransition` instead of hiding as generic fallback text.

- **Sunday** is a flexible slot with `Long Easy Run (can move days)` OR easy `SkiErg + RowErg` OR standalone RowErg/swimming OR the optional Petra Strength/Skill (max one SUN/MON/TUE). The athlete does NOT have to run specifically on Sundays, and Sunday easy stations are not a second full-intensity Station main.
- **Thursday** can show the existing Petra running class inside the seven-day overview. The independent **跑步** page prescribes *weekly amounts*: one quality run (usually Thu Petra), one Long Easy on any feasible day and an optional third short easy on any suitable day. Neither Long Easy nor short Easy is obligatorily scheduled on Sunday/Tuesday.
- **Station prescription stays on 力量／Station:** standard 4–5-round main stations remain visible with work/rest and actual station list; controlled Run→Station weeks include actual run distance, number of rounds and specific stations; never display only `依當週主課安排` when structured station data exists.
- The user prefers compact whiteboard-style exercise menus. One short rationale only if meaningful; omit long injury/recovery explanations in the UI while preserving coach-side rules. If a Wednesday hard Petra WOD is confirmed, it substitutes the Saturday hard station and affected strength days can be swapped after user feedback.
- This UI version makes **no new Garmin sync** and does **not** alter private Sheet data or the 17-week prescribed training plan.

Asset keys: `hyrox-v1-4-1-week-full-20261115-v32` and `./?app=v141-week`.

## 2026-11-14 · UI v31: concise workout menu, standalone running guide

At the athlete's request, the **力量／Station** page shows **only Mon/Tue/Wed/Fri/Sat strength and station cards**; Sunday Long Easy and Thursday Petra running belong on the separate **跑步** page. Each card presents a short list of actual movements with sets/reps/RIR and, at most, one useful scheduling note. No duplicate warnings, coaching essays, intake form or status questionnaire. Never invent absolute kg without verified athlete load records.

The **跑步** page now provides (a) this week's Thu Petra quality run + Sun Long Easy + optional Tue short Easy, (b) six race preparation stages over W01–17, and (c) low-impact substitution options: steady SkiErg / RowErg / swimming 25–35min at RPE3–4, or Ski 5min + Row 5min ×3 at easy pace. For W01, where the athlete recently reported calf fatigue and strength+sled stations, the option shown is easy Ski 10–12min + Row 15–20min, or easy Row alone. Do NOT make an easy day a maximal AMRAP/EMOM. An erg interval substitute such as 4×3min RPE7 / 2min easy is for recovered weeks only when it replaces—not stacks on—the Thu quality run or Wed hard WOD. Erg miles and metres never count as actual running mileage, and long-term running economy still requires running.

The days in the athlete's verbal example are **hypothetical, not confirmed attendance**. If they later confirm Wed hard Petra WOD, the coach can switch Mon Legs to Pull and defer Legs so there is adequate time to recover. Do not hardcode WOD attendance from a whiteboard photo. Chat-reported feedback should influence future plan revisions; no user-facing training intake controls.

This UI-only release retains existing `data/report.json` v1.4.1 (17-week plan, coach-side recovery model), Google Sheets, Garmin/Petra sync cadence. Cache now `hyrox-v1-4-1-simple-run-20261114-v31`, launch `./?app=v141-run`.

## 2026-11-14 v1.4.1 update — Easy aerobic, Wall Ball, calf-aware recovery

- **Private manual-workout handling:** An untracked, user-reported training session is recorded only in the private Google Sheet (`Athlete_Notes` / `Strength_Log`). Do not publish private session loads, subjective symptoms, or other detailed athlete notes in this public repository; do not fabricate Garmin activities or measured heart rates.
- PPL remains **Mon LEGS / Tue PULL / Fri WFH PUSH**, Thu Petra Interval, Wed optional Petra WOD, Sat Station or safe RunStation, Sun flexible Easy. The addition is **aerobic talk-test work** (easy, able to speak full sentences), **controlled Wall Ball sets with deliberate exhale on the throw and small rest breaks before technique fails**, and **Step-up / controlled Split Squat + Leg Curl** replacing existing Mon LEGS accessories, not an extra high-intensity session.
- Until calf soreness settles, do **not** schedule high-volume Wall Balls, heavy sled pushes, BBJ or hard running if walking, single-leg calf raises, gait or swelling indicate a problem. Use pain-free low-impact easy work/rest, and seek professional evaluation for persistent or abnormal symptoms. Do not diagnose an elevated subjective heart rate as low VO2max or cardiac illness; follow exercise red flags.
- Record valid Wall Ball repetitions and per-set effort, plus time to comfortably speak a complete sentence again; if a watch was actually recording, add measured HR and HR change one minute post-set for comparable training, recognizing wrist-based exercise artifacts. **Unknown measured HR remains unknown.**
- New current Google Sheets tabs: `Training_Plan_v1_4_1_CURRENT`, `Cardio_WallBall_v1_4_1`, `Sync_Cadence_v1_4_1`; v1.4 tabs preserved as historical references.

### Actual data processing cadence

- **Nov 15–30, 2026:** private Garmin Actions sync **daily about 09:15 Asia/Taipei**, subject to GitHub Actions schedule drift. A separate AI task checks Garmin+Petra Drive photo deltas **daily about 20:00** and updates analysis/app when authenticated access and genuinely new data permit.
- **From Dec 2026:** Garmin private workflow syncs **Sunday about 09:15**, and the existing weekly HYROX AI coaching task runs **Sunday about 20:00** (first Dec 6).
- Private workflow `.github/workflows/garmin-sync.yml` uses date-gated Nov daily and Dec Sunday scheduled triggers; manual `workflow_dispatch` and restricted `sync-now.request` trigger remain intact.
- Each AI run reads only metadata for Petra photos first, processing ID/modifiedTime deltas not re-OCR-ing historical analyzed images. Verify the actual Garmin run, Sheets new rows, photo Registry, public report commit and GitHub Pages success independently. Schedule configured ≠ successfully synced/processed/deployed. **At the time of update, future runs had not yet taken place.**
- Existing Sunday automation was moved to Dec 6 and amended. A separate daily-Nov automation ends Nov 30 automatically. The public app only shows a static published snapshot and device-local options; scheduling does not create a browser-resident service.

## Why v1.4

v1.3 corrected the weekday schedule and separated Legs/Pull/Push, but it still trained too few race-specific stations (especially Burpee Broad Jump, Sandbag Lunge and Wall Ball) and treated running and stations as mostly disconnected. v1.4 delivers a race-specific, periodized 17-week plan with explicit cumulative station exposure, conditional 400–800m run→station→run sessions, a third short easy run when recovered, and an **uncluttered weekly workout view with coach-side readiness rules**.

**Critical distinction:** Training prescriptions are **planned**, not completed sessions. Coach-side readiness decisions use actual user reports and available authenticated training logs, not guessed attendance or self-reported browser toggles.

## Fixed user constraints

- **World Gym PPL:** **MON LEGS** (Squat + Hinge), **TUE PULL** (Pulldown + Row), **FRI PUSH** (Bench/Incline/Shoulder). Friday is typically WFH and World Gym is **high-probability**. Push exercise loads can be downscaled when fatigue is high.
- **Petra Strength/Skill:** ONLY SUN or MON or TUE, **at most one class among those days per week**, entirely OPTIONAL. Its confirmed actual work replaces corresponding WorldGym muscle work, not an extra required workout. Low-intensity Skill is not automatically equivalent to heavy Strength. If Sun Petra, Long Easy may shift or shorten. Tue Petra removes the suggested Tue AM third easy run.
- **Petra WOD:** WEDNESDAY ONLY, approximately alternate weeks if attended; never infer attendance from class whiteboard photos. If Wed Petra WOD was hard, Thu Petra running scales to Easy/Technique and **SAT main Station / RunStation is cancelled**; if Thu class cannot scale, prefer skipping Wed hard WOD beforehand.
- **Petra Running Interval:** Every THURSDAY, **NO World Gym Thursday**; Thu is the primary running quality class if not preceded by hard Wed Petra WOD. W16 taper reduces it and W17 race week skips it entirely.
- **Running:** Sun movable Long Easy, Thu Petra Interval, **Tue AM short Easy 15–35 min preferred if recovered** (optional, skip when Mon Legs DOMS, Petra Tue, planned Wed hard WOD, injury warning, lack of recovery). Garmin counts only actual running. Do not force target kilometers from prescribed weekly ranges.
- **One main HYROX station session:** Typically Saturday (unless W14 special Friday rehearsal). **Choose one** of a 4–5-round indoor Ski/Row/Sled/Carry/WB station main OR an outdoor safe, actually connected Run→Station workout. Do not stack both. If Wed hard WOD attended, it substitutes for the main station.

## Race-specific training, safe venue requirement

Official HYROX format: **8×1km runs**, with stations in fixed order SkiErg 1000m, Sled Push 50m, Sled Pull 50m, Burpee Broad Jump 80m, Row 1000m, Farmers Carry 200m, Sandbag Lunges 100m, Wall Balls 100. Mixed Doubles and Men Open division equipment goals must follow the official **current** race rulebook and actual local surface friction: for the 2025/26 Men/Mixed rules, **Carry 2×24kg, Lunge 20kg, WB 6kg, Sled Push total incl. sled 152kg and Pull total incl. sled 103kg**. Do not assume that displayed local gym plates are equivalent to including-sled competition loads.

**Special transition weeks** (training prescriptions, not guaranteed feasible at every facility):

| Week | Main work (outdoor only with safe contiguous venue) | Running volume if actually performed |
|---|---|---:|
| W07 | 3 × (400m run → one short BBJ/Lunge/Carry station) | 1.2km |
| W09 | 3 × (600m run → short station, then next run) | 1.8km |
| W11 | 4 × (600m run → station) | 2.4km |
| W13 | 4 × (800m run → controlled station) | 3.2km |
| W14 | **FRI** 4 × (600m run → abbreviated stations), Thu Petra Easy, Sat Day2 recovery | 2.4km |

All transition work is a **replacement for** the regular station main, NOT a third hard metabolic session. The trainee must have a safe connected outdoor loop with legal access to nearby station equipment. **Never move World Gym equipment outdoors, cross active roads, or present separate gym work and outdoor runs as seamless transition.** If safe connected transition is unavailable, the Web App clearly offers a safer alternative: low-impact indoor stations and/or independent safe outdoor easy run with bodyweight technique only. No treadmill needed inside World Gym.

**W14 station-only fallback:** shortened eight-station flow (including BBJ/Lunge/WB) without 8×1km run. **This is not a full HYROX simulation** and cannot directly predict finish time.

## Progressive eight-station coverage

Each W01–16 stores `weakStationSkill` and `stationCoverage`, clearly distinguishing weekly **reference upper limits** from training actually done:

- **Burpee Broad Jump:** recover → short technique 3–5m → accumulate 20–30m → 40–60m in controlled weeks if landing quality/pain gate passes. Track **actual total metres**.
- **Sandbag Lunge:** unweighted controlled reps → 10kg technique → 15kg → 20kg only when competent and pain-free, progressive **actual metres × load**. Men/Mixed published race load 20kg; not a mandatory immediate gym load.
- **Wall Ball (6kg):** current continuous capacity approximately 10–15 reps. Practice short clean sets, build **valid weekly total** 32 → 40 → 50–60 → ~70–80; **W13 partitioned 100-rep rehearsal only if readiness and movement quality support it** (e.g., 10×10; otherwise stay 80). Never demand 100 unbroken or every week.
- **SkiErg:** repeated 350–500m controlled splits with priority over Row for skill/efficiency; optional longer 1000m sustained test only after recovery.
- **Row, Sled, Carry:** periodized technical workloads with timing, friction/load accuracy and carry grip. Track actual pace, load/surface and valid movement standard.

Friday may include an **8–12 minute low-intensity technique microdose for only one station category**, but it is NOT compulsory and must be counted toward (not added on top of) the weekly Station/Wed Petra amount. Traditional 0–2 easy rounds after strength are only technique finishers, not a main station session.

## Recovery and training adjustments (coach-side; clean App)

On 2026-11-14 the App UI was simplified at the athlete's request: **remove the three large weekly status / weak-station / aerobic-WallBall dashboard cards** and the user-operated dropdown controls. Training/weak-point/progression/readiness prescriptions remain in the structured private training plan and source JSON for the AI coach to use when the athlete reports actual session completion, fatigue and symptoms.

The **力量／Station** screen now prioritizes **weekly selector → seven daily workout cards**. Each daily card shows the most relevant exercises, sets/reps and main goals; an optional `查看完整課表與注意事項` section keeps expanded details hidden by default, without deleting the coaching prescription. Recovery logic is still applied by future coach reviews after verified data or direct feedback, not as a required survey in the App. Do not assume a Petra whiteboard means attendance.

Progression gate per week:
- **Progress one variable** only after ≥90% technically valid planned main work, stable erg splits (initial monitoring target ≤5–8% variation) and no next-day worsening.
- **Hold** if recovery is inadequate or Wed/Thu/Sat hard overload.
- **Reduce/stop provocative work** if pain increases, affects gait, causes swelling, or recovery deteriorates. Pain numeric thresholds are planning cues, not medical diagnosis.

## Periodization and race week

- Foundation W01–03; recovery/deload W04; build W05–07 with first safe run-station W07; recovery/deload W08.
- Transfer W09–11 with safe transitions W09 and W11; recovery/deload W12.
- Specific W13 (safe 4×800m), W14 (Friday limited rehearsal + Saturday recovery), W15 sharpening Station; W16 taper.
- Race W17 **Mar 7–13, 2027**: Friday Mar12 intended **Mixed Doubles** and Saturday Mar13 intended **Men Open**, subject to individual confirmed registration/wave times. Official **HYROX Taipei event runs Mar12–14**, with provisional Friday afternoon Mixed and Saturday Men Open windows; final specific start times are not yet published. Thu Mar11 Petra intense Interval is SKIPPED.
- No full eight 1km runs plus all eight stations training simulation has been prescribed; prioritize safer partial race adaptation and two-day recovery.

## Mixed Doubles with Stacy (optional, NOT extra training volume)

The user plans **Friday Mixed Doubles together with Stacy + Saturday Men's Open solo**. A solo-only plan is incomplete without short, controlled partner switching drills, but a separate extra full WOD would be an overload. **W06/W10/W14/W15** therefore contain an optional in-session substitution: when Stacy is available, replace some existing Station main work with a partner relay rehearsal. Otherwise complete the solo Men Open main session as written.

- Official principle: **both partners run together**, enter and leave stations together; stations are **You-Go/I-Go**, with only one actively working at a time and no mandatory 50/50 split. [HYROX official Doubles FAQ](https://hyroxevents.zendesk.com/hc/en-gb/articles/40274430499229-How-are-the-workout-reps-split-between-Doubles-partners).
- **SkiErg** Alvin starts. **Sled Pull** Alvin starts; keep workload near balanced without forcing Stacy to do much more. **Sled Push** Stacy is the stronger partner, so can take somewhat more of short sections when appropriate. Do not force maximal loading.
- **Row** practice **two switches** over a shortened 500m drill: Alvin 200m → Stacy 200m → Alvin 100m. In race day division, adapt to the full 1000m and fatigue.
- **Farmer Carry** practice **three switches** across 80m: Alvin25 → Stacy20 → Alvin20 → Stacy15, giving Alvin slightly more carry distance. For race, adapt to complete 200m.
- **BBJ** train short bursts **4–7 jumps per turn** to protect leg fatigue, subject to landing/nerve/knee recovery. **Wall Ball 6kg** short splits like Alvin12 and Stacy8 if technique is valid; Alvin may do somewhat more. Lunge use shorter balanced 10–15m turns.
- Friday doubles followed immediately by Saturday solo means **do not exhaust legs on the practice day**. W14 rehearses a shortened session, Saturday easy recovery, and W15 sharpening rather than maximal double day training.

Google Sheets: **`Mixed_Doubles_v1_4`** is a companion training reference. All sessions are optional and rely on Stacy attending; **never infer partner attendance or create fake completed activity records**. Rules/weights must be re-checked against the 2026/27 competition documents.

## Data and sync architecture

- App primary `data/report.json`: `version: 1.4.0`, `planRelease.label: v1.4`, 17 weeks with `runStationTransition`, `weakStationSkill`, `stationCoverage`, `progressionGates`, `readinessRules`, `weeklyQualityBudget` and `runningTrack.thirdEasyRun`.
- App UI `index.html`: simplified **weekly selector + daily workout cards**, with optional native expanded details; no user status form or standalone weak-station/aerobic info cards. The coach continues to use `readinessRules` and reported feelings internally. Running/analysis tabs remain; static site must not claim live training sync.
- `sw.js` cache key **hyrox-v1-4-1-lite-20261114-v30**, `manifest.webmanifest` launch `./?app=v141-lite`.
- Google Sheets: `Training_Plan_v1_4_CURRENT` active, `Run_Track_v1_4`, `Run_Station_v1_4`, `WeakStations_v1_4`, `Readiness_Rules_v1_4`, `Coaching_Rules_v1_4`. Older versions retained in separate tabs.
- `Weekly_Review` appended T:AB columns for actual BBJ metres, lunge metres/load, valid 6kg Wall Ball reps, actual compromised running kilometres and post-station pace notes, sled loading, confirmed Petra attendance, and readiness.
- **No new Garmin API call**: latest confirmed imported data still through **2026-11-13**. The private `hyrox-garmin-sync` repo and existing Sunday automation were NOT modified, so do not claim the automation already consumes v1.4. Future weekly review should explicitly reference `Coaching_Rules_v1_4` and latest actual logs when that automation is updated.

## Sources

- [HYROX official format & stations (Aug 2026)](https://hyroxevents.zendesk.com/hc/en-gb/articles/38624619510941-Which-exercises-are-in-HYROX)
- [Official HYROX 2025/26 division rulebook (Men and Mixed)](https://hyrox.com/wp-content/uploads/2025/06/25-26-Doubles-Rulebook_en-R1.pdf)
- [Official HYROX Taipei 2027 event & provisional schedule](https://hyrox.com/event/hyrox-taipei/)
- [ACSM 2026 resistance training position stand](https://pubmed.ncbi.nlm.nih.gov/41843416/)
- [2026 concurrent resistance + endurance training umbrella review](https://pubmed.ncbi.nlm.nih.gov/41762427/)

**Privacy:** GitHub Pages is a public read-only snapshot. Keep private Garmin credentials, raw GPS and FIT data, private coaching notes and personal Petra photos out of the public repo. Local UI settings are private to the device/browser unless someone uses the same device.
