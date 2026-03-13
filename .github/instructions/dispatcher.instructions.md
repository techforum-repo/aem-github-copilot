---
applyTo: "devops/**/*.{conf,any,vhost,farm}"
---

# Instructions for Dispatcher configuration

## Security
- `/filter` must default-deny — allow only explicitly needed paths.
- Block: `/crx`, `/system`, `/bin/wcmcommand`, `/bin/receive`, `/etc/replication`, `/mnt/overlay`, `/cf#`, `/editor.html`.
- Restrict or block `.json` and `.infinity.json` to prevent data exposure.
- Required response headers: `X-Frame-Options`, `X-Content-Type-Options: nosniff`, `Strict-Transport-Security`, `Content-Security-Policy`.

## Caching
- Never cache authenticated or user-specific responses.
- Use `/ignoreUrlParams` to prevent cache fragmentation from analytics query params.
- Cache invalidation paths must match what publish replication actually flushes.

## AEMaaCS Dispatcher
- Validate config with the Dispatcher SDK locally before pushing — config errors fail the Cloud Manager pipeline.
- Do not use Dispatcher directives not supported by the AEMaaCS Dispatcher SDK.

## Review focus
- default-deny filter rule present
- sensitive AEM paths blocked
- security response headers present
- authenticated content not cached
- Cloud Manager Dispatcher SDK compatibility
