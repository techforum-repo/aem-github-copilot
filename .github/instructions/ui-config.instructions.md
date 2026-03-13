---
applyTo: "ui.config/**/*.xml"
---

# Instructions for ui.config

This module contains AEM configuration content.

## Guidance
- Treat OSGi and environment configuration carefully.
- Keep configuration changes explicit and minimal.
- Preserve environment-safe defaults where possible.
- Avoid large or risky configuration updates unless explicitly requested.
- Explain expected runtime impact of configuration changes.

## Review focus
- runtime behavior changes
- backward compatibility
- environment sensitivity
- accidental wide-scope config updates