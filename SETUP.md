# Setup Guide

Detailed instructions for setting up Multi-Agent Crew.

## Prerequisites

- **Claude Code** — Install from [Anthropic](https://docs.anthropic.com/en/docs/claude-code)
- **Node.js 18+** — Required for MCP servers
- **Git** — For version control

### Optional

- **n8n instance** — For workflow automation (self-hosted or cloud)
- **GitHub account** — For the GitHub MCP server

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/ppablobr/multi-agent-crew.git
cd multi-agent-crew
```

### 2. Configure MCP servers

Copy the example configuration:

```bash
cp .mcp.json.example .mcp.json
```

Edit `.mcp.json` with your credentials:

#### n8n MCP Server

If you have an n8n instance:

```json
{
  "n8n-mcp": {
    "command": "npx",
    "args": ["n8n-mcp"],
    "env": {
      "N8N_API_URL": "https://your-n8n-instance.example.com",
      "N8N_API_KEY": "your-api-key"
    }
  }
}
```

To get your n8n API key:
1. Open your n8n instance
2. Go to Settings > API
3. Create a new API key

#### GitHub MCP Server

```json
{
  "github": {
    "command": "npx",
    "args": ["-y", "@modelcontextprotocol/server-github"],
    "env": {
      "GITHUB_PERSONAL_ACCESS_TOKEN": "your-github-pat"
    }
  }
}
```

To create a GitHub PAT:
1. Go to GitHub > Settings > Developer settings > Personal access tokens
2. Create a token with repo access

#### Google Sheets MCP Server

Enables agents to read and write Google Sheets directly (used by LinkedIn Agent for post tracking, Data Analytics Agent for dashboards, etc.).

**Step 1 — Create a Google Cloud project**

1. Go to [console.cloud.google.com](https://console.cloud.google.com)
2. Create a new project (or select an existing one)

**Step 2 — Enable the Google Sheets API**

1. Go to **APIs & Services > Library**
2. Search for "Google Sheets API" and click **Enable**

**Step 3 — Configure the OAuth consent screen**

1. Go to **APIs & Services > OAuth consent screen**
2. User type: **External** (or Internal for Google Workspace accounts)
3. Fill in app name and support email
4. Add scope: `https://www.googleapis.com/auth/spreadsheets`
5. Add your Google account as a test user

**Step 4 — Create OAuth2 credentials**

1. Go to **APIs & Services > Credentials**
2. Click **Create Credentials > OAuth Client ID**
3. Application type: **Desktop App**
4. Download the JSON file
5. Save it inside the `credentials/` directory:
   ```
   credentials/client_secret_YOUR_CLIENT_ID.apps.googleusercontent.com.json
   ```

**Step 5 — Generate the authentication token**

Start Claude Code and trigger any Google Sheets action (e.g., "list my spreadsheets"). The MCP server will open a browser window for OAuth authorization. After authorizing, the token is saved automatically to `credentials/token.json`.

**Step 6 — Update `.mcp.json`**

```json
{
  "google-sheets": {
    "command": "npx",
    "args": ["-y", "mcp-google-sheets"],
    "env": {
      "CREDENTIALS_PATH": "./credentials/client_secret_YOUR_CLIENT_ID.apps.googleusercontent.com.json",
      "TOKEN_PATH": "./credentials/token.json"
    }
  }
}
```

> Both `credentials/` and `.mcp.json` are in `.gitignore` — your credentials will never be committed.

### 3. Start Claude Code

```bash
claude
```

The orchestrator will greet you and list available agents.

## First Run

Try these commands to test the agents:

- "Create a LinkedIn post about AI agents"
- "Build an n8n workflow for sending Slack notifications"
- "Map the onboarding process"
- "Create a learning path for prompt engineering"

## Troubleshooting

### MCP servers not connecting

- Verify `.mcp.json` has correct credentials
- Ensure `npx` is available in your PATH
- Check that n8n instance is accessible

### Skills not triggering

- Verify SKILL.md files have correct YAML frontmatter
- Check that the `description` field matches your prompt
- See `shared/docs/skill-yaml-pattern.md` for the pattern

### Agent not found

- Ensure the agent has an `AGENT.md` in `agents/<name>/`
- Check that the agent is listed in `CLAUDE.md`
