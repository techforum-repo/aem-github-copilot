# Copilot request cheatsheet

## How to use this file

### Invoke prompts in Copilot Chat
Open GitHub Copilot Chat in VS Code, type `/`, and select a prompt from `.github\prompts\`.

### Copilot CLI and VS Code compatibility
This repository guidance is designed to work in both GitHub Copilot CLI and GitHub Copilot Chat in VS Code.

- In Copilot CLI, `.github\copilot-instructions.md` and `.github\instructions\` are applied automatically when the repository is in scope.
- In VS Code, the same instruction files apply, and prompt files in `.github\prompts\` are easier to discover through the slash-command picker.
- The request examples in this cheatsheet work in both tools, even when an entry is marked as a freeform example rather than a prompt file.

### How scoped instructions work
Files in `.github\instructions\` are applied automatically when the open file matches the `applyTo` pattern. You do not need to reference those instruction files manually.

### Tips for better results
- Attach the relevant file or folder as context whenever possible.
- For multi-file work, list the exact files after the prompt.
- Replace every `[placeholder]` before sending the request.
- Prefer concrete paths and clear change descriptions over generic wording.

### When LSP is available, prefer symbol-first requests
If Copilot CLI has working LSP support for the repo, prefer requests anchored to symbols instead of only file paths.

Better anchors include:
- class names
- interface names
- method names
- fields or constants
- callers, implementors, and dependencies

Examples:
- `Trace where JWTAuthenticationService is implemented and used in this repository.`
- `Explain SecurePageFilter and follow its direct dependencies.`
- `Show callers of validateAccessToken(...) and explain what could break if I change it.`
- `Compare SecurePageFilter and TokenIntrospectServlet in the authentication flow.`

### How to read the examples below
- Entries marked with `Prompt file:` correspond directly to a slash prompt in `.github\prompts\`.
- Entries marked with `Freeform example:` are ready-to-use requests you can paste into chat, even though they are not backed by a prompt file.

---

## Component requests

### Explain a component
Prompt file: `explain-aem-component.prompt.md`

Explain the AEM component at `[ui.apps component path]` and the related files across `core`, `ui.content`, `ui.config`, and frontend modules if relevant.

### Review a component end to end
Freeform example:

Review the AEM component at `[ui.apps component path]` end to end for AEM best practices, SonarCloud concerns, Cloud Manager risks, authoring impact, and missing validation.

### Identify impacted files
Freeform example:

For the change `[brief description]`, identify the files likely to change across `core`, `ui.apps`, `ui.content`, `ui.config`, and frontend modules.

### Create or update a component
Prompt file: `create-aem-component.prompt.md`

Help me create or update the AEM component at `[ui.apps component path]` following repository conventions.

### Review HTL and dialog
Freeform example:

Review these files for AEM best practices, HTL safety, authoring impact, and backward compatibility:
- `[HTL file path]`
- `[dialog xml path]`

---

## Sling Model and backend requests

### Review a Sling Model
Freeform example:

Review this Sling Model for repository conventions, null handling, unnecessary logic, performance issues, SonarCloud concerns, and missing tests:
`[core sling model path]`

Symbol-first variant:

Review the Sling Model class `[ClassName]` and explain its injectables, consumers, fallback behavior, and likely risks.

### Create or update a Sling Model
Prompt file: `create-sling-model.prompt.md`

Create or update a Sling Model for `[ui.apps component path]` following repository conventions.

### Review a Java class
Freeform example:

Review this Java file for AEM best practices, null safety, complexity, duplication, SonarCloud concerns, and Cloud Manager risks:
`[core java file path]`

Symbol-first variant:

Review the class `[ClassName]` or method `[methodName(...)]` for AEM best practices, complexity, null safety, and likely change risk.

### Create or refactor an OSGi service
Prompt file: `create-osgi-service.prompt.md`

Create or refactor an OSGi service for `[feature or use case]` following repository conventions.

### Explain backend flow
Freeform example:

Explain how this backend code works, which AEM components or services depend on it, and what could break if it changes:
`[core java file path]`

Symbol-first variant:

Explain `[ClassName]` and trace its direct dependencies, implementors, callers, and likely runtime role in the AEM request flow.

---

## Servlet, scheduler, and workflow requests

### Create or update a Sling Servlet
Prompt file: `create-servlet.prompt.md`

Create or update a Sling Servlet for `[use case]` following repository conventions.

### Review a servlet
Freeform example:

Review this Sling Servlet for registration choice, input validation, service user usage, null safety, SonarCloud concerns, and Cloud Manager risks:
`[core servlet file path]`

Symbol-first variant:

Review servlet class `[ClassName]`, explain its registration style, callers or request entry points, and identify the smallest safe cleanup opportunities.

### Create or update a Scheduler or Job
Prompt file: `create-scheduler.prompt.md`

Create or update an OSGi Scheduler or Sling Job for `[use case]` following repository conventions.

### Review a scheduler or job
Freeform example:

Review this Scheduler or Job for `Thread.sleep()` usage, admin resolver usage, exception handling, configurability, and Cloud Manager risks:
`[core scheduler or job file path]`

Symbol-first variant:

Explain scheduler or job class `[ClassName]`, trace what it invokes, and review whether its execution model is safe for AEMaaCS.

### Create a workflow process step
Prompt file: `create-workflow-step.prompt.md`

Create a custom AEM workflow process step for `[use case]` following repository conventions.

---

## Frontend requests

### Review frontend integration
Freeform example:

Review this frontend change in the context of AEM integration, authored content, rendered markup, and repository conventions:
`[frontend file path]`

Symbol-first variant:

Explain component `[ComponentName]` or function `[functionName]` and how it maps to AEM markup, clientlibs, model data, and authored content.

### Explain frontend linkage
Freeform example:

Explain how this frontend file is connected to AEM rendering, clientlibs, authored content, and backend data if applicable:
`[frontend file path]`

### Create or update frontend code
Prompt file: `create-frontend-integration.prompt.md`

Create or update frontend code for `[feature or component]` following the conventions of this frontend module.

---

## Test requests

### Create unit tests
Prompt file: `create-unit-test.prompt.md`

Create unit tests for this class following repository test conventions:
`[core java file path]`

### Review existing tests
Freeform example:

Review these tests for coverage gaps, over-mocking, missing edge cases, and `AemContext` misuse:
`[core test file path]`

### Add edge-case coverage
Freeform example:

Identify the missing null, empty, and error-path test cases for this class and generate them:
`[core java file path]`

---

## Quality and review requests

### General review
Prompt file: `review-aem-code.prompt.md`

Review these changes for AEM best practices, SonarCloud issues, Cloud Manager risks, null safety, duplication, complexity, and missing tests:
- `[file path 1]`
- `[file path 2]`

### Sonar and Cloud Manager focused review
Prompt file: `review-sonar-cloudmanager.prompt.md`

Review this implementation specifically for SonarCloud-style maintainability issues and likely Adobe Cloud Manager concerns:
`[file or folder path]`

### Null safety and complexity check
Freeform example:

Review this file for null safety, exception handling, deeply nested logic, duplication, and the smallest practical cleanups:
`[file path]`

### Test gap review
Freeform example:

Review this change and tell me what unit tests or integration tests are missing:
`[file or folder path]`

---

## Security and performance requests

### Review for security issues
Freeform example:

Review these files for service user usage, HTL XSS context, input validation, admin resolver usage, and sensitive data exposure:
- `[file path 1]`
- `[file path 2]`

### Create service user and Repoinit
Prompt file: `create-repoinit.prompt.md`

Create a Repoinit script and service user mapping for `[service or use case]` with least-privilege ACLs.

### Review for JCR query and performance issues
Freeform example:

Review this file for unindexed queries, queries in render paths, unbounded result sets, and `ResourceResolver` lifecycle issues:
`[file or folder path]`

---

## Bug investigation requests

### Investigate a bug
Prompt file: `investigate-bug.prompt.md`

Help me investigate this bug in the context of this repository: `[brief bug description]`. Start with likely impacted modules and root causes.

Symbol-first variant:

Investigate the issue around `[ClassName]`, `[interfaceName]`, or `[methodName(...)]` and trace likely root causes, callers, and impacted modules.

### Compare two implementations
Freeform example:

Compare these two implementations and tell me which better fits repository conventions, AEM best practices, and maintainability expectations:
- `[file path 1]`
- `[file path 2]`

### Trace impact
Freeform example:

Trace where this component or service is used and what could break if I change it:
`[file or folder path]`

Symbol-first variant:

Trace where `[ClassName]`, `[interfaceName]`, or `[methodName(...)]` is implemented, called, or referenced, and summarize what could break if it changes.

---

## PR and release requests

### Explain pipeline impact
Prompt file: `explain-pipeline-impact.prompt.md`

Explain the likely Cloud Manager pipeline, deployment, and runtime impact of these changes:
- `[file path 1]`
- `[file path 2]`

### Draft PR summary
Prompt file: `draft-pr-summary.prompt.md`

Draft a pull request summary for these changes:
- `[file path 1]`
- `[file path 2]`

### Draft testing notes
Freeform example:

Draft reviewer notes and testing notes for this change:
`[file or folder path]`

### Risks and rollback
Freeform example:

Summarize implementation risks, deployment impact, and rollback considerations for this change:
`[file or folder path]`

---

## Git and repository workflow requests

These are especially useful in Copilot CLI alongside built-in commands such as `/diff`, `/pr`, and `/review`.

### Summarize current changes
Freeform example:

Summarize my current staged and unstaged changes, grouped by module, and explain their purpose in the context of this repository.

### Explain staged vs unstaged work
Freeform example:

Compare my staged and unstaged changes and tell me whether they represent one logical change or should be split before commit.

### Draft a commit message
Freeform example:

Draft a commit message for my current changes using the repository context and changed files. Include a short subject and a concise body.

### Review commit readiness
Freeform example:

Review my current diff and tell me whether it is ready to commit. Call out missing tests, risky changes, and anything that should be cleaned up first.

### Assess PR risk from changed files
Freeform example:

Based on my changed files, summarize likely deployment, authoring, configuration, and release risks for this repository.

---

## Dispatcher and refactor requests

### Review Dispatcher configuration
Freeform example:

Review this Dispatcher configuration for default-deny filters, sensitive path exposure, security response headers, cache rules, and Cloud Manager SDK compatibility:
`[dispatcher config file path]`

### Suggest minimal refactor
Freeform example:

Suggest the smallest safe refactor for this file while preserving behavior:
`[file path]`

### Align with repository conventions
Freeform example:

Refactor this code to better match repository conventions without changing behavior:
`[file path]`

---

## Understanding and onboarding requests

### Explain a file
Freeform example:

Explain this file in the context of the repository and related modules:
`[file path]`

### Onboard me to this area
Freeform example:

Help me understand this area of the repository, the main files involved, and what to inspect next:
`[folder path]`
