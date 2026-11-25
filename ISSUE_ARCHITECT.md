# Issue Architect

This document describes how to create GitHub issues for the Chain of Command game project. The goal is to ensure that issues are clear, unambiguous, actionable, and easy to understand for other agents and contributors working to complete the game.

## Structure of an Issue

Issues should follow a consistent structure, with the following sections:

1. **Title**: A concise summary of the issue, ideally a statement of the problem or task to be completed. Use imperative mood and specific language. For example, "Implement player seating detection using NearbyInteraction on game start" is better than "Player seating detection". Further examples: "Add 'Redetect' button for player seating detection" or "Fix UI bug in visualization of player seating circle".
2. **Context**: A brief description of the context or background of the issue. This section should provide enough information for an agent/contributor who has decent context of the project to understand the issue without needing to read through all previous issues or documentation. Include relevant links to related issues.
3. **Scope**: A clear definition of what should and should not be done for this task.
4. **Acceptance Criteria**: A list of specific, measurable conditions that must be met for the issue to be considered complete. This section should include any relevant technical details, such as expected behavior.

An example of a well-structured issue is provided below, although note that it is not specifically relevant to this project, and doesn't necessarily have sufficient detail or length. It should serve only as a template.

# Implement terrain generation

## Context

Reconstruct the terrain-generation algorithm from the original game.

## Scope

- Implement `TerrainGenerator`.
- Do not modify the RNG or noise implementations.
- Do not modify rendering.
- Own `terrain_generator.rs` and its dedicated tests.

## Acceptance Criteria

- Same seed produces identical terrain.
- Sampled height values match the reference outputs.
- No regressions in existing terrain tests.
- Performance benchmark remains within the specified limit.
