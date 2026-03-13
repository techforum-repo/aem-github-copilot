---
applyTo: "ui.content/**/*.xml"
---

# Instructions for ui.content

## OakPAL rules
- `ui.content` is mutable — no `/apps` or `/libs` paths.
- No `rep:policy` nodes unless explicitly reviewed.
- No `authorizable` nodes (users, groups).
- No `/oak:index`, `/home`, or `/libs` in filter roots.
- Filter roots must not overlap with other packages in `all`.
- Non-default filter modes (`merge`, `replace`) affect existing content on install — flag for review.

## Review focus
- mutable vs immutable path separation
- rep:policy or authorizable nodes
- filter mode changes
- impact on existing authored content
