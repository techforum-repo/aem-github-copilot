---
applyTo: "ui.apps/**/*.{html,xml,js,css,scss}"
---

# Instructions for ui.apps

This module contains AEM components, dialogs, templates, and clientlibs.

## HTL security — output context
HTL auto-escapes output but the context must be correct:
- **Never use `${var @ context='unsafe'}`** — this disables all escaping and is a XSS risk. Flag for security review if found.
- **`${var @ context='html'}`** — only for trusted, pre-sanitized HTML. Never for user-supplied input.
- **`${var @ context='uri'}`** — must be used for all href, src, and action attribute values to prevent open redirect and XSS.
- **`${var @ context='scriptString'}`** — required when embedding values inside `<script>` blocks.
- Default context escaping is correct for text content — do not override without reason.

## HTL guidance
- Keep business logic out of HTL.
- Use Sling Models or backend services for computed values.
- Keep templates readable and maintainable.
- Preserve placeholders, edit mode behavior, and authoring support if already present.
- Follow the existing component structure and markup conventions used nearby.

## Dialog guidance
- Keep dialogs consistent with existing project conventions.
- Avoid unnecessary duplication of fields or inconsistent field names.
- Preserve backward compatibility for authored content where practical.
- Be careful when renaming or removing fields because it may affect existing content.

## Clientlib guidance
- Keep JavaScript scoped and modular.
- Avoid unnecessary global variables.
- Follow the existing clientlib organization and categories.
- Do not add dependencies unless there is a clear need.

## General
- Preserve resource type conventions.
- Mention impact across dialog, Sling Model, HTL, and clientlibs when relevant.
- Avoid breaking authoring behavior unless explicitly requested.
- Prefer minimal, targeted changes over broad rewrites.

## OakPAL / Cloud Manager package rules — flag these specifically
These rules are enforced by OakPAL during the Cloud Manager code quality step:

- **Do not place OSGi configuration XML under `/apps`**. OSGi configs must live in `ui.config` under `apps/.../config`, `apps/.../config.author`, `apps/.../config.publish`, etc. Configs in `ui.apps` will cause an OakPAL violation.
- **`ui.apps` is an immutable package** — it must not contain mutable content paths (e.g., `/content`, `/conf` editable templates content). Mutable content belongs in `ui.content`.
- **Package filters must not include `/home`, `/oak:index`, or `/libs`** unless there is a documented and reviewed reason. These paths are high-risk for OakPAL violations.
- **`rep:policy` (ACL) nodes must not appear in `ui.apps`** unless explicitly required and reviewed. Unintentional ACL entries in packages can break security policies on install.
- **Filter roots in `ui.apps` must not overlap with filter roots in other embedded packages** in the `all` module. Overlapping filters cause unpredictable install behavior.
- **Do not include `authorizable` nodes** (users, groups) in application packages.