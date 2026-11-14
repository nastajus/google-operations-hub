# Calendar Concept

## Status

This module is an idea, not a prototype. Its current implementation is limited to a landing page that records the intended product behavior.

## Core Idea

Conventional calendars preserve the current location of an event but do not make repeated movement easy to study. The proposed system gives every intention a stable identity and appends an immutable record whenever its scheduled time, duration, category, or state changes.

The working theme is **the tension between intention and action**.

## Intended Views

- **Placement shadows:** show earlier scheduled positions behind the current event.
- **Movement ledger:** list every reschedule, cancellation, completion, and category change.
- **Delay measures:** calculate move count, accumulated delay, unresolved age, and time from first intention to action.
- **Type comparison:** compare health, career, administration, rest, social, and custom intention categories.
- **Pattern review:** find repeatedly deferred categories across weeks, months, and years.
- **Calendar maintenance:** separately review stale recurring events, duplicates, abandoned calendars, and historical clutter.

## Design Boundary

Google Calendar can remain the operational calendar. This module would add memory and analysis around it. Necessary rest, health management, and deliberate reprioritization should not automatically be classified as failure; the system must expose evidence without pretending to know the reason for every move.

## First Research Questions

1. Which Google Calendar APIs or local snapshots preserve enough event identity to detect moves reliably?
2. How should an intentional reschedule differ from avoidance, cancellation, or completion?
3. Can recurring events retain useful lineage without producing misleading movement counts?
4. What event categories can be inferred safely, and which require explicit user labels?
