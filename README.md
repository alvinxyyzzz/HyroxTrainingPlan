# HYROX PERFORMANCE LAB · v1.3

**Release date:** 2026-11-14. **Training evidence verified through:** 2026-11-13 (prior Garmin/Petra snapshot). This is a programming revision, **not** a fresh private Garmin API sync.

**Web App:** https://alvinxyyzzz.github.io/HyroxTrainingPlan/  
**Master Google Sheet:** https://docs.google.com/spreadsheets/d/1o48IfYCb14lNhEYOX8cgBFSrbD0CscJocKCYXgef8M0/edit

## Why v1.3 was necessary

The previous v1.2 combined upper push/pull work on Tuesday, put recovery on Friday despite Alvin normally working from home and likely going to World Gym, and showed multiple 2-round station segments after strength as though they were a complete station workout. This release audits and rewrites **all 17 weeks' visible daily plan cards** and session classPlan aliases to distinguish independent strength, station main, technique finishers, and genuine recovery.

## PPL: three main World Gym strength days

- **MON · LEGS:** Main Squat + Hinge/Trap-bar variation, followed by unilateral leg, hamstring and knee control; primary lifts generally 2–3 work sets by phase with RIR / real kg logged. **0–2 easy rounds** of Sled Push + Row are optional technique, **NOT Station main**.
- **TUE · PULL:** Lat Pulldown / assisted pull-up, Chest-supported Row, optional 1-arm Row, Face Pull and biceps. Optional Easy SkiErg **6–12 minutes RPE3–4** for technique; not a second high-intensity station main. No heavy squat/hinge in the pull day.
- **FRI · PUSH:** Normally World Gym while WFH, and considered a high-likelihood training anchor, not a recovery day. Bench, Incline Dumbbell Press, Shoulder Press, Lateral Raise, Triceps. Wall Ball **0–2 easy skill rounds**, not main Station. **W14 is exception**: Friday abbreviated eight-station simulation replaces full Push day; W17 is race week.
- Main sets 2–3, assistance 1–3 depending on training phase and fatigue. Progressive resistance work requires logging actual kg/reps/RIR rather than fictitious one-rep-max values. Some cross-muscle accessory is reasonable but the *main intent* is deliberately separated Legs / Pull / Push. ACSM 2026 evidence: https://pubmed.ncbi.nlm.nih.gov/41843416/

## Petra exact availability and substitutions

- **Petra Strength or Skill:** only **SUN, MON, or TUE**, up to **one of those three days per week**, **entirely optional**. If attended, classify actual exercise / muscle group / session RPE and **replace matching World Gym work**, not add a compulsory fourth hard strength day. A low-intensity Skill class is not automatically equivalent to all heavy work sets. Sunday Petra class can substitute for or displace scheduled Long Easy. Do not force makeup sessions.
- **Petra WOD:** **WED ONLY**, optional approximately every other week. Actual attendance must be confirmed with the athlete; a Petra whiteboard photo alone does not prove attendance. A hard Wed Petra WOD replaces the Saturday hard station main. If Wednesday WOD was hard, Thursday running must be scaled or Wednesday WOD skipped.
- **Petra Running Interval:** **THU EVERY WEEK** (unless deload symptoms or race week adjustment); **no World Gym Thursday**. When Wed was not a hard WOD, Thursday is the main quality running class RPE7–8, actual workout from Petra coach. If Wed was hard, attend only easy/technique or coach-downscaled class RPE4–5; if scaling is not possible, prioritize Thu run and skip Wed hard WOD.

## Main Station versus strength finisher

- **Real Station main** is typically **Saturday 4–5 ROUNDS and ~22–40 minutes** with deliberate 60–90 s rest between rounds, **only when no hard Wed Petra WOD** and recovery after Thu running is sufficient.
  - Early foundation: 4 rounds (example: Ski 350m → Farmer Carry 35m → Wall Ball 8–10; rest 75–90s).
  - Build / transfer: 5 rounds (e.g., Ski 400–450m → Carry 40m → Wall Ball 10–12; or Row 300–350m → Sled Push 12.5–15m → Sled Pull 12.5–15m).
  - Race-specific W13: 5 rounds SkiErg 500m + Carry + Wall Ball if recovered.
  - W15: 4 rounds sharpen, avoiding last-minute huge cumulative load.
