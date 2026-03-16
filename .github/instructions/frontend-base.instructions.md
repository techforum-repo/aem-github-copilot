---
applyTo: "ui.frontend/**/*.{js,jsx,ts,tsx,css,scss}"
---

# Instructions for `ui.frontend`

## Scope
Use this guidance for the traditional frontend/clientlib module that integrates with AEM-rendered markup.

## Key rules
- Follow the patterns already used in this module; do not mix in SPA or other frontend-module conventions.
- Preserve integration with AEM-rendered markup, data attributes, and clientlib categories.
- Keep assumptions about authored content and server-rendered HTML explicit.
- Call out any required changes to HTL, dialogs, or clientlib inclusion when frontend behavior depends on them.

## Review focus
- accidental mixing of patterns from other frontend modules
- broken markup or clientlib contracts with AEM components
- hidden assumptions about authored content or DOM structure
