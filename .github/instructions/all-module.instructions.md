---
applyTo: "all/**/*.xml"
---

# Instructions for the all module

## OakPAL and deployment rules
- Embedding order matters: `ui.apps.structure` → `ui.apps` → `ui.content` and `ui.config`. Wrong order breaks installation.
- Filter roots across all embedded packages must not overlap — causes OakPAL violations and unpredictable installs.
- Do not add or remove embeds unless explicitly requested — a missing embed means that module is not deployed.
- Do not add content filters directly in `all` for paths owned by a sub-package.

## Review focus
- embedding order correctness
- overlapping filter roots across packages
- missing embeds after module additions
- filter paths that could delete content on install
