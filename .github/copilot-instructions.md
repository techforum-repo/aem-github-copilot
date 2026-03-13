# GitHub Copilot Instructions for This Repository

This is an Adobe Experience Manager as a Cloud Service (AEMaaCS) project.

## Module structure
- `core/` — Sling Models, OSGi services, servlets, schedulers, business logic
- `ui.apps/` — AEM components, dialogs, HTL, clientlibs (immutable package — no `/content` paths)
- `ui.apps.structure/` — repository structure definitions
- `ui.content/` — mutable content (no `/apps` or `/libs` paths)
- `ui.config/` — OSGi configurations and Repoinit scripts (not in `ui.apps`)
- `ui.frontend/`, `ui.frontend.react/`, `ui.frontend.spa/` — frontend modules (do not mix patterns across them)
- `all/` — aggregation package
- `devops/` — deployment and environment support
- `hooks/` — local developer workflow scripts

## Key rules for this project
- Sling Models for component logic — keep business logic out of HTL
- OSGi services for shared or reusable logic
- All JCR access must use a service user — never admin `ResourceResolver` or `loginAdministrative`
- `ResourceResolver` must always be closed with try-with-resources (CQBP-72)
- OSGi configs belong in `ui.config`, not `ui.apps` (OakPAL)
- No `Thread.sleep()` in Servlets, Jobs, or Schedulers (CQBP-75)
- SLF4J only — no `System.out` or `System.err` (CQBP-84)
- All JCR queries must be backed by an Oak index

## Conventions
- Follow patterns already used in the same module — do not introduce new patterns unless asked
- Do not modify package filters, build config, or generated files unless explicitly requested
- Keep changes minimal and scoped

## Output
- Explain assumptions briefly for non-trivial changes
- Mention Cloud Manager or SonarCloud risks when relevant
- Suggest tests when logic is added or changed
