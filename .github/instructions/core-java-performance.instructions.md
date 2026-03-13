---
applyTo: "core/**/*.java"
---

# Performance instructions for Java files in core

## JCR queries — avoid traversal, always use indexes
Unindexed queries cause full repository traversal and are blocked or heavily logged in AEMaaCS. Cloud Manager also flags them.

- **Never construct queries by string concatenation with user input** — use `QueryBuilder` or parameterized JCR-SQL2.
- **All JCR-SQL2 and XPath queries must be covered by an Oak index**. Validate with the AEM Query Debugger (`/libs/granite/operations/content/diagnosis/tool.html`) or `EXPLAIN` before committing.
- **Avoid `session.getWorkspace().getQueryManager()` for broad queries** — prefer `QueryBuilder` which integrates with Oak indexing.
- **Always set a query limit** (`query.setLimit(n)`) to prevent unbounded result sets.
- **Do not traverse all children of large nodes** (e.g., `/content` subtrees) with `listChildren()` — use a targeted query or pagination with `RangeIterator`.
- **Avoid queries in loops** — batch lookups or restructure to query once and iterate results.

## Sling Model performance
- Do not execute JCR queries or heavy resource traversals inside `@PostConstruct` methods for components that render on every page request — this blocks the rendering thread.
- Use **lazy initialization** (`@Lazy` or manual null-check pattern) for expensive data that may not always be needed.
- Do not cache `ResourceResolver` or `Session` as instance fields on Sling Models — they have request scope and must not be held beyond the request lifecycle.
- Avoid adapting the same resource to the same type multiple times in one request — adapt once and reuse.

## Caching awareness
- Sling Models annotated with `@Model(adaptables = SlingHttpServletRequest.class)` are **request-scoped** — a new instance is created per request. Keep construction lightweight.
- Sling Models annotated with `@Model(adaptables = Resource.class)` may be cached by the Sling Model cache in some contexts — do not store request-specific state in them.
- OSGi services are singletons — never store request or session state in OSGi service instance fields.
- Use `@Reference(policy = ReferencePolicy.DYNAMIC)` carefully — unnecessary dynamic references can impact startup and performance.

## Resource and session lifecycle
- Do not hold `ResourceResolver` or `Session` objects open across multiple unrelated operations — open, use, and close promptly.
- Do not store `ResourceResolver` or `Session` in static fields or in long-lived OSGi service fields without explicit lifecycle management.

## Review focus
- unindexed or potentially traversing JCR queries
- queries inside loops or @PostConstruct
- unbounded query results (no limit set)
- heavy logic in request-scoped Sling Model constructors
- ResourceResolver or Session held longer than necessary
- repeated adaptation of the same resource
