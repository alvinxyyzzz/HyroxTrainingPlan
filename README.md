# HYROX PERFORMANCE LAB · v1.4.1

**Release:** 2026-11-14. **Training-data snapshot verified through:** 2026-11-13 (NOT refreshed for this programming release).

**Live Web App:** https://alvinxyyzzz.github.io/HyroxTrainingPlan/  
**Google Sheets central training database:** https://docs.google.com/spreadsheets/d/1o48IfYCb14lNhEYOX8cgBFSrbD0CscJocKCYXgef8M0/edit

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
