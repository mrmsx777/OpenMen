---
name: "web_osint"
description: "Stealth web browsing, news monitoring, and trend OSINT."
tools:
  - name: "web_osint_scan"
    description: "Run targeted OSINT scans over web sources (news, blogs, social) via the headless browser."
  - name: "web_news_brief"
    description: "Pull news headlines and summaries for specific topics and time windows."
  - name: "web_search_snapshot"
    description: "Capture and summarize SERP and page snapshots for later reference."
---

Web OSINT, News, and Trends

This skill instructs the agent to:
- Use the integrated headless browser to open target URLs, scroll, and extract key content into markdown summaries.
- Check multiple news sources for a topic and synthesize a neutral, de-duplicated brief.

Example command patterns:
- `browser.open` → load the page, then extract main article text and metadata.
- `browser.search` → run a search query, capture top results, and open selected links.
- When an external search API is configured, use:
  `newsapi latest --topic "cybersecurity" --json`
  or
  `serp query --q "CVE-2026-*" --json`

Always:
- Record sources and timestamps into memory/YYYY-MM-DD.md.
- Flag strong signals (new CVEs, active campaigns, breaking incidents) for Telegram reporting.
