# Threat model overview

This is the public summary. The complete threat model lives in `thornveil-ai/mycelium` under controlled access; contact `federal@thornveil.ai` for evaluation NDA.

## Adversarial assumptions

- **Untrusted network** — assume the mesh runs on networks where any single hop may be observed, replayed, or intercepted
- **Untrusted endpoint** — individual mesh nodes may be compromised; the mesh must continue functioning when up to N-1 of N nodes are degraded or hostile
- **Authorized but accidental insiders** — operator nodes may issue requests that should be blocked by policy; the gate must catch them before they reach the model
- **Authorized but compromised insiders** — adversaries with valid credentials must be detectable post-hoc via the audit chain

## Out of scope (explicitly)

- Physical security of node hardware
- TEMPEST / side-channel resistance beyond standard FIPS 140-3 cryptographic boundaries
- Trusted operator initial bootstrap (the first joining node must establish trust through provisioning channels)

## Key mitigations

| Threat | Mitigation |
|---|---|
| Compromised worker substitutes corrupt output | Proof-of-Inference verification + reputation tracking + worker substitution |
| Replay of a successful chat completion | Request nonces + HMAC chain entries with per-request UUID |
| Operator issues out-of-scope request | Capability-based gate at admission; classification-gate before routing |
| Audit log tampered with post-hoc | HMAC chain with per-entry chained signature; `GET /audit/verify` detects any single-entry mutation |
| Untrusted transport intercepts plaintext | mTLS on worker channel; TLS 1.3 on operator channel; FIPS 140-3 algorithm set |