- **A technique Finisher is separate**: 0–2 easy rounds after Mon Legs or Fri Push, RPE≤5, and never counted as Station main. W01 recovery and W04/W08/W12 deload and W16 taper legitimately show only 0–3 easy rounds with role **TECHNIQUE_ONLY**, not a misleading under-dosed main workout.
- **W14 simulation:** Fri WFH World Gym **abbreviated eight-station flow once**, Saturday easy Day2 recovery. It **does not** reproduce the official HYROX 8×1km run and is explicitly labeled as an abbreviated station rehearsal.
- SkiErg takes priority for station engine development, but RowErg, Sled push/pull, Carry, Lunges and Wall Balls are included. World Gym station main can avoid treadmill entirely; user still trains independent running (Thu Petra, Sun or other-day Long Easy). Erg meters are **not** running kilometers.

## 17 weeks and data consistency

- Unchanged Sunday–Saturday calendar W01 2026-11-15–11-21 through W17 2027-03-07–03-13.
- Phases: foundation W01–03, deload W04; build W05–07, deload W08; transition W09–11, deload W12; specific W13–15 with W14 abbreviated simulation; taper W16; race W17 (tentative Fri Mar12 Mixed Doubles, Sat Mar13 Men Open; verify confirmed registration).
- **JSON:** `data/report.json`, top-level `version: 1.3.0`, `planRelease.label: v1.3`, each `seasonPlan.weeks[].dailyPlan`, `stationPrescription`, `weeklyStrengthSplit`, and `petraStrengthSkillDays`. Former `trainingTracks.gym.strengthProgression.weekly` is updated to match Mon Legs / Tue Pull / Fri Push. `sessions[id=legs|pull|push|wod|interval|easy].classPlan.blocks` are synchronized.
- **Google Sheet:** `Training_Plan_v1_3_CURRENT` is the active plan; `PPL_Strength_v1_3`, `Station_Progression_v1_3`, `Petra_FlexRules_v1_3`, `Coaching_Rules_v1_3` provide granular workout plans and flexible session classification. All prior v1.2/v1.1/numeric versions are preserved as history.
- **Weekly feedback:** existing `Weekly_Review` fields K:S include hard session count, session RPE, calf pain, knee pain, Ski/Row volume, Station quality, next-week modification. Real strength kg/reps/RIR belong in `Strength_Log` and Petra actual attendance must be confirmed; no fabricated workout completions.
- **Privacy:** GitHub Pages stores only aggregated training data and coaching prescriptions. Garmin private access credentials, raw FIT, GPS traces, and personal private Petra photo content remain outside the public GitHub repo. Daily private Garmin sync and existing weekly coaching automation are **not modified** by v1.3. Last verified data remain through 2026-11-13.

## Publishing

`index.html` presents the v1.3 label and revised week guidance, `sw.js` cache key `hyrox-v1-3-20261114-v27`, and `manifest.webmanifest` app query `v13`. GitHub Pages deploy must be verified separately. If an older iPhone Home Screen PWA view persists, reopen while online and refresh.

## Scientific context
- Official HYROX race requires 8×1km running plus eight functional stations, unlike an abbreviated station-only workout: https://hyrox.com/the-fitness-race/
- ACSM 2026 resistance training position stand: https://pubmed.ncbi.nlm.nih.gov/41843416/
- Concurrent strength + endurance sequence review: https://pubmed.ncbi.nlm.nih.gov/41669271/

Prior releases v1.0 / v1.1 / v1.2 remain in Git history. Historic Garmin/Petra evidence and personal goals were not rewritten.
