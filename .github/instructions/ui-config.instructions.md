---
applyTo: "ui.config/**/*.xml"
---

# Instructions for ui.config

## OSGi configuration rules
- OSGi configs belong here — not in `ui.apps` (OakPAL violation if placed there).
- Use correct runmode folder names: `config`, `config.author`, `config.publish`, `config.dev`, `config.stage`, `config.prod`. Other names are silently ignored in AEMaaCS.
- Config file names must match the OSGi PID exactly, including factory PID format: `com.example.Service~identifier.xml`.
- Do not hardcode secrets or tokens in config values — use Cloud Manager secret environment variables.

## Repoinit
- Service user creation and ACL setup belong here as Repoinit scripts.
- Grant only minimum required privileges for each service user.

## Review focus
- configs placed here vs incorrectly placed in ui.apps
- runmode folder name correctness
- OSGi PID / filename match
- hardcoded secrets
