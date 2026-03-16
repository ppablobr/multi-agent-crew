# 🏗️ Multi-Agent Crew — Arquitetura do Sistema

> **Última atualização**: 2026-03-14
> **Status**: Documentação da correlação entre agentes, skills, tools e workflows

---

## 📊 Visão Geral

Este documento mapeia a correlação entre todos os componentes do sistema multi-agente:
- **8 Agentes** (com AGENT.md no projeto)
- **18+ Skills** (YAML skills no Claude Code)
- **2 MCP Servers** (n8n-mcp e github)
- **Evaluations** (testes automatizados)
- **Memory** (contexto persistente)

---

## 🤖 Agentes e Skills — Mapeamento Completo

### 1️⃣ Designer Agent

| Componente | Localização | Status |
|---|---|---|
| **AGENT.md** | `agents/designer/AGENT.md` | ✅ Ativo |
| **Skill YAML** | `~/.claude/skills/designer/SKILL.md` | ✅ Ativo |
| **Memory** | `agents/designer/memory/` | ✅ Ativo |

**Sub-skills disponíveis:**
- `canvas-design` — Arte estática (posters, banners)
- `frontend-design` — Interfaces web production-ready
- `theme-factory` — Aplicação de temas visuais
- `web-artifacts-builder` — Artefatos React complexos
- `excalidraw-diagram` — Diagramas editáveis

**Arquivos de memória:**
- `history.md` — Log de designs criados
- `design-library.md` — Componentes e paletas reutilizáveis

**MCP Tools utilizados:**
- `github` — Para versionamento de código frontend

---

### 2️⃣ LinkedIn Agent

| Componente | Localização | Status |
|---|---|---|
| **AGENT.md** | `agents/linkedin/AGENT.md` | ✅ Ativo |
| **Skill YAML** | `~/.claude/skills/linkedin/SKILL.md` | ✅ Ativo |
| **Memory** | `agents/linkedin/memory/` | ✅ Ativo |

**Sub-skills disponíveis:**
- Nenhuma (agente usa skills do Designer para criar imagens)

**Arquivos de memória:**
- `history.md` — Posts criados e engajamento
- `content-library.md` — Temas explorados e templates de posts

**Colaborações frequentes:**
- **Designer Agent** → Para criar imagens de posts
- **n8n Agent** → Para criar workflows de agendamento

**MCP Tools utilizados:**
- `github` — Para versionamento de conteúdo

---

### 3️⃣ n8n Agent

| Componente | Localização | Status |
|---|---|---|
| **AGENT.md** | `agents/n8n/AGENT.md` | ✅ Ativo |
| **Skill YAML** | `~/.claude/skills/n8n/SKILL.md` | ✅ Ativo |
| **Memory** | `agents/n8n/memory/` | ✅ Ativo |

**Sub-skills disponíveis:**
- `n8n-code-javascript` — Escrever código JavaScript em Code nodes
- `n8n-code-python` — Escrever código Python em Code nodes
- `n8n-expression-syntax` — Validar e escrever expressões n8n
- `n8n-mcp-tools-expert` — Guia de uso das ferramentas MCP
- `n8n-node-configuration` — Configurar nós com parâmetros corretos
- `n8n-validation-expert` — Interpretar e corrigir erros de validação
- `n8n-workflow-patterns` — Padrões arquiteturais de workflows

**Arquivos de memória:**
- `history.md` — Workflows criados
- `snippets.md` — Código e expressões reutilizáveis

**MCP Tools utilizados:**
- `n8n-mcp` — **Ferramenta principal** (acesso direto à instância n8n)
  - `n8n_create_workflow`
  - `n8n_update_partial_workflow`
  - `n8n_validate_workflow`
  - `n8n_test_workflow`
  - `n8n_deploy_template`
  - `search_nodes` / `get_node`
  - `search_templates` / `n8n_list_workflows`
- `github` — Para versionamento de workflows

