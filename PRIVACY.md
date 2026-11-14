# Repository Data Boundary

This repository is intended to remain suitable for eventual public distribution.

## Public

- Application source, styles, and generic UI assets
- Scripts that operate on user-supplied data
- Example configuration with placeholder values
- Documentation that does not identify an account, person, device, or location
- Tests and synthetic fixtures

## Private

- OAuth clients, tokens, cookies, API keys, and rclone configuration
- Health and fitness measurements, device identifiers, and sync metadata
- Timeline exports, coordinates, inferred places, searches, and home locations
- Recorder transcripts, audio, screenshots, manifests, and inventories
- Gmail, Drive, Calendar, Keep, Tasks, Photos, or YouTube account exports
- Personalized reports, quota snapshots, logs, caches, databases, and archives
- Paths containing a Windows username or unique external-drive layout

Private runtime data belongs under ignored `data/`, `local/`, or `secrets/` directories. New integrations should default to those locations and provide synthetic examples separately when needed.

Before every commit, inspect `git status` and the staged diff for identifying content. When uncertain, treat content as private.

## Publication status

The ignored runtime boundary is effective, but this working repository should not be pushed publicly with its complete history yet. Tracked operational documentation and defaults still contain machine-specific drive layouts, device-model labels, and dated archive names. These are not credentials, but they disclose personal operating context and remain present in earlier commits even after current files are edited.

For the first public release, create a sanitized repository with a fresh root commit or rewrite and re-audit the complete history. Verify the result from a clean clone that has no access to local `data/`, `local/`, or `secrets/` directories.

## Private reports

Git cannot make selected committed files private inside an otherwise public repository. Use two histories:

1. The public application repository contains generic code, examples, and public-safe documentation.
2. A separate private repository outside the public checkout contains personalized reports and machine-specific manifests.
3. The dashboard may discover that overlay through an ignored `local/reports/manifest.json` file in a future implementation.
4. OAuth credentials, tokens, browser sessions, and raw personal archives remain untracked even in the private report repository unless protected by a dedicated encrypted-secrets workflow.

The tracked dashboard report is deliberately public-safe. It describes the boundary and audit result without embedding account identifiers or personal records.

## Commit policy

Implementation requests should produce one focused commit after verification. Discussion-only requests do not create empty commits. Generated personal data remains outside those commits even when it is needed to test the feature.

