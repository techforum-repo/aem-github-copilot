---
applyTo: "{ui.content,ui.config}/**/*.xml"
---

# Instructions for Sling Context-Aware Configuration (CAConfig)

## When to use CAConfig vs OSGi config

- Use **CAConfig** for site-specific or environment-neutral settings that authors or operations may need to change per content tree (e.g. API endpoint per site, feature flags per country).
- Use **OSGi config** for infrastructure settings that are environment-specific (e.g. timeouts, credentials, thread pool sizes).
- Do not duplicate the same setting in both — pick one owner.

## Content placement

- Store config nodes under `/conf/<project>/sling:configs/<config-name>` in `ui.content`.
- Inherit order: resource → `/conf/<site>` → `/conf/global` → defaults.
- Use `sling:configRef` on the content root to point to the correct `/conf` bucket.
- Keep Java-specific CAConfig interface and consumption rules in a companion Java-scoped instruction file so they apply when editing `core` code.

## Review focus

- Is the config node placed in `ui.content` under `/conf`?
- Is `sling:configRef` set on the content root to wire up inheritance?
- Is the same setting owned by CAConfig or OSGi config, but not both?
