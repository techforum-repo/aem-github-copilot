Create or update a Sling Model for this AEM component.

Requirements:
- follow the existing package structure and annotation style in this repository
- adapt from the appropriate source used by nearby models
- expose only data needed by HTL or consumers
- keep business logic minimal and focused
- handle nulls and fallback behavior explicitly
- suggest tests if logic is non-trivial

Before generating code:
1. identify nearby model patterns that should be followed
2. state assumptions
3. mention likely SonarCloud or Cloud Manager concerns if any