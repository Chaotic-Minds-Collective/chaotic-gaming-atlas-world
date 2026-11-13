# CMG World

World/grid policy management for configurable gameplay rules.

This Chaotic Minds Gaming-specific module extends [Chaotic Gaming Core](https://github.com/Chaotic-Minds-Collective/chaotic-gaming-core) and the [ATLAS integration adapter](https://github.com/Chaotic-Minds-Collective/chaotic-gaming-atlas); it does not replace either foundation.

## Feature scope
- Per-grid/server structure and tame limits
- Safe zones, no-collision and protected areas
- Personal/tribe ownership and claims
- Custom loot and supply/drop config
- Creature spawn profiles, caps and regions
- World/PvP/PvE rules and schedules
- Versioned config, dry-run diff and rollback

## Architecture and dependencies
- Core server registry, RBAC, audit and plugin config persistence
- ATLAS adapter: verified world/structure/tame/spawn/loot hooks
- Tribes for ownership; Sentinel for audit; GridForge for map data

Core remains authoritative for shared identity, authorization and platform records. ATLAS-native calls pass through the shared adapter. This module owns its domain state and must not connect directly to PostgreSQL.

## Implementation plan
See [docs/IMPLEMENTATION_PLAN.md](docs/IMPLEMENTATION_PLAN.md) for data ownership, milestones and technical gates.

## Readiness
Planning scaffold only. Native ATLAS compatibility and feature-specific callbacks are not yet verified on an isolated server. No production deployment is implied.
