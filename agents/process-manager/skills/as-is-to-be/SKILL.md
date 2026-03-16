---
name: process-map
description: >
  Sub-skill do Process Manager para mapear processos AS-IS e propor melhorias TO-BE.
  Use when analyzing how a process currently works, identifying bottlenecks, and designing improvements.
  Examples: "map our onboarding process", "analyze the current sales flow", "identify automation
  opportunities in X process", "what can we improve in Y workflow".
  Typically invoked by the process-manager orchestrator skill, not directly.
---

# Sub-skill: Mapeamento AS-IS e TO-BE

## Quando usar
Entender como um processo funciona hoje, identificar gargalos e propor versão melhorada com automações.

---

## Processo

### 1. Entender o processo (pergunte se não souber)
- **Nome do processo:** Como ele é chamado?
- **Objetivo:** Para que serve? Qual o resultado final?
- **Frequência:** Com que frequência acontece?
- **Volume:** Quantas instâncias por semana/mês?
- **Participantes:** Quem faz o quê?
- **Sistemas envolvidos:** Quais ferramentas são usadas?
- **Problemas atuais:** O que incomoda? O que atrasa?

### 2. Mapear AS-IS

```markdown
# Processo: [Nome]
**Versão AS-IS** | Data: YYYY-MM-DD
**Dono do processo:** [Nome/Cargo]
**Frequência:** [Diário / Semanal / Mensal / Por demanda]

## Objetivo
[O que este processo alcança]

## Participantes
- [Pessoa/Cargo A]: [Papel no processo]

## Gatilho
[O que inicia este processo]

## Etapas
| # | Atividade | Quem | Sistema | Tempo médio | Notas |
|---|---|---|---|---|---|
| 1 | [Atividade] | [Pessoa] | [Sistema] | [X min] | |

## Saída / Resultado
[O que é produzido ao final]

## Métricas atuais
- Tempo total médio: [X horas]
- Taxa de erro: [X%]

## Problemas identificados
1. [Problema 1] — impacto: Alto / Médio / Baixo
```

### 3. Criar diagrama visual

**OBRIGATÓRIO**: Use a skill **`excalidraw-diagram`** para criar o fluxograma visual do AS-IS. O diagrama é o entregável principal — o mapeamento em texto é apenas o rascunho.

### 4. Analisar oportunidades de automação

| Etapa | Manual? | Repetitiva? | Regras claras? | Pode automatizar? |
|---|---|---|---|---|
| [Etapa 1] | Sim | Sim | Sim | ✅ Alta prioridade |
| [Etapa 2] | Sim | Não | Não | ❌ Requer julgamento |

**Critérios:**
- ✅ Alta prioridade: manual + repetitiva + regras claras
- 🟡 Média: manual + repetitiva + regras parciais
- ❌ Não automatizar: requer julgamento humano

### 5. Propor TO-BE

- Etapas eliminadas ou simplificadas
- Etapas automatizadas (referencie workflows n8n existentes se houver)
- Responsabilidades redistribuídas
- Novos pontos de controle de qualidade

### 6. Calcular impacto

```
Tempo economizado = (Tempo AS-IS - Tempo TO-BE) × Frequência mensal
Exemplo: (4h - 0.5h) × 20 instâncias = 70h economizadas/mês
```

### 7. Checklist de qualidade
- [ ] Todas as etapas têm responsável claro?
- [ ] Os sistemas foram identificados em cada etapa?
- [ ] Os tempos médios são realistas?
- [ ] Os problemas foram validados com quem executa?
- [ ] O diagrama visual foi criado com `excalidraw-diagram`?
- [ ] O impacto das melhorias foi calculado?