**Evaluations (testes automatizados):**
```
agents/n8n/evaluations/
├── code-javascript/      (5 evals)
├── code-python/          (5 evals)
├── expression-syntax/    (4 evals)
├── mcp-tools/            (5 evals)
├── node-configuration/   (4 evals)
├── validation-expert/    (4 evals)
└── workflow-patterns/    (5 evals)
```

**Total**: 32 evaluations cobrindo todas as sub-skills

---

### 4️⃣ AI Project Manager Agent

| Componente | Localização | Status |
|---|---|---|
| **AGENT.md** | `agents/ai-pm/AGENT.md` | ✅ Ativo |
| **Skill YAML** | `~/.claude/skills/ai-pm/SKILL.md` | ✅ Ativo |
| **Memory** | `agents/ai-pm/memory/` | ✅ Ativo |

**Sub-skills disponíveis:**
- Nenhuma (usa Tech Docs Writer para documentação)

**Arquivos de memória:**
- `history.md` — Projetos gerenciados

**Colaborações frequentes:**
- **Tech Docs Writer** → Para criar PRDs, roadmaps
- **Designer Agent** → Para dashboards de KPIs
- **Process Manager** → Para mapear processos do projeto

**MCP Tools utilizados:**
- `github` — Para issues, milestones, projects

---

### 5️⃣ Process Manager Agent

| Componente | Localização | Status |
|---|---|---|
| **AGENT.md** | `agents/process-manager/AGENT.md` | ✅ Ativo |
| **Skill YAML** | `~/.claude/skills/process-manager/SKILL.md` | ✅ Ativo |
| **Memory** | `agents/process-manager/memory/` | ✅ Ativo |

**Sub-skills disponíveis:**
- Nenhuma (usa Designer Agent para diagramas visuais)

**Arquivos de memória:**
- `history.md` — Processos mapeados

**Colaborações frequentes:**
- **Designer Agent** → Para criar diagramas visuais de processos
- **n8n Agent** → Para automatizar processos mapeados
- **Tech Docs Writer** → Para documentar SOPs

**MCP Tools utilizados:**
- `github` — Para versionamento de documentação de processos

---

### 6️⃣ Education Agent

| Componente | Localização | Status |
|---|---|---|
| **AGENT.md** | `agents/education/AGENT.md` | ✅ Ativo |
| **Skill YAML** | `~/.claude/skills/education/SKILL.md` | ✅ Ativo |
| **Memory** | `agents/education/memory/` | ✅ Ativo |

**Sub-skills disponíveis:**
- Nenhuma (usa Designer Agent para materiais visuais)

**Arquivos de memória:**
- `history.md` — Conteúdos educacionais criados

**Colaborações frequentes:**
- **Designer Agent** → Para criar slides e materiais visuais
- **n8n Agent** → Para criar workflows educacionais de exemplo

**MCP Tools utilizados:**
- `github` — Para versionamento de conteúdo educacional

---

### 7️⃣ Agent Manager Agent

| Componente | Localização | Status |
|---|---|---|
| **AGENT.md** | `agents/agent-manager/AGENT.md` | ✅ Ativo |
| **Skill** | Slash command `/agent-manager` | ✅ Ativo (não é YAML skill) |
| **Memory** | `agents/agent-manager/memory/` | ⚠️ Sem memória criada |

**Sub-skills disponíveis:**
- `skill-creator` — Criar e modificar skills

**Arquivos de memória:**
- (Nenhum criado ainda)

**MCP Tools utilizados:**
- `github` — Para versionamento de agentes criados

---

### 8️⃣ Data Analytics Agent

| Componente | Localização | Status |
|---|---|---|
| **AGENT.md** | `agents/data-analytics/AGENT.md` | ✅ Ativo |
| **Skill YAML** | ❌ Não criada | ⚠️ Agente sem skill YAML |
| **Memory** | `agents/data-analytics/memory/` | ⚠️ Sem memória criada |

**Status**: Agente definido mas não implementado como skill YAML

---

