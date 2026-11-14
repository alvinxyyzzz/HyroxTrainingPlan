# HYROX PERFORMANCE LAB · ALVIN

iPhone-first, static GitHub Pages dashboard for **HYROX Taipei 2027** (Fri 12 March Mixed Doubles, Sat 13 March Men's Open). Stable finish first; Sub-90 is optional.

## Open the app
https://alvinxyyzzz.github.io/HyroxTrainingPlan/

Tabs:
- **今日** – next/recovery session, single most important coaching decision, quick metrics.
- **分析** – Garmin running and FIT lap evidence, Petra results, with explicit limitations.
- **課表** – 17-week integrated HYROX classes: Force & Transfer, HYROX Engine, Petra sessions, AM/PM Long Run, adaptive recovery and Petra-intensity switches.

The frontend is `index.html` and reads `data/report.json` network-first. It is read-only; exercise logs are recorded in Garmin/Petra, never typed into the app. All CSS/JS/brand glyphs are inline; no third-party assets/scripts.

## iPhone app icon
- HTML embeds a fully self-contained **Base64 PNG** in both `rel=apple-touch-icon` and `rel=icon`. This mirrors the pattern used by CarbonPocket and ScreeningTool, avoiding an icon fetch for those references.
- `apple-touch-icon.png` in repo root is a **Safari fallback**.
- `icon-180-v7.png`, `icon-192-v7.png`, `icon-512-v7.png` are compatible PWA manifest icons. iOS may still require a fetched file for some installation paths, so retain the fallback.
- After changing an already installed icon, remove the old Home Screen shortcut, open the webpage again in Safari, and use **Share → Add to Home Screen**. No icon technique guarantees an iOS cached shortcut will update in place.
- Service Worker `sw.js` is versioned and uses **network-first** for `data/report.json`; cached reports are used only offline.

## Private data and weekly refresh
- Garmin Personal API credentials and authorization are **only** in the separate private repository `alvinxyyzzz/hyrox-garmin-sync` GitHub Secrets.
- Its Actions schedule checks Garmin daily at 09:15 Taipei time; manual on-demand refresh is possible. The Google Sheets central source is spreadsheet `1o48IfYCb14lNhEYOX8cgBFSrbD0CscJocKCYXgef8M0`.
- Petra photos stay in private Drive `Hyrox Training data/Alvin/Petra_Photos`. The already reviewed **35 files** are indexed in `Petra_Photo_Audit_v5` and `Petra_Photo_Registry`.
- The weekly coaching automation (Sunday 20:00 Asia/Taipei) should **list metadata only**, compare Drive file ID and modified time against `Petra_Photo_Registry`, and open **only new or changed photos**. Do not reprocess the 35 already analyzed images. Reuse the audit/history tables for past sessions. Keep activity IDs when joining Garmin records to avoid double counting.
- Weekly updates to this public repository should **only** publish aggregate analysis and four-week plans in `data/report.json`, never raw FIT files, personal routes/GPS, keys, or private photos. The UI does not read Google Drive or Garmin directly.

## Status vs. guarantees
A scheduled task being enabled is not evidence of a successful weekly revision. Each coaching update must report the latest actual Garmin Actions result, Google Sheets sync log, photo registry status, report commit, and Pages deployment. Distinguish **scheduled**, **executed**, **written**, and **published**.

## Repository privacy
**Public GitHub Pages is public.** Anyone with the URL can view the aggregate performance figures in `data/report.json`. For private analytics, change the hosting approach rather than putting sensitive data into the public repository.


## Two Connected Tracks v2.9.1 · 2026-11-14 Foundational Strength + Multi-station WOD

The public Web App has FOUR navigation tabs: **17-week roadmap**, **World Gym/Petra (strength + station main line)**, **Running (separate flexible line)**, and **Data**. Weekly selection is shared. DO NOT reintroduce user-input controls for Petra type, soreness, weakness, 5/6 days or extra replacement configuration. No complicated substitution text on workout cards.

### Single source of truth
- `data/report.json > trainingTracks`: two-track principles and provenance, authoritative as of 2026-11-13 Garmin/Sheets. Latest plan date 2026-11-14 may be newer than verified training data.
- `seasonPlan.weeks[].dailyPlan` = World Gym/Petra seven-day cards, Sunday→Saturday; each `{day,dayZh,date,kind,title,time,sections:[{name,lines,format}]}`. W01 Sun 2026-11-15, W17 Saturday 2027-03-13.
- `seasonPlan.weeks[].runningTrack` = independent reference weekly mileage range and THREE flexible run options: Easy Run, Long Easy, Interval/Threshold (except race week). Run entries are **not fixed to weekdays**; morning opportunities are welcome, distance ranges are guidelines rather than required quotas. Old `runningPlan` is a historical legacy field and not displayed.
- `weeks[].trainingIntegration` = how combined hard sessions are managed. Running Quality + WOD generally supply two hard stimuli. Tuesday Station intervals are controlled moderate intensity, not a third all-out HIIT session when running Quality is included.
- `weeks[].gymTrack` = metadata for the main gym/station track. `dailyPlan` remains the displayed class details.



### Friday WOD update: 16 distinct station workouts, not DB-only (2026-11-14)
- `data/report.json > seasonPlan.weeks[0..15].sessions[id=wod].classPlan.blocks[0]` and corresponding `dailyPlan[day=fri].sections` MUST remain in sync; daily cards are the public UI. W17 is actual 2027-03-12 Mixed and 03-13 Men Open and has no additional WOD.
- Examples: W01 3× Run 200m→Ski 150m→Farmer 25m→Row 150m; W02 4× Run 250m→Sled Push 10m→Sled Pull 10m→Row 150m; W03 4× Run 300m→Ski 200m→Carry 30m→Wall Ball 8; W05 Row+BBJ; W06 Sled+Lunge; W09 run-Ski-BBJ-Carry; W10 5×Run/Sled Push/Sled Pull/Row; W11 Lunge+Wall Ball; W13 partial race-order run bricks; W14 all 8 station mini simulation with 8×400m run and ~25–50% station doses; W15 reduced sharpener. W04/W08/W12/W16 deload/taper have short easy Station work, not hard WOD.
- Each non-race week has `dailyPlan[day=fri].wodRunKm`, `periodization.wodRunKm`, and `runningTrack.wodRunKm`. Total weekly running reference `runningTrack.targetKm` **includes Friday WOD planned run distance**; the independent morning running reference is `runningTrack.independentRunKmRange = total range minus WOD planned run km`. Count actual Garmin runs and actual Petra run segments, not both planned circuits and completed replacements. These are intended doses, never claims of completed sessions.
- WOD templates deliberately sample ALL eight HYROX stations plus running: SkiErg, Sled Push, Sled Pull, BBJ, RowErg, Farmer Carry, lunge, Wall Ball; they use the gym's confirmed sleds, Ski/Row, turf, wall ball and kettlebells. Sandbag availability is unverified, so use front-rack KB lunges; sled load must be scaled to local friction and actual technique rather than blindly prescribing race weight.
- HYROX official order is Race Run→Ski→Run→Sled Push→Run→Sled Pull→Run→BBJ→Run→Row→Run→Farmer→Run→Lunge→Run→Wall Ball. Mini circuits are training drills **not full race simulations**. The W14 eight-station rehearsal is a scaled run/volume session, followed by easy day-2 recovery checks; the user's separate quality-run session is easy that week.
- Evidence: official HYROX station standards <https://hyroxevents.zendesk.com/hc/en-gb/articles/38624619510941-Which-exercises-are-in-HYROX>; Centr HYROX Hybrid Strength 2026 plan <https://centr.com/blogs/features/hyrox-hybrid-strength-program-guide>; Centr HYROX station split examples <https://try.centr.com/programs/43149>; HWPO HYROX progressive programming <https://www.hwpotraining.com/programs/hwpo-hyrox>. Workouts are customized original prescriptions, not claimed to be copied from those coaches.
- The UI should keep two simple tracks (running/strength+station), seven Sunday→Saturday gym cards, no Petra question forms, no soreness questions. The 11/14 Push kickoff remains unchanged; W01 Wednesday is Pull. Weekly automation must not regenerate DB-only WODs, lose independent run accounting, or mix estimated/actual session completion.

### Saturday Nov 14 kickoff and week continuity
- **Kickoff class is on 2026-11-14 (Saturday)** and is explicitly visible in the roadmap and at the top of gym Week W01. It is a standalone full **Push hypertrophy + functional + Wall Ball/Sled Push technique** day (Bench 3×6–8, Incline DB 3×8–10, Shoulder 2×8–10, accessories + functional, then controlled station circuit).
- **W01 remains Sunday Nov 15 → Saturday Nov 21**. Do not shift the weekly Sunday-first convention or lose 17 full weeks up to the Mar 13 race.
- To avoid duplicate pressing immediately after kickoff, W01 Wednesday is **Pull hypertrophy + Pull Station**, Thursday is only an optional lighter Push accessory/Petra skill session. W02 Wednesday is Push, W03 Wednesday Pull as planned by progression.
- Running track remains separate and begins with W01 Nov 15, with flexible morning placement, not a Saturday-start week. A 2026-11-14 lifting kickoff does **not** count as an extra running workout.
- Public UI source is `seasonPlan.kickoff` for kickoff and `seasonPlan.weeks[0].dailyPlan` for W01; the kickoff must not be counted twice or be misreported as a completed workout. This is the scheduled workout; actual weights, reps and attendance require later confirmation.

### Foundation-lift periodization v2.9.1 — 2026-11-14

Keep squat, bench press, hinge/deadlift and vertical/horizontal pull as foundational movement families, not a mandatory checklist every workout.

- W01–03 foundation: squat and bench practice, row/pull volume; W03 conventional barbell deadlift technique 2×5 RIR4 on Wednesday and no Monday RDL. W04 deload.
- W05–07 strength build: repeat trap-bar deadlift as the SAME Monday anchor for three consecutive weeks (W05 3×6 RIR3, W06 3×5–6 RIR2–3, W07 3×4–5 RIR2). Squat secondary 2 sets; bench main or technique 2–3 sets weekly. Pull-ups/pulldowns and chest-supported rows continue. W08 deload.
- W09–11 HYROX transfer: reduce lifting volume to roughly 2 quality sets, W09 conventional deadlift 2×4–5 RIR3 as maintenance after W03 technique, Monday without RDL. W10–11 squat/bench with modest RDL to retain strength while Run-Station and WOD take priority. W12 deload.
- W13–15 specific: W13 trap-bar 2×4 RIR3–4 for maintenance. W14 no heavy deadlift during 8-station shortened simulation. W15 squat+bench 2 sets, no PR attempt.
- W16–17 taper/races: W16 bench/squat 1×5 RIR5 and no heavy hinge; W17 Fri mixed/Sat men's race without extra WOD.
- In each block the principal lifts come first with full rest (typically 2–3 minutes). Progress by adding a repetition OR small weight step only when proper form and planned RIR can be maintained, not both at once. Do not fabricate kg or 1RM; Strength_Log has no reliable actual loads.
- Never stack heavy trap bar, conventional barbell deadlift and heavy RDL in one week; back work also includes direct pulldown/rowing.
- Source of truth: `seasonPlan.weeks[].dailyPlan` (rendered), `sessions[].classPlan.blocks[0].steps` (mirrored), `periodization.strengthPhase/strengthAnchor`, and `trainingTracks.gym.strengthProgression`. Do not regenerate old rigid alternating trap vs conventional prescriptions in scheduled weekly reviews.
- Preserve Sunday–Saturday, 11/14 Push kickoff, two independent but jointly managed Running and Gym/Petra tracks, multi-station WOD, four deload weeks and W17 race week.
- Evidence: 2026 ACSM stand https://pubmed.ncbi.nlm.nih.gov/41843416/ and concurrent training review https://pubmed.ncbi.nlm.nih.gov/41762427/ . Block choices are coaching design, not claims that periodization is always superior when volume is matched.

### Gym Track: fixed Sunday→Saturday recommendation
Sunday low-intensity Ski/Row aerobic base; Monday Legs hypertrophy + unilateral stability and sled technique; Tuesday Ski/Row/Sled/Carry engine at controlled intensity; Wednesday Push or Pull hypertrophy + function; Thursday OPTIONAL complementary upper hypertrophy or Petra Strength/Skill; Friday ONE WOD (World Gym fallback or Petra WOD if actually attended); Saturday rest. W14 is shortened simulation plus light recovery day; W16 taper and W17 Friday/Saturday races. Strength classes start with mechanical tension then short relevant station circuits.

### Running Track: free scheduling and progression
Grounded in Garmin data through November 13 (64 logged activities, typical recent 12–16 km/week, one 25.84 km week; 2026-11-07 Easy 5.93km, HR143; 2026-11-13 run 5.86km, HR150). Program weekly volume guidance starts 12–16km, rises gradually as tolerated toward 20–26km across later blocks, includes deloads W04/W08/W12/W16, race-week no extra runs. Focus on sustainable Easy and Long sessions, one controlled quality session when recovery and station load permit. Do not infer precise training zones from single HR readings or treat one 25.84km week as baseline.

### Garmin and Petra verified context
Google Sheet `ALVIN HYROX | Central Training Database`, ID `1o48IfYCb14lNhEYOX8cgBFSrbD0CscJocKCYXgef8M0`, has Garmin_API_Activities, Garmin_API_Syncs, Petra_Whiteboard, Petra_Photo_Registry, Athlete_Notes, Strength_Log, Equipment_Inventory. 2026-11-10 Petra team AMRAP23, 17R+15 is TEAM score, Garmin HIIT 23:11 avg HR169/max192. 2026-11-12 intervals 5×~400m +4×~600m FIT-confirmed; 100 air squats are athlete-reported (not 100 Wall Balls). 2026-11-07 World Gym squat/trap-bar/lunge/Wall Ball/Ski are user-reported but verified kilograms, reps, RIR not yet available. Petra whiteboard photo by itself is NOT evidence of Alvin attendance; do not count shared team reps as individual score.

### Update safety
- When a new verified Garmin/Petra week arrives, update aggregated evidence and fine-tune both track prescriptions and shared hard-day load. Don't regenerate single-line station+running schedules, force the running track to fixed dates, or add back Petra questionnaires.
- Keep W04/W08/W12/W16 deloads, W14 shortened simulation, and W17 race-specific taper.
- Avoid raw FIT, GPS, precise route, private Google Drive photos, credentials or athlete-sensitive private notes in public repo; public aggregated information only.
- GitHub Pages deployment status must be checked independently of a successful GitHub commit. PWA cache must be bumped when UI changes.
