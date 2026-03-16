---
description: Create or update an AEM component following repository conventions
---

Create or update an AEM component following the conventions already used in this repository.

Before generating code, first provide:
1. the modules and files likely to change across `core`, `ui.apps`, `ui.content`, `ui.config`, and frontend modules if relevant
2. the expected `sling:resourceType`, component mapping, or inheritance pattern
3. any authoring, template, policy, or content impacts
4. key assumptions
5. likely risks and validation points

Requirements:
- reuse nearby component, dialog, Sling Model, clientlib, and template patterns instead of inventing new structure
- use Sling Model or service backing if logic is required
- keep business logic out of HTL
- preserve authoring experience, style system behavior, and existing naming conventions
- call out any required `ui.content` or `ui.config` updates when the component depends on templates, policies, CA config, or OSGi config
- avoid unnecessary refactors or cross-module churn
- suggest tests or validation steps if backend or frontend behavior is introduced or changed

Output format:
1. implementation plan
2. code changes
3. validation steps
