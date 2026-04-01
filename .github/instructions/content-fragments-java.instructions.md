---
applyTo: "core/src/main/**/*.java"
---

# Java instructions for Content Fragments and headless delivery

## Scope
Apply these rules when Java code in `core` reads, writes, or exposes Content Fragment data.

## Content Fragment access

- Adapt `Resource` to `ContentFragment` with `resource.adaptTo(ContentFragment.class)` and null-check the result.
- Access fields through `ContentFragment.getElement(name)` and handle missing elements safely.
- Never adapt `SlingHttpServletRequest` directly to `ContentFragment`.
- For programmatic fragment creation or updates, use supported APIs such as `AssetManager` or `FragmentTemplate` instead of manual JCR writes.

## Headless delivery integration

- Keep headless delivery aligned with persisted GraphQL queries; do not create custom Java endpoints that expose raw repository structure unnecessarily.
- Do not leak internal repository paths, schema assumptions, or sensitive content details in logs or responses.
- Treat field-name changes and variation handling as backward-compatibility concerns for consuming clients.

## Review focus

- Are `ContentFragment` and `ContentElement` accesses null-safe?
- Does the code avoid raw JCR writes for fragment creation/update?
- Does the implementation preserve existing fragment contracts and variation handling?
- Is Java code avoiding custom endpoints where the GraphQL servlet should own delivery?
