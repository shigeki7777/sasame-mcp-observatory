# Methodology

How SaSame observes a public MCP server. Deterministic, no LLM, reproducible.

## The probe

1. **SSRF guard** — only public `http(s)`; the hostname is DNS-resolved and rejected if it maps to a private / loopback / link-local / unique-local / CGNAT address. Non-`http(s)` schemes are rejected.
2. **Legitimate MCP handshake only** — a JSON-RPC 2.0 `initialize`, then `notifications/initialized`, then `tools/list` (forwarding the `Mcp-Session-Id` so stateful servers are not false-negatives), then **one** read-only `tools/call`, then a malformed-method probe for error behavior.
3. **No auth-bypass, no payment, no destructive calls.** Priced/x402 endpoints are recorded as *delivery UNVERIFIED* — never asserted as returning content.
4. **Rate-limited & rolling.** We audit a bounded batch per run and roll across the full population over time; certificates are short-lived because liveness decays.

## Scoring

Each of the 10 criteria yields a boolean with attached evidence; the grade is a deterministic function of the pass count with an honesty cap. Every certificate embeds, per criterion, an `evidence_sha256` and the issuer pubkey, so anyone can re-run the audit and recompute the hashes — **the verdict carries its own falsification procedure.**

## What we do NOT do

No named "dead/worst/fake" lists (failure patterns are aggregated anonymously). No private data, no PII enrichment, no ToS-violating mass automation. Public-registry data only.
