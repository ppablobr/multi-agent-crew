---
name: education-trail
description: >
  Sub-skill do Education Agent para criar trilhas de aprendizado estruturadas. Use when creating
  multi-week learning programs, onboarding paths, or skill development curricula.
  Examples: "create a 4-week trail on AI agents", "design an onboarding program for the team",
  "build a learning path for prompt engineering".
  Typically invoked by the education orchestrator skill, not directly.
---

# Sub-skill: Trilha de Aprendizado

## Quando usar
Programa estruturado de aprendizado com múltiplos módulos, progressão clara e objetivos por semana.
Ideal para onboarding, desenvolvimento de habilidades ou capacitação de times.

---

## Processo

### 1. Coletar insumos
- **Tema:** O que será ensinado?
- **Público:** Quem são os aprendizes? (iniciante / intermediário / avançado)
- **Objetivo final:** O que eles conseguirão fazer ao terminar?
- **Duração:** Quantas semanas? Quantas horas por semana?
- **Formato de entrega:** Assíncrono (self-paced) ou síncrono (sessões ao vivo)?
- **Pré-requisitos:** O que precisam saber antes de começar?

### 2. Estrutura da trilha

**Princípios:**
- Progressão lógica: cada semana prepara a próxima
- Balanceamento: 40% teoria + 60% prática
- Cada semana tem um objetivo verificável
- Incluir checkpoints de avaliação (quiz, exercício, projeto)

### 3. Template de trilha

```markdown
# Trilha: [Nome da Trilha]
**Duração:** [N semanas] | **Nível:** [Iniciante / Intermediário / Avançado]
**Objetivo final:** [O que o aprendiz conseguirá fazer ao concluir]
**Pré-requisitos:** [O que precisa saber antes]

---

## Semana 1 — [Título]
**Objetivo:** Ao final desta semana, o aprendiz conseguirá [verbo de ação + resultado]

### Teoria (40%)
- [Conceito 1]: [Explicação resumida]
- [Conceito 2]: [Explicação resumida]

### Prática (60%)
- [Exercício 1]: [Objetivo + instruções resumidas]
- [Exercício 2]: [Objetivo + instruções resumidas]

### Recursos
- [Leitura / vídeo / documentação]

### Checkpoint
[Como saber se o aprendiz absorveu o conteúdo da semana]

---

## Semana 2 — [Título]
[repetir estrutura]

---

## Projeto Final
**Objetivo:** [Descrição do projeto integrador]
**Critérios de avaliação:**
- [ ] [Critério 1]
- [ ] [Critério 2]
```

### 4. Revisão
- [ ] Cada semana tem objetivo verificável com verbo de ação?
- [ ] A progressão é lógica (não pula etapas)?
- [ ] Há pelo menos 60% de conteúdo prático?
- [ ] Os exercícios têm soluções completas?
- [ ] Há checkpoint de avaliação em cada semana?
- [ ] O projeto final integra os aprendizados de todas as semanas?
