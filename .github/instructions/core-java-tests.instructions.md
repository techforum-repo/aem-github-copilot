---
applyTo: "core/src/test/**/*.java"
---

# Instructions for Java test files in core

This module uses JUnit 5 and Mockito for unit testing. AEM-specific tests use the AEM Mocks library (AemContext).

## Preferred patterns
- Use `AemContext` from `io.wcm.testing.mock.aem` or `org.apache.sling.testing.mock.sling` for Sling Model and component tests.
- Use `@ExtendWith(MockitoExtension.class)` for service and utility tests that do not require AEM context.
- Follow the test class structure and naming conventions already used in nearby test files.
- Name test methods clearly to describe behavior, not implementation (e.g., `shouldReturnNullWhenResourceNotFound`).

## Test scope
- Unit test Sling Models by registering them on an `AemContext` and adapting from a resource or request.
- Unit test OSGi services by activating them with a config object or mock collaborators.
- Do not write tests that only verify mocking setup — test actual behavior.
- Keep tests focused on one unit of behavior per test method.

## Quality
- Avoid test duplication across test classes.
- Keep setup concise — prefer `@BeforeEach` for shared context setup.
- Do not introduce test utilities or helpers that are not already used in the repository unless the need is clear.
- Avoid over-mocking: prefer real objects where construction is simple.

## Review focus
- missing coverage for null/edge cases
- tests that only pass due to mock setup rather than real behavior
- AemContext misuse or unnecessary context scope
- missing assertions
