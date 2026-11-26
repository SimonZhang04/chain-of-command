---
name: Bug report
about: Report broken behavior. Follows ISSUE_ARCHITECT.md.
title: "Fix "
---

<!-- Name the broken behavior and where it happens:
     good — "Fix seating circle not animating when the server broadcasts a new order"
     bad  — "Fix UI bug" -->

## Expected behavior

<!-- What should happen, with a pointer to the spec: Milestones.md bullet,
     protocol/PROTOCOL.md, docs/architecture.md, or Manual section. -->

## Actual behavior

<!-- What happens instead, with the observed error/log/screenshot. -->

## Repro steps

1. <!-- Numbered and exact: simulator model or device, server deployment (LAN vs tunnel), bot counts, room code source. -->

## Environment

- App/server: <!-- commit or build -->
- Device: <!-- simulator model / iPhone model -->
- Deployment: <!-- LAN / Cloudflare Tunnel / other -->

## Scope

**Do not** grow the fix into a refactor — discovered refactors become separate issues.

**Owns:** `paths/**` <!-- the failing area -->

## Acceptance Criteria

- [ ] A regression test **fails on current `main`** and passes after the fix.
- [ ] The existing suite still passes: `xcodebuild test -scheme ChainOfCommand -destination 'platform=iOS Simulator,name=iPhone 15'` and/or `go test ./...` <!-- adjust to the area -->
