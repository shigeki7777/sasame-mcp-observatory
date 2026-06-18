# Agent Passports

An **Agent Passport** is the per-agent rollup of this Observatory: for each public
MCP / x402 endpoint we have indexed, one machine-readable record that joins
*what it self-declared*, *what we observed from outside*, and *what is still
unconfirmed* — with an explicit confidence about **who controls the endpoint**.

This is the same discipline as the rest of the Observatory, applied per agent:
**public endpoint observability only.** It is **not** KYC, identity verification of
humans, enforcement, a deny-list, or operator geolocation. We make **no badness
verdict** about any named agent. The strongest caution we ever publish is
*"verify before trust"*, and it is **always clearable by claiming** (see
[`../CLAIM.md`](../CLAIM.md)).

## Why there is no "risk score" here

An earlier internal draft carried a numeric `risk_level`. We removed it from the
published record on purpose. A label like "high risk" on a *named, unclaimed*
third party reads as an accusation we cannot prove from public evidence — and a
GET probe is a **weak signal** (MCP servers answer over **POST**, so "content not
verified via GET" is *expected*, not a defect). Publishing an accusation we can't
prove would burn the one thing this project runs on: verifiable honesty. So the
public record states only **verification status** — what we could and could not
confirm — never a verdict.

## Identity confidence (who controls the endpoint)

| `identity_status` | `identity_confidence` | meaning |
|---|---|---|
| `unclaimed` | `unconfirmed` | auto-indexed from a public registry; owner not confirmed (the default) |
| `self_claimed` | `self_asserted` | endpoint self-declares an identity, but control is not proven |
| `claimed` | `owner_proven` | owner proved control (`.well-known` / DNS / repo / agent-card) |
| `verified` | `corroborated` | claimed **and** independently corroborated (signed audit / cert) |

`identity_confidence` (who controls it) and `audit_grade` (how the endpoint
behaved) are **separate axes** on purpose: an `unclaimed` server can still be a
perfectly good grade-A server, and a `verified` identity is not automatically
"recommended".

## What's here (lightweight, in-repo)

- [`summary.json`](summary.json) — aggregate counts only (identity status, audit
  level, grade, registry, protocol, category). No accusations.
- [`agent-map.summary.json`](agent-map.summary.json) — the coarse, **non-operator-location**
  Agent Map as histograms + a `category × grade_band` cluster matrix. "Location"
  here is **topological** (registry / protocol / category / grade / TLD-class),
  **never geographic** — no IP, city, datacenter, or operator.
- [`samples/`](samples/) — six representative full passport records so the schema
  is browsable without downloading the full set.

## Full dataset (GitHub Release)

The full per-agent records are large, so they are published as **Release assets**
(kept out of git history), regenerated from local Census/Audit evidence with
**zero network I/O**:

- `passports-public.jsonl` — all per-agent public passports.
- `passports-index.json` — full index (one row per agent).
- `agent-map-public.json` — full Agent Map incl. per-agent markers.

See this repo's [Releases](https://github.com/shigeki7777/sasame-mcp-observatory/releases).

## The numbers (latest)

- **21137** passports generated from the local Census.
- Almost all are `unclaimed` (owner-unconfirmed) and most are `unaudited` — an
  honest picture of an early, mostly-unverified agent economy.

## Claim / correct / remove

Being observed, claiming, correcting, and delisting are **all free** — identity is
never paywalled. See [`../CLAIM.md`](../CLAIM.md) and [`../DELIST.md`](../DELIST.md).
You can also just open an issue or PR on this repo.
