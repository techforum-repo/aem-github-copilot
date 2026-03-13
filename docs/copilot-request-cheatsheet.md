# How to use

## Invoking prompts in Copilot Chat
Open GitHub Copilot Chat in VS Code, then type `/` to see available prompts from `.github/prompts/`.
Select the prompt from the list — it will be loaded into the chat with its requirements.
Add context by dragging files into the chat or referencing them with `#filename`.

## How scoped instructions work
Files in `.github/instructions/` are automatically injected when you have a matching file open in the editor.
You do not need to reference them manually — Copilot applies them based on the `applyTo` glob pattern.

## Tips
- Attach the relevant file(s) as context when invoking a prompt for best results.
- For multi-file tasks, list each file explicitly in the chat after invoking the prompt.
- Use the cheatsheet requests below as inline chat starting points (`Ctrl+I` / `Cmd+I` in the editor).
- Replace all `[placeholders]` with actual paths or descriptions before sending.

## Using git context in Copilot Chat
- `#changes` — attaches your current working tree diff (staged + unstaged) as context
- `@git` — ask Copilot about commits, history, or branch differences
- `@git /diff` — explicitly show the current diff
- Combine with prompts: invoke `/draft-pr-summary` then attach `#changes` for a summary of your actual modifications

---

# GIT - Summarize current changes
@git what have I changed? Summarize the modified files and their purpose in the context of this AEM repository.

# GIT - Draft PR summary from current diff
@git #changes Draft a pull request summary for my current changes. Include modules changed, purpose, risks, and Cloud Manager or SonarCloud notes.

# GIT - Explain pipeline impact of current changes
@git #changes Explain the likely Cloud Manager pipeline, deployment, and runtime impact of my current changes in this AEM repository.

# GIT - Review current changes for AEM issues
@git #changes Review my current changes for AEM best practices, SonarCloud concerns, Cloud Manager risks, and missing tests.

# GIT - Review current changes for security issues
@git #changes Review my current changes for service user usage, HTL XSS context, admin resolver usage, and sensitive data exposure.

# GIT - Generate commit message
@git #changes Suggest a concise and accurate git commit message for these changes.

# GIT - What could break
@git #changes What existing behavior could break from these changes? Focus on AEM authoring impact, package filters, and downstream dependencies.

---

# COMPONENT - Explain a component
Explain the AEM component at `[ui.apps component path]` and related files.

# COMPONENT - Review a component end to end
Review the AEM component at `[ui.apps component path]` end to end for AEM best practices, SonarCloud concerns, Cloud Manager risks, and authoring impact.

# COMPONENT - Identify impacted files
For the change `[brief description]`, identify the files likely to change across core, ui.apps, ui.content, ui.config, and frontend modules.

# COMPONENT - Create or update a component
Help me create or update the AEM component at `[ui.apps component path]` following repository conventions.

# COMPONENT - Review HTL and dialog
Review these files for AEM best practices and authoring impact:
- `[HTL file path]`
- `[dialog xml path]`

# MODEL - Review a Sling Model
Review this Sling Model for repository conventions, null handling, unnecessary logic, SonarCloud concerns, and missing tests:
`[core sling model path]`

# MODEL - Create or update a Sling Model
Create or update a Sling Model for `[ui.apps component path]` following repository conventions.

# SERVICE - Review a Java class
Review this Java file for AEM best practices, null safety, complexity, duplication, SonarCloud concerns, and Cloud Manager risks:
`[core java file path]`

# SERVICE - Create or refactor an OSGi service
Create or refactor an OSGi service for `[feature or use case]` following repository conventions.

# SERVICE - Explain backend flow
Explain how this backend code works and which AEM components or services depend on it:
`[core java file path]`

# SERVLET - Create or update a Sling Servlet
Create or update a Sling Servlet for `[use case]` following repository conventions.

# SERVLET - Review a servlet
Review this Sling Servlet for resource type vs path registration correctness, security, null safety, SonarCloud concerns, and Cloud Manager risks:
`[core servlet file path]`

