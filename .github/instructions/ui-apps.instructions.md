---
applyTo: "ui.apps/**/*.{html,xml,js,css,scss}"
---

# Instructions for ui.apps

This module contains AEM components, dialogs, templates, and clientlibs.

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