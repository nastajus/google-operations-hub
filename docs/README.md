# Documentation Index

The root `README.md` is the public landing page. Each substantive module owns a directory under `docs/` so its setup, architecture, operations, and limitations can grow without turning the project overview into a manual.

## Active Modules

- [Health](health/README.md)
  - [Google Health API setup](health/google-health-setup.md)
  - [Movement explorer notes](../GOOGLE_HEALTH_MOVEMENT.md)
- [Sound Recorder](sound-recorder/README.md)
- [Timeline](timeline/README.md)
- [Calendar concept](calendar/README.md)

## Prototype And Utility Modules

- Calendar is a documented product idea for event-movement history and intent-versus-action analysis; it has not been implemented.
- Timeline already has a working local map and search prototype, but its operational notes contain machine-specific defaults.
- Google Drive remains a low-priority utility lane until its product purpose is clearer.

## Related Projects

- [Photos and Video project assessment](reports/photos-video-project-assessment.md)
- [YouTube project assessment](reports/youtube-project-assessment.md)

These are existing projects with independent data models and runtimes. The reports document current features and integration boundaries without prematurely merging their code into this repository.

## Scaffolded Modules

Gmail, Keep, and Tasks currently provide portal structure but do not yet have enough implementation to justify separate manuals. Add `docs/<module>/README.md` when a module acquires a real data source, workflow, or operational contract.

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
