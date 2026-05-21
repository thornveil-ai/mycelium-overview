# Right to Integrate (R2I) compliance evidence

This document expands on the R2I alignment summary in the [README](../README.md).

## R2I evaluation matrix

| Criterion | Mycelium implementation |
|---|---|
| Exposed APIs | OpenAI-compatible `/v1/*` endpoints + operator-surface endpoints |
| Published documentation | OpenAPI 3.1.0 spec, this repository, threat model, compliance mapping |
| Vendor-neutral clients | Any OpenAI-compatible client connects without code changes |
| Modular Open Systems Architecture | Coordinator/workers separated; backend pluggable |
| Cryptographic auditability | HMAC-chained audit log per request; `GET /audit/verify` returns chain integrity |
| No vendor lock-in | Cosign-signed release binaries; reproducible build; SBOM published |

## Test against the EXO Labs ecosystem

The OpenAPI surface is validated against the EXO Labs OSS client ecosystem. Any EXO-compatible client (or any client speaking the OpenAI chat-completions protocol) connects to a Mycelium endpoint without code changes.

## Integration contact

For prime integration: `jesse@thornveil.ai`. Thornveil provides:

- OpenAPI specs ([docs/openapi.yaml](openapi.yaml))
- Sample clients (forthcoming in this repo)
- 30-day evaluation deployment on your infrastructure
