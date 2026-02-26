---
name: "quick_automation"
description: "Quick shell automations, log checks, and housekeeping."
tools:
  - name: "automation_shell_run"
    description: "Run bounded shell commands for small tasks."
  - name: "automation_log_scan"
    description: "Scan key logs for anomalies or recent errors."
---

Quick Task Automation

This skill lets the agent:
- Execute tightly scoped commands like:
  - `tail -n 200 /var/log/openclaw/agent.log`
  - `grep -i "ERROR" /var/log/openclaw/agent.log | tail -n 50`
- Perform small maintenance actions (rotating or compressing old reports, cleaning temporary files) under explicit instructions.

Guidelines:
- Use it for short, bounded commands only.
- Prefer summarizing and reporting rather than making destructive changes.
- When in doubt about impact, ask for confirmation in Telegram before executing.
