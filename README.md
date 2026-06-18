# SaSame MCP Observatory

> A public, reproducible observatory of MCP servers: external readiness observations, signed MCP-Ready certificates, and curated portfolios of agent-callable tools.

We continuously and externally audit public MCP (Model Context Protocol) servers — does each one actually complete the handshake, list valid tools, return real content, and stay reachable — and publish **signed, time-limited readiness observations**. This repo is the transparent mirror of https://live-vps.sasame.online/observatory/.

## The numbers (latest)

- **34548** public MCP entries indexed (21332 with an auditable remote endpoint)
- **587** audited · **129** currently meet the **Observed MCP-Ready** bar (A/B)
- Full numbers: [`data/latest/summary.json`](data/latest/summary.json)

## Three levels (we do not over-claim)

| Level | Meaning |
|---|---|
| **Observed** | SaSame measured the public endpoint **from the outside**; owner NOT confirmed (`unclaimed: true`). A third-party observation, not an endorsement. |
| **Claimed** | The owner proved control (`.well-known` / DNS / repo / agent-card). |
| **Certified** | SaSame continuously monitors or has fixed the server. Used sparingly. |

## What's here

- [`STANDARD.md`](STANDARD.md) — the Agent-Tool Discoverability Standard (the 10 criteria, each spec-derived or measured)
- [`METHODOLOGY.md`](METHODOLOGY.md) — exactly how we probe (GET + legitimate MCP handshake only; SSRF-guarded; no auth-bypass, no payment, no destructive calls)
- [`CLAIM.md`](CLAIM.md) — claim your server (Observed → Claimed)
- [`DELIST.md`](DELIST.md) — correct or remove a listing
- [`PORTFOLIOS/`](PORTFOLIOS/) — curated Observed MCP-Ready servers by use-case
- [`data/latest/`](data/latest/) — lightweight machine-readable index + observed-ready set
- [`certs/`](certs/) — ed25519-signed MCP-Ready certificates (A/B), offline-verifiable

## Verify a certificate yourself (no callback to us)

```js
import crypto from "node:crypto";
function verify(cert) { // {signature, canonical_json}
  const body = JSON.parse(cert.canonical_json);
  const pub = crypto.createPublicKey({ key: Buffer.from(body.issuer_pubkey_spki_hex, "hex"), format: "der", type: "spki" });
  return crypto.verify(null, Buffer.from(cert.canonical_json, "utf8"), pub, Buffer.from(cert.signature, "base64"));
}
```
Then re-run the audit against the subject and recompute each `evidence_sha256`.

## Honesty

This is a **v0.1 draft**, not affiliated with the official MCP project. Observations are **snapshots** and **time-limited** (certs expire ~14 days; liveness decays). We list only A/B servers (positive); we **never** publish a "worst/dead/fake" list — failure patterns are aggregated anonymously as *common failure modes*. We disclose our interest: SaSame helps builders make MCP servers AI-callable. That is exactly why the criteria, the verifier, and every certificate's evidence are open — **re-run it and tell us if we're wrong.**

_Generated 2026-06-18T10:34:49.880Z · data CC-BY · delist: consulting@srl-sasame.com_
