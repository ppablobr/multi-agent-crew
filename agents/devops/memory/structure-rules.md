# DevOps Agent — Structure Rules

> Convenções e padrões aprendidos da estrutura do projeto multi-agent-crew

---

## 📁 Directory conventions

### Established patterns (inferred from existing structure):

```
multi-agent-crew/
├── agents/[name]/          → Agent-specific files
│   ├── AGENT.md           → Agent documentation (persona, specialties)
│   └── memory/            → Agent memory files
│       └── *.md           → Memory files in markdown
│
├── .claude/
│   ├── skills/[name]/     → Skills YAML
│   │   ├── SKILL.md       → Skill definition (YAML frontmatter + instructions)
│   │   └── evals/         → Optional evaluation files
│   └── commands/          → Slash commands (deprecated for most agents)
│
├── shared/                → Cross-agent resources
│   ├── memory/            → Shared memory (world.md, handoff.md)
│   ├── processes/         → Process documentation and diagrams
│   └── workflows/         → Workflow documentation
│
├── docs/                  → Documentation, diagrams, architecture files
│   └── *.excalidraw       → Excalidraw diagrams live here
│
└── [root]                 → Only CLAUDE.md, README.md, configs (.mcp.json, etc)
```

---

## 🏷️ Naming conventions

### Files and directories:
- **Agents:** `kebab-case` (e.g., `agent-manager`, `ai-pm`, `devops`)
- **Skills:** `kebab-case` (e.g., `linkedin`, `n8n`, `devops`)
- **Memory files:** `kebab-case` (e.g., `ecosystem-map.md`, `history.md`, `structure-rules.md`)
- **Slash commands:** `kebab-case` with leading `/` (e.g., `/agent-manager`)

### Pattern: All lowercase, words separated by hyphens, no underscores or camelCase

---

## 📝 File type locations

| File type | Location | Example |
|---|---|---|
| `.excalidraw` diagrams | `docs/` | `docs/multi-agent-crew-architecture.excalidraw` |
| Process maps | `shared/processes/` | `shared/processes/cobranca-parceiros-ecommerce.md` |
| Workflow docs | `shared/workflows/` | `shared/workflows/verificacao-cobrancas-workflow.md` |
| Agent documentation | `agents/[name]/AGENT.md` | `agents/devops/AGENT.md` |
| Skills | `.claude/skills/[name]/SKILL.md` | `.claude/skills/devops/SKILL.md` |
| Shared memory | `shared/memory/` | `shared/memory/world.md` |
| Agent memory | `agents/[name]/memory/` | `agents/devops/memory/history.md` |

---

## ✅ Standards reference

Documented standards maintained by Agent Manager:
- See `agents/agent-manager/memory/standards.md` for full conventions
- YAML Skills format is the current standard (as of 2026-03-12)
- Slash commands deprecated except for Agent Manager

---

## 🔄 Learning process

When encountering new file types:
1. Search for similar files in the project
2. Identify patterns (where do they currently live?)
3. Check standards.md for documented rules
4. Apply pattern consistently
5. Document new pattern here if it's a new type

---

_This file is maintained by the DevOps Agent. Update whenever you learn new conventions._
