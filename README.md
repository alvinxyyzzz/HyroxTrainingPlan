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


## Two Connected Tracks v2.5 · 2026-11-14

The public Web App has FOUR navigation tabs: **17-week roadmap**, **World Gym/Petra (strength + station main line)**, **Running (separate flexible line)**, and **Data**. Weekly selection is shared. DO NOT reintroduce user-input controls for Petra type, soreness, weakness, 5/6 days or extra replacement configuration. No complicated substitution text on workout cards.

### Single source of truth
- `data/report.json > trainingTracks`: two-track principles and provenance, authoritative as of 2026-11-13 Garmin/Sheets. Latest plan date 2026-11-14 may be newer than verified training data.
- `seasonPlan.weeks[].dailyPlan` = World Gym/Petra seven-day cards, Sunday→Saturday; each `{day,dayZh,date,kind,title,time,sections:[{name,lines,format}]}`. W01 Sun 2026-11-15, W17 Saturday 2027-03-13.
- `seasonPlan.weeks[].runningTrack` = independent reference weekly mileage range and THREE flexible run options: Easy Run, Long Easy, Interval/Threshold (except race week). Run entries are **not fixed to weekdays**; morning opportunities are welcome, distance ranges are guidelines rather than required quotas. Old `runningPlan` is a historical legacy field and not displayed.
- `weeks[].trainingIntegration` = how combined hard sessions are managed. Running Quality + WOD generally supply two hard stimuli. Tuesday Station intervals are controlled moderate intensity, not a third all-out HIIT session when running Quality is included.
- `weeks[].gymTrack` = metadata for the main gym/station track. `dailyPlan` remains the displayed class details.

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
