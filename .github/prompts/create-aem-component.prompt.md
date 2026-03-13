Create or update an AEM component following the conventions already used in this repository.

Requirements:
- identify the impacted files across `core`, `ui.apps`, `ui.content`, `ui.config`, and frontend modules if relevant
- use Sling Model backing if logic is required
- keep business logic out of HTL
- preserve authoring experience
- preserve existing naming and resource type conventions
- mention assumptions and risks before generating code
- suggest tests or validation steps if backend or frontend logic is introduced

Before generating code, first provide:
1. files likely to change
2. expected resource type or component mapping
3. assumptions
4. likely risks or validation points