---
name: education-workshop
description: >
  Sub-skill do Education Agent para criar workshops e sessões ao vivo. Use when creating a
  single training session, mentoring session, or live workshop with slides, demos, and exercises.
  Examples: "prepare a workshop on prompt engineering", "create a 2-hour session on RAG",
  "design a mentoring session about AI agents", "build training for the product team".
  Typically invoked by the education orchestrator skill, not directly.
---

# Sub-skill: Workshop / Sessão ao Vivo

## Quando usar
Sessão educacional única para entrega presencial ou ao vivo: tem timing definido, slides, demo e exercício prático.
Duração típica: 60 a 120 minutos.

---

## Processo

### 1. Coletar insumos
- **Tema:** O que será ensinado na sessão?
- **Público:** Quem vai assistir? Nível de conhecimento?
- **Duração:** Quantos minutos?
- **Objetivo:** O que os participantes vão conseguir fazer depois?
- **Formato:** Apresentação + demo + exercício? Só discussão? Hands-on?
- **Ferramentas disponíveis:** O público tem acesso a quê (n8n, Claude, etc.)?

### 2. Estrutura de timing

Para sessões de **90 minutos** (adapte proporcionalmente):

| Bloco | Duração | Conteúdo |
|---|---|---|
| Abertura | 5 min | Objetivo da sessão, agenda, check de expectativas |
| Contexto | 10 min | Por que este tema importa? O que o público vai ganhar? |
| Teoria | 20 min | Conceitos centrais com exemplos reais |
| Demo ao vivo | 15 min | Demonstração prática do conceito principal |
| Exercício | 25 min | Prática guiada — o público faz, não só assiste |
| Revisão | 10 min | O que aprendemos? Perguntas abertas |
| Encerramento | 5 min | Próximos passos, recursos, onde tirar dúvidas |

### 3. Template de roteiro de workshop

```markdown
# Workshop: [Título]
**Data:** YYYY-MM-DD | **Duração:** [X min] | **Público:** [perfil]
**Objetivo:** Ao final, os participantes conseguirão [resultado verificável]

---

## Slides

### Slide 1 — Abertura
- Título da sessão
- Seu nome e contexto
- "Hoje vocês vão aprender a [objetivo]"

### Slide 2 — Agenda
- [Bloco 1] — X min
- [Bloco 2] — X min
- [Exercício] — X min

### Slides 3-N — Teoria
[Conteúdo central — um conceito por slide]

### Slide N+1 — Demo
"Agora vou mostrar ao vivo como isso funciona"
[Passo a passo da demo]

### Slide N+2 — Exercício
**Objetivo:** [O que o participante vai fazer]
**Tempo:** [X minutos]
**Instruções:** [Passo a passo]
**Resultado esperado:** [O que devem ter ao final]

---

## Script da demo ao vivo
[Passo a passo detalhado do que você vai fazer durante a demo, incluindo o que falar em cada momento]

---

## Exercício completo
**Objetivo:** [verbo de ação + resultado]
**Pré-requisitos:** [O que o participante precisa ter/saber]
**Instruções:**
1. [Passo 1]
2. [Passo 2]
**Output esperado:** [O que deve existir ao final]
**Solução completa:** [A solução correta para referência do facilitador]

---

## Perguntas para debate
- [Pergunta 1 — abre discussão]
- [Pergunta 2 — aprofunda reflexão]
```

### 4. Revisão
- [ ] O objetivo é verificável e alcançável no tempo disponível?
- [ ] O exercício tem solução completa documentada?
- [ ] O timing está realista (inclui 10% de buffer)?
- [ ] A demo pode ser refeita se der problema ao vivo?
- [ ] As perguntas de debate geram discussão genuína?
