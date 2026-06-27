# Claim your MCP server

If your server is listed as **Observed MCP-Ready (unclaimed)**, the signed certificate is already yours to use. To upgrade **Observed → Claimed**:

1. Call MCP `claim_start` (get a challenge token) then `claim_confirm` on `https://live-vps.sasame.online/public-mcp`, **or** email **consulting@srl-sasame.com** from the server's domain.
2. Prove control via any one of: a `.well-known/mcp-ready-claim.txt` file, a DNS TXT record, your GitHub repo, or your agent-card.
3. Once verified, your listing shows **Claimed** (owner-confirmed) and your certificate's `level` becomes `claimed`.

Want your real-time grade now? Run the free audit: MCP `audit_mcp(url)` / `verify_mcp_ready(url)` on `https://live-vps.sasame.online/public-mcp`.

**Embed your badge** (A/B): `[![SaSame MCP Readiness](https://live-vps.sasame.online/observatory/badge/<your-server>.svg)](https://live-vps.sasame.online/observatory/)`
