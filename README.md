# Sample HTML – 3D Asset Viewer with GA4 Tracking

## Folder structure
```
sample_html/
├── index.html        # Viewer + Google Analytics (GA4) tracking
├── metadata.json     # Metadata fed into GA events
└── assets/
    └── model.glb     # Your 3D asset
```

## Setup
1. Open `index.html` and replace **G-XXXXXXXXXX** (2 places) with your GA4 Measurement ID.
2. Fill in `metadata.json`:
   - `title_name`  – Title Name
   - `chapter_no`  – Chapter No.
   - `page_number` – Page Number
   - `asset_name`  – Asset Name (defaults to model.glb)
   - `isbn`        – ISBN
3. Serve over HTTP (module scripts and fetch won't work from file://):
   ```
   cd sample_html
   python3 -m http.server 8000
   ```
   Then open http://localhost:8000

## Events sent to GA4
Every event carries all 5 metadata fields as custom parameters:

| Event            | Fires when                          |
|------------------|-------------------------------------|
| `asset_view`     | Page opens                          |
| `model_loaded`   | GLB finishes loading                |
| `model_interact` | First orbit/zoom by the user        |
| `asset_time`     | On exit (adds `engagement_seconds`) |

## GA4 note
Register the 5 fields (title_name, chapter_no, page_number, asset_name, isbn)
plus engagement_seconds as **custom dimensions/metrics** in GA4
(Admin → Custom definitions) so they appear in reports.
