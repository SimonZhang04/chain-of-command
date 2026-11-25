- should spawn a worktree to avoid conflicting with other agents that might be working on the same machine
- MUST include tests for all new functionality. Must run and pass tests before putting up a PR
- should not regress on previous tests, unless we are changing functionality or a feature
- should not exceed or underserve the scope of the issue

## PR Formatting

A new PR should include the following sections:

1. **Title**: Should reference the issue number and issue title.
2. **Description**: A brief description of the changes made in the PR, including any relevant context or background information. Should include a clickable link to the issue being addressed.
3. **UI Changes**: If applicable, describe using words any changes made to the user interface.
4. **Testing**: Describe any testing that was done to ensure the changes work as expected, and how they protect against regressions.
5. **Implementation Notes**: Any relevant notes about the implementation, such as design decisions, trade-offs made during development, or blockers.
