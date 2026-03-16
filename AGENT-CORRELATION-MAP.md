# 🗺️ Mapa de Correlação — Multi-Agent Crew

> Visualização da arquitetura e interdependências do sistema

---

## 📊 Diagrama de Camadas

```
┌─────────────────────────────────────────────────────────────────┐
│                     🧠 ORQUESTRADOR (CLAUDE.md)                  │
│                                                                 │
│  Identifica intenção → Roteia para agente → Coordena handoffs  │
└─────────────────────────────────────────────────────────────────┘
                                ▼
┌─────────────────────────────────────────────────────────────────┐
│                    🤖 CAMADA DE AGENTES                          │
│                                                                 │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐             │
│  │  Designer   │  │  LinkedIn   │  │    n8n      │             │
│  │   Agent     │  │   Agent     │  │   Agent     │             │
│  └─────────────┘  └─────────────┘  └─────────────┘             │
│                                                                 │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐             │
│  │   AI PM     │  │  Process    │  │ Education   │             │
│  │   Agent     │  │   Manager   │  │   Agent     │             │
│  └─────────────┘  └─────────────┘  └─────────────┘             │
│                                                                 │
│  ┌─────────────┐  ┌─────────────┐                              │
│  │   Agent     │  │    Data     │                              │
│  │  Manager    │  │  Analytics  │ ⚠️ Sem skill YAML            │
│  └─────────────┘  └─────────────┘                              │
└─────────────────────────────────────────────────────────────────┘
                                ▼
┌─────────────────────────────────────────────────────────────────┐
│                    ⚙️ CAMADA DE SKILLS YAML                      │
│                                                                 │
│  Skills principais (auto-invocadas pelo Claude Code):          │
│  • designer                                                     │
│  • linkedin                                                     │
│  • n8n                                                          │
│  • ai-pm                                                        │
│  • process-manager                                              │
│  • education                                                    │
│                                                                 │
│  Skills globais:                                                │
│  • tech-docs-writer (PRDs, roadmaps, kanbans)                   │
│  • skill-creator (criar/modificar skills)                       │
│  • mcp-builder (criar MCP servers)                              │
└─────────────────────────────────────────────────────────────────┘
                                ▼
┌─────────────────────────────────────────────────────────────────┐
│                   🔧 CAMADA DE SUB-SKILLS                        │
│                                                                 │
│  Designer Agent:                                                │
│  ├─ canvas-design (arte estática)                               │
│  ├─ frontend-design (interfaces web)                            │
│  ├─ theme-factory (temas visuais)                               │
│  ├─ web-artifacts-builder (React complexo)                      │
│  └─ excalidraw-diagram (diagramas)                              │
│                                                                 │
│  n8n Agent:                                                     │
│  ├─ n8n-code-javascript (Code nodes JS)                         │
│  ├─ n8n-code-python (Code nodes Python)                         │
│  ├─ n8n-expression-syntax (expressões n8n)                      │
│  ├─ n8n-mcp-tools-expert (guia de MCP tools)                    │
│  ├─ n8n-node-configuration (config de nodes)                    │
│  ├─ n8n-validation-expert (validação)                           │
│  └─ n8n-workflow-patterns (padrões arquiteturais)               │
└─────────────────────────────────────────────────────────────────┘
                                ▼
┌─────────────────────────────────────────────────────────────────┐
│                    🔌 CAMADA DE MCP TOOLS                        │
│                                                                 │
│  n8n-mcp (https://your-n8n-instance.example.com)                              │
│  ├─ n8n_create_workflow                                         │
│  ├─ n8n_update_partial_workflow                                 │
│  ├─ n8n_validate_workflow                                       │
│  ├─ n8n_test_workflow                                           │
│  ├─ n8n_deploy_template                                         │
│  ├─ search_nodes / get_node                                     │
│  └─ search_templates / n8n_list_workflows                       │
│                                                                 │
│  github                                                         │
│  ├─ create_or_update_file                                       │
│  ├─ create_issue / create_pull_request                          │
│  └─ push_files                                                  │
└─────────────────────────────────────────────────────────────────┘
                                ▼
┌─────────────────────────────────────────────────────────────────┐
│                     💾 CAMADA DE MEMÓRIA                         │
│                                                                 │
│  Memória por agente (agents/<nome>/memory/):                    │
│  • history.md — log cronológico de ações                        │
│  • <specific>.md — arquivos específicos (design-library, etc)   │
│                                                                 │
│  Memória compartilhada (shared/memory/):                        │
│  • world.md — contexto global do sistema                        │
│  • handoff.md — protocolo de handoff entre agentes              │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🔗 Matriz de Interdependências

### Quem usa quem?

| Agente Origem | Invoca | Para |
|---|---|---|
| **LinkedIn Agent** | Designer Agent | Criar imagens para posts |
| **LinkedIn Agent** | n8n Agent | Criar workflows de agendamento |
| **n8n Agent** | Designer Agent | Criar dashboards para workflows |
| **n8n Agent** | Process Manager | Entender processo antes de automatizar |
| **AI PM Agent** | Designer Agent | Criar dashboards de KPIs |
| **AI PM Agent** | Tech Docs Writer | Criar PRDs e roadmaps |
| **Process Manager** | Designer Agent | Criar diagramas visuais de processos |
| **Process Manager** | n8n Agent | Automatizar processos mapeados |
| **Process Manager** | Tech Docs Writer | Documentar SOPs |
| **Education Agent** | Designer Agent | Criar slides e materiais visuais |
| **Agent Manager** | skill-creator | Criar novas skills |
| **Agent Manager** | AI PM Agent | Integrar novo agente ao roadmap |
| **Todos** | github MCP | Versionamento e colaboração |

---

## 🎯 Fluxos de Trabalho por Tipo de Tarefa

### 📱 Criar Post para LinkedIn

```
Usuário: "Cria um post sobre automação com n8n"
    ↓
