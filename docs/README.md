# Documentation Index

The root `README.md` is the public landing page. Each substantive module owns a directory under `docs/` so its setup, architecture, operations, and limitations can grow without turning the project overview into a manual.

## Active Modules

- [Health](health/README.md)
  - [Google Health API setup](health/google-health-setup.md)
  - [Movement explorer notes](../GOOGLE_HEALTH_MOVEMENT.md)
- [Sound Recorder](sound-recorder/README.md)

## Prototype And Utility Modules

Timeline and Google Drive currently have internal operational notes containing machine-specific defaults. Their public manuals will be added after those workflows are generalized.

## Scaffolded Modules

Photos, Gmail, Calendar, Keep, Tasks, and YouTube currently provide portal structure but do not yet have enough implementation to justify separate manuals. Add `docs/<module>/README.md` when a module acquires a real data source, workflow, or operational contract.

## Documentation Convention

Each active module should eventually contain:

```text
docs/<module>/
  README.md          Purpose, architecture, status, and links
  setup.md           Account/API/device setup when required
  operations.md      Routine workflows and recovery procedures
  limitations.md     Known source, API, and inference boundaries
```

Do not place personalized exports, screenshots, account identifiers, local inventories, OAuth values, or private operational reports in `docs/`.
