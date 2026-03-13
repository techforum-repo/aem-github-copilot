# GitHub Copilot Instructions for This Repository

This repository is an Adobe Experience Manager project with multiple modules for backend code, AEM components and content, frontend implementations, and Adobe Cloud Manager support.

## Repository structure
- `core/` contains Java backend code such as Sling Models, OSGi services, servlets, schedulers, configuration classes, and business logic.
- `ui.apps/` contains AEM components, dialogs, templates, clientlibs, and application-level repository definitions.
- `ui.apps.structure/` contains structural package or repository definitions used by the application.
- `ui.content/` contains content package structures, repository content, site content, and related mappings.
- `ui.config/` contains AEM configuration content and environment-aware configuration artifacts.
- `ui.frontend/` contains frontend assets and general frontend code integrated with AEM.
- `ui.frontend.react/` contains React-based frontend code integrated with AEM.
- `ui.frontend.spa/` contains SPA-related frontend code integrated with AEM.
- `all/` is the package aggregation module.
- `devops/` contains deployment, automation, or environment support files.
- `hooks/` contains local developer workflow or pre-commit related scripts.

## General expectations
- Follow existing repository conventions before introducing new patterns.
- Prefer consistency with nearby code over generic best practices that conflict with the repo.
- Keep changes minimal, scoped, and reviewable.
- Reuse existing services, utilities, component patterns, helper functions, and frontend conventions where possible.
- Do not invent project-specific APIs, services, resource types, or utilities that do not already exist in the repository unless explicitly requested.
- Do not modify generated files, package filters, deployment structure, or build logic unless explicitly requested.
- Explain assumptions briefly when suggesting non-trivial changes.

## AEM expectations
- Prefer Sling Models for component-backed logic.
- Keep business logic out of HTL.
- Keep HTL presentation-focused and maintainable.
- Preserve authoring behavior, placeholders, and editing experience unless change is explicitly requested.
- Respect existing component inheritance, resource type conventions, dialog patterns, and clientlib organization.
- Avoid deprecated AEM APIs where practical.
- Be careful with repository content, mappings, package filters, and OSGi config changes.

## Java expectations
- Write maintainable, testable Java code.
- Keep methods focused and readable.
- Avoid duplication and unnecessary complexity.
- Handle nulls and edge cases explicitly.
- Follow the repository's existing dependency injection and annotation style.
- Suggest tests when logic is added or changed.

## Frontend expectations
- Follow the conventions of the module being edited.
- Do not mix React, SPA, and non-SPA patterns unless the codebase already does so in that area.
- Keep components modular and readable.
- Avoid unnecessary dependencies and broad refactors unless requested.
- Preserve AEM integration patterns for rendered markup, data attributes, and clientlibs.

## SonarCloud expectations
- Avoid dead code, duplication, and overly complex methods or components.
- Prefer small, readable units of logic.
- Watch for null-safety, maintainability, readability, and testability issues.
- Point out likely code smells and the smallest safe fix.

## Adobe Cloud Manager expectations
- Consider AEM Cloud Manager code quality expectations when suggesting changes.
- Avoid risky repository or session handling patterns.
- Avoid heavy logic in presentation layers.
- Keep code secure, maintainable, and aligned with AEM engineering practices.
- Mention likely pipeline or code quality risks when relevant.

## Additional guidance
- Prefer nearby implementations in the same module as the primary pattern source.
- When working on AEM components, identify related dialog, HTL, Sling Model, clientlib, frontend, and content/config files only when relevant.
- Prefer the smallest safe implementation that avoids increasing duplication, complexity, or pipeline risk.

## Output expectations
When proposing changes:
1. align with the conventions of the current module
2. explain assumptions briefly
3. mention likely risks for SonarCloud or Cloud Manager if relevant
4. keep implementations minimal and practical
5. suggest tests or validation steps when appropriate

When reviewing code:
- review for AEM best practices
- review for SonarCloud-style maintainability concerns
- review for likely Cloud Manager quality concerns
- review for test gaps
- review for null-safety, security, and integration risks