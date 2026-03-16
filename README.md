# Multi-Agent Crew

A multi-agent orchestration framework for [Claude Code](https://docs.anthropic.com/en/docs/claude-code) — 10 specialized AI agents with shared memory, YAML skills, and collaboration protocols.

## What is this?

Multi-Agent Crew is a framework that turns Claude Code into a team of specialized AI agents. Each agent has its own persona, memory, and skills defined as YAML files. The orchestrator (CLAUDE.md) routes tasks to the right agent, enables collaboration between agents via a handoff protocol, and maintains shared context across sessions.

**Key features:**
- 10 specialized agents (Designer, LinkedIn, n8n, AI PM, Process Manager, Education, Agent Manager, Data Analytics, DevOps, Tech Docs Writer)
- YAML-based skill system with auto-invocation
- Persistent memory per agent + shared global memory
- Sequential handoff protocol for multi-agent collaboration
- 32 evaluation tests for the n8n agent
- MCP server integration (n8n, GitHub)

## Agents

| Agent | Skill | Specialty |
|---|---|---|
| **Designer** | `designer` | Visual design, frontend interfaces, web artifacts |
| **LinkedIn** | `linkedin` | Professional posts, social content about AI/tech |
| **n8n** | `n8n` | Workflows, automations, and integrations |
| **AI Project Manager** | `ai-pm` | Project management, roadmaps, sprints |
| **Process Manager** | `process-manager` | Process mapping, SOPs, optimization |
| **Education** | `education` | Learning materials about AI, LLMs, automation |
| **Agent Manager** | `/agent-manager` | Creating and managing agents |
| **Data Analytics** | `data-analytics` | Data analysis, ROI, dashboards |
| **DevOps** | `devops` | Project organization, structure auditing |
| **Tech Docs Writer** | `tech-docs-writer` | PRDs, roadmaps, technical documentation |

## Architecture

The system is organized in layers:

```
Orchestrator (CLAUDE.md)
    ↓ routes tasks
Agent Layer (AGENT.md per agent)
    ↓ invokes
Skill Layer (SKILL.md with YAML frontmatter)
    ↓ uses
Sub-skill Layer (specialized skills per agent)
    ↓ connects to
MCP Tools (n8n-mcp, GitHub)
    ↓ persists to
Memory Layer (per-agent + shared)
```

### How agents collaborate

Agents collaborate using a sequential handoff pattern:

```
[Agent A executes] → writes output to shared/memory/handoff.md → [Agent B reads and continues]
```

Example: Process Manager maps a process → n8n Agent builds the automation → Tech Docs Writer creates the SOP.

## Quick Start

### Prerequisites

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) installed
- Node.js 18+ (for MCP servers)
- (Optional) An n8n instance for workflow automation

### Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/ppablobr/multi-agent-crew.git
   cd multi-agent-crew
   ```

2. Configure MCP servers by copying the example config:
   ```bash
   cp .mcp.json.example .mcp.json
   ```
   Edit `.mcp.json` with your actual credentials.

3. Start Claude Code in the project directory:
   ```bash
   claude
   ```

4. The orchestrator will greet you and list available agents. Try:
   - "Create a LinkedIn post about AI agents"
   - "Build an n8n workflow to sync data from A to B"
   - "Map the process for customer onboarding"

See [SETUP.md](SETUP.md) for detailed setup instructions.

## Project Structure

```
multi-agent-crew/
├── CLAUDE.md                    # Orchestrator instructions
├── ARCHITECTURE.md              # System architecture documentation
├── AGENT-CORRELATION-MAP.md     # Agent interdependency map
├── agents/
│   ├── designer/                # Designer Agent
│   │   ├── AGENT.md             # Agent persona and rules
│   │   ├── memory/              # Agent-specific memory
│   │   └── skills/              # Agent skills
│   ├── linkedin/                # LinkedIn Agent
│   ├── n8n/                     # n8n Agent (7 sub-skills, 32 evals)
│   ├── ai-pm/                   # AI Project Manager
│   ├── process-manager/         # Process Manager
│   ├── education/               # Education Agent
│   ├── agent-manager/           # Agent Manager
│   ├── data-analytics/          # Data Analytics Agent
│   ├── devops/                  # DevOps Agent
│   └── tech-docs-writer/        # Tech Docs Writer
├── shared/
│   ├── memory/                  # Shared memory (world.md, handoff.md)
│   ├── docs/                    # Shared documentation
│   └── protocols/               # Collaboration protocols
├── .claude/
│   ├── skills/                  # Global skills (theme-factory, etc.)
│   ├── agents/                  # Agent definitions
│   └── commands/                # Slash commands
├── examples/                    # Real-world usage examples
└── .mcp.json.example            # MCP server config template
```

## Customizing

### Adding a new agent

1. Create `agents/your-agent/AGENT.md` with the agent's persona, skills, and rules
2. Create `agents/your-agent/memory/history.md` for the agent's memory
3. Create `agents/your-agent/skills/your-skill/SKILL.md` with YAML frontmatter
4. Update `CLAUDE.md` to include the new agent in the routing table
5. Update `shared/memory/world.md` to register the agent

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines and the [skill YAML pattern](shared/docs/skill-yaml-pattern.md).

### Modifying an existing agent

- Edit `agents/<name>/AGENT.md` to change the agent's persona or rules
- Edit skill files in `agents/<name>/skills/` to modify behavior
- Add evaluations in `agents/<name>/evaluations/` to test the agent

## Examples

See the [`examples/`](examples/) directory for real-world usage demonstrations:

- **[Billing Verification](examples/billing-verification/)** — Multi-agent collaboration (Process Manager → n8n Agent → Tech Docs Writer) to automate a finance process

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on adding agents, writing skills, and submitting PRs.

## License

[MIT](LICENSE) — Pedro Oliveira, 2026
