# SaSame MCP Observatory

> A public, reproducible observatory of MCP servers: external readiness observations, signed MCP-Ready certificates, and curated portfolios of agent-callable tools.

We continuously and externally audit public MCP (Model Context Protocol) servers — does each one actually complete the handshake, list valid tools, return real content, and stay reachable — and publish **signed, time-limited readiness observations**. This repo is the transparent mirror of https://live-vps.sasame.online/observatory/.

> 🔭 **Live viewer:** https://shigeki7777.github.io/sasame-mcp-observatory/ — browse the Agent Passport Registry (dashboard + identity-confidence ladder + coarse Map + search over all indexed endpoints).
>
> 🪪 **Is your endpoint here?** Search your domain in the viewer — if it is `unclaimed`, **claim it for free** ([CLAIM.md](CLAIM.md)) and embed an [Agent Passport badge](BADGE.md). No account setup, no cost, no sales pitch.

## The numbers (latest)

- **30000** public MCP entries indexed (21137 with an auditable remote endpoint)
- **1031** audited · **205** currently meet the **Observed MCP-Ready** bar (A/B)
- **2,286** owner-identifiable **claimable** endpoints (A/B grade + priced) — ranked in [`passports/claim-targets.json`](passports/claim-targets.json)
- Full numbers: [`data/latest/summary.json`](data/latest/summary.json)

> 📊 **Scoreboard (daily):** [`gold-rush-scoreboard.json`](gold-rush-scoreboard.json) — North Star = **external claims** (owner-proven control by a non-SaSame party). History: [`scoreboard-history.jsonl`](scoreboard-history.jsonl). We measure what is real and report unmeasurable KPIs as null.

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

## Agent Passports

The per-agent rollup of this Observatory lives in [`passports/`](passports/): one
machine-readable record per indexed endpoint, joining self-declaration + outside-in
observation + what is still unconfirmed, with an explicit **identity confidence**
(`unconfirmed` → `self_asserted` → `owner_proven` → `corroborated`).

We publish **verification status only — never a risk verdict** on a named agent.
(A GET probe is a weak signal; MCP answers over POST, so "content not verified via
GET" is expected, not a defect.) Full per-agent data ships as
[Release](https://github.com/shigeki7777/sasame-mcp-observatory/releases) assets;
lightweight summaries + samples are in [`passports/`](passports/).

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

_Generated 2026-06-18T12:48:17.573Z · data CC-BY · delist: consulting@srl-sasame.com_
