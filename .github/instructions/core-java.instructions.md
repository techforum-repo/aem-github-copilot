---
applyTo: "core/**/*.java"
---

# Instructions for Java files in core

## Project-specific patterns
- Prefer Sling Models for component-backed logic; OSGi services for shared logic.
- Follow existing package structure, annotation style, and injection patterns used in nearby classes.
- Reuse existing utilities and helpers before introducing new ones.

## WCM Core Components delegation
If this component extends a WCM Core Component, use the delegation pattern:
- Annotate the delegate with `@Self @Via(type = ResourceSuperType.class)`.
- Only override what differs from the Core Component — do not re-implement inherited logic.

## AEMaaCS-specific rules
- Never use admin `ResourceResolver` or `loginAdministrative` — use a service user.
- Always close `ResourceResolver` and `Session` with try-with-resources (CQBP-72).
- Never call `Thread.sleep()` in Servlets, Jobs, or Schedulers (CQBP-75).
- Use SLF4J parameterized logging only — no `System.out`, no string concatenation in log calls (CQBP-84).
- Do not use deprecated AEM/Sling/JCR APIs (CQBP-71).

## Review focus
- admin resolver or session usage
- unclosed ResourceResolver or Session
- Thread.sleep in Servlets or Jobs
- deprecated API usage
- System.out / System.err
- test coverage gaps
