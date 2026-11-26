---
name: Feature / Task
about: Implement a feature, service, screen, or task. Follows ISSUE_ARCHITECT.md.
title: "Implement "
---

<!-- Start the title with an imperative verb and be specific:
     good  — "Implement UWB ranging service with NearbyInteraction and simulated backends"
     bad   — "Player seating detection" (no action) -->

## Context

<!-- Background an agent with zero memory of previous issues can act on.
     Define any domain terms inline. Point to the Milestones.md bullets,
     protocol/PROTOCOL.md, docs/architecture.md, or Manual pages this implements.
     State key API facts the agent would otherwise have to research. -->

**Depends on:** #[issue] — **Blocks:** #[issue]
<!-- Remove one side if empty. An agent must know if it can start now. -->

## References

- New/changed code: `path/to/area/`
- Specs to read first: `Milestones.md`, `protocol/PROTOCOL.md`, `docs/architecture.md`
- Related issues: #[issue] (one line on its role)

## Scope

**Do**

- <!-- What to build, at design level: target paths, key signatures when they are part of the contract, expected behavior. -->

**Do not**

- <!-- Exclusion — reason or pointer to the issue that owns it, e.g. "Implement rotate/swap/mirror (#18)." -->

**Owns:** `paths/**` and its tests
<!-- No two open issues may claim overlapping paths. -->

## Acceptance Criteria

<!-- Checklist. Every item machine-verifiable: a test, a benchmark number,
     a command with expected output, or an observable behavior with stated commands.
     No judgment words ("intuitive", "polished", "robust"). -->

- [ ]
- [ ] Run with: `xcodebuild test -scheme ChainOfCommand -destination 'platform=iOS Simulator,name=iPhone 15'` <!-- adjust; for server work: `go test ./...` -->

<!-- UWB / NearbyInteraction: all criteria here must be runnable in simulator or CI.
     Physical-device verification is tracked in a `needs-device` issue (currently #19): -->
- [ ] Physical-device verification is tracked in #19.
