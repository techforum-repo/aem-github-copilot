---
applyTo: "core/**/*.java"
---

# Security instructions for Java files in core

## Service users — never use admin session or admin ResourceResolver
- Do not obtain a `ResourceResolver` using admin credentials (`loginAdministrative` is banned in AEMaaCS).
- Every service that accesses the JCR must use a **dedicated service user** with least-privilege ACLs.
- Service user mappings are defined in `ui.config` as `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended~<name>.xml`.
- Service users and their ACLs are provisioned via **Repoinit scripts** — do not create users or set ACLs in Java code.
- Inject `ResourceResolverFactory` and call `getServiceResourceResolver(Map.of(ResourceResolverFactory.SUBSERVICE, "my-service-user"))`.
- Always close the resolver in a `try-with-resources` block (CQBP-72).

## HTL XSS — output context must be correct
- HTL auto-escapes output based on context. Never override this without a documented security reason.
- `${var @ context='unsafe'}` — bypasses all escaping. Flag any usage for security review.
- `${var @ context='html'}` — only for trusted, sanitized HTML. Never for user-supplied input.
- `${var @ context='uri'}` — must be used for all link and URL outputs to prevent open redirect and XSS.
- `${var @ context='scriptString'}` — must be used when embedding values inside `<script>` blocks.
- Default context escaping is correct for text content — do not override it unnecessarily.

## Input validation and injection
- Never construct JCR-SQL2, XPath, or OSGI LDAP queries by concatenating user input — use parameterized queries or `QueryBuilder`.
- Never pass user-supplied `path` parameters directly to `resourceResolver.getResource()` without validation against an expected path prefix.
- Sanitize or reject unexpected characters in parameters used in repository paths or queries.
- Do not expose internal exception messages, stack traces, or JCR paths in HTTP responses.

## Sensitive data
- Do not log passwords, tokens, session IDs, or personal data (PII).
- Do not store sensitive values in JCR node properties that are accessible to anonymous users.
- Use AEM Cloud Manager environment variables or the Secret type for sensitive OSGi config values — not hardcoded strings (java:S2068).

## Servlet security
- Sling Servlets registered by resource type are only accessible via valid resources — prefer this over path-based registration.
- Path-based servlet registration (`/bin/...`) is publicly accessible by default; protect with Sling authentication requirements or dispatcher filter rules.
- Always validate and sanitize request parameters before use.
- Return appropriate HTTP status codes — do not return 200 for errors.

## Review focus
- admin session or admin ResourceResolver usage
- missing service user for JCR access
- `context='unsafe'` or `context='html'` in HTL without a documented reason
- user input concatenated into queries or paths
- sensitive data logged or exposed in responses
- path-based servlet registration without access control
- hardcoded credentials (java:S2068)
