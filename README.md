# SaSame MCP Observatory

> **MCP Readiness Passports for agent discovery** — agent-readable readiness records for public MCP servers: reachable, callable, and schema-valid (owner-confirmed and continuously monitored only at Claimed/Certified level). Verification status only; never a safe/good/worth-using verdict.

**🪪 Is your MCP server listed here? [Claim your MCP Readiness Passport free →](https://github.com/shigeki7777/sasame-mcp-observatory/issues/new?template=claim-passport.yml)** — a public, owner-controlled, agent-readable record of measured readiness. Prove control via `.well-known` / DNS / repo. No account setup, no cost, no sales pitch.

💬 **Early Access & feedback:** join the [SaSame MCP Readiness Discord](https://discord.gg/bAKtSKqKT) — ask questions, share feedback, get help claiming your passport.

We continuously and externally audit public MCP (Model Context Protocol) servers — does each one actually complete the handshake, list valid tools, return real content, and stay reachable — and publish **signed, time-limited readiness observations**. This repo is the transparent mirror of https://live-vps.sasame.online/observatory/.

## The numbers (latest)

- **30000** public MCP entries indexed (20876 with an auditable remote endpoint)
- **3606** audited · **1108** currently meet the **Observed MCP-Ready** bar (A/B)
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

## Participate (humans + agents welcome)

This is an **open participation entrance**, not a sales list. Three ways in:

- 🤖 **Bring your agent.** Hand it the public toolbelt and let it audit a server, submit itself, or call the tools: https://live-vps.sasame.online/for-agents/
- 🪪 **Builders:** [claim your passport](https://github.com/shigeki7777/sasame-mcp-observatory/issues/new?template=claim-passport.yml), [request an audit](https://github.com/shigeki7777/sasame-mcp-observatory/issues/new?template=request-mcp-audit.yml), or [submit your agent](https://github.com/shigeki7777/sasame-mcp-observatory/issues/new?template=submit-your-agent.yml).
- 🛠️ **Developers:** see [CONTRIBUTING.md](CONTRIBUTING.md). Issues labelled `good first issue` and `agent-task` are small, well-scoped, and PR-friendly.

**Pick one concrete action:**
- Get an audit: drop an MCP URL in [Discussion #8](https://github.com/shigeki7777/sasame-mcp-observatory/discussions/8).
- Attack the instrument: tell us what the Standard mismeasures in [Discussion #9](https://github.com/shigeki7777/sasame-mcp-observatory/discussions/9).
- Show the signal: post your agent's first external `tools/call` in [Discussion #10](https://github.com/shigeki7777/sasame-mcp-observatory/discussions/10).
- Take a small task: start with [#4 verifier port](https://github.com/shigeki7777/sasame-mcp-observatory/issues/4), [#5 audit disagreement](https://github.com/shigeki7777/sasame-mcp-observatory/issues/5), or [#7 offline cert verifier](https://github.com/shigeki7777/sasame-mcp-observatory/issues/7).

💬 Coordinate in [GitHub Discussions](https://github.com/shigeki7777/sasame-mcp-observatory/discussions) (the durable forum: Show and tell, Q&A, Ideas) or the [Discord](https://discord.gg/bAKtSKqKT) (live chat).

## Honesty

This is a **v0.1 draft**, not affiliated with the official MCP project. Observations are **snapshots** and **time-limited** (certs expire ~14 days; liveness decays). We list only A/B servers (positive); we **never** publish a "worst/dead/fake" list — failure patterns are aggregated anonymously as *common failure modes*. We disclose our interest: SaSame helps builders make MCP servers AI-callable. That is exactly why the criteria, the verifier, and every certificate's evidence are open — **re-run it and tell us if we're wrong.**

_Generated 2026-06-22T04:44:41.285Z · data CC-BY · delist: consulting@srl-sasame.com_
