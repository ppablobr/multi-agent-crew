---
name: linkedin-carousel
description: >
  Sub-skill do LinkedIn Agent para criar posts em formato carrossel (múltiplos slides).
  Use when educational content needs visual structure across multiple slides, step-by-step guides,
  concept comparisons, or frameworks. Examples: "carousel about prompt engineering", "slides explaining
  RAG", "create a mini-guide about AI agents", "visual breakdown of X".
  This skill is typically invoked by the linkedin orchestrator skill, not directly.
  After generating the carousel script, always invoke the designer skill (canvas-design) to create the visual slides.
---

# Sub-skill: Carrossel LinkedIn

## Quando usar
Conteúdo educativo com múltiplos conceitos, guias passo-a-passo, frameworks, comparações ou qualquer tema que se beneficie de estrutura visual em slides.

Carrossel funciona melhor quando:
- O conteúdo tem 4-10 "peças" que fazem sentido visuais e separadas
- O tema é denso e precisa ser digerido em partes
- Quer alto tempo de tela (o algoritmo favorece carrosséis)

---

## Estrutura obrigatória

```
Slide 1 — CAPA: Gancho + promessa clara (o que o leitor vai aprender)
Slide 2 — Problema ou contexto (por que isso importa)
Slides 3-8 — Conteúdo principal (um conceito por slide)
Slide N-1 — Resumo ou framework visual
Slide N — CTA + onde saber mais
```

---

## Processo

### 1. Definir estrutura do carrossel
- **Quantidade de slides:** 5 a 10 (menos de 5 é fraco, mais de 10 cansa)
- **Um conceito por slide** — sem textos longos
- **Título + 2-4 bullet points por slide** (máximo)
- **Progressão lógica** — cada slide prepara o próximo

### 2. Escrever o script de cada slide

Para cada slide entregue:
```
**Slide X**
Título: [título do slide]
Conteúdo:
- [bullet 1]
- [bullet 2]
- [bullet 3]
Nota visual: [sugestão de como visualizar — ícone, diagrama, destaque]
```

### 3. Escrever o texto do post (legenda)

O carrossel precisa de uma legenda no post:
```
[Gancho — primeira linha que para o scroll]

Criei um guia completo sobre [tema].

Deslize para ver →

[2-3 linhas de contexto do que vai encontrar]

[CTA — "Salva para consultar depois" ou "Compartilha com quem precisa ver isso"]

[3-5 hashtags]
```

### 4. Acionar Designer para criar os slides visuais

**OBRIGATÓRIO após gerar o script:** Use a skill **`designer`** (sub-skill `canvas-design`) para criar os slides visuais do carrossel.

Passe para o designer:
- Script completo com título e bullets de cada slide
- Tom visual desejado (profissional, colorido, minimalista)
- Paleta de cores preferida (ou deixe o designer sugerir com base no `design-library.md`)

### 5. Revisão
- [ ] A capa tem gancho claro e promessa específica?
- [ ] Cada slide tem no máximo 1 ideia central?
- [ ] A progressão de slides conta uma história lógica?
- [ ] O último slide tem CTA claro?
- [ ] A legenda do post funciona sozinha (sem os slides)?

---

## Exemplo de estrutura de carrossel

**Tema:** Como construir um AI Agent em n8n

```
Slide 1 — CAPA
Título: Como construir um AI Agent em n8n em 30 minutos
Conteúdo: Guia completo para iniciantes
Nota visual: Ícone de robô + logo n8n

Slide 2 — O QUE É UM AI AGENT
Título: O que é um AI Agent?
Conteúdo:
- Um sistema que percebe, decide e age
- Diferente de um chatbot: tem memória e ferramentas
- Pode executar ações reais (enviar email, criar ticket)
Nota visual: Diagrama simples: Input → LLM → Tool → Output

Slide 3 — COMPONENTES
Título: 3 componentes essenciais
Conteúdo:
- 🧠 O LLM (Claude, GPT) — o cérebro
- 🔧 As ferramentas — o que ele pode fazer
- 💾 A memória — o que ele lembra
Nota visual: Três caixas com ícones

[... slides 4-8 ...]

Slide 9 — RESUMO
Título: O que você aprendeu
Conteúdo:
- Agente = LLM + Tools + Memory
- n8n conecta tudo visualmente
- Comece simples, evolua iterando
Nota visual: Mini-framework visual

Slide 10 — CTA
Título: Quer o template?
Conteúdo:
- Link do workflow no comentário
- Me segue para mais conteúdo sobre IA
Nota visual: Foto ou avatar + CTA visual
```
