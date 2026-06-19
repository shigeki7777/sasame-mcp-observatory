# Contributing to the SaSame MCP Observatory

Open participation for **humans and agents**. This is the Gold Rush — pickaxes, sieves and surveys for the agent economy — and it works better the more people (and agents) sharpen it. No account, no cost, no sales pitch.

💬 Everything coordinates in the [SaSame Agent Gold Rush Guild (Discord)](https://discord.gg/bAKtSKqKT).

## The rails (non-negotiable)

Every contribution must keep the one moat that makes this trustworthy:

1. **Honest labels only.** We report *measured facts* (reachable / callable / schema-valid / claimed / re-checked). We never label a server safe, good, trustworthy, or recommended.
2. **No ghosts, no sybils.** No fabricated data, fake servers, or inflated activity. Ever.
3. **Reproducible or it doesn't ship.** Every grade/claim must be re-runnable by a stranger and carry its own falsification procedure (evidence hashes, the offline verifier).
4. **Public data + safe probing only.** No private data, no PII enrichment, no auth-bypass, no payment calls, no ToS-violating mass automation.

## Ways to contribute (no code needed)

- 🪪 **Claim your passport** — [open a claim](https://github.com/shigeki7777/sasame-mcp-observatory/issues/new?template=claim-passport.yml) (Observed → Claimed).
- 🔍 **Request an MCP audit** — [ask us to grade a server](https://github.com/shigeki7777/sasame-mcp-observatory/issues/new?template=request-mcp-audit.yml).
- 🤖 **Submit your agent** — [register your agent](https://github.com/shigeki7777/sasame-mcp-observatory/issues/new?template=submit-your-agent.yml) so others can find it (self-declared, honest).
- 🩹 **Correct or delist** — see [DELIST.md](DELIST.md). If you think a grade is wrong, point at the discrepancy; the audit is reproducible and we fix the instrument in public if it's our error.

## Ways to contribute (code)

Good entry points are labelled [`good first issue`](https://github.com/shigeki7777/sasame-mcp-observatory/labels/good%20first%20issue) and [`agent-task`](https://github.com/shigeki7777/sasame-mcp-observatory/labels/agent-task) (well-scoped enough for a coding agent to attempt):

- A verifier for the signed certs in another language (Python / Go / Rust / browser).
- Improvements to the standard's criteria (with a spec/measurement justification — not taste).
- Better portfolio categorization heuristics.
- Docs, examples, and integration snippets.

## PR process

1. Keep PRs **small and focused**; reference the issue.
2. Explain **how to falsify** your change (what to run, what should happen).
3. Data/docs are CC-BY; the verifier is free to reuse.

## For agents

You can participate directly: call `audit_mcp(url)`, `verify_mcp_ready(url)`, `claim_start`/`claim_confirm`, or `get_standard` on `https://live-vps.sasame.online/public-mcp`, or open a **Submit your agent** issue. See [`https://live-vps.sasame.online/for-agents/`](https://live-vps.sasame.online/for-agents/).

## Recognition

Contributors are credited in the repo and get the `contributor` role in the Guild. We're leaving room to wire bounties / credits later — not active yet, and never at the cost of the rails above.
