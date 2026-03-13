# COMPONENT - Explain a component
Explain the AEM component at <ui.apps component path> and related files.

# COMPONENT - Review a component end to end
Review the AEM component at <ui.apps component path> end to end for AEM best practices, SonarCloud concerns, Cloud Manager risks, and authoring impact.

# COMPONENT - Identify impacted files
For the change <brief description>, identify the files likely to change across core, ui.apps, ui.content, ui.config, and frontend modules.

# COMPONENT - Create or update a component
Help me create or update the AEM component at <ui.apps component path> following repository conventions.

# COMPONENT - Review HTL and dialog
Review these files for AEM best practices and authoring impact:
- <HTL file path>
- <dialog xml path>

# MODEL - Review a Sling Model
Review this Sling Model for repository conventions, null handling, unnecessary logic, SonarCloud concerns, and missing tests:
<core sling model path>

# MODEL - Create or update a Sling Model
Create or update a Sling Model for <ui.apps component path> following repository conventions.

# SERVICE - Review a Java class
Review this Java file for AEM best practices, null safety, complexity, duplication, SonarCloud concerns, and Cloud Manager risks:
<core java file path>

# SERVICE - Create or refactor an OSGi service
Create or refactor an OSGi service for <feature or use case> following repository conventions.

# SERVICE - Explain backend flow
Explain how this backend code works and which AEM components or services depend on it:
<core java file path>

# FRONTEND - Review frontend integration
Review this frontend change in the context of AEM integration and repository conventions:
<frontend file path>

# FRONTEND - Explain frontend linkage
Explain how this frontend file is connected to AEM rendering, clientlibs, and authored content:
<frontend file path>

# FRONTEND - Create or update frontend code
Create or update frontend code for <feature or component> following the conventions of this frontend module.

# QUALITY - General review
Review these changes for AEM best practices, SonarCloud issues, Cloud Manager risks, null safety, duplication, complexity, and missing tests:
- <file path 1>
- <file path 2>

# QUALITY - Sonar and Cloud Manager focused review
Review this implementation specifically for SonarCloud-style maintainability issues and likely Adobe Cloud Manager concerns:
<file or folder path>

# QUALITY - Null safety and complexity check
Review this file for null safety, exception handling, deeply nested logic, duplication, and smallest practical cleanups:
<file path>

# QUALITY - Test gap review
Review this change and tell me what unit tests or integration tests are missing:
<file or folder path>

# BUG - Investigate a bug
Help me investigate this bug in the context of this repository: <brief bug description>. Start with likely impacted modules and root causes.

# BUG - Compare two implementations
Compare these two implementations and tell me which better fits repository conventions, AEM best practices, and maintainability expectations:
- <file path 1>
- <file path 2>

# BUG - Trace impact
Trace where this component or service is used and what could break if I change it:
<file or folder path>

# PR - Draft PR summary
Draft a pull request summary for these changes:
- <file path 1>
- <file path 2>

# PR - Draft testing notes
Draft reviewer notes and testing notes for this change:
<file or folder path>

# PR - Risks and rollback
Summarize implementation risks, deployment impact, and rollback considerations for this change:
<file or folder path>

# REFACTOR - Suggest minimal refactor
Suggest the smallest safe refactor for this file while preserving behavior:
<file path>

# REFACTOR - Align with repository conventions
Refactor this code to better match repository conventions without changing behavior:
<file path>

# UNDERSTANDING - Explain a file
Explain this file in the context of the repository and related modules:
<file path>

# UNDERSTANDING - Onboard me to this area
Help me understand this area of the repository, the main files involved, and what to inspect next:
<folder path>