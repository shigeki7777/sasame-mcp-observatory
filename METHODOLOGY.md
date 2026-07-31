# Methodology

How SaSame observes a public MCP server. Deterministic, no LLM, reproducible. Exact instrument: `agent-tool-discoverability-standard/0.4`.

## The probe

1. **SSRF guard** — only public `http(s)`; the hostname is DNS-resolved and rejected if it maps to a private / loopback / link-local / unique-local / CGNAT address. Non-`http(s)` schemes are rejected.
2. **Revision-aware protocol entry** — try MCP 2026-07-28 `server/discover` first. Fall back to legacy `initialize` only after a bounded unsupported-method result; send `notifications/initialized` and `Mcp-Session-Id` only on that legacy path.
3. **Legitimate MCP calls only** — `tools/list`, then **one** read-only `tools/call`, then a malformed-method probe for error behavior. Modern follow-ups repeat negotiated request metadata and remain sessionless.
4. **No auth-bypass, no payment, no destructive calls.** Priced/x402 endpoints are recorded as *delivery UNVERIFIED* — never asserted as returning content.
5. **Rate-limited & rolling.** We audit a bounded batch per run and classify endpoints as `legacy_only`, `modern_only`, `dual_stack`, or `indeterminate`; unknown is never silently treated as failure.

## Scoring

C1, C6 and C8 are revision-neutral: they measure successful protocol entry, entry latency and machine-discoverable identity using the negotiated era. Each criterion yields a boolean with attached evidence; the grade is a deterministic function of the pass count with an honesty cap. Every certificate embeds, per criterion, an `evidence_sha256` and the issuer pubkey, so anyone can re-run the audit and recompute the hashes — **the verdict carries its own falsification procedure.**

## What we do NOT do

No named "dead/worst/fake" lists (failure patterns are aggregated anonymously). No private data, no PII enrichment, no auth-bypass, no payment calls, no ToS-violating mass automation. Public-registry data only.
