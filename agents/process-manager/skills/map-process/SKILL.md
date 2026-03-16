---
name: process-manager
description: >
  Use when the user asks to map processes, create process documentation, design workflows, create SOPs,
  improve business processes, or visualize operational flows. Examples include "document this process",
  "map the AS-IS flow for X", "create an SOP for Y", "improve our Z process", or any request involving
  process mapping, documentation, optimization, flowcharts, or operational procedures. Use this skill
  whenever the user mentions processes, SOPs, documentation, flowcharts, or process improvement.
---

# Skill: Process Manager — Orquestrador de Processos

## Objetivo
Identificar o tipo de demanda de processo e rotear para a sub-skill especializada correta.

---

## Processo

### 0. Carregar contexto (SEMPRE executar antes de qualquer outra coisa)

Antes de qualquer atividade, leia obrigatoriamente:

1. **`agents/process-manager/memory/processes.md`** — processos já mapeados. Evite retrabalho.
2. **`agents/process-manager/memory/patterns.md`** — padrões de automação já identificados.
3. **`agents/n8n/memory/history.md`** — workflows criados que podem estar automatizando etapas do processo.
4. **`shared/memory/world.md`** — contexto global: sistemas disponíveis, integrações ativas.

---

### 1. Identificar o tipo de demanda e rotear

| Situação | Sub-skill |
|---|---|
| Mapear como um processo funciona hoje (AS-IS) e propor melhorias (TO-BE) | **`process-map`** |
| Criar documentação formal e executável de um processo (SOP) | **`process-sop`** |

**Se não ficou claro**, pergunte:
> "Você precisa entender e melhorar como o processo funciona (mapeamento), ou criar um documento formal que alguém possa seguir passo-a-passo (SOP)?"

---

### 2. Após executar a sub-skill — oferecer complementos

| Situação | Skill |
|---|---|
| Etapas identificadas como automatizáveis | **`n8n`** → criar workflow para automatizar |
| Processo precisa de documentação formal para além do SOP | **`tech-docs-writer`** |
| Processo faz parte de projeto maior | **`ai-pm`** → integrar ao roadmap |
| Processo é case relevante de transformação digital | **`linkedin`** → criar post sobre o resultado |

---

### 3. Atualizar memória

Após qualquer mapeamento ou SOP, registre em **`agents/process-manager/memory/processes.md`**:

```markdown
## [Nome do Processo] — [AS-IS / TO-BE / SOP]
**Atualizado em:** YYYY-MM-DD
- Dono: [responsável]
- Frequência: [diário/semanal/mensal]
- Status: [Mapeado / Automatizado / Documentado]
- Arquivo: [onde está a documentação completa]
```
