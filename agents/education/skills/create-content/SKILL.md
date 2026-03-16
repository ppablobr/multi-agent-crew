---
name: education
description: >
  Use when the user asks to create educational materials, learning content, training programs,
  mentoring sessions, workshops, or teach AI/automation concepts. Examples include "create a learning
  path for X", "prepare a workshop about Y", "design training for Z", "explain prompt engineering",
  "teach how to build agents", "create exercises for N", or any request involving teaching, learning
  trails, exercises, educational content, onboarding, or skill development in AI, LLMs, automation,
  or n8n. Use this skill whenever the user mentions education, learning, training, teaching,
  workshops, or mentoring.
---

# Skill: Education — Orquestrador de Conteúdo Educacional

## Objetivo
Identificar o formato de conteúdo educacional mais adequado e rotear para a sub-skill especializada.

---

## Processo

### 0. Carregar contexto (SEMPRE executar antes de qualquer outra coisa)

Antes de criar qualquer conteúdo, leia obrigatoriamente:

1. **`agents/education/memory/history.md`** — materiais já criados. Evite duplicação e construa sobre o que existe.
2. **`agents/education/memory/content-library.md`** — biblioteca de conteúdo reutilizável: exercícios, slides, exemplos.
3. **`agents/education/memory/learner-feedback.md`** — feedbacks recebidos. Aplique melhorias já identificadas.
4. **`agents/n8n/memory/history.md`** — workflows existentes que podem ser usados como exemplos práticos.

---

### 1. Identificar o tipo de conteúdo e rotear

| Situação | Sub-skill |
|---|---|
| Programa estruturado de aprendizado (4-8 semanas, múltiplos módulos) | **`education-trail`** |
| Sessão presencial ou ao vivo (90-120 min, slides + demo + exercício) | **`education-workshop`** |
| Atividade prática isolada com objetivo específico | **`education-exercise`** |

**Se não ficou claro**, pergunte:
> "Você precisa de uma trilha de aprendizado completa, uma sessão/workshop para entregar ao vivo, ou um exercício prático isolado?"

---

### 2. Após executar a sub-skill — oferecer complementos

| Situação | Skill |
|---|---|
| Material precisa de diagrama ou visual de arquitetura | **`designer`** |
| Criar carrossel educativo para LinkedIn sobre o tema | **`linkedin-carousel`** → depois **`designer`** |
| Material usa workflows n8n como exemplo | **`n8n`** → criar workflow real para o exercício |
| Programa educacional faz parte de projeto maior | **`ai-pm`** → integrar ao roadmap |
| Processo de educação precisa de documentação formal | **`tech-docs-writer`** |

---

### 3. Atualizar memória

Após entregar qualquer material, registre em **`agents/education/memory/history.md`**:

```markdown
## YYYY-MM-DD — [Título do material]
- **Formato:** Trilha / Workshop / Exercício
- **Público:** [nível e perfil]
- **Tópicos:** [lista de tópicos cobertos]
- **Feedback:** (preencher após entrega)
```

E adicione conteúdo reutilizável em **`agents/education/memory/content-library.md`**.
