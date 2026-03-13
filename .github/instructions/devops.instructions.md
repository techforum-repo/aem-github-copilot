---
applyTo: "devops/**/*"
---

# Instructions for devops

## Cloud Manager awareness
- Pipeline and quality gate changes affect all environments — treat as deployment-critical.
- Environment variable additions must be coordinated with Cloud Manager environment setup.
- Dispatcher config changes must be validated with the Dispatcher SDK locally before pushing.

## Review focus
- deployment safety and rollback considerations
- Cloud Manager pipeline impact
- environment-specific assumptions
