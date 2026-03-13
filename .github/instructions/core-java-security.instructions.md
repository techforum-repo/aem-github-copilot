---
applyTo: "core/**/*.java"
---

# Security instructions for Java files in core

## Service users
- Never use admin `ResourceResolver` — use `resourceResolverFactory.getServiceResourceResolver(Map.of(ResourceResolverFactory.SUBSERVICE, "<name>"))`.
- Service user mappings live in `ui.config` as `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended~<name>.xml`.
- Service users and ACLs are provisioned via Repoinit in `ui.config` — not in Java code.

## Input and query safety
- Never concatenate user input into JCR-SQL2, XPath, or LDAP queries — use parameterized queries or `QueryBuilder`.
- Validate path parameters against an expected prefix before passing to `resourceResolver.getResource()`.
- Do not expose stack traces, JCR paths, or internal error details in HTTP responses.

## Servlet registration
- Prefer resource type registration over path-based registration.
- Path-based servlets (`/bin/...`) are publicly reachable — ensure Dispatcher filter rules protect them.

## Review focus
- admin ResourceResolver or Session usage
- user input in queries or paths
- path-based servlet registration without access control
- sensitive data in logs or responses
- hardcoded credentials (java:S2068)
