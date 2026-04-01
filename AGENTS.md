# Agent Instructions

This repository contains an Adobe Experience Manager as a Cloud Service (AEMaaCS) project. Apply AEM package boundaries, Cloud Manager safety rules, and existing module conventions before suggesting or generating changes.

## Module structure

- `core/` — Sling Models, OSGi services, servlets, schedulers, workflow steps, and shared Java logic
- `ui.apps/` — AEM components, dialogs, HTL, clientlibs, and immutable `/apps` content
- `ui.apps.structure/` — repository structure definitions that must install before `ui.apps`
- `ui.content/` — mutable content, editable templates, policies, and experience/content structure
- `ui.config/` — OSGi configurations, service user mappings, and Repoinit scripts
- `ui.frontend/`, `ui.frontend.react/`, `ui.frontend.spa/` — distinct frontend modules with different integration patterns
- `all/` — aggregation package that embeds deployable modules
- `it.tests/` — integration tests run by Cloud Manager after deployment against a live AEM environment
- `ui.tests/` — UI tests run by Cloud Manager against the publish environment using browser automation
- `devops/` — deployment, environment, and pipeline-related assets
- `hooks/` — local developer workflow scripts

## Java version

This project targets **Java 21**. Prefer Java 21 language features:
- Records for immutable value objects and DTOs
- Pattern matching for `instanceof`
- Text blocks for multi-line strings (JCR-SQL2, JSON)
- Switch expressions (`->` syntax)
- `var` for local variable type inference where the type is obvious
- Sealed classes to restrict Sling Model or service hierarchies

## Core rules

- Prefer Sling Models for component-backed presentation logic and OSGi services for reusable business logic.
- Keep business logic out of HTL.
- Place OSGi configuration and Repoinit in `ui.config`, not `ui.apps`.
- Keep `ui.apps` immutable; keep mutable content in `ui.content`.
- Use service users for repository access — never use admin `ResourceResolver` or `loginAdministrative`.
- Always close `ResourceResolver` and `Session` objects correctly.
- Never call `Thread.sleep()` in servlets, jobs, schedulers, or workflow steps.
- Use SLF4J parameterized logging only; do not use `System.out`, `System.err`, or string concatenation in log calls.
- Ensure JCR queries are indexed, bounded, and not executed in tight rendering loops.
- Follow existing patterns in the same module before introducing new abstractions or structures.

## Change guidance

- Keep changes minimal, scoped, and aligned with the owning module.
- Call out assumptions for non-trivial work.
- Mention Cloud Manager, OakPAL, Dispatcher, or SonarCloud risks when they are relevant.
- Suggest validation steps or tests when logic, rendering, configuration, or packaging changes.

## Build commands

- Full build: `mvn clean install`
- Deploy to author: `mvn clean install -PautoInstallPackage -Daem.host=localhost -Daem.port=4502`
- Build without tests: `mvn clean install -DskipTests`
- Run tests only: `mvn test`
- Format code: `mvn spotless:apply`

## Code tracing

- For definition, reference, implementation, and rename requests, use LSP symbol tracing first when available.
- Provide exact file and line locations for each result.
- Fall back to text search only when LSP is unavailable and state the fallback reason.
