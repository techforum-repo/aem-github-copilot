---
applyTo: "ui.frontend.react/**/*.{js,jsx,ts,tsx,css,scss}"
---

# Instructions for ui.frontend.react

This module contains React-based frontend code integrated with AEM.

## Guidance
- Follow the React conventions already used in this module.
- Preserve current state management, folder structure, and component patterns used nearby.
- Avoid mixing patterns from unrelated modules unless already present.
- Keep components readable and modular.
- Avoid unnecessary re-renders and over-complex component structure.

## AEM integration
- Preserve expected props, mapping, data flow, and integration points with AEM.
- Explain how the React change affects AEM-authored content or rendered behavior if relevant.

## Quality
- Avoid dead code, giant components, and duplicated logic.
- Consider testability, maintainability, and SonarCloud-style readability concerns.