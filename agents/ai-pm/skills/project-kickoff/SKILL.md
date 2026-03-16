---
name: ai-pm
description: >
  Use when the user asks to manage AI projects, create roadmaps, plan sprints, define project scope,
  track progress, or organize AI initiatives. Examples include "create a roadmap for X project",
  "plan the next sprint", "define success metrics for Y", "manage this AI initiative", "kickoff project Z",
  or any request involving project management, planning, OKRs, stakeholder management, or AI project
  strategy. Use this skill whenever the user mentions projects, roadmaps, sprints, planning, or
  AI/ML project management.
---

# Skill: AI PM — Orquestrador de Gestão de Projetos de IA

## Objetivo
Identificar o tipo de demanda de gestão de projeto e rotear para a sub-skill especializada correta.

---

## Processo

### 0. Carregar contexto (SEMPRE executar antes de qualquer outra coisa)

Antes de iniciar qualquer atividade, leia obrigatoriamente:

1. **`agents/ai-pm/memory/projects.md`** — projetos em andamento e encerrados. Verifique relacionamentos e dependências.
2. **`agents/ai-pm/memory/history.md`** — decisões tomadas, padrões de planejamento que funcionaram.
3. **`shared/memory/world.md`** — contexto global: prioridades atuais, projetos ativos, restrições conhecidas.

**Com base no que leu**, adapte:
- Se há projeto relacionado em andamento → proponha integração ao invés de projeto isolado
- Se há padrões de planejamento já validados → reutilize estrutura de fases/timeline
- Se o contexto global indica restrições → incorpore sem precisar perguntar

---

### 1. Identificar o tipo de demanda e rotear

| Situação | Sub-skill |
|---|---|
| Novo projeto de IA — estruturar escopo, stakeholders, riscos e timeline | **`ai-pm-kickoff`** |
| Projeto existente precisa de roadmap trimestral ou anual | **`ai-pm-roadmap`** |
| Time precisa planejar o próximo sprint ou ciclo de entrega | **`ai-pm-sprint`** |

**Se não ficou claro**, pergunte:
> "Você precisa estruturar um novo projeto (kickoff), criar um roadmap de médio/longo prazo, ou planejar o próximo sprint?"

---

### 2. Após executar a sub-skill — oferecer complementos

| Situação | Skill |
|---|---|
| Projeto precisa de PRD, kanban, ADR ou user stories | **`tech-docs-writer`** |
| Projeto envolve processos operacionais | **`process-manager`** |
| Projeto precisa de dashboard de KPIs visual | **`designer`** (sub-skill `frontend-design`) |
| Projeto envolve automações | **`n8n`** |
| Projeto é relevante para comunicação pública | **`linkedin`** |

---

### 3. Atualizar memória

Após qualquer entrega, registre em **`agents/ai-pm/memory/projects.md`**:

```markdown
## [Nome do Projeto] — Status: [Kickoff / Em andamento / Concluído]
**Atualizado em:** YYYY-MM-DD
- Problema: [resumo]
- KPI principal: [métrica → meta]
- Fase atual: [fase]
- Próximos passos: [ações]
```
