---
applyTo: "core/src/test/**/*.java"
---

# Instructions for Java test files in core

## Framework
- Use `AemContext` for Sling Model and component tests.
- Use `@ExtendWith(MockitoExtension.class)` for service or utility tests with no AEM context needed.
- Follow the test class structure and naming conventions used in nearby test files.

## Scope
- Test actual behavior — not just mock setup.
- Cover null inputs, edge cases, and primary behavior paths.
- Keep each test focused on one behavior.

## Review focus
- missing null and edge case coverage
- tests that only pass due to mock setup
- missing assertions
- AemContext misuse
