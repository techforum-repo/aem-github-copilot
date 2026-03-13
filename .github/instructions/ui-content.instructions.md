---
applyTo: "ui.content/**/*.xml"
---

# Instructions for ui.content

This module contains repository content, site content, mappings, and package content structures.

## Guidance
- Treat content structure changes carefully.
- Keep changes minimal and explicit.
- Avoid broad content moves or renames unless explicitly requested.
- Explain content impact clearly when changing mappings, paths, or repository structure.
- Be cautious with changes that could affect existing authored content, redirects, sitemap behavior, or rollout assumptions.

## OakPAL / Cloud Manager package rules — flag these specifically
- **`ui.content` is a mutable package** — it must not contain immutable paths such as `/apps` or `/libs`. Immutable content belongs in `ui.apps`.
- **Do not include `rep:policy` (ACL) nodes** in content packages unless explicitly required and reviewed by someone with security responsibility.
- **Do not include `authorizable` nodes** (users, groups) in content packages. User and group management must follow the project's identity management approach.
- **Package filters must not include `/oak:index`, `/home`, or `/libs`** unless explicitly required and reviewed.
- **Filter roots must not overlap** with filter roots in other packages embedded in `all`. Overlapping filters produce unpredictable install behavior.
- **`mode="merge"` or `mode="replace"` on filters** affects how existing content is handled on install — flag any non-default filter modes for review.

## Review focus
- content compatibility
- path and mapping impact
- existing authored content risk
- minimality of change
- mutable vs immutable path separation (OakPAL)
- rep:policy or authorizable nodes (OakPAL)
- filter mode changes (merge/replace/update)