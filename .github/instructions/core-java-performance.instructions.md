---
applyTo: "core/**/*.java"
---

# Performance instructions for Java files in core

## JCR queries
- All queries must be backed by an Oak index — validate with the Query Debugger before committing.
- Always set a query limit to prevent unbounded result sets.
- Never run queries inside loops.
- Never traverse large node trees with `listChildren()` — use a targeted query with pagination instead.

## Sling Model rendering performance
- Do not run JCR queries or heavy resource traversals in `@PostConstruct` methods — this blocks every page render.
- Use lazy initialization for data that may not always be needed.
- OSGi services are singletons — never store request or session state in service instance fields.

## Review focus
- queries without an index or without a limit
- queries inside loops or in @PostConstruct
- ResourceResolver or Session held longer than the immediate operation
- request state stored in OSGi service fields
