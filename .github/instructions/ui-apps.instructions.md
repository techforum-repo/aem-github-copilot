---
applyTo: "ui.apps/**/*.{html,xml,js,css,scss}"
---

# Instructions for ui.apps

## HTL security — output context
- Never use `${var @ context='unsafe'}` — disables all escaping, flag for security review.
- Use `${var @ context='uri'}` for all href, src, and action values.
- Use `${var @ context='html'}` only for trusted, pre-sanitized HTML — never for user input.
- Use `${var @ context='scriptString'}` when embedding values inside `<script>` blocks.

## HTL
- Keep business logic out of HTL — use Sling Models for computed values.
- Preserve placeholders and edit mode behavior.

## Dialogs
- Preserve backward compatibility — renaming or removing fields breaks existing authored content.

## OakPAL rules
- `ui.apps` is immutable — no `/content` paths, no mutable `/conf` editable template content.
- No OSGi configuration XML here — belongs in `ui.config`.
- No `rep:policy` nodes unless explicitly reviewed.
- No `authorizable` nodes.
- Filter roots must not overlap with other packages in `all`.
