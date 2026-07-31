# The Agent-Tool Discoverability Standard v0.4

A falsifiable standard for whether an MCP/agent server is findable, understandable, trustable, and callable by AI. Each criterion is bound to the MCP spec, the registry schema, crypto/information-theory, or direct measurement — **never taste** — so a competitor's checker reaches the same booleans.

Live + machine-readable: https://live-vps.sasame.online/research/agent-tool-discoverability-standard.html

## The 10 criteria

| # | Criterion | Bound to |
|---|---|---|
| C1 | **Protocol entry conformance** | MCP 2026-07-28 server/discover, with revision-aware fallback to legacy initialize |
| C2 | **Tool listability** | MCP spec /server/tools — tools/list MUST return result.tools[] |
| C3 | **Tool object validity** | MCP spec Tool — STRICT v0.3: valid name + non-empty description + an object inputSchema (type:object, declared properties, OR a bare {} = a valid JSON Schema 'accepts anything' for no-arg tools; missing/null inputSchema rejected) |
| C4 | **Description sufficiency / selectability** | STRICT v0.3: every description >=12 chars, median >=20, distinctness ratio >=0.6 (templated/duplicate descriptions are unselectable) |
| C5 | **Safety annotation presence** | MCP spec ToolAnnotations — STRICT v0.3: a valid boolean hint (readOnly/destructive/idempotent/openWorld) on >=50% of tools |
| C6 | **Liveness & latency** | Direct measurement — STRICT v0.4: successful revision-appropriate protocol entry within <5000ms |
| C7 | **Returns real content (anti-ghost)** | STRICT v0.3: a SAFE (read-only) tool returns substantive MCP content[] (non-echo); priced/x402 -> UNVERIFIED |
| C8 | **Machine-discoverable identity** | Official MCP Registry server.json schema 2025-12-11 — name/version self-description |
| C9 | **Token efficiency** | Measurement: DECODED tools/list result payload bytes (Buffer.byteLength(JSON.stringify(result))) < 40000 (token-bloat is a known ecosystem failure) |
| C10 | **Honest error behavior** | JSON-RPC 2.0: malformed/unknown method returns a structured error, not a hang/crash |

Grade: A = a perfect 10/10, B = 8–9, C = 5–7, D otherwise (an unreachable server is a measured D), with an **honesty cap** (no verified real content ⇒ max B; priced/x402 ⇒ delivery UNVERIFIED, never asserted).

_CC-BY. The standard and the offline verifier are free and open forever._
