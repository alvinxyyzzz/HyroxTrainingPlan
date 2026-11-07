# HYROX Performance Lab

Phone-first **read-only** training report for Alvin's 2027 Taipei HYROX weekend: Friday Mixed Doubles and Saturday Men's Open.

## App

- `index.html` — mobile-first app, no frameworks
- `data/report.json` — summarized weekly coach review and four-week plan
- `manifest.webmanifest`, `icon*.png`, `sw.js` — iPhone home-screen support
- Race countdown, run-volume and interval graphs, Petra verified highlights, 4-week plan, World Gym Big Three, periodization to race week

## Publish to GitHub Pages

**Settings → Pages → Build and deployment → Deploy from a branch → main → /(root) → Save.**

Then open **https://alvinxyyzzz.github.io/HyroxTrainingPlan/** on iPhone Safari → Share → Add to Home Screen.

If the page is not yet enabled, GitHub Pages settings must be changed by the repository owner. A commit alone does not turn on Pages.

## Weekly updates

The connected ChatGPT weekly automation (Sunday evening Asia/Taipei) reviews Google Drive Petra whiteboards and `Garmin_API_*` data in the user's existing Google Sheet, checks for duplicates, recalculates training recommendations, and, where its GitHub permissions allow, updates **only `data/report.json`**. The app fetches this JSON with cache disabled online. The automated job is **not a guaranteed unattended model deployment**: review the weekly task result and GitHub commit history.

Garmin private synchronization remains in separate private repository `hyrox-garmin-sync`. That repository pulls Garmin Personal API into a *private* Google Sheet. **No Garmin credentials or Google Service Account JSON are needed here.**

## Public-data warning

**This repository is PUBLIC.** Do not commit original FIT files, complete Google Sheets exports, GPS tracks, health diagnoses, unredacted Petra photos, Drive permission links, or any credentials. `data/report.json` includes summarized training metrics, heart-rate averages, and coach notes visible to anyone with the Pages URL.

For strict privacy, don't use publicly hosted static health metrics: switch to authentication/private delivery before publishing data.

## Analysis safeguards

- Running distance from Garmin actual run activities only; WOD estimate never double-counted.
- 10/29: 12 x 400m work reps avg 120.0 sec. 11/05: 8 x 400m work reps avg 101.9 sec. Different work volume; NOT a controlled improvement test.
- 11/04: Petra 4R with uncertain 12.5kg note, matched Garmin HIIT HR avg164/max186.
- 10/27: Row 1500m photo 6:18 vs Garmin 6:20.5; both retained.
- Strength load trends omitted until reliable set/weight data become available.
- Science: [HYROX Official](https://hyrox.com/event/hyrox-taipei/), [Lauren Weeks interview](https://bradkearns.com/lauren-weeks-hyrox-world-champion-podcast/), [taper meta-analysis](https://pubmed.ncbi.nlm.nih.gov/37163550/).
