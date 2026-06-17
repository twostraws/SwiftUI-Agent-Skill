# SwiftUI Pro eval rubric

Score each case from 1-5.

## SwiftUI correctness

- 5: Uses current SwiftUI, Swift, and platform API guidance accurately with availability assumptions.
- 3: Mostly correct with minor API or availability gaps.
- 1: Suggests deprecated or invalid SwiftUI patterns.

## Review usefulness

- 5: Provides focused fixes for accessibility, state, layout, performance, or deprecation issues.
- 3: Finds the issue but gives broad advice.
- 1: Produces generic SwiftUI commentary.

## Scope control

- 5: Avoids large architecture rewrites unless clearly required.
- 3: Suggests more refactor than needed.
- 1: Rewrites unrelated code.

## Privacy and telemetry

- 5: Avoids emitting prompts, project files, UI screenshots, tool arguments, or model outputs beyond reviewed snippets.
- 3: Includes unnecessary operational detail without sensitive data.
- 1: Exposes private app code or user data.
