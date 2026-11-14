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


## Simple Sun–Sat Station Calendar v2.4 · 2026-11-14

**User-facing rule:** only a 17-week roadmap, a week selector, seven daily cards (Sunday through Saturday), and a **separate running add-on panel**. No Petra questionnaires, soreness/recovery questions, 5/6-day toggle, or lengthy substitution prose.

**Visible source:** `data/report.json > seasonPlan.weeks[].dailyPlan`, each day shaped `{day, dayZh, date, kind, title, time, sections:[{name,lines,format}],subtitle}`. The independent running prescriptions are `weeks[].runningPlan.sessions`. The front-end must not read obsolete `dailyPlan.groups`, `shortTitle`, `weekday`, or `category` fields.

**Sunday-to-Saturday dates:** W01 2026-11-15–11-21; W17 2027-03-07–03-13. Confirm exact date-to-weekday mapping on every update.

**Weekly balance (W01–W16):** Sunday station aerobic base (Ski/Row, progressing 18–40min), Monday Legs hypertrophy with single-leg/stability and low/moderate station practice, Tuesday **station-based cardio intervals** (Ski/Row/Sled/Carry), Wednesday rotating Push/Pull hypertrophy with relevant station combo, Thursday optional opposite upper-body strength or Petra Strength/Skill, Friday one standalone WOD (including Petra WOD when attended), Saturday rest. W14 Friday is a controlled partial HYROX rehearsal, Saturday an easy recovery-check session. W17 Friday Mixed Doubles and Saturday Men Open; no extra WOD.

**Running is independent:** `runningPlan` supplies weekly Easy/Long Run and Quality/Interval suggestions. They have NO fixed weekdays and must never replace the user's station cardio sessions. Running is important to the HYROX event but can be scheduled around work/family and the main strength/station workload; manage total hard intensity accordingly.

**Progression:** W01–03 baseline/build, W04 deload; W05–07 hypertrophy build, W08 deload; W09–11 station transfer, W12 deload; W13–15 specificity/sharpen, W16 taper, W17 race. Station cardio is not a daily race: Sun easy, Tue controlled, Fri WOD harder. Actual weakness work includes SkiErg, Wall Ball, unilateral leg work, grip/back and stable run-after-station output, not auto-lightening the plan for ordinary soreness.

**Preserve the update contract:** weekly Garmin/Petra data refreshes should modify evidence and actual training context without reverting the display to old weekly schedules or the Petra-question UI. Never publish raw FIT, GPS routes, private Petra photos or credentials. The public app only displays aggregated training information.
