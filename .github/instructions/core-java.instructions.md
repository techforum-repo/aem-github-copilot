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

## WCM Core Components — delegation pattern
If this component extends a WCM Core Component, use the Sling Model delegation pattern:
- Annotate the delegate field with `@Self @Via(type = ResourceSuperType.class)` to delegate to the parent Core Component model.
- Only override the methods or properties that differ from the Core Component behavior.
- Do not re-implement logic already provided by the Core Component model.
- Expose the delegate via the component's Sling Model interface so HTL can access both custom and inherited properties cleanly.

## Code quality
- Keep methods small and focused.
- Avoid deeply nested conditionals.
- Avoid duplication and large utility classes with mixed responsibilities.
- Handle nulls and invalid input explicitly.
- Use meaningful names.
- Log usefully, but avoid noisy or redundant logging.

## SonarCloud rules — flag these specifically
These correspond to rules in the SonarCloud Sonar way Java profile that commonly cause pipeline failures:

- **java:S3776** — Cognitive Complexity must not exceed 15. Count nested conditions, loops, and branches; refactor if exceeded.
- **java:S2095** — Closeable resources (streams, connections, resolvers) must be closed. Use try-with-resources.
- **java:S2259** — Null dereference. Check for null before accessing optional or nullable references.
- **java:S4973** — String and boxed type comparisons must use `.equals()`, not `==`.
- **java:S1206** — If `equals()` is overridden, `hashCode()` must also be overridden and vice versa.
- **java:S106**  — Do not use `System.out` or `System.err`. Use SLF4J (`@Slf4j` or injected `Logger`).
- **java:S2068** — Do not hardcode credentials, tokens, or passwords in source code.
- **java:S108**  — Empty catch blocks must have a comment explaining why the exception is intentionally ignored.
- **java:S1481** — Remove unused local variables.
- **java:S1172** — Remove unused method parameters.
- **java:S107**  — Methods must not have more than 7 parameters. Introduce a parameter object if needed.
- **java:S2696** — Do not write to static non-final fields from instance methods (mutable static state).
- **java:S1161** — Always add `@Override` when implementing or overriding a method.
- **java:S2276** — Do not use `Thread.sleep()` in production code paths (use schedulers or event-driven patterns).
- **java:S1135** — TODO/FIXME comments are code smells; resolve or create a ticket before merging.

## Adobe Cloud Manager rules — flag these specifically
Cloud Manager runs OakPAL and CQ quality rules that block pipeline promotion:

- **CQBP-71** — Do not use deprecated AEM, Sling, or JCR APIs. Check the AEM deprecation annotations and Javadoc.
- **CQBP-72** — `ResourceResolver` must always be closed. Obtain via `try-with-resources` or ensure `close()` is called in a `finally` block. A leaked resolver fails the pipeline.
- **CQBP-75** — Do not call `Thread.sleep()` inside Sling Servlets, Sling Jobs, or OSGi Schedulers. This blocks threads and degrades AEM runtime stability.
- **CQBP-84** — Do not use `System.out` or `System.err` anywhere in production code. Use SLF4J logging only.
- **CQBP-84** — Do not use string concatenation in log statements. Use parameterized logging: `log.debug("Value: {}", value)`.
- **AMSCORE-304** — `ResourceResolver` instances obtained from `ResourceResolverFactory` must be closed in all code paths including exception paths.
- **General** — Do not use `Session` or `ResourceResolver` as static or instance fields without a clear lifecycle management strategy.

## AEM guidance
- Keep presentation logic out of backend classes unless architecture requires it.
- Do not introduce deprecated AEM APIs unless the surrounding code already depends on them and migration is out of scope.
- Preserve adaptation and injection patterns already established in nearby classes.
- Always close `ResourceResolver` and `Session` using try-with-resources or a finally block (CQBP-72, AMSCORE-304).
- Never call `Thread.sleep()` in Servlets, Jobs, or Schedulers (CQBP-75).

## Testing
- Suggest unit tests for changed logic.
- Keep classes easy to test.
- Prefer smaller units of behavior over hard-to-test monoliths.
- Aim for line coverage that meets or exceeds the project quality gate threshold.

## Review focus
- null safety (java:S2259)
- resource leaks — ResourceResolver, Session, streams (CQBP-72, java:S2095)
- cognitive complexity exceeding 15 (java:S3776)
- System.out / System.err usage (java:S106, CQBP-84)
- Thread.sleep in Servlets or Jobs (CQBP-75)
- deprecated API usage (CQBP-71)
- hardcoded credentials (java:S2068)
- empty catch blocks (java:S108)
- test coverage gaps
- string concatenation in log calls (CQBP-84)