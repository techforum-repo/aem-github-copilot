---
applyTo: "ui.frontend.spa/**/*.{js,jsx,ts,tsx,css,scss}"
---

# Instructions for `ui.frontend.spa`

## Scope
Use this guidance for the AEM SPA module that depends on AEM model JSON, SPA component mapping, and SPA Editor integration.

## Key rules
- Follow the existing SPA architecture and conventions used in this module.
- Preserve routing, component mapping, and AEM SPA Editor integration points.
- Keep contracts between AEM model JSON and React components explicit.
- Explain authored-content impact when changing mapping, routes, page containers, or data expectations.

## Review focus
- broken model mapping or routing behavior
- regressions in SPA Editor integration
- hidden authored-content or JSON contract changes
