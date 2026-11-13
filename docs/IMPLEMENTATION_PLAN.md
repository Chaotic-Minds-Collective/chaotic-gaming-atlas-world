# CG World — Implementation Plan

## Purpose
World/grid policy management for configurable gameplay rules.

## Feature scope
- Per-grid/server structure and tame limits
- Safe zones, no-collision and protected areas
- Personal/tribe ownership and claims
- Custom loot and supply/drop config
- Creature spawn profiles, caps and regions
- World/PvP/PvE rules and schedules
- Versioned config, dry-run diff and rollback

## Dependencies
- Core server registry, RBAC, audit and plugin config persistence
- ATLAS adapter: verified world/structure/tame/spawn/loot hooks
- Tribes for ownership; Sentinel for audit; GridForge for map data

## Data ownership
World owns policy docs, regions, limit snapshots, loot/spawn profiles and history. Core owns server identity, authorization and generic plugin configuration.

## Milestones
1. Define declarative policy schema
2. Implement config import/export, dry-run and audit
3. Observe structure/tame limits before enforcement
4. Add safe zones/ownership after spatial hooks verified
5. Add loot/spawn config with rollback
6. Add scheduled policies and cross-grid checks

## Technical gates and risks
- Collision/ownership/loot/spawn may require native hooks/client assets
- Start observe-only; enforcement reversible
- No live world changes without separate approval

## Shared engineering requirements
- Use authenticated, least-privilege Core APIs; no direct database credentials in plugins.
- Preserve provider identifiers as strings; display names are not identifiers.
- Carry cluster, grid and server context on applicable records/events.
- Use stable event IDs, idempotency keys and correlation IDs.
- Keep network work off game-critical threads; use bounded timeouts, retries and circuit breakers.
- Keep secrets out of source control and separate credentials per server/integration.
- Add unit tests, fake-adapter contract tests and isolated runtime compatibility tests.
- Gate unsupported features behind explicit capabilities; fail closed for privileged actions.
- Do not deploy to production or change live server configuration during repository planning.

## Current readiness
Documentation and planning scaffold. Exact ATLAS server build, loader, SDK, callbacks and feature-specific capabilities require isolated reproducible validation.
