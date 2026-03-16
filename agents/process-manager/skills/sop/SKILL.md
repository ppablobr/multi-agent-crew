---
name: process-sop
description: >
  Sub-skill do Process Manager para criar SOPs (Standard Operating Procedures) — documentação
  formal e executável de processos. Use when creating step-by-step operational guides, procedure
  manuals, or documented standards that someone can follow independently.
  Examples: "create an SOP for onboarding", "document the release process", "write the procedure
  for handling customer escalations", "make a manual for X process".
  Typically invoked by the process-manager orchestrator skill, not directly.
---

# Sub-skill: SOP (Standard Operating Procedure)

## Quando usar
Processo já mapeado (ou bem conhecido) que precisa de documentação formal, executável por qualquer pessoa do time sem depender de conhecimento tácito.

---

## Processo

### 1. Coletar insumos
- **Processo:** Qual processo será documentado?
- **Já foi mapeado?** Há um AS-IS em `agents/process-manager/memory/processes.md`?
- **Público do SOP:** Quem vai seguir este documento? (novo colaborador, time operacional, etc.)
- **Nível de detalhe:** Precisa de prints/vídeos ou só texto é suficiente?
- **Frequência de revisão:** Com que frequência este SOP deve ser revisado?

### 2. Template de SOP

```markdown
# SOP: [Nome do Processo]
**Versão:** 1.0 | **Data:** YYYY-MM-DD
**Dono:** [Nome/Cargo responsável pelo processo]
**Revisão prevista:** [Data da próxima revisão]
**Aprovado por:** [Quem aprovou]

---

## Objetivo
[1-2 frases: o que este SOP permite fazer e qual o resultado esperado]

## Escopo
**Aplica-se a:** [Quem deve seguir este SOP]
**Não se aplica a:** [Exceções ou casos fora do escopo]

## Pré-requisitos
- [Acesso ou permissão necessária 1]
- [Ferramenta ou sistema necessário]
- [Conhecimento prévio necessário]

## Gatilho
[O que inicia este processo — evento, solicitação, schedule]

---

## Procedimento

### Etapa 1 — [Nome da etapa]
**Responsável:** [Cargo ou pessoa]
**Sistema:** [Ferramenta usada]
**Tempo estimado:** [X minutos]

**Instruções:**
1. [Ação específica]
2. [Ação específica]

**Critério de conclusão:** [Como saber que esta etapa está completa]
**Se algo der errado:** [O que fazer em caso de erro ou exceção]

---

### Etapa 2 — [Nome da etapa]
[repetir estrutura]

---

## Pontos de controle de qualidade
| Checkpoint | Quando | Como verificar |
|---|---|---|
| [Verificação 1] | [Após etapa X] | [Como checar] |

## Exceções e casos especiais
| Situação | O que fazer |
|---|---|
| [Exceção 1] | [Procedimento alternativo] |

## Glossário
| Termo | Definição |
|---|---|
| [Sigla/Termo] | [O que significa no contexto deste processo] |

## Histórico de versões
| Versão | Data | Autor | Mudança |
|---|---|---|---|
| 1.0 | YYYY-MM-DD | [Nome] | Versão inicial |
```

### 3. Revisão do SOP
- [ ] Qualquer pessoa do público-alvo consegue seguir sem ajuda?
- [ ] Todas as etapas têm responsável e sistema identificados?
- [ ] Os casos de exceção mais comuns estão documentados?
- [ ] Os checkpoints de qualidade estão claros?
- [ ] O glossário cobre todos os termos não-óbvios?
- [ ] A data de revisão foi definida?
