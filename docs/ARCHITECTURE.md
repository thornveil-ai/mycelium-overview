# Mycelium architecture

This document expands the eight-layer model summarized in the [README](../README.md).

## Layer-by-layer

### L8 — Application Layer

OpenAI-compatible HTTP API at `/v1/chat/completions`, `/v1/models`, `/v1/embeddings`. Plus operator-surface endpoints: `/healthz`, `/mesh/status`, `/mesh/dashboard.json`, `/audit/verify`.

### L7 — Routing and Verification

Cascade router selects expert tier by capability and load. Proof-of-Inference (PoI) verifies expert outputs match expected behavior signature. Reputation tracking demotes nodes that diverge.

### L6 — Style Consistency

Post-generation normalization layer that handles cross-model style drift when the mesh routes between heterogeneous backends (Ollama vs llama.cpp vs SGLang).

### L5 — Expert Orchestrator

Registry of available experts. Proxy layer that forwards requests to the selected expert. Prefetching system that warms up the likely-next-expert based on conversation context.

### L4 — Transport Layer

HTTP/SSE for chat completions. NAT-traversal helpers. mTLS on the worker channel.

### L3 — Network Topology

Kademlia DHT for peer discovery. Gossip protocol for state propagation. mDNS-based local discovery via Zeroconf.

### L2 — Backend Abstraction

Pluggable inference backend layer. Currently supports Ollama, llama.cpp, SGLang. Each backend is an interface; new backends add by implementing it.

### L1 — Hardware Detection

GPU / CPU / NPU discovery on node startup. Tier assignment based on detected hardware. Drives capacity advertisement in the DHT.

## Substitute-on-failure

When an expert call fails or times out, the substitute-on-failure mechanism produces a zero-filled tensor with adjusted scaling so the generation continues. The application surface sees no interruption; the chat stream continues; the failure is logged into the audit chain.

This is the headline DDIL property: any individual node may drop and the workload continues without operator action.

## See also

- [NIST 800-53 compliance mapping](COMPLIANCE-NIST-800-53.md)
- [Threat model](THREAT-MODEL.md)
- [R2I compliance evidence](R2I-COMPLIANCE.md)
- [OpenAPI specification](openapi.yaml)
