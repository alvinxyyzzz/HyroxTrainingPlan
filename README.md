# HYROX PERFORMANCE LAB · v1.1
**Release:** 2026-11-14. **Data verified through:** 2026-11-13 (64 Garmin activities + 37 Petra photos). Version upgrade does not imply fresh Garmin Connect sync.

**Web App:** https://alvinxyyzzz.github.io/HyroxTrainingPlan/  
**Repository:** https://github.com/alvinxyyzzz/HyroxTrainingPlan  
**Authoritative structured log:** [ALVIN HYROX Central Training Database](https://docs.google.com/spreadsheets/d/1o48IfYCb14lNhEYOX8cgBFSrbD0CscJocKCYXgef8M0/edit)

## v1.1 changes (supersedes v1.0 coaching prescriptions)

- **Petra WOD optional about once every two weeks.** Only actual attendance counts; a photo or planned class is not an automatically completed workout. If Petra WOD is high intensity, it **replaces** the weekly World Gym WOD or other quality session. Never stack two WODs as default.
- **One World Gym WOD weekly when no Petra WOD**, with **no mandatory treadmill**. Use SkiErg / RowErg / Farmer Carry / Sled / Wall Ball / KB Lunges. A = Ski+Carry+Wall Ball, B = Row+Sled+KB Lunge, C = easy Ski/Row EMOM; W14 is a deliberately shortened eight-station rehearsal that has *no running* and cannot be claimed to simulate the full race.
- **Running remains a separate track**, ideally about 2–3 sessions/week (Easy, Long Easy; interval conditional). Ski/Row heart-rate work can substitute for treadmill portions in a gym WOD but **not** for 8 × 1 km running in a real HYROX race. Do not convert Ski/Row meters into running kilometers.
- **Two World Gym strength sessions** are program anchors; protect main squat/bench/hinge/pull quality. Tuesday station conditioning is *optional* or controlled and may be downgraded to skill/easy when a run interval or Petra hard class is completed. Thursday Petra Strength/Skill or upper accessory remains optional.
- **Joint load budget:** During 11/12 post-interval calf recovery, prioritize comfortable walking/heel raises and low-impact aerobic, no mandatory hard session. On recovered weeks generally at most two hard engine sessions total, with at least ~48 hours between as practical; no hard WOD plus hard run plus hard Tuesday by default.
- **Feedback loop:** Google Sheets `Weekly_Review` adds hard-session count, average RPE, calf/knee pain, Ski/Row volume, station technique, next-week modification, and data completeness. Keep unreported values blank, never fabricate strength loads.

## Calendar / source of truth
The web app retains its original **Sunday–Saturday 17-week calendar**:
- W01: 2026-11-15 to 2026-11-21, with separate 2026-11-14 Push kickoff.
- W17: 2027-03-07 to 2027-03-13; tentative races Friday 2027-03-12 Mixed Doubles, Saturday 2027-03-13 Men Open (verify actual registration).
- Periodization remains: foundation W01–03, deload W04; strength build W05–07, deload W08; HYROX transfer W09–11, deload W12; race specific W13–15 including W14 shortened station rehearsal; taper W16, race W17.
- The Google Sheet `Training_Plan_v1_1_CURRENT`, `WOD_Library_v1_1`, `Coaching_Rules_v1_1` are the coaching reference. Old `Training_Plan_v16_CURRENT` and prior numeric plan tabs are preserved for history. The app snapshot does **not** live-query Google Sheets.

## Data architecture and safe interpretation
- App frontend: `index.html`. App JSON: `data/report.json`, top-level `version: 1.1.0`, `planRelease.label: v1.1`. Daily World Gym cards: `seasonPlan.weeks[].dailyPlan`; independent running: `seasonPlan.weeks[].runningTrack`. WOD details in `seasonPlan.weeks[].sessions[id=wod].classPlan.blocks` and `sessions[id=wod].wod.classPlan.blocks` stay consistent with Friday cards.
- Garmin private API: separate **private** repository `alvinxyyzzz/hyrox-garmin-sync` → Google Sheets activities/laps/syncs. **Do not** put credentials, raw FIT, GPS paths, or medical/private notes in public GitHub Pages.
- Petra source folder in Google Drive `Hyrox Training data/Alvin/Petra_Photos`, 37 photos; compare file IDs/modified times to `Petra_Photo_Registry`, analyze only changed/unreviewed uploads. Partner scores never become individual performance.
- v1.1 publication updates coach prescriptions and cache version, not the private Garmin sync code or scheduled automation. Data through 2026-11-13, no claim of newer sync. Week dashboard is a **plan**, not proof of sessions completed.

## Web app deployment
GitHub Pages serves the `main` branch. Commits and Sheets updates do not alone prove a live deployment. `sw.js` cache changes to `hyrox-v1-1-20261114-v25`; `index.html` registers the updated service worker. On iOS, reload once online; if stale, close/reopen the PWA and refresh.

## Scientific context
Concurrent training and resistance training support: https://pmc.ncbi.nlm.nih.gov/articles/PMC11688070 and https://pmc.ncbi.nlm.nih.gov/articles/PMC8891239 . Individualized volume, RPE and HYROX station prescriptions are coaching judgments, not universally validated clinical protocols.

## Historical v1.0 baseline
v1.0 FINAL was committed 2026-11-14 with two training tracks and the same Sunday–Saturday 17-week calendar. Its strength anchors, historic Garmin/Petra provenance and standalone Saturday Push kickoff are retained. Prior WODs that required alternating treadmill runs during World Gym have been replaced by treadmill-free station variants in v1.1.