# SCHEDULER - Create or update a Scheduler or Job
Create or update an OSGi Scheduler or Sling Job for `[use case]` following repository conventions.

# SCHEDULER - Review a scheduler or job
Review this Scheduler or Job for Thread.sleep usage, admin resolver usage, exception handling, configurability, and Cloud Manager risks:
`[core scheduler/job file path]`

# WORKFLOW - Create a workflow process step
Create a custom AEM workflow process step for `[use case]` following repository conventions.

# FRONTEND - Review frontend integration
Review this frontend change in the context of AEM integration and repository conventions:
`[frontend file path]`

# FRONTEND - Explain frontend linkage
Explain how this frontend file is connected to AEM rendering, clientlibs, and authored content:
`[frontend file path]`

# FRONTEND - Create or update frontend code
Create or update frontend code for `[feature or component]` following the conventions of this frontend module.

# TEST - Create unit tests
Create unit tests for this class following repository test conventions:
`[core java file path]`

# TEST - Review existing tests
Review these tests for coverage gaps, over-mocking, missing edge cases, and AemContext misuse:
`[core test file path]`

# TEST - Add edge case coverage
Identify the missing null, empty, and error-path test cases for this class and generate them:
`[core java file path]`

# QUALITY - General review
Review these changes for AEM best practices, SonarCloud issues, Cloud Manager risks, null safety, duplication, complexity, and missing tests:
- `[file path 1]`
- `[file path 2]`

# QUALITY - Sonar and Cloud Manager focused review
Review this implementation specifically for SonarCloud-style maintainability issues and likely Adobe Cloud Manager concerns:
`[file or folder path]`

# QUALITY - Null safety and complexity check
Review this file for null safety, exception handling, deeply nested logic, duplication, and smallest practical cleanups:
`[file path]`

# QUALITY - Test gap review
Review this change and tell me what unit tests or integration tests are missing:
`[file or folder path]`

# SECURITY - Review for security issues
Review these files for service user usage, HTL XSS context, input validation, admin resolver usage, and sensitive data exposure:
- `[file path 1]`
- `[file path 2]`

# SECURITY - Create service user and Repoinit
Create a Repoinit script and service user mapping for `[service or use case]` with least-privilege ACLs.

# PERFORMANCE - Review for JCR query and performance issues
Review this file for unindexed queries, queries in render paths, unbounded result sets, and ResourceResolver lifecycle issues:
`[file or folder path]`

# BUG - Investigate a bug
Help me investigate this bug in the context of this repository: `[brief bug description]`. Start with likely impacted modules and root causes.

# BUG - Compare two implementations
Compare these two implementations and tell me which better fits repository conventions, AEM best practices, and maintainability expectations:
- `[file path 1]`
- `[file path 2]`

# BUG - Trace impact
Trace where this component or service is used and what could break if I change it:
`[file or folder path]`

# PR - Explain pipeline impact
Explain the likely Cloud Manager pipeline, deployment, and runtime impact of these changes:
- `[file path 1]`
- `[file path 2]`

# PR - Draft PR summary
Draft a pull request summary for these changes:
- `[file path 1]`
- `[file path 2]`

# PR - Draft testing notes
Draft reviewer notes and testing notes for this change:
`[file or folder path]`

# PR - Risks and rollback
Summarize implementation risks, deployment impact, and rollback considerations for this change:
`[file or folder path]`

# DISPATCHER - Review Dispatcher configuration
Review this Dispatcher configuration for default-deny filters, sensitive path exposure, security response headers, cache rules, and Cloud Manager SDK compatibility:
`[dispatcher config file path]`

# REFACTOR - Suggest minimal refactor
Suggest the smallest safe refactor for this file while preserving behavior:
`[file path]`

# REFACTOR - Align with repository conventions
Refactor this code to better match repository conventions without changing behavior:
`[file path]`

# UNDERSTANDING - Explain a file
Explain this file in the context of the repository and related modules:
`[file path]`

# UNDERSTANDING - Onboard me to this area
Help me understand this area of the repository, the main files involved, and what to inspect next:
`[folder path]`
