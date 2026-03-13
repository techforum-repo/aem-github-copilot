---
description: Create or update unit tests for a Sling Model, OSGi service, or utility class
---

Create or update unit tests for the selected class following the conventions already used in this repository's test suite.

Requirements:
- follow the existing test framework setup (JUnit 5, Mockito, AemContext where applicable)
- use `AemContext` for Sling Model tests and component-backed logic
- use `@ExtendWith(MockitoExtension.class)` for service or utility tests with no AEM context needed
- cover null inputs, edge cases, and primary behavior paths
- name test methods to describe behavior clearly
- keep each test focused on one behavior
- avoid over-mocking — prefer real objects where construction is simple

Before generating tests:
1. identify which test framework and base patterns are already used in nearby test files
2. list the behaviors and edge cases to cover
3. state assumptions about dependencies or AemContext registration needs
4. mention any SonarCloud or coverage concerns if relevant
