# Tavros Camel Components — DEPRECATED

> **Status: deprecated as of 2026-08-28. No further development. Superseded by
> `org.apache.camel.springboot:camel-opentelemetry-starter`.**

This repository contains Tavros forks of Apache Camel's `camel-tracing` and `camel-opentracing`
components, pinned to **Camel 3.7.1** and **OpenTracing 0.33.0**. Its last commit was February 2021.

## Why it is deprecated

OpenTracing merged into OpenTelemetry and is no longer the tracing API the ecosystem targets. The
original decision to fork these components — recorded in Tavros
[ADR-0004](https://github.com/MS3Inc/tavros/blob/main/docs/adr/0004-opentracing-for-in-process-tracing-api.md) —
was made in 2020, when OpenTelemetry's design had not yet stabilized. That reasoning no longer holds.

The migration has in fact **already happened**. The October 2024 refresh of the Tavros Camel
archetypes moved generated projects to `camel-opentelemetry-starter` and the OpenTelemetry Java
agent. Nothing has referenced this repository since. A search across all six CDX MOSA repositories
in August 2026 found no consumer: no Maven coordinate reference, no import of
`org.apache.camel.opentracing` or `org.apache.camel.tracing`, and no remaining OpenTracing
dependency anywhere except the text of ADR-0004 itself.

There is a second reason not to revive it. These modules publish into Camel's **own** package
namespaces — `org.apache.camel.opentracing` and `org.apache.camel.tracing` — so the artifact shadows
upstream Camel classes wherever both are on a classpath. That was a deliberate technique for
patching Camel 3.7.1 in place; it is a liability to carry forward.

## What to use instead

Camel/Spring Boot projects on Tavros get tracing from:

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-opentelemetry-starter</artifactId>
</dependency>
```

together with the OpenTelemetry Java agent, both of which the Tavros Camel archetypes already
configure. Nothing needs to be added by hand for a project scaffolded from the archetypes.

## What happens to the published artifact

**Nothing is being unpublished.** `com.ms3-inc.tavros:camel-components:3.7.1-002` remains available
on Maven Central for any historical consumer still building against Camel 3.7.1. This repository is
being archived, not deleted — the source stays readable, and the git history stays intact.

No further releases will be made. Security issues will not be patched here; the fix is to move to
`camel-opentelemetry-starter`.

## References

- Superseding decision: Tavros ADR-0030, *OpenTelemetry for distributed tracing*
- Superseded decision: Tavros ADR-0004, *OpenTracing for in-process tracing API*
- Upstream replacement: https://camel.apache.org/components/current/others/opentelemetry.html
