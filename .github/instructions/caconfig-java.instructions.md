---
applyTo: "core/src/main/**/*.java"
---

# Java instructions for Sling Context-Aware Configuration (CAConfig)

## Scope
Apply these rules when Java code in `core` defines or consumes Sling Context-Aware Configuration.

## Configuration interface

- Define CAConfig types as `@interface` declarations annotated with `@Configuration` (`org.apache.sling.caconfig.annotation.Configuration`).
- Set `name` and `label` on `@Configuration` so the editor remains understandable for authors and administrators.
- Give every property a default to keep resolution safe when no content configuration exists.
- Use `@Property` labels and descriptions for author-facing clarity.

## Java usage

- Resolve CAConfig from request- or resource-scoped code, typically Sling Models, not from singleton OSGi service state.
- Inject `ConfigurationBuilder` and resolve with `configurationBuilder.as(MyConfig.class)` rather than reading raw `ValueMap` structures.
- Treat resolved config objects as request-scoped data; do not cache them in OSGi fields.
- Handle inherited/defaulted values explicitly in business logic instead of assuming authored config exists.

## Review focus

- Is the `@Configuration` interface in `core`, not a UI module?
- Are defaults defined for every property?
- Is the config resolved per request or per adaptation rather than cached globally?
- Is Java code using typed CAConfig interfaces instead of raw maps?
