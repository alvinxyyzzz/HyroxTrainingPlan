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

## Hypertrophy-first HYROX coach v5 (2026-11-13)

The **source of truth** for the weekly plan is `data/report.json > seasonPlan.weeks[].sessions[].classPlan`. HYROX conditioning is not a body-part finisher and strength is not a random full-body circuit.

### Weekly programming

- **World Gym Push:** ~28–36 min hypertrophy (bench, incline DB press, shoulders, triceps) → ~8–10 min shoulder/core stability → ~8–12 min low/moderate Wall Ball / Sled Push skill.
- **World Gym Pull:** ~28–36 min hypertrophy (pulldowns, rows, rear delt, biceps) → grip/carry/core → ~10–14 min technique-oriented SkiErg / RowErg / Sled Pull. No heavy hinge on this day.
- **World Gym Legs:** squat, RDL, single-leg work and leg curls with complete rests → step-down / single-leg balance → low/moderate Sled or Lunge technique. Do not duplicate max Sled fatigue with WOD.
- **WOD: one formal weekly slot** (20–35 min, except recovery/deload/taper): `World Gym` circuit, `Home` low-equipment substitute, or `Petra WOD`. Petra WOD **replaces**, never adds to, World/Home WOD. If attending Petra Strength turns out to be a hard AMRAP, change the Petra selector to WOD rather than stack a second WOD.
- **Petra Strength or Skill** is variable week to week: when Strength targets Push/Pull/Legs, it replaces the corresponding World Gym module (subject to verified sets/intensity); when Skill targets one group, its station/skill block is omitted from the matching World Gym session, leaving hypertrophy work intact. Non-attendance must never be assumed to count.
- **Running:** one quality interval session and Long Easy every week as appropriate. An optional second session after Long Easy can be low-intensity upper/core or Ski/Row technique, not an additional hard workout.
- **5-day mode:** 2 of Push/Pull/Legs rotate week to week + Interval + one WOD + Long Easy. This means hypertrophy exposure is **reduced compared with 6 days**, never hidden or misreported. **6-day mode:** Push + Pull + Legs + Interval + one WOD + Long Easy. Petra replaces related work, it does not create an automatic seventh session.
- Preserve recovery gates. For calf/knee issues, use `recoverySwap` or rest. Week 1 Home WOD is low-stress reentry and Week 16 Home WOD is taper-only. Week 17 is the actual Fri Mixed / Sat Men Open race week, with no additional WOD.

### Data and frontend contract

- `classPlan.blocks` has `tag`, `title`, `minutes`, `format`, `steps` and `note`. Keep hypertrophy-first blocks in the defined order and ensure any PETRA/WOD substitutions share the same weekly slot.
- `classPlan.homeSwap`, `classPlan.petraSwap`, and `classPlan.recoverySwap` are optional mutually exclusive alternatives for that session.
- Frontend `index.html` stores per-week selectors in localStorage (`hyrox_petra_type_<Wxx>`, `hyrox_petra_focus_<Wxx>`, `hyrox_wod_place_<Wxx>`, `hyrox_recovery_<Wxx>`) and must not claim those selectors verify actual attendance or completion.
- Weekly coaching automations **must retain this schema**. Do not recreate the deprecated `sessionDetail.strength + station`, `wod` alternative add-on, or the old Force & Transfer / Engine paired-deadlift-and-bench classes. When updating Garmin/Petra evidence, only modify performance-dependent doses, recovery conditions and relevant class blocks; do not wipe this structure.
- Public `data/report.json` must remain aggregate and omit GPS, raw FIT, photos and credentials.

### Reference design principles

- [HWPO HYROX](https://www.hwpotraining.com/programs/hwpo-hyrox)
- [Centr HYROX Hybrid Strength](https://centr.com/blogs/thewarmup/hyrox-hybrid-strength-program-guide)
- [ACSM 2026 resistance training Position Stand](https://pubmed.ncbi.nlm.nih.gov/41843416/)
- [Concurrent training 2026 umbrella review](https://pubmed.ncbi.nlm.nih.gov/41762427/)
