---
applyTo: "all/**/*.xml"
---

# Instructions for the all module

This module is the aggregation package. It defines what gets deployed together and controls package embedding and dependency ordering.

## Guidance
- Do not add new embedded packages or dependencies unless explicitly requested.
- Preserve the existing embedding order — it affects deployment correctness.
- Changes here affect what is installed on AEM and in what order; treat them as deployment-critical.
- Filter changes in the `all` module must be consistent with filter changes in the embedded modules.
- Do not remove existing embeds unless the module itself has been removed from the project.

## OakPAL / Cloud Manager rules — flag these specifically
- **Filter roots across all embedded packages must not overlap**. Overlapping filter roots between `ui.apps`, `ui.content`, `ui.config`, and `ui.apps.structure` will cause OakPAL violations and unpredictable install behavior.
- **Embedding order matters**. `ui.apps.structure` must be embedded before `ui.apps`. `ui.apps` must be embedded before `ui.content` and `ui.config`. Incorrect order can break package installation.
- **Do not add filters directly in the `all` package** for content that should be owned by an embedded sub-package. Filters in `all` should only cover paths not owned by any sub-package.
- **The `all` package must embed all sub-packages required for a complete deployment**. A missing embed means that module is not deployed by Cloud Manager.

## Review focus
- missing or mismatched embeds after module additions
- incorrect filter paths that could cause content to be deleted on install
- overlapping filter roots across embedded packages (OakPAL)
- embedding order correctness (ui.apps.structure → ui.apps → ui.content/ui.config)
- ordering issues that could break dependencies between packages
- unnecessary changes that could destabilize the deployment
