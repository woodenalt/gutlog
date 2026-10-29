# GutLog — Offline-first private digestive journal (v2.0)

A zero-dependency, static Progressive Web App for recording bowel movements and food. Data is stored only in the browser's IndexedDB; no analytics, logins, backend database, or automatic cloud sync. Supports creation, editing, deletion, recent entries, full JSON backup/restore, separate CSV exports, and offline loading after the first successful online visit.

**IMPORTANT:** The Home Screen web app can use a different storage container from the Safari browser tab. Record data in the **Home Screen app**, not interchangeably between the tab and app. Back up from the container where you actually entered data.

## Technical note

The UI uses plain JavaScript, HTML, and CSS without CDN dependencies; a service worker caches app files; IndexedDB stores two object stores. The app doesn't include cross-device synchronization, automatic encrypted backups, automated test suites, or statistical symptom analysis yet.
