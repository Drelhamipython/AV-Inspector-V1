# AV Inspector — Punch List PWA

A mobile-first field inspection app for Amin Ventures. Inspectors capture defects on-site (photos with annotation, voice notes, severity, location) and email a PDF report when finished.

## Features

- **Offline-first** — all data stored locally via IndexedDB. Works in basements, stairwells, no signal.
- **Photo capture + annotation** — draw arrows/circles directly on photos in 4 colors.
- **Voice notes** — record narration per defect, attach unlimited per item.
- **Severity tagging** — Critical / Major / Minor with color-coded badges.
- **Quick-pick library** — common defects ("Paint touch-up", "Drywall crack", etc.) for one-tap entry.
- **Auto GPS + timestamp** captured silently.
- **PDF report** — generated client-side with cover page, summary, and one page per defect with inline photos.
- **Email export** — opens device mail app with subject/body pre-filled; PDF is saved to Downloads to attach.
- **Installable PWA** — Add to Home Screen on iOS/Android, looks and behaves like a native app.

## Deploy to GitHub Pages

1. Create a new repository (e.g. `AV-Inspector-V1`)
2. Upload all files in this folder to the root
3. Settings → Pages → Deploy from `main` branch, root folder
4. Your app will be live at `https://<username>.github.io/AV-Inspector-V1/`

## Files

| File | Purpose |
|------|---------|
| `index.html` | The entire app — UI, IndexedDB, photo annotation, voice recording, PDF generation |
| `manifest.json` | PWA install manifest |
| `sw.js` | Service worker for offline caching |
| `icon-192.png`, `icon-512.png` | App icons (replace with real Amin Ventures logo) |

## Inspector Flow

1. Open app → tap "Change" to set the project (e.g. "Alexander")
2. Tap **+** to add a defect
3. Fill in: location, trade, description (or pick from library), severity
4. Tap photo grid → camera opens → take photos
5. Tap any photo → annotation overlay → draw arrows/circles on the defect
6. Tap mic button → record voice note
7. Save defect, repeat for each item
8. When done → bottom nav "Send Report" → tap "Email Report"
9. PDF downloads to device, mail app opens with body pre-filled — attach the PDF and send

## Notes & Limitations

- **Browsers cannot auto-attach files to mailto links** (security restriction). The app downloads the PDF to the device and the inspector attaches it manually before sending. This is the only path that works fully offline without a backend.
- **Storage is per-device.** If the inspector clears browser data or uninstalls the PWA, defects are lost. Use "Send Report" at the end of each site visit so the PDF is always saved.
- **iOS install:** open in Safari → Share → "Add to Home Screen". (Chrome on iOS cannot install PWAs.)
- **Android install:** Chrome shows an "Install app" prompt automatically, or use the menu → "Install app".

## Future enhancements (when ready)

- Cloud sync via Firebase / Supabase so reports appear on a web dashboard in real-time
- Re-inspection workflow (mark defect Fixed, capture new photo, close)
- Per-trade subcontractor email routing (each trade gets its own punch list automatically)
- Project list synced from your main Amin Ventures app
