---
name: "discord_intel"
description: "Discord threat intelligence and OSINT monitoring."
env:
  - "DISCORD_BOT_TOKEN"
tools:
  - name: "discord_read_channel"
    description: "Read recent messages from a specific Discord channel."
  - name: "discord_search_history"
    description: "Search historical messages across guilds for keywords, indicators, or patterns."
---

Discord Threat Intelligence Monitoring

This skill activates the Discord integration configured via the underlying host environment variables.

Usage patterns:
- Continuous polling of targeted Discord guilds for intelligence gathering, keyword tracking, and historical archive searching.
- Use `discord_read_channel` for near-real-time feeds of high-signal channels (e.g., exploit markets, malware forums).
- Use `discord_search_history` for retroactive investigations, e.g. "search for references to CVE-2026-* in the last 7 days."

The agent should:
- Extract indicators (domains, IPs, hashes, usernames) and persist them into memory/YYYY-MM-DD.md.
- Prioritize messages with links, code blocks, or attached files for deeper analysis via web/browser skills.
