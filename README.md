# HYROX PERFORMANCE LAB · v1.0 FINAL

**Release:** 2026-11-14 · Two-Track baseline. Training data verified through **2026-11-13**, not through the release date.

**Web App:** https://alvinxyyzzz.github.io/HyroxTrainingPlan/  
**Repository:** https://github.com/alvinxyyzzz/HyroxTrainingPlan

## Program overview

The UI has four simple tabs: Roadmap, Strength / Station, Running, Data. The 17 calendar weeks are **Sunday to Saturday**: W01 2026-11-15–11-21, W17 2027-03-07–03-13. A separate 2026-11-14 Saturday Push kickoff is displayed in W01. Friday 2027-03-12 is Mixed Doubles, Saturday 03-13 Men Open.

**Two training tracks, one shared training-load budget:**
- Gym × Petra: Sunday easy SkiErg/RowErg, Monday lower-body foundational strength, Tuesday **challenging Station Conditioning**, Wednesday foundational Push/Pull, Thursday optional accessory / Petra Strength or Skill, Friday varied mixed HYROX Run→Station WOD, Saturday rest.
- Running: morning-friendly Easy and Long Easy with free scheduling. Quality/Interval is **optional** when both Tuesday Station and Friday WOD have been performed; no fixed run weekdays or automatic mileage quotas.
- Petra: Verified actual Petra hard WOD substitutes for the Friday World Gym hard WOD; do not stack both. Whiteboard photographs do not by themselves prove attendance.

## Seventeen-week training phases and intensity

| Weeks | Training emphasis | Lifting anchor | Station quality |
|---|---|---|---|
| W01–03 | Technique, base and muscle | Squat, Bench, Pull, W03 conventional Deadlift technique | Tue RPE7, Fri RPE7 |
| W04 | Deload | RIR4–5, reduced sets | Tue/Fri RPE4 |
| W05–07 | Strength build and station engine | **Trap-bar DL three consecutive weeks**: 3×6 RIR3 → 3×5–6 RIR2–3 → 3×4–5 RIR2; Bench/Squat/Pull continued | Tue RPE7–8, Fri RPE7–8 |
| W08 | Deload | Lower volume | Tue/Fri RPE4 |
| W09–11 | HYROX transfer | About two sets for Squat/Bench/Hinge maintenance, W09 conventional DL | Tue RPE7–8, Fri RPE8 |
| W12 | Deload | Low volume | Tue RPE4, Fri RPE5 |
| W13 | Specific | Trap-bar 2×4 RIR3–4 | Tue/Fri RPE8 |
| W14 | Scaled race simulation | No heavy DL, reduced lifting | Tue RPE5, Fri eight-station shortened simulation RPE8 |
| W15 | Sharpen | Two sets of Squat/Bench | Tue/Fri RPE7 |
| W16 | Taper | Light 1×5 Squat/Bench, no heavy hinge | RPE3–4 |
| W17 | Race | Activation, no extra WOD | Friday Mixed / Saturday Men |

Tuesday Station Conditioning is a **genuine quality interval session**: SkiErg / RowErg / Carry, occasional Sled Pull, explicit sets, rests and RPE7–8 on build weeks. Friday WOD is race-oriented mixed Run/Ski/Row/Sled/Carry/BBJ/Lunge/Wall Ball RPE7–8; Sunday stays easy, and post-strength technique finishers stay RPE5–6. Harder is not a requirement to train all-out daily. If a demanding Petra class or running interval is actually done, count it toward total hard-session load before repeating a planned session.

Fundamental Squat, Bench, Deadlift/hinge and direct pulling are periodized by **phase**, not compulsively inserted every session. Work on the chosen primary lift for several consecutive weeks with RIR-based progression, then maintain during HYROX specificity. No fictional 1RM or weight kilograms: Strength_Log has not recorded verified working loads.

## Authoritative program fields

- Primary JSON: data/report.json, top-level version **1.0.0**, planRelease.label **v1.0**; the v1.0 baseline can still be updated using verified new training evidence.
- Sunday–Saturday Gym cards: seasonPlan.weeks[].dailyPlan; standalone kickoff: seasonPlan.kickoff.
- Independent running cards: seasonPlan.weeks[].runningTrack. Its targetKm includes planned Friday WOD run segments; independentRunKmRange is the remaining reference range, not a mandatory quota. Only completed verified workouts count as actual mileage.
- Weekly intensity: seasonPlan.weeks[].periodization.highIntensityDistribution and trainingTracks.gym.intensityModel. W04/W08/W12/W16 deload/taper, W14 scaled simulation. Do not reintroduce old Petra questionnaire, weakness toggles, or soreness selectors.
- Synchronization: Any change to displayed Monday/Wednesday foundational lifting steps must also update the corresponding sessions[].classPlan.blocks[0].steps. Friday WOD displayed sections and sessions[id=wod].classPlan.blocks must remain synchronized. Preserve W01 Wed Pull after the Nov14 Push kickoff.
- Data release is aggregated ONLY. No raw FIT, GPS traces, private Petra images, credentials, or sensitive personal notes in public GitHub Pages.

## Garmin, Petra and Drive organization

- **Central Training Database** native Google Sheet ID 1o48IfYCb14lNhEYOX8cgBFSrbD0CscJocKCYXgef8M0, with Garmin_API_Activities/Laps/Syncs, Petra_Whiteboard, Petra_Photo_Registry, Strength_Log, Equipment_Inventory, Athlete_Notes, historical plans. Do not delete individual historical tabs until verifying automation dependencies.
- Private Petra_Photos folder: 37 original images as of this audit, preserved in place. Weekly photo workflow should compare ID and modified time against Petra_Photo_Registry; only review newly modified/unreviewed photos, do not repeatedly analyze 35 previously marked reviewed images.
- Garmin private API secrets and daily sync are in the separate private repository alvinxyyzzz/hyrox-garmin-sync. Do not claim scheduled automations were updated unless verified.
- Evidence through Nov13: 64 Garmin activities, usual recent running weeks ~12–16 km and one 25.84 km week; Nov7 Easy 5.93km avg HR143. Nov10 Petra partner AMRAP23 shared **team score** 17R+15, Garmin HR169 avg. Nov12 FIT confirms approximately 5×400m +4×600m intervals; 100 Air Squats are athlete-reported, not Wall Ball counted reps. Heavy Squat/Trap-bar working kg and RIR remain unverified.
- Drive cleanup 2026-11-14: **39 legacy files and deployment folders moved, not permanently deleted**, into the archive folder (ID 1HzeZHLI23Hs89zRriw1ZZeGrS07RlPhY) located under Hyrox Training data/Alvin/Archive_Pre_v1.0_20261114. The Alvin root now contains only the central Sheet, Petra_Photos and this archive. Original Drive IDs are preserved.

## Deploy and maintenance

The public site should be checked separately for actual GitHub Pages deployment. GitHub commits are not proof of successful Pages availability. Service worker uses versioned caching and network-first report loading; update the cache version whenever the frontend changes. On iOS, an old Home Screen icon may require deleting the shortcut and adding it again.

A weekly coaching task's schedule does not prove it executed. Distinguish scheduled, executed, committed and live-published statuses. Update the baseline plan using new verified Garmin/Petra evidence without reverting to one-track programming or adding extra mandatory intensity days.

**Research background:** Concurrent training review https://pmc.ncbi.nlm.nih.gov/articles/PMC11688070 and systematic review https://pmc.ncbi.nlm.nih.gov/articles/PMC8891239. The exact HYROX intensity calendar is tailored coaching design, not an experimentally validated universal protocol.
