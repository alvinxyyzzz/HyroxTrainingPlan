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


## Studio Mesocycle v6 · 2026-11-14 (authoritative plan)

### Why and where

The current planning source of truth is `data/report.json > seasonPlan.weeks[].periodization` together with `sessions[].classPlan`. Public evidence is `metrics`, `petra`, `weeklyKm`, etc. Historic `prescriptionEngine.strength` is **legacy**, not the current generator. Do NOT replace current plan with old `lifts`, `flexiblePlan.modules` or `sessionDetail.strength + station` structures on weekly refresh.

### Periodization: 17 weeks (2026-11-16 to race 2027-03-13)

- **W01–04 (foundation):** symptom gate/baseline, controlled first WOD, volume growth, W04 deload.
- **W05–08 (hypertrophy):** 3 → 4 quality working sets for main compound exercise when recovered, meaningful shoulder/back/leg accessory work; W08 deload.
- **W09–12 (HYROX transfer):** preserve hypertrophy and strength, progress run-to-station circuits and repeatable running after Ski/Sled/Wall Ball; W12 deload.
- **W13–15 (race specificity):** sustainable race order, W14 60–70% shortened mixed-race-style circuit plus low-intensity next-day test rather than two max-effort days; W15 sharpen with volume reduced.
- **W16–17 (taper/race):** W16 lighter stations and 1-set primary strength with plenty of reserve; W17 actual Fri mixed/Sat men's solo events (NO additional gym WOD).

### Class construction

- **Push:** 25–40 min bench/incline/shoulder/lateral/triceps near RIR2–3 (as week permits) → 8 min shoulder/core stability → **2–3 round** Push Press + Wall Ball + Push-up sequence, at controlled fatigue. Adjust if Petra high-volume pressing or legs.
- **Pull:** pulldown/rows/rear-delt/curl → carry, anti-rotation and grip → repeated SkiErg/Sled Pull/Carry/Row combinations. Erg output is not counted as hypertrophy sets.
- **Legs:** squat/RDL/reverse lunge/leg curl → step-down/single-leg balance → controlled Sled Push/Step-up/Easy Row mini-circuit. Hard Sled loading belongs in separate WOD if appropriate, not two days back-to-back.
- **Standalone WOD:** one slot per week, World Gym / Petra WOD / home alternative. Formats include 4-round DB Thruster/Hang Clean/Reverse Lunge/Push-up/Sit-up, EMOM, AMRAP, run-station bricks, and a single W14 controlled shortened rehearsal. Each week sets its own time and RPE. A Petra hard AMRAP counts as the WOD regardless of its nominal class name.
- **Running:** interval quality (Petra class can replace), long easy by time, optional later easy Ski/Row/upper/core (non-required), controlling total fatigue.

### UI and update contract

- Users choose Petra `none/strength/skill/wod`, focus `general/push/pull/legs`, WOD location `world/home` and calf/knee `normal/pain`. They are manual localStorage values, NOT confirmed attendance. If Petra WOD is selected, World/Home WOD is replaced and PPL class C circuits are hidden. Petra Strength can replace a corresponding strength class *only if real working sets match*; Petra Skill can replace matching class C.
- **5 training days:** interval + standalone WOD + long easy + the week's `periodization.priorityMuscles` (two PPL classes); priority rotates with weekly focus. **6 days:** all PPL + interval + WOD + long easy. Petra replaces work, not a seventh day.
- Every week's `periodization` fields must be kept in sync with class block sets, WOD duration/RPE, and long-easy target. Deload weeks are W04/W08/W12/W16 (not inconsistent historic W03/W07/W11). Main set counts are per *primary lift*, not total direct muscle-group weekly sets.
- Keep all private Garmin FIT, GPS and Drive photos out of GitHub Pages. Only publish aggregated evidence. Never invent kilograms or attendance.
- Do not automatically lift caps or override symptom gates based on a single activity. Ask for additional confirmed recovery information before upgrading major intensity.

### External programming evidence

- [Centr HYROX Hybrid Strength, 2026 four-phase program](https://centr.com/blogs/features/hyrox-hybrid-strength-program-guide)
- [HYROX / HWPO partner programming](https://hyrox.com/training-partner/hwpo-training/)
- [2026 ACSM resistance training position stand](https://pubmed.ncbi.nlm.nih.gov/41843416/)
- [2026 concurrent training umbrella review](https://pubmed.ncbi.nlm.nih.gov/41762427/)