## 🔌 MCP Servers

### n8n-mcp

**Configuração**: `.mcp.json`

```json
{
  "mcpServers": {
    "n8n-mcp": {
      "command": "npx",
      "args": ["n8n-mcp"],
      "env": {
        "N8N_API_URL": "https://your-n8n-instance.example.com",
        "N8N_API_KEY": "[REDACTED]"
      }
    }
  }
}
```

**Usado por**: n8n Agent

**Tools disponíveis**:
- Criação e gestão de workflows
- Validação e testes
- Deploy de templates
- Busca de nodes e templates

### github

**Configuração**: `.mcp.json`

```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "[REDACTED]"
      }
    }
  }
}
```

**Usado por**: Todos os agentes

**Tools disponíveis**:
- Criar/editar arquivos em repos
- Gerenciar issues e PRs
- Workflows do GitHub Actions

---

## 📊 Skills no Claude Code

### Total de skills: 18

**Skills mapeadas para agentes do projeto:**
1. `designer` → Designer Agent
2. `linkedin` → LinkedIn Agent
3. `n8n` → n8n Agent
4. `ai-pm` → AI Project Manager
5. `process-manager` → Process Manager
6. `education` → Education Agent

**Sub-skills (invocadas pelas skills principais):**
7. `canvas-design` (Designer)
8. `frontend-design` (Designer)
9. `theme-factory` (Designer)
10. `web-artifacts-builder` (Designer)
11. `excalidraw-diagram` (Designer)
12. `n8n-code-javascript` (n8n)
13. `n8n-code-python` (n8n)
14. `n8n-expression-syntax` (n8n)
15. `n8n-mcp-tools-expert` (n8n)
16. `n8n-node-configuration` (n8n)
17. `n8n-validation-expert` (n8n)
18. `n8n-workflow-patterns` (n8n)

**Skills globais (não específicas do projeto):**
- `skill-creator` — Criar e gerenciar skills
- `mcp-builder` — Criar MCP servers
- `keybindings-help` — Customizar atalhos do Claude Code
- `obsidian-life-os` — Sistema de gestão de vida no Obsidian
- `tech-docs-writer` — Criar PRDs, roadmaps, kanbans, ADRs

---

## 🧪 Evaluations (Testes Automatizados)

### n8n Agent — 32 evaluations

| Categoria | Quantidade | Localização |
|---|---|---|
| `code-javascript` | 5 evals | `agents/n8n/evaluations/code-javascript/` |
| `code-python` | 5 evals | `agents/n8n/evaluations/code-python/` |
| `expression-syntax` | 4 evals | `agents/n8n/evaluations/expression-syntax/` |
| `mcp-tools` | 5 evals | `agents/n8n/evaluations/mcp-tools/` |
| `node-configuration` | 4 evals | `agents/n8n/evaluations/node-configuration/` |
| `validation-expert` | 4 evals | `agents/n8n/evaluations/validation-expert/` |
| `workflow-patterns` | 5 evals | `agents/n8n/evaluations/workflow-patterns/` |

**Exemplos de evals:**
- `eval-001-webhook-body-gotcha.json` — Teste de acesso correto a dados de webhook
- `eval-002-nodetype-format.json` — Teste de formato correto de nodeType
- `eval-003-validation-workflow.json` — Teste de validação de workflow
- `eval-004-ai-agent.json` — Teste de criação de AI Agent workflow

---

## 💾 Memory Structure

### Padrão de memória por agente

Cada agente mantém memória em `agents/<nome>/memory/`:

| Agente | Arquivos de memória | Status |
|---|---|---|
| **designer** | `history.md`, `design-library.md` | ✅ Ativo |
| **linkedin** | `history.md`, `content-library.md` | ✅ Ativo |
| **n8n** | `history.md`, `snippets.md` | ✅ Ativo |
| **ai-pm** | `history.md` | ✅ Ativo |
| **process-manager** | `history.md` | ✅ Ativo |
| **education** | `history.md` | ✅ Ativo |
| **agent-manager** | (vazio) | ⚠️ Não inicializado |
| **data-analytics** | (vazio) | ⚠️ Não inicializado |

