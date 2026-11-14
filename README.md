# Google Operations Dashboard

A local-first dashboard for managing Google-related archives and workflows. The application centralizes service portals while keeping credentials, account records, health data, location history, recordings, and generated inventories outside the public source tree.

> **Publication status:** This public documentation preview intentionally omits application source and machine-specific operational notes while the first sanitized source release is prepared.

## Modules

| Module | Status | Documentation |
| --- | --- | --- |
| Health | Active | [Health overview](docs/health/README.md) / [Google Health setup](docs/health/google-health-setup.md) |
| Sound Recorder | Active | [Recorder overview](docs/sound-recorder/README.md) |
| Timeline | Prototype | Public documentation planned |
| Drive | Utilities | Public documentation planned |
| Photos | Scaffold | Planned |
| Gmail | Scaffold | Planned |
| Calendar | Scaffold | Planned |
| Keep | Scaffold | Planned |
| Tasks | Scaffold | Planned |
| YouTube | Scaffold | Planned |

See the [documentation index](docs/README.md) for the intended public documentation structure.

## Run

Install the browser-automation dependency once:

```powershell
npm install
```

Double-click `launch-dashboard.cmd`, or run:

```powershell
.\launch-dashboard.ps1
```

The launcher starts the local server and opens `http://127.0.0.1:8787/google/` in Firefox when available.

## Repository Layout

```text
assets/        Browser application code and styling
config/        Generic example configuration only
docs/          Public project and module documentation
scripts/       Local sync, import, analysis, and automation tools
data/          Private generated records; ignored
local/         Private browser profiles and working state; ignored
secrets/       OAuth clients and tokens; ignored
```

## Privacy And Publication

The repository is designed around a public-code/private-data boundary, but the current working history should be audited and sanitized before its first public push. Credentials, health records, location exports, transcripts, audio, account inventories, and private reports must never be committed.

See [PRIVACY.md](PRIVACY.md) for the data boundary. The dashboard also contains a local developer-facing privacy report under **Reports**.

