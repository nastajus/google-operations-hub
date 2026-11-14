# Photos And Video Project Assessment

![Photos and Video portal](../assets/images/module-photos.png)

## Purpose

The existing media project is a storage-pressure and evidence system, not just a gallery. Its job is to determine whether phone media has trustworthy offline or cloud evidence before proposing transfers or deletion. This directly supports the Hub's original quota-recovery goal.

## Existing Capabilities

- Builds an inventory-oriented media dashboard from phone, staging-drive, offline-drive, Google Photos, and Takeout evidence.
- Matches files using names, byte sizes, dates, hashes, and progressively richer similarity evidence.
- Pulls selected Pixel videos into controlled offline destinations and records transfer history.
- Maintains protected-media and deletion-history records for guarded phone cleanup.
- Parses Google Takeout archives and produces reconciliation manifests and coverage reports.
- Builds video similarity groups, location maps, duration caches, and candidate review batches.
- Keeps Google Photos cloud reconciliation separate from phone deletion and requires offline evidence before cloud-side deletion is considered.
- Prototypes mobile swipe review, desktop batch review, browser-assisted cloud inspection, and an Android connectivity monitor.

## Current Product Shape

The project is already a family of cooperating tools:

1. **Media dashboard:** evidence, status, maps, groups, and transfer decisions.
2. **Cloud reconciliation:** read-first matching between local evidence and Google Photos.
3. **Media pruner concepts:** mobile intent capture and desktop batch application.
4. **Automation scripts:** Takeout ingestion, matching, thumbnails, similarity, transfer, and guarded deletion.

## Recommended Hub Integration

Do not merge its data store or processing scripts into the Hub yet. Treat it as an independently runnable subsystem and integrate through a small contract:

- a Photos landing page that explains its quota-management purpose;
- launch and status links into the media dashboard and cloud reconciliation interface;
- a compact generated summary containing inventory counts, protected items, unresolved cloud matches, and reclaimable bytes;
- explicit links back to this assessment and the project's own operational documentation.

This keeps high-risk deletion logic in the project that already owns its evidence model while allowing the Hub to become the navigation and status layer.

## Boundary To Preserve

Raw media, Takeout archives, phone inventories, face evidence, location caches, and deletion targets are private operational data. None belong in the Hub's public repository or public screenshots.
