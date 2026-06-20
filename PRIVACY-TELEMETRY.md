# Telemetry & Privacy Note (SaSame public surfaces)

SaSame runs **passive, defensive** telemetry on its own public endpoints (Observatory + live MCP). We observe what arrives at our surface; we never intrude on, bait, or fingerprint visitors.

**What we record** (scrubbed): request path (no query string), method, status, timing, protocol, referer, User-Agent, and MCP events (initialize / tools/list / tools/call). For tool calls we keep only the *shape* of arguments (key names) and a salted hash — never raw argument values.

**What we never store**: Authorization headers, cookies, raw query strings, raw MCP arguments, and we run no tracking pixels and no device/canvas fingerprinting.

**IP handling (EU/Romania-aligned)**: raw IP is used transiently to derive ASN / organisation / country / reverse-DNS, then dropped. Long-term we keep only a salted hash plus those network-level facts. Raw access logs rotate within ~30 days.

**Purpose**: classify the crawlers, registries, AI agents and scanners that fetch us — to tell reach from demand — and to flag blind/hostile scanning defensively. We never block, reverse-scan, or return different dangerous content to bots.

**Your control**: if your service appears in the [Observer Census](observers.html), you can claim or correct your entry for free.
