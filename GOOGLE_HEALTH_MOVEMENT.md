# Google Health Movement Explorer

The movement explorer syncs Google Health records into ignored local storage and derives browser-ready, multi-resolution movement data.

For project creation, scopes, OAuth client configuration, and the Inspire 2 profile, see [Google Health API setup](docs/health/google-health-setup.md).

## Private data layout

- `data/google-health/raw/*.jsonl`: complete paginated API records by data type; aggregate-only types use chunked daily rollups
- `data/google-health/metadata.json`: profile, settings, identity, and paired-device metadata
- `data/google-health/movement.json`: derived visualization bins, segments, gaps, and inference notes
- `data/google-health/sync-status.json`: progress and per-type record counts

None of these files belong in Git.

## Sync

```powershell
node scripts\google_health_sync.mjs
```

Rebuild the derived movement dataset without downloading again:

```powershell
node scripts\google_health_sync.mjs --analyze-only
```

The analyzer distinguishes explicit true-zero movement records from missing data. Missing intervals are described as off-wrist or unsynced; short gaps may be labeled possible charging with low confidence. Recorded sleep takes precedence over nighttime inference.

Google limits each daily-rollup request to 14 or 90 days depending on the data type. The synchronizer automatically walks the full known history in compliant chunks. Raw skin-temperature sensor telemetry uses the API's `v4beta` endpoint and may be empty on unsupported devices.