### Memória compartilhada

- `shared/memory/world.md` — Contexto global do sistema
- `shared/memory/handoff.md` — Protocolo de handoff entre agentes

---

## 🔄 Fluxos de Colaboração Comuns

### 1. LinkedIn Post com Imagem

```mermaid
LinkedIn Agent → escreve conteúdo
    ↓
Designer Agent → cria imagem
    ↓
LinkedIn Agent → finaliza post
```

### 2. Workflow n8n com Interface

```mermaid
n8n Agent → cria workflow
    ↓
Designer Agent → cria dashboard/interface
    ↓
n8n Agent → conecta workflow à interface
```

### 3. Projeto de IA Completo

```mermaid
AI PM Agent → define roadmap
    ↓
Process Manager → mapeia processos
    ↓
n8n Agent → automatiza processos
    ↓
Tech Docs Writer → documenta projeto (PRD, ADRs)
    ↓
LinkedIn Agent → comunica resultado
```

### 4. Novo Agente

```mermaid
Agent Manager → cria AGENT.md e skill YAML
    ↓
AI PM Agent → integra ao roadmap
    ↓
Tech Docs Writer → documenta decisão (ADR)
```

---

## ⚠️ Lacunas Identificadas

### 1. Data Analytics Agent
- ✅ AGENT.md criado
- ❌ Skill YAML não criada
- ❌ Memory não inicializada
- **Ação**: Criar skill YAML e inicializar memória

### 2. Agent Manager
- ✅ AGENT.md criado
- ⚠️ Usa slash command `/agent-manager` (não é skill YAML)
- ❌ Memory não inicializada
- **Ação**: Considerar migração para skill YAML

### 3. Tech Docs Writer
- ✅ Skill YAML existe (global, não específica do projeto)
- ❌ Sem AGENT.md no projeto
- ❌ Sem memória específica
- **Ação**: Criar AGENT.md e memória se necessário para contexto do projeto

### 4. Falta de scripts/tools customizados
- Não há pasta `scripts/` ou `tools/`
- Tudo está baseado em MCP tools e skills YAML
- **Ação**: Avaliar se seria útil criar scripts auxiliares

---

## 🎯 Próximos Passos Recomendados

1. **Completar Data Analytics Agent**
   - Criar `~/.claude/skills/data-analytics/SKILL.md`
   - Inicializar `agents/data-analytics/memory/history.md`
   - Definir sub-skills necessárias

2. **Documentar Tech Docs Writer no projeto**
   - Criar `agents/tech-docs-writer/AGENT.md`
   - Criar `agents/tech-docs-writer/memory/`
   - Mapear casos de uso específicos do projeto

3. **Criar evaluations para outros agentes**
   - Designer Agent (5-10 evals testando criação de diferentes artefatos)
   - LinkedIn Agent (5-10 evals testando diferentes formatos de post)
   - Process Manager (5-10 evals testando mapeamento de processos)

4. **Explorar criação de tools customizados**
   - Script para deploy automatizado de agentes
   - Tool para análise de performance de skills
   - Workflow n8n para monitoring de agentes

5. **Documentação de padrões de handoff**
   - Criar guia detalhado de quando e como fazer handoff entre agentes
   - Padronizar formato de `shared/memory/handoff.md`

---

## 📈 Métricas do Sistema

- **8 agentes** definidos (6 com skills YAML completas)
- **18+ skills** no Claude Code
- **2 MCP servers** configurados
- **32 evaluations** no n8n Agent
- **8 pastas de memória** (6 ativas)
- **100% dos agentes** usam o padrão AGENT.md
- **75% dos agentes** têm skills YAML funcionais

---

**Última atualização**: 2026-03-14
**Próxima revisão recomendada**: Quando novos agentes forem criados ou skills modificadas
