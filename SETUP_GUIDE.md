# OpenMen Repository Initialization Guide

This guide details exactly how to initialize your local OpenMen repository from scratch, set up Git tracking securely, and configure your foundational environment variables so that your OpenClaw Daemon, APIs, and scripts operate seamlessly.

---

## 1. Initializing Git
Before doing anything with secrets, it is critical to initialize the folder as a Git repository and secure the `.gitignore` so no API keys ever leak.

### A. Initialize the Repository
Run the following inside your `OpenMen/` folder:
```bash
# Initialize a new git repository
git init

# (Optional) Switch default branch name to 'main'
git branch -M main

# Add your remote origin (Replace with your actual GitHub/GitLab URL)
git remote add origin https://github.com/YourUsername/OpenMen.git
```

### B. Secure Your `.gitignore`
It is essential that your `.gitignore` explicitly prevents the commitment of your operational `.env` file or SQLite database state. 

Open/Create a `.gitignore` file in your root directory and ensure these lines are present:
```bash
# Environment secrets
.env
.env.local

# Database state
*.db
*.sqlite

# Temporary Python files
__pycache__/
*.pyc

# IDE configs
.vscode/
.idea/
```

### C. Commit Your Base Structure
With the `gitignore` secured, commit your initial scripts and configurations:
```bash
git add .
git commit -m "Initial commit: Set up repository structure"
git push -u origin main
```

---

## 2. Managing Environment Variables
The OpenMen ecosystem relies heavily on a single `.env` file for API keys (e.g., Gemini, Moonshot, Discord). We manage this by utilizing a dummy `.env.example` file that *can* be safely pushed to GitHub. 

### A. Create the Dummy Template (`.env.example`)
Create `.env.example` in your root folder:
```bash
# Cognitive Engine Keys
GEMINI_API_KEY=""
MOONSHOT_API_KEY=""

# Telegram Bot
TELEGRAM_BOT_TOKEN=""

# Discord Integration
DISCORD_BOT_TOKEN=""

# Google Workspace CLI
GOG_ACCOUNT="your_bot_address@gmail.com"
```
You can safely `git add .env.example && git commit -m "Added .env template"` because it contains no actual secrets.

### B. Clone the Template to your Operational `.env`
Whenever you set up a new machine or pull down the repo, you simply copy the template and fill in your actual private keys:
```bash
cp .env.example .env
```
Now, **open the `.env` file** in your editor and paste in your actual `sk-YOUR_MOONSHOT_KEY` and `AIzaSy_YOUR_GEMINI_KEY`. 

Because you configured `.gitignore` in Step 1, this file will never accidentally push to GitHub.

---

## 3. Provisioning the OpenClaw Daemon
By default, the daemon processes configuration out of the `~/.openclaw` directory. 

### A. Injecting the Configs
Since your configuration files actually live inside your `OpenMen` repo, you must ensure the OpenClaw daemon can read your `.env` locally. 

In your `openclaw.json` configuration file, make sure the `envFile` path points absolutely to your repository:
```json
{
    "envFile": "/home/ubuntu/OpenMen/.env",
    "models": { ... }
}
```

### B. Securing the `.env` File
Run the following Linux permission command to lock down the file. This prevents other users on a shared AWS instance from reading your precious keys:
```bash
chmod 600 .env
```

### C. Testing the Environment in the Shell
If you are writing standalone Python scripts (like a `dashboard.py`), they will need access to these keys. You can manually push your `.env` to your current bash session using:
```bash
export $(grep -v '^#' .env | xargs)
```
After running this command, you will be able to verify the keys are active by typing `echo $MOONSHOT_API_KEY`.

---

### You are now fully initialized.
Your environment is secure, git history cleanly tracks only configuration templates, and your AWS/local machine correctly references a single, centralized `.env` file.
