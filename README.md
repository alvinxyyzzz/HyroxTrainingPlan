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

## Hybrid coach v4 — session programming contract (2026-11-13)

This is NOT a bodybuilding Push/Pull/Legs split with an optional station finisher. The 17-week planner lives at `data/report.json > seasonPlan.weeks[]`; each World Gym module is a full coached class in `sessions[].classPlan`, with ordered `blocks[]` that specify format, minutes, intervals, and transitions.

- **World Gym A / FORCE & TRANSFER**: squat strength with full rest → press/row antagonistic superset → Sled Push/Pull with Ski/Row transitions (low-to-moderate strength-to-station transfer).
- **World Gym B / HYROX ENGINE**: hinge/bench strength and upper pulling → 20–32 minute multi-station Engine / run-to-station circuit (the formal planned conditioning workout, **not an alternative, bonus, or seventh session**).
- **Long Run**: morning easy run with an OPTIONAL evening easy Ski/Row, upper-body or core skill block. No second hard session on a long-run day; no PM double in W16 taper or W17 race week.
- **Petra Strength/Interval**: the actual coach whiteboard/verified Garmin data take priority. If Petra was a hard WOD, switch World Gym B to `petraHardSwap` (Easy Engine) instead of stacking a third hard day. If calf/knee symptoms persist, use `recoverySwap` or rest; never override injury signals to hit numbers.
- Frontend selectors for Petra intensity and symptom state are per-week `localStorage` flags only. They do not sync back to GitHub or automatically determine attendance or recovery. The UI never claims they are live Garmin observations.
- Keep progression: heavy lift sets with adequate rest (RIR tracked), then efficient paired movements, then a distinct multi-station conditioning block with measurable pace/reps. Periodize build, deload, specificity, taper. W17 is the two-day race itself and must not be rewritten as five normal workouts.

**Weekly automation requirement:** On every coaching refresh, update evidence/status and adapt the existing `classPlan` fields. Do not regenerate old `sessionDetail.strength + station`, or reintroduce standalone `wod` / “Alternative HYROX Session”. Preserve week-by-week dose and local recovery gates. Public data remains aggregate only.
