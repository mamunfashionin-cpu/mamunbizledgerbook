# Base44 Dev Environment

## Project Overview
Single-file static HTML app ("Mamun Fashion BizLedger Book"). No backend, no build step, no external credentials. All data is stored in the browser via localStorage. jsPDF is loaded from a CDN for PDF export.

## Running the App
```bash
docker compose -f docker-compose.base44.yml up -d
```
The app is served by Vite (installed globally in the container) on port 3000 with live reload. The source `index.html` is bind-mounted, so edits appear immediately in the preview.

## Verification
- Curl `http://localhost:3000/` — should return the HTML page.
- The app renders a mobile-first (max-width 480px) ledger/bookkeeping UI.

## Notes
- No secrets or environment variables are required.
- No database — all state is client-side localStorage (via a `window.storage` polyfill that maps to `localStorage`).
- The original `index.html` was truncated (ended mid-function at ~66KB). The following missing functions were reconstructed following existing code patterns: `deleteLedger`, `openAddTransaction`, `saveTransaction`, `openTxnDetail`, `deleteTxn`, `openAddParty`, `saveParty`, `openPartyDetail`, `deleteParty`, `openSetPin`, `savePin`, plus the bootstrap/init code and closing `</script></body></html>` tags. A `window.storage` → `localStorage` polyfill and loader-hide call were added to the init code.
