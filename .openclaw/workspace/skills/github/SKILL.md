---
name: "github_automation"
description: "Automate GitHub issues, PRs, and repo intelligence."
env:
  - "GITHUB_TOKEN"
tools:
  - name: "github_repo_scan"
    description: "List issues, PRs, and security alerts for a repo."
  - name: "github_issue_create"
    description: "Create new GitHub issues with structured metadata."
---

GitHub Automation and Repo Intelligence

This skill lets the agent:
- Fetch open issues, PRs, and security alerts using commands like:  
  `gh issue list --repo OWNER/REPO --json title,number,labels,state`  
  `gh pr list --repo OWNER/REPO --json title,number,state`
- Create issues for follow-up tasks and automation reminders via:  
  `gh issue create --repo OWNER/REPO --title "Automated task" --body file:issue.md`

Use this for:
- Converting findings from OSINT scans or Gmail into trackable tasks.
- Maintaining a backlog of investigations or automations directly from the agent.
