# GutLog — Offline-first private digestive journal (v1.0)

A zero-dependency, static Progressive Web App for recording bowel movements and food. Data is stored only in the browser's IndexedDB; no analytics, logins, backend database, or automatic cloud sync. Supports creation, editing, deletion, recent entries, full JSON backup/restore, separate CSV exports, and offline loading after the first successful online visit.

## Deploy using GitHub Pages (no terminal required)

1. Unzip the GutLog package. Create a **new public GitHub repository** (e.g. `gutlog-app`). Public GitHub Pages exposes the app's **source code** but **not** your personal records; records never get uploaded to GitHub by this app. Do not commit any exported personal data. If you prefer private source hosting, use another HTTPS static host that supports private deployments.
2. Upload the **contents** of this `gutlog` directory (not the enclosing directory) to the repository's root: `index.html`, `app.js`, `styles.css`, `sw.js`, `manifest.webmanifest`, and the three icons.
3. In the repository, open **Settings → Pages → Build and deployment → Deploy from a branch**, select `main` and `/ (root)` and save.
4. Wait for GitHub to show the HTTPS Pages URL (typically `https://YOUR-USERNAME.github.io/gutlog-app/`). Open that URL on iPhone in **Safari** while online. Confirm the app opens and you can save a test entry.
5. Safari: tap **Share → Add to Home Screen → Add** (on some iOS releases select **Open as Web App** when available). Launch GutLog from its new Home Screen icon.
6. Test offline: load GutLog at least once online, enable Airplane Mode, launch it from Home Screen, and create/view a record. After restoring connectivity, test JSON backup and export.

**IMPORTANT:** The Home Screen web app can use a different storage container from the Safari browser tab. Record data in the **Home Screen app**, not interchangeably between the tab and app. Back up from the container where you actually entered data.

## Run on Mac for development

In Terminal: `cd /path/to/gutlog && python3 -m http.server 8000` and visit `http://localhost:8000` on your Mac. Web app recording works over localhost; the offline service worker is registered only on HTTPS hosts in this release. For iPhone installation, use an HTTPS deployment, not a `file://` URL or arbitrary local-network HTTP address.

## Data format

- Stool: `id, at, type, ease, color, blood, duration, notes`.
- Food: `id, at, meal, foods[], notes`.
- `at` is the user's local date and time (`YYYY-MM-DDTHH:mm`); export does not attach a timezone offset. This matches the simple entry UI but should be upgraded for travel across time zones.
- JSON is the full-fidelity backup; CSV is for Excel, Numbers, DuckDB, etc. CSV stores food lists separated by semicolons in a single field. UTF-8 BOM is included for Excel compatibility.
- Restore supports merging by unique ID and replacing all records. Invalid backups are rejected before import. Exported files are **not encrypted**.

## Privacy considerations

- Data sits in IndexedDB of the app's website origin and storage profile. An unlocked device or browser profile may expose it. There is no application-specific encryption or PIN in v1.
- Do not use a third-party online JSON/CSV viewer for exported health data. Prefer AirDrop, Files → On My iPhone, or your chosen secure cloud destination; use iCloud Drive only if you accept its privacy/security tradeoffs.
- iOS can evict website data; deleting the app, removing website storage, or using private browsing can also lose data. Export JSON regularly, ideally after each week of use, and verify a restore with a test backup.
- This is not a medical diagnostic tool. Black or red stools and blood present can indicate bleeding; seek clinical assessment as appropriate.
- Source files are static and are served by the web host when first opened or updated. The app makes no explicit data-collection requests. A host still sees ordinary page requests and associated connection metadata. Use hosting you trust.

## Updating

Replace the files in the repository. **Increment the CACHE string in `sw.js`** when shipping an updated app so old cached resources are removed. Reload online to activate an update. Export a JSON backup before updates or browser maintenance.

## Technical note

The UI uses plain JavaScript, HTML, and CSS without CDN dependencies; a service worker caches app files; IndexedDB stores two object stores. The app doesn't include cross-device synchronization, automatic encrypted backups, automated test suites, or statistical symptom analysis yet.
