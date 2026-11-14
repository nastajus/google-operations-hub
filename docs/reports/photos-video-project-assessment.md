# Photos And Video Project Assessment

![Media Backup Dashboard tagging and evidence table](../assets/images/photos-media-tagging.png)

## Purpose

The media project helps a user keep Google Photos within a fixed storage limit without losing irreplaceable photos or videos. It combines fast visual tagging with backup evidence so large batches can be reviewed, organized, protected, transferred, or proposed for deletion with understandable safeguards.

## Existing Capabilities

- Builds an inventory-oriented media dashboard from phone, staging-drive, offline-drive, Google Photos, and Takeout evidence.
- Matches files using names, byte sizes, dates, hashes, and progressively richer similarity evidence.
- Pulls selected Pixel videos into controlled offline destinations and records transfer history.
- Maintains protected-media and deletion-history records for guarded phone cleanup.
- Parses Google Takeout archives and produces reconciliation manifests and coverage reports.
- Builds video similarity groups, location maps, duration caches, and candidate review batches.
- Supports drag-and-drop emoji tagging for rapid review intent, grouping, and later batch decisions.
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

This keeps high-risk deletion logic beside the evidence and review model while allowing the Hub to become the navigation and status layer.

The Hub's Photos module can now start this existing local application and open it in a new browser tab. This is process-level integration only; the media project continues to own its server and private records.

## Boundary To Preserve

Raw media, Takeout archives, phone inventories, face evidence, location caches, and deletion targets are private operational data. None belong in the Hub's public repository or public screenshots.
