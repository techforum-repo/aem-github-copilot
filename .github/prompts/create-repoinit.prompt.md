---
description: Create a Repoinit script to provision a service user and ACLs for AEMaaCS
---

Create a Repoinit script to provision the service user and minimum required ACLs for this use case.

Requirements:
- use `create service user` statement to create the service user (not a regular system user)
- grant only the minimum permissions required for the use case (principle of least privilege)
- prefer path-specific ACLs over broad `/content` or `/` grants
- use `set ACL for <service-user>` with explicit `allow` statements and specific privileges (`jcr:read`, `rep:write`, `jcr:modifyProperties`, etc.)
- the Repoinit script belongs in `ui.config` as an OSGi config for `org.apache.sling.jcr.repoinit.RepositoryInitializer~<name>.xml`
- the service user mapping belongs in `ui.config` as `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended~<name>.xml`
- the Java code that uses this service user must call `resourceResolverFactory.getServiceResourceResolver(Map.of(ResourceResolverFactory.SUBSERVICE, "<subservice-name>"))`

Before generating:
1. describe the paths the service needs to read or write
2. list the minimum JCR privileges needed
3. confirm the subservice name that will be used in the Java code
4. note any author-vs-publish differences in access requirements
