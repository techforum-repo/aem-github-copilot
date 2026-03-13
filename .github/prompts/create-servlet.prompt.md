---
description: Create or update a Sling Servlet following AEMaaCS and repository conventions
---

Create or update a Sling Servlet following the conventions already used in this repository.

Requirements:
- prefer `@SlingServletResourceTypes` over path-based registration unless path registration is already the pattern in this repository
- use `SlingSafeMethodsServlet` for GET-only servlets; use `SlingAllMethodsServlet` only when POST/PUT/DELETE is required
- keep request handling focused — delegate business logic to OSGi services
- validate and sanitize all request parameters before use
- return appropriate HTTP status codes (do not return 200 for errors)
- never use admin `ResourceResolver` — use a service user if JCR access is needed (CQBP-72, security)
- do not call `Thread.sleep()` (CQBP-75)
- use SLF4J logging only, no `System.out` (CQBP-84)
- suggest unit tests covering happy path, missing parameters, and error paths

Before generating code:
1. confirm whether resource type or path registration is appropriate and why
2. identify any OSGi services this servlet will depend on
3. identify service user needs if JCR access is required
4. state assumptions
5. mention likely SonarCloud or Cloud Manager risks
