---
name: ai-pm-roadmap
description: >
  Sub-skill do AI PM para criar roadmaps de projetos de IA. Use when a project needs a quarterly
  or annual roadmap, milestone planning, or a visual timeline of deliverables.
  Examples: "create a roadmap for Q2", "plan the next 6 months of project X", "build a roadmap for our AI initiative".
  Typically invoked by the ai-pm orchestrator skill, not directly.
---

# Sub-skill: Roadmap de Projeto de IA

## Quando usar
Projeto existente ou iniciativa de IA que precisa de planejamento de médio/longo prazo com milestones, fases e entregáveis.

---

## Processo

### 1. Entender o horizonte e contexto
- **Projeto:** Qual projeto ou iniciativa?
- **Horizonte:** Trimestral (Q), semestral ou anual?
- **Estado atual:** O que já foi feito? Onde estamos?
- **Objetivo final:** O que define o sucesso ao fim do roadmap?
- **Restrições:** Budget, headcount, dependências técnicas?

### 2. Estruturar em fases

Organize o roadmap em fases com:
- **Nome da fase** (ex: "Foundation", "PoC", "Scale")
- **Duração estimada**
- **Objetivo principal** da fase
- **Entregáveis concretos**
- **Critério de conclusão** (o que define que a fase está pronta)

### 3. Template de roadmap

```markdown
# Roadmap: [Nome do Projeto]
**Horizonte:** [Q1 2026 — Q2 2026 / Semestre 1 2026 / etc.]
**Última atualização:** YYYY-MM-DD

## Visão geral

| Fase | Período | Objetivo | Status |
|---|---|---|---|
| 🔵 Foundation | Jan–Fev | Infraestrutura e dados | ✅ Concluído |
| 🟡 PoC | Mar–Abr | Validar hipótese central | 🔄 Em andamento |
| 🟠 MVP | Mai–Jun | Primeiro usuário real | ⬜ Planejado |
| 🟢 Scale | Jul–Set | Expansão para 100% dos usuários | ⬜ Planejado |

---

## Fase 1 — Foundation (Jan–Fev)
**Objetivo:** [objetivo]

### Entregáveis
- [ ] [Entregável 1] — [Responsável] — [Prazo]
- [ ] [Entregável 2] — [Responsável] — [Prazo]

### Critério de conclusão
[O que define que essa fase está 100% pronta]

### Riscos desta fase
- [Risco 1]: [Mitigação]

---

## Fase 2 — [Nome] ([Período])
[repetir estrutura acima]

---

## Dependências críticas
| Item | Depende de | Impacto se atrasado |
|---|---|---|
| [Entregável X] | [Time/Sistema Y] | [Consequência] |

## KPIs do roadmap
| Métrica | Baseline | Meta Q2 | Meta Q4 |
|---|---|---|---|
| [KPI 1] | [valor atual] | [meta Q2] | [meta Q4] |
```

### 4. Checklist de roadmap completo
- [ ] Fases têm objetivos claros e mensuráveis?
- [ ] Cada entregável tem responsável e prazo?
- [ ] Dependências críticas foram mapeadas?
- [ ] Há margem de buffer (pelo menos 20%) no timeline?
- [ ] KPIs de sucesso definidos para cada fase?
- [ ] Riscos identificados com mitigação?
