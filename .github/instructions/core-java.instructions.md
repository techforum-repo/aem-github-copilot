---
applyTo: "core/**/*.java"
---

# Instructions for Java files in core

This module contains AEM backend Java code.

## Preferred patterns
- Prefer Sling Models for component-backed logic.
- Use OSGi services for shared or reusable business logic.
- Follow existing service interfaces, package conventions, and naming patterns.
- Reuse existing utilities and helper classes before introducing new ones.
- Follow the existing annotation and injection style already used in the repository.

## Code quality
- Keep methods small and focused.
- Avoid deeply nested conditionals.
- Avoid duplication and large utility classes with mixed responsibilities.
- Handle nulls and invalid input explicitly.
- Use meaningful names.
- Log usefully, but avoid noisy or redundant logging.

## AEM guidance
- Keep presentation logic out of backend classes unless architecture requires it.
- Do not introduce deprecated AEM APIs unless the surrounding code already depends on them and migration is out of scope.
- Preserve adaptation and injection patterns already established in nearby classes.
- Be mindful of resolver/session usage and close resources properly where applicable.

## Testing
- Suggest unit tests for changed logic.
- Keep classes easy to test.
- Prefer smaller units of behavior over hard-to-test monoliths.

## Review focus
- null safety
- exception handling
- unnecessary complexity
- test coverage gaps
- AEM anti-patterns
- SonarCloud-style maintainability issues