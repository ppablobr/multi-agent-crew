---
name: ai-pm-sprint
description: >
  Sub-skill do AI PM para planejamento de sprints e ciclos de entrega. Use when a team needs to
  plan the next sprint, prioritize backlog items, define sprint goals, or structure a delivery cycle.
  Examples: "plan the next sprint", "what should we work on this week", "prioritize our backlog",
  "create the sprint 12 planning", "define sprint goal for next cycle".
  Typically invoked by the ai-pm orchestrator skill, not directly.
---

# Sub-skill: Sprint Planning

## Quando usar
Time precisa planejar o próximo ciclo de entrega: priorizar itens, definir meta do sprint e distribuir capacidade.

---

## Processo

### 1. Coletar insumos
- **Sprint número/nome:** Qual é este sprint?
- **Duração:** 1 semana, 2 semanas?
- **Capacidade do time:** Quantas pessoas? Quantos dias úteis disponíveis?
- **Backlog disponível:** Quais itens estão prontos para entrar?
- **Meta do ciclo anterior:** O que ficou pendente?

### 2. Definir a meta do sprint

A meta do sprint deve ser:
- **Uma frase** que descreve o resultado esperado (não uma lista de tarefas)
- **Verificável** — é possível dizer claramente se foi alcançada ou não
- **Orientada a valor** — foca no impacto, não na atividade

**Exemplo:**
> ❌ "Implementar features A, B e C"
> ✅ "Usuário consegue completar o fluxo de onboarding sem intervenção manual"

### 3. Priorizar o backlog com MoSCoW

| Prioridade | Critério |
|---|---|
| **Must** | Bloqueia outras tarefas ou é crítico para a meta do sprint |
| **Should** | Importante, mas não bloqueia — entra se couber |
| **Could** | Desejável, entra só se sobrar capacidade |
| **Won't** | Explicitamente fora deste sprint |

### 4. Template de sprint planning

```markdown
# Sprint [N] — Planning
**Período:** DD/MM a DD/MM/YYYY
**Meta:** [Uma frase descrevendo o resultado esperado]

## Capacidade
- Time: [N pessoas]
- Dias úteis: [N dias]
- Capacidade estimada: [N story points ou N horas]

## Itens do sprint

### 🔴 Must (bloqueantes / críticos)
- [ ] [Item 1] — [Responsável] — [Estimativa]
- [ ] [Item 2] — [Responsável] — [Estimativa]

### 🟡 Should (importantes)
- [ ] [Item 3] — [Responsável] — [Estimativa]

### 🟢 Could (se couber)
- [ ] [Item 4] — [Responsável] — [Estimativa]

## Riscos e impedimentos conhecidos
- [Risco 1]: [Plano de mitigação]

## Definição de pronto (DoD)
- [ ] [Critério 1]
- [ ] [Critério 2]

## Retrospectiva do sprint anterior
- ✅ O que funcionou bem:
- ⚠️ O que precisamos melhorar:
- 🎯 Uma ação concreta para este sprint:
```

### 5. Checklist de sprint planning completo
- [ ] Meta do sprint definida em uma frase verificável?
- [ ] Itens priorizados com MoSCoW?
- [ ] Capacidade do time considerada?
- [ ] Responsáveis definidos para cada item Must?
- [ ] Impedimentos conhecidos mapeados?
- [ ] Definição de pronto acordada?