LinkedIn Agent (skill auto-invocada)
    ├─ Escreve conteúdo do post
    ├─ Consulta n8n Agent (se precisa de detalhes técnicos)
    └─ Chama Designer Agent
           └─ Designer Agent invoca canvas-design
                  └─ Cria imagem
    ↓
LinkedIn Agent finaliza e entrega post + imagem
    ↓
Atualiza agents/linkedin/memory/history.md
```

### ⚙️ Criar Workflow n8n

```
Usuário: "Cria um workflow para sincronizar leads do CRM com Slack"
    ↓
n8n Agent (skill auto-invocada)
    ├─ Clarifica requisitos
    ├─ Consulta n8n-mcp-tools-expert (qual tool MCP usar)
    ├─ Consulta n8n-workflow-patterns (qual padrão arquitetural)
    └─ Usa n8n-mcp tools:
           ├─ search_nodes (busca nodes necessários)
           ├─ n8n_create_workflow (cria o workflow)
           ├─ n8n_validate_workflow (valida)
           └─ n8n_test_workflow (testa)
    ↓
n8n Agent entrega URL do workflow
    ↓
Atualiza agents/n8n/memory/history.md
```

### 📊 Criar Dashboard de Projeto

```
Usuário: "Cria um dashboard para acompanhar KPIs do projeto X"
    ↓
AI PM Agent (skill auto-invocada)
    ├─ Define métricas e KPIs
    ├─ Estrutura layout do dashboard
    └─ Chama Designer Agent
           └─ Designer Agent invoca frontend-design
                  ├─ Cria interface com React/Tailwind
                  └─ Integra com dados (via n8n workflow se necessário)
    ↓
AI PM Agent entrega dashboard
    ↓
Atualiza agents/ai-pm/memory/history.md
```

### 📝 Documentar Projeto com PRD

```
Usuário: "Preciso de um PRD para a feature de autenticação SSO"
    ↓
