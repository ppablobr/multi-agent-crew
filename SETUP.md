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
