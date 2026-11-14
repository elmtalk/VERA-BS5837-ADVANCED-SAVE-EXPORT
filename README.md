# VERA + BS5837 — Advanced Save & Export (experimental)

This repository is a **separate test build** of the existing [VERA BS5837 Survey Integrated](https://github.com/elmtalk/VERA-BS5837-Survey-Integrated-) application, without changes to that original repository.

## Build
The GitHub Actions workflow clones the original integrated app, copies its complete HTML/assets, and injects `advanced-save-export.js` before the closing body tag. Run **Actions → Sync integrated VERA and advanced save/export → Run workflow**, or push changes to the enhancement script. The source HTML is intentionally not edited by hand.

## New tools
A small **Advanced save/export** panel adds:
- **VERA backup JSON**: snapshot of VERA-related IndexedDB stores plus VERA localStorage keys. Includes binary photos/Blob records as tagged base64, if stored in these databases.
- **VERA project bundle ZIP**: portable ZIP with JSON backup, manifest and one CSV per captured object store.
- **Restore backup**: import the exported JSON or this app's ZIP and rehydrate saved records. Existing records sharing the same key may be overwritten; download a backup first.
- Export metadata: version, timestamp, database and store identities; source is not deleted after backup.

**Important limitations:** This is a browser-level backup layer, not a replacement for the app's own project-specific `.vera.json` save/restore. It includes **all VERA-related browser storage on the same GitHub Pages origin**, not exclusively the currently selected project. It does not automatically back up browser File System Access handles or files held outside the app's browser storage. Inspect the included manifest before sending backups to anyone. Browser IndexedDB introspection requires a compatible modern browser. Always test restoration with disposable data before relying on it in the field. GitHub Pages hosting, if required, is enabled under **Settings → Pages → Deploy from branch → main / root**.

## Test checklist
1. Confirm original VERA and BS5837 assessments still load normally.
2. Create a sample project and save an assessment containing a photo.
3. Download JSON and ZIP; verify the manifest lists relevant stores and counts.
4. Reload, confirm the original project persists.
5. On a separate browser profile, restore the JSON/ZIP, reload and verify the project/assessment/photo is editable.
6. Test installed PWA, offline use, and a second project separately.

**Deployment status is determined by the GitHub Actions run**, not simply by committing these files.