Tech Docs Writer (skill auto-invocada)
    ├─ Consulta AI PM Agent (contexto do projeto, roadmap)
    ├─ Cria estrutura do PRD
    │     ├─ Contexto e objetivo
    │     ├─ Requisitos funcionais
    │     ├─ Requisitos não-funcionais
    │     ├─ User stories
    │     ├─ Critérios de aceitação
    │     ├─ Estimativas e timeline
    │     └─ Riscos e mitigações
    └─ Entrega PRD completo
    ↓
Salva em docs/ ou repositório apropriado
```

### 🔄 Mapear e Automatizar Processo

```
Usuário: "Preciso mapear e automatizar o processo de onboarding de clientes"
    ↓
Process Manager (skill auto-invocada)
    ├─ Mapeia processo (AS-IS)
    ├─ Identifica gargalos
    ├─ Propõe melhorias (TO-BE)
    └─ Chama Designer Agent
           └─ Designer Agent invoca excalidraw-diagram
                  └─ Cria diagrama visual do processo
    ↓
Process Manager consulta n8n Agent
    ├─ n8n Agent cria workflow de automação
    └─ n8n Agent testa e valida
    ↓
Process Manager consulta Tech Docs Writer
    └─ Tech Docs Writer documenta SOP
    ↓
Entrega: Diagrama + Workflow + SOP
    ↓
Atualiza agents/process-manager/memory/history.md
```

### 🤖 Criar Novo Agente

```
Usuário: "Quero criar um agente para análise de sentimento"
    ↓
Agent Manager (invocado via /agent-manager)
    ├─ Define especialização do agente
    ├─ Cria AGENT.md em agents/sentiment-analysis/
    ├─ Invoca skill-creator
    │     └─ Cria SKILL.md em ~/.claude/skills/sentiment-analysis/
    ├─ Inicializa memory/ folder
    └─ Atualiza CLAUDE.md com novo agente
    ↓
Consulta AI PM Agent (integrar ao roadmap?)
    ↓
Consulta Tech Docs Writer (criar ADR da decisão?)
    ↓
Entrega agente funcional
```

---

## 🧪 Cobertura de Evaluations

### n8n Agent — 100% coberto (32 evals)

| Sub-skill | Evals | Cobertura |
|---|---|---|
| n8n-code-javascript | 5 | ✅ Alta |
| n8n-code-python | 5 | ✅ Alta |
| n8n-expression-syntax | 4 | ✅ Alta |
| n8n-mcp-tools | 5 | ✅ Alta |
| n8n-node-configuration | 4 | ✅ Alta |
| n8n-validation-expert | 4 | ✅ Alta |
| n8n-workflow-patterns | 5 | ✅ Alta |

### Demais agentes — 0% cobertos

| Agente | Evals | Status |
|---|---|---|
| Designer Agent | 0 | ❌ Sem evaluations |
| LinkedIn Agent | 0 | ❌ Sem evaluations |
| AI PM Agent | 0 | ❌ Sem evaluations |
| Process Manager | 0 | ❌ Sem evaluations |
| Education Agent | 0 | ❌ Sem evaluations |

**Recomendação**: Criar evaluations para validar qualidade de outputs dos agentes

---

## 📦 Estrutura de Arquivos do Projeto

```
multi-agent-crew/
├── CLAUDE.md                    # Instruções do orquestrador
├── ARCHITECTURE.md              # Este documento
├── AGENT-CORRELATION-MAP.md     # Mapa visual (este arquivo)
├── .mcp.json                    # Configuração MCP servers
│
├── agents/
│   ├── designer/
│   │   ├── AGENT.md            # Persona e regras
│   │   └── memory/
│   │       ├── history.md
│   │       └── design-library.md
│   │
│   ├── linkedin/
│   │   ├── AGENT.md
│   │   └── memory/
│   │       ├── history.md
│   │       └── content-library.md
│   │
│   ├── n8n/
│   │   ├── AGENT.md
│   │   ├── memory/
│   │   │   ├── history.md
│   │   │   └── snippets.md
│   │   └── evaluations/
│   │       ├── code-javascript/    (5 evals)
│   │       ├── code-python/        (5 evals)
│   │       ├── expression-syntax/  (4 evals)
│   │       ├── mcp-tools/          (5 evals)
│   │       ├── node-configuration/ (4 evals)
│   │       ├── validation-expert/  (4 evals)
│   │       └── workflow-patterns/  (5 evals)
│   │
│   ├── ai-pm/
│   │   ├── AGENT.md
│   │   └── memory/
│   │       └── history.md
│   │
│   ├── process-manager/
│   │   ├── AGENT.md
│   │   └── memory/
│   │       └── history.md
│   │
│   ├── education/
│   │   ├── AGENT.md
│   │   └── memory/
│   │       └── history.md
│   │
│   ├── agent-manager/
│   │   ├── AGENT.md
│   │   └── memory/              ⚠️ vazio
│   │
│   └── data-analytics/
│       ├── AGENT.md
│       └── memory/              ⚠️ vazio
│
└── shared/
    └── memory/
        ├── world.md            # Contexto global
        └── handoff.md          # Protocolo de handoff
