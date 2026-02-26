---
name: "gog_workspace"
description: "Google Workspace automation via gogcli (Gmail, Docs, Drive)."
requires:
  - "gogcli"
env:
  - "GOG_ACCOUNT"
tools:
  - name: "gog_gmail_read"
    description: "Read and search Gmail threads for the configured GOG_ACCOUNT."
  - name: "gog_docs_write"
    description: "Create and update Google Docs from local markdown or text files."
  - name: "gog_drive_list"
    description: "List and locate files in Google Drive."
---

Google Workspace Automation (gog)

This skill exposes the Google Workspace CLI, bridging the agent to Gmail, Drive, and Google Docs.

Execution mapping:
- For Gmail: use commands like  
  `gog gmail list --label INBOX --max-results 50 --json --no-input`  
  `gog gmail read --thread-id THREAD_ID --json --no-input`
- For Docs: use commands like  
  `gog docs create --title "Emerging Threats Report" --content-file report.md --json --no-input`
- For Drive search:  
  `gog drive search --query "name contains 'intel' and mimeType = 'application/vnd.google-apps.document'" --json --no-input`

Always use `--json` and `--no-input` for deterministic, machine-readable responses.
The agent should:
- Prefer summaries and doc drafts for long email threads.
- Create a new Google Doc for substantial intelligence reports and link back in Telegram.
