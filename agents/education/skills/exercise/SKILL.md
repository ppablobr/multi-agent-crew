---
name: education-exercise
description: >
  Sub-skill do Education Agent para criar exercícios práticos isolados. Use when creating a
  single hands-on activity, coding challenge, or practical task with clear instructions and solution.
  Examples: "create an exercise on chain-of-thought prompting", "make a hands-on task for RAG",
  "build a coding challenge for n8n workflow", "design a practice activity for AI agents".
  Typically invoked by the education orchestrator skill, not directly.
---

# Sub-skill: Exercício Prático

## Quando usar
Atividade prática isolada com objetivo específico, instruções claras e solução completa.
Pode ser parte de uma trilha ou workshop, ou entregue de forma independente.

---

## Processo

### 1. Coletar insumos
- **Habilidade que treina:** O que o exercício desenvolve?
- **Público:** Nível de conhecimento (iniciante / intermediário / avançado)?
- **Ferramentas disponíveis:** O que o aprendiz vai usar (Claude, n8n, Python...)?
- **Tempo estimado:** Quanto tempo para completar?
- **Contexto:** Faz parte de uma trilha ou é standalone?

### 2. Estrutura obrigatória de um exercício

Todo exercício deve ter exatamente estas seções:

```markdown
# Exercício: [Título descritivo]
**Nível:** Iniciante / Intermediário / Avançado
**Tempo estimado:** [X minutos]
**Ferramentas:** [lista do que será usado]

## Objetivo
Ao final deste exercício, você conseguirá [verbo de ação + resultado concreto].

## Pré-requisitos
- [O que o aprendiz precisa saber antes]
- [Ferramenta ou acesso necessário]

## Contexto
[1-2 parágrafos explicando o problema real que o exercício simula. Evite "foo/bar" — use cenários corporativos reais.]

## Instruções
1. [Passo 1 — específico e verificável]
2. [Passo 2]
3. [Passo N]

## Output esperado
[O que deve existir ao final — seja específico: "um workflow com X nós", "um prompt que gera Y", etc.]

## Desafio extra (opcional)
[Variação mais difícil para quem terminar antes ou quiser se aprofundar]

## Solução completa
[A solução correta e comentada — não oculte, o aprendiz precisa poder verificar]

## Pontos de atenção
- [Erro comum 1 que iniciantes cometem]
- [Gotcha ou detalhe importante]
```

### 3. Calibrar a dificuldade

| Nível | Características |
|---|---|
| **Iniciante** | Instruções passo-a-passo detalhadas, sem ambiguidade, solução linear |
| **Intermediário** | Instruções gerais com pontos de decisão, múltiplos caminhos válidos |
| **Avançado** | Objetivo claro, sem instruções detalhadas — o aprendiz decide a abordagem |

### 4. Usar cenários reais
- Evite nomes genéricos (João, Maria, empresa fictícia sem contexto)
- Use contextos do mundo real: CRM, pipeline de dados, automação de email, análise de feedback
- Se for para Méliuz: use contextos de cashback, parceiros, transações, CS

### 5. Revisão
- [ ] O objetivo usa verbo de ação verificável?
- [ ] As instruções são claras o suficiente para o nível definido?
- [ ] O output esperado é concreto e mensurável?
- [ ] A solução completa está documentada e funciona?
- [ ] Há pelo menos 1 ponto de atenção sobre erro comum?
- [ ] O contexto usa cenário real (não "foo/bar")?
