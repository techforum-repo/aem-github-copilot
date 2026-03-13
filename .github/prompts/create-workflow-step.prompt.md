---
description: Create or update a custom AEM workflow process step
---

Create or update a custom AEM workflow process step following the conventions already used in this repository.

Requirements:
- implement `WorkflowProcess` and annotate with `@Component(service = WorkflowProcess.class)` with a `process.label` property for the authoring UI
- keep execution logic focused — delegate to OSGi services where possible
- access payload resource via `workItem.getWorkflowData().getPayload()` — validate the payload type before use
- never use admin `ResourceResolver` — use a service user with appropriate ACLs (CQBP-72, security)
- always close `ResourceResolver` in try-with-resources
- do not call `Thread.sleep()` (CQBP-75)
- handle exceptions explicitly — an uncaught exception terminates the workflow instance
- use SLF4J parameterized logging only (CQBP-84)
- read process arguments from `metaData.getMetaDataMap()` — make behavior configurable, not hardcoded
- suggest unit tests for the process logic, testing both happy path and exception scenarios

Before generating code:
1. describe the expected payload type (page, asset, or other)
2. list the process arguments this step will accept
3. identify OSGi services and service user needs
4. mention likely SonarCloud, Cloud Manager, or workflow stability risks
