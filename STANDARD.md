# The Agent-Tool Discoverability Standard v0.1

A falsifiable standard for whether an MCP/agent server is findable, understandable, trustable, and callable by AI. Each criterion is bound to the MCP spec, the registry schema, crypto/information-theory, or direct measurement — **never taste** — so a competitor's checker reaches the same booleans.

Live + machine-readable: https://live-vps.sasame.online/research/agent-tool-discoverability-standard.html

## The 10 criteria

| # | Criterion | Bound to |
|---|---|---|
| C1 | **Protocol handshake conformance** | MCP spec 2025-11-25 — JSON-RPC 2.0 initialize MUST return protocolVersion + capabilities |
| C2 | **Tool listability** | MCP spec /server/tools — tools/list MUST return result.tools[] |
| C3 | **Tool object validity** | MCP spec Tool: name [A-Za-z0-9_-]{1,128} + description + inputSchema(object) |
| C4 | **Description sufficiency / selectability** | Registry schema description minLength>=1; info-theory: empty/duplicate descriptions are unselectable |
| C5 | **Safety annotation presence** | MCP spec ToolAnnotations (readOnlyHint/destructiveHint/idempotentHint/openWorldHint) |
| C6 | **Liveness & latency** | Direct measurement: endpoint answers over the wire within a bounded latency |
| C7 | **Returns real content (anti-ghost)** | Empirical (SaSame census ~80% return nothing) + info-theory: a real result carries >0 bits |
| C8 | **Machine-discoverable identity** | Official MCP Registry server.json schema 2025-12-11 — name/version self-description |
| C9 | **Token efficiency** | Measurement: total tools/list payload bytes (token-bloat is a known ecosystem failure) |
| C10 | **Honest error behavior** | JSON-RPC 2.0: malformed/unknown method returns a structured error, not a hang/crash |

Grade: A ≥ 9 passes, B ≥ 7, C ≥ 4, D otherwise, with an **honesty cap** (no verified real content ⇒ max B; priced/x402 ⇒ delivery UNVERIFIED, never asserted).

_CC-BY. The standard and the offline verifier are free and open forever._
