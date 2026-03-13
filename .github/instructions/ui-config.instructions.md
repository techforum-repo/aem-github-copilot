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

## OakPAL / Cloud Manager config rules — flag these specifically
- **OSGi configuration belongs here, not in `ui.apps`**. Placing config XML under `/apps` in `ui.apps` will trigger an OakPAL violation in Cloud Manager.
- **Use runmode-aware folder naming** to scope configs correctly: `config` (all), `config.author`, `config.publish`, `config.dev`, `config.stage`, `config.prod`. Mismatched runmodes mean configs deploy to the wrong environment.
- **Do not include secrets, tokens, or credentials** in OSGi config XML. Use AEM Cloud Service secret environment variables or the Cloud Manager variable API for sensitive values.
- **Avoid wide-scope or global OSGi factory configurations** that affect all instances unless that is intentional and reviewed.
- **Configuration file names must match the OSGi PID exactly** (including factory PID format `com.example.MyService~identifier.xml`). A mismatch means the config is silently ignored.

## Review focus
- runtime behavior changes
- backward compatibility
- environment sensitivity
- accidental wide-scope config updates
- configs placed here vs incorrectly placed in ui.apps (OakPAL)
- runmode folder correctness
- hardcoded secrets in config values
- OSGi PID / filename correctness