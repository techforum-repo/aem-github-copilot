---
applyTo: "devops/**/*"
---

# Instructions for devops

These files support deployment, automation, or environment-related workflows.

## Guidance
- Keep changes explicit and minimal.
- Preserve current workflow assumptions unless requested otherwise.
- Explain operational impact of changes.
- Avoid hidden behavior changes in scripts or automation.

## Cloud Manager pipeline awareness
- Pipeline configuration changes affect all environments — treat them as deployment-critical.
- Quality gate changes (coverage thresholds, SonarCloud ratings) must be intentional and agreed upon.
- Environment variable additions or changes must be coordinated with the Cloud Manager environment setup.
- Dispatcher configuration is validated during the pipeline — test with the Dispatcher SDK locally before pushing.

## Review focus
- deployment safety
- environment assumptions
- script readability
- rollback considerations
- Cloud Manager pipeline impact
- Dispatcher SDK compatibility if Dispatcher config is changed