---
applyTo: "devops/**/*.{conf,any,vhost,farm}"
---

# Instructions for Dispatcher configuration

Dispatcher is the AEM caching and security layer. Incorrect configuration causes cache poisoning, security vulnerabilities, or broken invalidation.

## Security — filter rules
- **Default deny**: the `/filter` section must deny all requests by default and explicitly allow only what is needed.
- Never allow direct access to `/crx`, `/system`, `/bin/wcmcommand`, `/bin/receive`, `/etc/replication`, or `/libs` through Dispatcher.
- Do not expose author-side paths (`/cf#`, `/editor.html`, `/mnt/overlay`, `/content/dam/...` admin paths) through publish Dispatcher.
- Validate that selector-based attacks are mitigated — restrict allowed selectors to known safe values where possible.
- Ensure `.json` and `.infinity.json` extensions are blocked or tightly controlled to prevent data leakage.

## Security — response headers
Every vhost or farm should set the following security headers:
- `X-Frame-Options: SAMEORIGIN` or `DENY` — prevents clickjacking.
- `X-Content-Type-Options: nosniff` — prevents MIME type sniffing.
- `Strict-Transport-Security: max-age=31536000; includeSubDomains` — enforces HTTPS.
- `Content-Security-Policy` — scope to the site's actual needs; do not use `unsafe-inline` or `unsafe-eval` without a strong reason.
- `Referrer-Policy: strict-origin-when-cross-origin`.

## Caching rules
- **Cache authenticated responses only if they are genuinely public** — never cache responses with `Set-Cookie` or user-specific content.
- Use `/ignoreUrlParams` to prevent cache fragmentation from irrelevant query parameters (e.g., analytics UTM params).
- Ensure cache invalidation (`/invalidate`) is configured correctly so that publish replication flushes the right cache paths.
- Do not cache error responses (4xx, 5xx) — configure `/rules` to skip caching on these.
- Set appropriate `Cache-Control` and `Expires` headers from the AEM response layer, not only from Dispatcher, so CDN behavior is also correct.

## URL rewriting
- Keep rewrite rules minimal and documented — complex rewrite chains are hard to debug and can produce security issues.
- Avoid rewrite rules that expose internal path structures in URLs.
- Validate that vanity URL handling does not conflict with cache rules.

## Cloud Manager / AEMaaCS Dispatcher
- Dispatcher configuration for AEMaaCS is validated by Cloud Manager during pipeline — config errors fail the pipeline.
- Use the `dispatcher-sdk` locally to validate configuration before pushing (`./bin/docker_run.sh`).
- Do not use deprecated Dispatcher directives that are not supported in AEMaaCS Dispatcher SDK.
- Environment-specific vhost or farm files should use the correct naming convention for Cloud Manager to pick them up per environment.

## Review focus
- default-deny filter rule present
- sensitive AEM paths blocked (crx, system, bin/wcmcommand)
- security response headers present
- authenticated or user-specific content not cached
- cache invalidation paths correct
- query parameter handling to prevent cache fragmentation
- Cloud Manager Dispatcher SDK compatibility