```

### Skills YAML (fora do projeto, no Claude Code)

```
~/.claude/skills/
├── designer/
│   ├── SKILL.md
│   └── evals/
│
├── linkedin/
│   ├── SKILL.md
│   └── evals/
│
├── n8n/
│   ├── SKILL.md
│   ├── memory/
│   └── evals/
│
├── ai-pm/
│   ├── SKILL.md
│   └── evals/
│
├── process-manager/
│   ├── SKILL.md
│   └── evals/
│
├── education/
│   ├── SKILL.md
│   └── evals/
│
├── canvas-design/           (sub-skill)
├── frontend-design/         (sub-skill)
├── theme-factory/           (sub-skill)
├── web-artifacts-builder/   (sub-skill)
├── excalidraw-diagram/      (sub-skill)
│
├── n8n-code-javascript/     (sub-skill)
├── n8n-code-python/         (sub-skill)
├── n8n-expression-syntax/   (sub-skill)
├── n8n-mcp-tools-expert/    (sub-skill)
├── n8n-node-configuration/  (sub-skill)
├── n8n-validation-expert/   (sub-skill)
├── n8n-workflow-patterns/   (sub-skill)
│
├── tech-docs-writer/        (skill global)
├── skill-creator/           (skill global)
└── mcp-builder/             (skill global)
```

---

## 🎯 Checklist de Saúde do Sistema

### ✅ Completo e funcional
- [x] 6 agentes com AGENT.md + SKILL.md + memory ativa
- [x] MCP server n8n-mcp configurado e funcional
- [x] MCP server github configurado
- [x] n8n Agent com 32 evaluations
- [x] Sistema de handoff entre agentes funcional
- [x] Memória compartilhada (world.md, handoff.md)

### ⚠️ Parcialmente implementado
- [ ] Data Analytics Agent (tem AGENT.md, falta skill YAML)
- [ ] Agent Manager (tem AGENT.md, usa slash command ao invés de skill YAML)
- [ ] Tech Docs Writer (skill global existe, falta AGENT.md no projeto)

### ❌ Faltando
- [ ] Evaluations para Designer, LinkedIn, AI PM, Process Manager, Education
- [ ] Scripts/tools customizados (pasta scripts/ ou tools/)
- [ ] Documentação de padrões de handoff detalhada
- [ ] Métricas de performance de agentes

---

## 📈 Estatísticas do Sistema

- **Agentes definidos**: 8
- **Agentes com skills YAML**: 6 (75%)
- **Skills totais no Claude Code**: 18+
- **Sub-skills por agente**:
  - Designer: 5
  - n8n: 7
  - Outros: 0
- **MCP servers**: 2
- **Evaluations**: 32 (apenas n8n Agent)
- **Memória ativa**: 6/8 agentes (75%)

---

**Última atualização**: 2026-03-14
