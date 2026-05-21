# NIST 800-53 compliance mapping

Initial public release. Full control-by-control mapping is maintained in the private `thornveil-ai/mycelium` repository under controlled access.

This summary indicates control families implemented; reach out to `federal@thornveil.ai` for the detailed mapping under evaluation NDA.

## Control families implemented

| Family | Controls | Coverage |
|---|---|---|
| AC — Access Control | AC-2, AC-3, AC-4, AC-6, AC-7, AC-17 | mTLS on worker channel; capability-gated tool calls; per-classification routing |
| AU — Audit and Accountability | AU-2, AU-3, AU-9, AU-10, AU-12 | HMAC-chained audit log; tamper-evident with `GET /audit/verify` |
| CM — Configuration Management | CM-2, CM-3, CM-6, CM-7 | Reproducible build; signed configuration; least-functionality default |
| IA — Identification and Authentication | IA-2, IA-5, IA-7 | mTLS client certificates; JWT for operator surface |
| SC — System and Communications Protection | SC-7, SC-8, SC-12, SC-13, SC-23, SC-28 | mTLS in transit; HMAC at rest for audit chain; FIPS 140-3 algorithms |
| SI — System and Information Integrity | SI-3, SI-4, SI-7, SI-10 | Proof-of-Inference verification; reputation demotion; cosign-signed releases |

## See also

- [Architecture overview](ARCHITECTURE.md)
- [Threat model](THREAT-MODEL.md)
