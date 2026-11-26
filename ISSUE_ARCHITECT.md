# Issue Architect

This document describes how to create GitHub issues for the Chain of Command game project. The goal is to ensure that issues are clear, unambiguous, actionable, and easy to understand for other agents and contributors working to complete the game.

Issues are written for agents that start each task with **zero memory of previous work**. Everything an agent needs to start — background, pointers, dependencies, and how to verify its work — must be in the issue itself or one link away.

The examples in this document are drawn from the project's real issues (the Milestone 1 set, #1–#19). Follow the conventions they show.

Start every new issue from a template in `.github/ISSUE_TEMPLATE/` — `Feature / Task` or `Bug report`. Blank issues are disabled, so the structure below is the default path, not a convention to remember; fill every section (delete the guidance comments when done). Keep the templates and this document in sync when the conventions change.

## Structure of an Issue (Feature / Task)

Issues should follow a consistent structure, with the following sections:

1. **Title**: A concise summary of the issue, a statement of the task to be completed. Use imperative mood, lead with a verb, and be specific. For example, "Implement UWB ranging service with NearbyInteraction and simulated backends" or "Wire automatic seat detection and Re-detect button into the seating screen" are good. "Player seating detection" (no action) and "Fix UI bug in visualization of player seating circle" (doesn't say *what* the bug is or what correct behavior looks like) are not.

2. **Context**: Enough background for an agent with decent project context to understand the issue without reading through previous issues or documentation. Include:
   - Any domain terms the issue relies on, defined inline (e.g., "detection attempt", "seating phase").
   - Where this piece fits: the relevant `Milestones.md` bullets, protocol docs (`protocol/PROTOCOL.md`, `docs/architecture.md`), or Manual/Role Book sections for rules questions.
   - Key API facts the agent would otherwise have to research (e.g., "each peer pairing needs its own `NISession` with its own `discoveryToken`").
   - A **Depends on / Blocks** line, e.g. `**Depends on:** #8, #15, #16. **Blocks:** #18.` An agent must know at a glance whether it can start now or must wait for another issue to merge. Listing what this issue blocks lets future authors find their dependencies.

3. **References**: Pointers to where the work lives, so the agent doesn't burn context exploring:
   - Files and directories the issue will touch, including planned new files (e.g., `ios/ChainOfCommand/Ranging/`).
   - Frameworks and APIs involved (`NearbyInteraction`, `NINearbyObject`, Gin, …).
   - Shared docs to read first (`Milestones.md`, `protocol/PROTOCOL.md`, `docs/architecture.md`) and Manual page numbers for rules behavior.
   - Related issues by number with a word about their role ("the orchestration in #8 calls this").

   For very small issues the References content can be folded into Context and Scope, but the pointers themselves are mandatory.

4. **Scope**: Split into **Do**, **Do not**, and an **Owns:** line.
   - **Do**: what to build, at design level — target file paths, key type/function signatures when they're part of the contract, and expected behavior. Say what may be adjusted and what must stay fixed (e.g., "You may adjust the exact signatures if justified in the PR, but keep the prepare / receiveToken / measure / stop lifecycle").
   - **Do not**: explicit exclusions, each with a one-line reason or a pointer to the issue that owns it — e.g., "Do not implement rotate/swap/mirror (#18)." The reason stops an agent from "helpfully" doing it anyway.
   - **Owns:** the files and directories this issue creates or modifies, e.g. `**Owns:** ios/ChainOfCommand/Ranging/** and its tests.` See Multi-Agent Coordination below — this line is a coordination contract, not a formality.

5. **Acceptance Criteria**: A GitHub checklist (`- [ ]`) of conditions that must hold for the issue to be complete.
   - Every item must be **machine-verifiable**: a test, a benchmark number, a command with expected output, or an observable behavior reproducible with stated commands. No judgment words ("intuitive", "polished", "robust", "responsive") unless paired with an objective proxy.
   - Include the exact verification commands where they exist, e.g. `xcodebuild test -scheme ChainOfCommand -destination 'platform=iOS Simulator,name=iPhone 15'`, `go test ./internal/seating/...`, `go run ./cmd/bots --room CODE --count 4`.
   - State the required margins numerically: "correct order in ≥ 99% of seeded trials", "`BenchmarkSolve10` < 20 ms per solve".
   - ACs double as the agent's Definition of Done and should be copy-pasteable into the PR description (see CODE_WRITER.md).

## Multi-Agent Coordination

Agents work in parallel, often on the same machine, each in its own worktree (CODE_WRITER.md). The issue author is responsible for keeping parallel work safe:

- **File ownership.** No two *open* issues may claim overlapping paths in their **Owns:** lines. If a new issue needs to touch files owned by an open issue, either sequence it with **Depends on:** or merge the ownership deliberately — don't leave two agents to collide in a merge.
- **Issue sizing.** One issue = one verifiable outcome, sized for a single agent session. If the Scope starts naming more than ~3 modules, or the AC checklist grows past ~10 items, split the issue into sequenced parts.
- **Scope growth.** If an agent discovers work outside an issue's scope mid-flight, it files a *new* issue linked to the original rather than expanding scope. CODE_WRITER.md already tells writers not to exceed scope; architects must support that by keeping issues narrow and naming where adjacent work belongs.

## Hardware Verification (UWB / NearbyInteraction)

NearbyInteraction needs physical UWB-capable iPhones: the iOS Simulator has no UWB, CI has no devices, and some players' phones lack UWB or deny permission. Every issue touching ranging or position detection must state how it is verified *without* hardware:

- Hardware-dependent code goes behind a protocol (e.g., `RangingService` in #15) so all logic is testable against fakes or a deterministic simulated backend (seeded RNG, time-scaled delays).
- Acceptance criteria must be runnable in simulator or CI: pure-logic tests, fake-session conformance tests, deterministic simulated measurements. Anything that isn't belongs in the device issue, not here.
- Physical-device verification is tracked in a separate issue labeled `needs-device` (the Milestone 1 sign-off is currently #19). Implementation issues say so in their checklist instead of requesting device runs — e.g. "Physical-device verification is tracked in #19."
- An agent must never claim on-device behavior was verified when it could not run it. Mark hardware-dependent criteria as unverified and defer to the `needs-device` issue.

## Bug Issues

The template above is task-shaped. Bug reports use this structure instead (mirrored by the `Bug report` issue template; keep the References, Owns, and coordination conventions where they apply):

- **Title**: Imperative, naming the broken behavior and where it happens — "Fix seating circle not animating when the server broadcasts a new order", not "Fix UI bug".
- **Expected behavior**: What should happen, with a pointer to the spec (Milestone bullet, protocol doc, Manual section).
- **Actual behavior**: What happens instead, with the observed error/log/screenshot.
- **Repro steps**: Numbered, with the exact commands and setup (simulator model, server deployment — LAN vs tunnel — bot counts, room code source).
- **Environment**: App/server commit, device or simulator, deployment configuration.
- **Scope / Owns**: The failing area; the fix must not grow into a refactor — refactors discovered while debugging become separate issues.
- **Acceptance Criteria**: Must include a regression test that **fails on current `main` and passes after the fix**, plus the existing suite still passes.

## Example: Well-Structured Issue

Condensed from the real issue #15 ("Implement UWB ranging service with NearbyInteraction and simulated backends"); read that issue directly for a full-size reference.

> ### Implement UWB ranging service with NearbyInteraction and simulated backends
>
> **Context**
>
> Seat detection uses Apple's [NearbyInteraction](https://developer.apple.com/documentation/nearbyinteraction) framework (UWB) to measure the distance from this phone to every other player's phone. The iOS Simulator has no UWB, CI has no devices, and many players' phones may lack UWB or deny permission. So all ranging sits behind a `RangingService` protocol with two backends: NearbyInteraction for real devices, and a Simulated backend using the shared geometry rule from `docs/architecture.md` (the same one the Go bots in #10 use). This issue builds only the service; wiring it to the server is #17.
>
> Key NearbyInteraction facts: each peer pairing needs its own `NISession` with its own `discoveryToken`; run a session with `NINearbyPeerConfiguration(peerToken:)` using the *peer's* token; use distance only — direction is unreliable with phones lying flat.
>
> **Depends on:** #3. **Blocks:** #17.
>
> **References**
>
> - New code: `ios/ChainOfCommand/Ranging/`.
> - Geometry rule shared with the bots: `docs/architecture.md`.
> - Consumer of this service: `DetectionCoordinator` in #17.
>
> **Scope**
>
> **Do**
> - `Ranging/RangingService.swift`: protocol with a `prepare / receiveToken / measure / stop` lifecycle plus `RangingResult`, `PeerMeasurement`, and `RangingError` types. Signatures may be adjusted if justified in the PR, but the lifecycle must stay.
> - `Ranging/NearbyInteractionRangingService.swift`: one `NISession` per peer; token (de)serialization with secure coding; delegate collecting distance samples; handle invalidation, suspension, and removal. Wrap `NISession` in a protocol so the logic is testable without hardware.
> - `Ranging/SimulatedRangingService.swift`: the shared geometry rule, Gaussian noise (σ default 0.05), seeded RNG.
> - `Ranging/MedianAggregator.swift`: pure median/sample-count helper, ignoring NaN and negative values.
> - `Ranging/RangingServiceFactory.swift`: pick Simulated on the simulator or with the Debug toggle, else NearbyInteraction.
>
> **Do not**
> - Send anything over the network or touch `GameSession` (that's #17).
> - Build UI (#16/#17).
> - Use direction/azimuth or camera assistance — direction is unreliable for our use case.
>
> **Owns:** `ios/ChainOfCommand/Ranging/**` and its tests.
>
> **Acceptance Criteria**
>
> - [ ] `MedianAggregator` tests: odd/even counts, single sample, NaN/negative filtered, empty → no measurement.
> - [ ] Simulated backend tests: with σ = 0, distances equal the chord length `2·0.8·sin(π·|i−j|/n)` for sorted-ID indices; deterministic for a fixed seed.
> - [ ] NearbyInteraction logic tests with a fake `NISessionProtocol`: one session per peer; `userDidNotAllow` → `permissionDenied`; `stop()` invalidates every session.
> - [ ] Concurrent-session-limit findings documented in a doc comment and the PR description.
> - [ ] Final verification on two physical UWB iPhones is tracked in #19 (`needs-device`).

## Example: Bad Issue

> **Fix UI bug in visualization of player seating circle**
>
> The seating circle looks wrong sometimes. Fix it.

What's wrong with it:
- **Title** doesn't say what the bug is or what correct behavior is.
- **No context or references** — which screen, which view file, which spec does "looks wrong" violate?
- **No repro steps** — "sometimes" isn't reproducible; no environment (simulator? device? bots?).
- **No scope/ownership** — an agent might "fix" this by rewriting the whole seating feature.
- **No verifiable criteria** — nothing here can be checked by an agent or a reviewer.
