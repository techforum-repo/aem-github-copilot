---
applyTo: "{devops,dispatcher}/**/*.{conf,any,vhost,farm}"
---

# Instructions for Dispatcher configuration

## Scope
Use this guidance for Dispatcher configuration affecting security, caching, domain setup, and Cloud Manager compatibility. The etc/map entries in `ui.content` are part of domain setup and must be updated together with vhost and farm changes.

## Complete domain setup checklist

When adding a new domain, **all four steps must be done together**:

1. Vhost in `dispatcher/src/conf.d/available_vhosts/`
2. Farm in `dispatcher/src/conf.dispatcher.d/available_farms/`
3. Symlinks in the corresponding `enabled_*` directories
4. **JCR etc/map entry** in `ui.content/src/main/content/jcr_root/etc/map.publish/`

Never complete one without the others unless explicitly asked.

## vhost and farm setup pattern

- Always create files in `available_*`, never directly in `enabled_*`.
- Symlink to enable using relative paths:
  ```bash
  cd dispatcher/src/conf.d/enabled_vhosts && ln -s ../available_vhosts/<name>.vhost <name>.vhost
  cd dispatcher/src/conf.dispatcher.d/enabled_farms && ln -s ../available_farms/<name>.farm <name>.farm
  ```
- For domain-specific farms, list hostnames inline in `/virtualhosts` rather than via `$include`:
  ```
  /virtualhosts {
    "www.example.com"
    "example.com"
  }
  ```
- Never edit `default.vhost` or `default.farm` — these are AEMaaCS SDK reference files.
- Remind the user to add `/etc/hosts` entries for local testing.

## JCR etc/map pattern

Always read the existing entries in `ui.content/.../etc/map.publish/` before creating a new one — match the exact folder structure, node types, and property names already in use.

Typical domain folder `.content.xml` pattern:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
          xmlns:jcr="http://www.jcp.org/jcr/1.0"
    jcr:primaryType="sling:Mapping"
    sling:match="www.example.com.80/"
    sling:internalRedirect="/content/my-site/"/>
```

- `jcr:primaryType="sling:Mapping"` is always required.
- `sling:match` — incoming host+port pattern (e.g. `www.example.com.80/`).
- `sling:internalRedirect` — maps to the JCR content path.
- Create entries for both HTTP (port 80) and HTTPS (port 443) unless the project uses only one protocol.

## Rewrite rules

- Rewrite rules in `conf.d/rewrites/rewrite.rules` apply globally across all enabled vhosts.
- If a new domain serves different content, add a `RewriteCond %{HTTP_HOST}` guard rather than changing the global rule.
- Add per-domain rewrites under a `RewriteCond %{HTTP_HOST}` guard to avoid affecting other vhosts.

## Security filter rules

- `/filter` should default deny; allow only explicitly required paths.
- Block or tightly restrict sensitive AEM endpoints such as `/crx`, `/system`, `/bin/wcmcommand`, `/bin/receive`, `/etc/replication`, `/mnt/overlay`, `/editor.html`, and Content Fragment authoring routes (e.g. `/assets.html`, `/mnt/overlay/dam/cfm`).
- Restrict `.json` and especially `.infinity.json` exposure unless a specific public use case exists.
- Ensure required security headers are present:
  - `Content-Security-Policy` — restrict scripts and frame sources
  - `X-Content-Type-Options: nosniff`
  - `X-Frame-Options: SAMEORIGIN` (or `DENY`)
  - `Referrer-Policy: strict-origin-when-cross-origin`
  - `Strict-Transport-Security` — for HTTPS-only deployments

## Caching rules

- Never cache authenticated, personalized, or user-specific responses.
- Use `/ignoreUrlParams` to avoid unnecessary cache fragmentation from analytics-style query parameters.
- Keep cache invalidation rules aligned with actual publish flush behavior.
- Use only Dispatcher directives supported by the AEMaaCS Dispatcher SDK.

## Review focus

- All four domain setup steps completed together (vhost, farm, symlinks, etc/map)
- etc/map entries match existing project structure and node types
- Both HTTP and HTTPS mapping entries created
- `available_*/enabled_*` symlink pattern followed
- Default-deny filter posture
- Exposure of sensitive endpoints or JSON data
- Security header coverage (CSP, X-Content-Type-Options, X-Frame-Options)
- Caching of authenticated or personalized content
- Dispatcher SDK and Cloud Manager compatibility
