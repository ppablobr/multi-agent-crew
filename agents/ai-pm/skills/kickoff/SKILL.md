---
name: ai-pm-kickoff
description: >
  Sub-skill do AI PM para estruturar o kickoff de um novo projeto de IA. Use when starting a new
  AI project from scratch: defining scope, stakeholders, success metrics, risks, and timeline.
  Examples: "kickoff project X", "structure this new AI initiative", "create a project brief for Y".
  Typically invoked by the ai-pm orchestrator skill, not directly.
---

# Sub-skill: Project Kickoff de IA

## Quando usar
Novo projeto de IA que precisa ser estruturado do zero: problema, escopo, stakeholders, riscos e plano de execução.

---

## Processo

### 1. Discovery — entender o problema (pergunte tudo que não souber)
- **Problema de negócio:** O que estamos tentando resolver?
- **Impacto esperado:** KPI que vai melhorar? Quanto?
- **Stakeholders:** Quem patrocina? Quem usa? Quem aprova?
- **Dados disponíveis:** Quais dados existem? Onde estão? Qual qualidade?
- **Prazo:** Tem deadline? É hard ou soft?
- **Restrições:** Budget, tecnologia, compliance?

### 2. Gerar o Project Brief

```markdown
# Project Brief: [Nome do Projeto]
**Data:** YYYY-MM-DD
**Status:** Kickoff

## Problema
[1-2 frases descrevendo o problema de negócio]

## Solução proposta
[1-2 frases descrevendo a abordagem de IA]

## Impacto esperado
- KPI primário: [métrica] → de [X] para [Y] em [Z meses]
- KPI secundário: [métrica]

## Stakeholders
| Nome | Papel | Responsabilidade |
|---|---|---|
| [Nome] | Sponsor | Aprova budget e direção |
| [Nome] | Product Owner | Define prioridades |
| [Nome] | Tech Lead | Decisões técnicas |

## Escopo
### IN (incluso)
- [Item 1]

### OUT (não incluso)
- [Item 1]

## Fases e timeline
| Fase | Duração | Entregável |
|---|---|---|
| Discovery | 2 semanas | Problem statement validado |
| Prototipagem | 3 semanas | PoC funcional |
| Desenvolvimento | 8 semanas | MVP em produção |
| Lançamento | 2 semanas | Rollout completo |

## Riscos identificados
| Risco | Probabilidade | Impacto | Mitigação |
|---|---|---|---|
| Qualidade dos dados insuficiente | Alta | Alto | Auditoria de dados na semana 1 |
| Mudança de escopo | Média | Médio | Change request process |

## Critérios de sucesso
- [ ] [Critério 1 — mensurável]
- [ ] [Critério 2 — mensurável]

## Próximos passos (próximas 2 semanas)
1. [Ação] — [Responsável] — [Prazo]
```

### 3. Checklist de kickoff completo
- [ ] Problema de negócio definido e validado com stakeholder
- [ ] KPIs de sucesso definidos e mensuráveis
- [ ] Dados disponíveis mapeados
- [ ] Riscos principais identificados
- [ ] Timeline realista (inclui margem de 20% para imprevistos)
- [ ] Próximos passos claros com responsáveis
- [ ] Project Brief aprovado pelo sponsor
