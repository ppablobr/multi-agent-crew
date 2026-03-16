# Contributing to Multi-Agent Crew

Thank you for your interest in contributing! This guide explains how to add agents, write skills, and submit changes.

## How to Add a New Agent

### 1. Create the agent structure

```bash
mkdir -p agents/your-agent/memory
mkdir -p agents/your-agent/skills/your-skill
```

### 2. Write `AGENT.md`

This is the agent's persona. It should include:

- **Persona** — Who the agent is and what it specializes in
- **Skills** — What it can do
- **Rules** — Behavioral guidelines
- **Collaboration** — When to involve other agents
- **Memory** — What files it reads/writes

Example structure:
```markdown
# Agent Name

## Persona
You are a specialist in [domain]...

## Skills
- Skill 1
- Skill 2

## Rules
1. Always do X
2. Never do Y

## Collaboration
| Situation | Agent to consult |
|---|---|
| Need visuals | Designer Agent |

## Memory
- `agents/your-agent/memory/history.md` — Action log
```

### 3. Write `SKILL.md` with YAML frontmatter

Every skill MUST have YAML frontmatter for auto-invocation. See [shared/docs/skill-yaml-pattern.md](shared/docs/skill-yaml-pattern.md) for the complete pattern.

```yaml
---
name: your-skill-name
description: >
  Use when the user asks to [action]. Examples include
  "[example 1]", "[example 2]", or any request involving
  [keywords]. Use this skill whenever the user mentions [triggers].
---

# Skill Title

## Objective
[What this skill does]

## Process
[Step-by-step instructions]
```

**Key rules:**
- `name` must be in kebab-case
- `description` must be in English
- Description must start with "Use when..."
- Include examples and trigger keywords

### 4. Initialize memory

Create `agents/your-agent/memory/history.md`:
```markdown
# History: your-agent Agent
> Chronological log of agent actions and outputs.

---

<!-- Add entries here -->
```

### 5. Register the agent

- Add the agent to the table in `CLAUDE.md`
- Add the agent to the table in `shared/memory/world.md`

## Writing Evaluations

Evaluations test that skills produce correct outputs. See the n8n agent's evaluations as examples:

```
agents/n8n/evaluations/
├── code-javascript/     (5 evals)
├── code-python/         (5 evals)
├── expression-syntax/   (4 evals)
├── mcp-tools/           (5 evals)
├── node-configuration/  (4 evals)
├── validation-expert/   (4 evals)
└── workflow-patterns/   (5 evals)
```

Each eval is a JSON file with an input prompt and expected output criteria.

## Pull Request Process

1. Fork the repository
2. Create a feature branch (`git checkout -b feat/your-agent`)
3. Make your changes following the patterns above
4. Test your agent/skill manually with Claude Code
5. Submit a PR with:
   - Clear description of what the agent/skill does
   - Example prompts that trigger it
   - Any new dependencies or MCP servers needed

## Code of Conduct

This project follows the [Contributor Covenant](https://www.contributor-covenant.org/version/2/1/code_of_conduct/) Code of Conduct.

## Questions?

Open an issue with the `question` label or check existing issues for similar topics.
