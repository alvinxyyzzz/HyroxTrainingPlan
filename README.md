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


## Simple Sun–Sat Calendar v2.3 · 2026-11-14

The user-facing view is deliberately simple. Only select the week (W01–W17) or use previous/next. No Petra questionnaire, recovery/soreness selector, WOD-location selector, 5/6-day toggle, or lengthy replacement instructions in course cards.

**Date convention:** All 17 weeks are Sunday to Saturday. W01: 2026-11-15–2026-11-21. W17: 2027-03-07–2027-03-13. Align firstWeek, weekStart, week dates, phase ranges, and every dailyPlan date.

**Primary UI source:** data/report.json > seasonPlan.weeks[].dailyPlan supplies visible daily classes; weeks[].focus and weeks[].weaknessFocus supply the weekly summary. Always retain seven ordered entries per week, starting Sunday.

**Weekly pattern:** Sunday Long Easy (+ optional light evening Ski/Core); Monday first Push/Pull/Legs hypertrophy and focused functional circuit; Tuesday Petra Strength/Skill optional or rest; Wednesday interval; Thursday second strength and functional class; Friday rest; Saturday standalone WOD. Five core sessions + optional Tuesday. W14 has a Friday 60–70% reduced HYROX simulation and Saturday Day-2 easy aerobic check. W17 has Friday Mixed Doubles and Saturday Men Open.

**Coaching goal:** systematically improve weak links with planned hypertrophy, single-leg stability, SkiErg hip hinge/pace, back/grip work, and 6kg Wall Ball leg/shoulder endurance. Ordinary soreness is not a reason to auto-switch workouts. Significant pain, swelling or injury still warrants assessment. Respect deloads W04, W08, W12, W16.

**Automation contract:** Update complete dailyPlan together with class prescriptions. Never reinstate Petra class-type questions or default soreness switches. Keep Sunday-first dates consistent, and distinguish verified Garmin data date from plan update date. Do not publish private Garmin FIT/GPS or Petra photos.
