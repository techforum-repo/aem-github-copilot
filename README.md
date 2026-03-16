# AEM GitHub Copilot Guidance

This repository contains reusable GitHub Copilot guidance for an enterprise Adobe Experience Manager as a Cloud Service (AEMaaCS) project.

It is designed to help teams use GitHub Copilot more effectively in both:
- GitHub Copilot CLI
- GitHub Copilot Chat in VS Code

The repository provides:
- global repository guidance
- module-scoped instructions
- reusable prompt files
- practical request examples
- optional repo-level LSP configuration for Copilot CLI

## Repository structure

### `.github\copilot-instructions.md`
Top-level repository guidance. This file defines the shared rules Copilot should follow across the project, including module boundaries, AEMaaCS conventions, Cloud Manager safety, OakPAL concerns, and general change guidance.

### `.github\instructions\`
Scoped instruction files that apply automatically based on file path patterns.

These cover areas such as:
- `core`
- `ui.apps`
- `ui.apps.structure`
- `ui.content`
- `ui.config`
- frontend modules
- `all`
- `devops`
- Dispatcher
- hooks

Each instruction file is structured to make usage predictable:
- `Scope`
- `Key rules`
- `Review focus`

### `.github\prompts\`
Reusable prompt files for common AEM development and review tasks.

Examples include:
- creating AEM components
- creating Sling Models
- creating servlets
- creating OSGi services
- creating schedulers
- creating workflow steps
- creating Repoinit and service-user mappings
- writing unit tests
- reviewing code
- investigating bugs
- drafting PR summaries

### `.github\lsp.json`
Optional repository-level Language Server Protocol configuration for Copilot CLI.

The starter config in this repo includes:
- Java via `jdtls`
- TypeScript and JavaScript via `typescript-language-server`

This does not affect runtime behavior. It improves Copilot CLI's code intelligence for tasks such as:
- go-to-definition
- hover information
- diagnostics
- better symbol understanding across Java and frontend modules

### Java 21 and `jdtls` setup on Windows
If you want Java LSP support in Copilot CLI, install Java 21 and `jdtls` locally.

1. Install JDK 21:
   ```powershell
   winget install EclipseAdoptium.Temurin.21.JDK
   ```
2. Open a new terminal and verify Java:
   ```powershell
   java -version
   ```
3. If the terminal still resolves an older Java version, update `JAVA_HOME` and `Path` to the JDK 21 installation, then open a new terminal again.
4. Download and extract Eclipse JDT Language Server from the official milestones or snapshots site:
   - `https://download.eclipse.org/jdtls/milestones/`
5. Place it in a stable location such as `C:\Tools\jdtls`.
6. Add the `jdtls` launcher to your system `Path` so the shared `.github\lsp.json` can use it without machine-specific changes.
   - This is the preferred setup for team use because it keeps the repo configuration portable.
   - If you cannot add `jdtls` to `Path`, use a user-level Copilot LSP config to point to your exact local launcher path as a fallback.
7. Start Copilot CLI in the target repository and run:
   ```text
   /lsp
   ```
8. Test a Java scenario by asking Copilot to explain or trace a class under `core\src\main\java`.

Expected benefits after setup:
- better Java symbol understanding
- better dependency tracing
- better diagnostics and class navigation in Copilot CLI

Best request style with LSP enabled:
- prefer class, interface, and method names over only file paths
- ask for implementors, callers, dependencies, and impact analysis
- use file paths as supporting context, not the only anchor

### `docs\`
Supporting documentation for developers using the guidance set.

Current docs include:
- `docs\copilot-request-cheatsheet.md`

This cheatsheet explains how to use prompts and provides ready-to-paste requests for common AEM tasks, code reviews, bug investigations, PR work, and git/repository workflows.

## How this works in Copilot CLI

Copilot CLI respects:
- `.github\copilot-instructions.md`
- `.github\instructions\**\*.instructions.md`

That means the CLI can automatically apply repository guidance when you work inside this repo.

Useful CLI notes:
- use `/instructions` to inspect loaded instruction files
- use `/lsp` to check configured language servers
- use `/diff`, `/pr`, and `/review` for git and pull request workflows

If you want repo-level LSP support in CLI, install the configured language servers locally so `.github\lsp.json` can be used.

## How this works in VS Code

In VS Code:
- prompt files in `.github\prompts\` are easier to discover via slash-command selection in Copilot Chat
- scoped instructions from `.github\instructions\` still apply automatically based on file matching
- the same repo guidance can be reused across editor and terminal workflows

## Recommended usage model

Use the repository like this:

1. Keep broad standards in `.github\copilot-instructions.md`
2. Keep module-specific rules in `.github\instructions\`
3. Keep reusable task templates in `.github\prompts\`
4. Keep developer-facing examples in `docs\`

This separation keeps the guidance easier to maintain and makes it clearer which assets are:
- always-on rules
- path-scoped rules
- reusable prompts
- human-readable examples

## Suggested next steps

If you want to extend this repo further, the most useful next improvements are:
- refine prompts based on real team usage
- expand docs with team-specific examples
- keep `lsp.json` aligned with the languages actually used in the target AEM repo
- optionally add `AGENTS.md` if you want broader cross-tool compatibility beyond Copilot

## Summary

This repository is set up as a reusable enterprise AEMaaCS Copilot guidance package.

It is already suitable for:
- enterprise AEM development guardrails
- Copilot CLI workflows
- VS Code Copilot workflows
- code review and PR support
- onboarding developers to large AEM codebases
