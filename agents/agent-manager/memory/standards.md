# 📐 Padrões e Convenções do Sistema

Padrões mantidos pelo Agent Manager para garantir coesão do ecossistema de agentes.

---

## 📁 Estrutura de diretórios

```
agents/[nome-do-agente]/
├── AGENT.md           → Documentação principal do agente (referência)
└── memory/
    └── history.md     → Log de ações do agente
```

```
.claude/skills/[nome-agente]/
├── SKILL.md           → Skill YAML do agente (formato OBRIGATÓRIO)
└── evals/
    └── evals.json     → Casos de teste (3 mínimo, 2/3 aprovados)
```

> **Mudança em 2026-03-12**: Agentes agora são implementados como **YAML Skills** em `.claude/skills/`, não mais como slash commands em `.claude/commands/`. Apenas o Agent Manager mantém slash command.

---

## 📝 Estrutura de AGENT.md

Todo AGENT.md deve conter:
1. **Título** com emoji e nome
2. **Persona** — quem é o agente
3. **Especialidades** — o que sabe fazer
4. **Colaborações** — quando chamar outros agentes
5. **Memória** — arquivos de memória do agente
6. **Regras** — regras específicas do agente

---

## 🎯 Convenções de nomenclatura

- **Agentes**: kebab-case (ex: `agent-manager`, `ai-pm`)
- **Slash commands**: kebab-case (ex: `/agent-manager`, `/ai-pm`)
- **Skills**: kebab-case (ex: `linkedin-post`, `n8n-workflow`)
- **Arquivos de memória**: kebab-case (ex: `ecosystem-map.md`, `history.md`)

---

## 🤝 Protocolo de handoff

Quando um agente precisa passar contexto para outro:
1. Escreve output em `shared/memory/handoff.md`
2. Menciona qual agente deve assumir
3. Próximo agente lê handoff.md e continua

---

## ✅ Criação de agentes (com skill creator)

**OBRIGATÓRIO**: Todo novo agente deve ser criado seguindo:
1. Planejamento da especialidade e persona
2. **Uso da skill creator** para criar a skill YAML em `.claude/skills/[nome-agente]/`
3. **Teste da skill** — 3 casos de teste enxutos; 2/3 aprovados = aprovado
4. Documentação em `agents/[nome-agente]/AGENT.md` (referência)
5. Criação de estrutura de memória em `agents/[nome-agente]/memory/`
6. Atualização do mapa em `shared/memory/world.md`

**Formato obrigatório**: Skills YAML com frontmatter:
```markdown
---
name: nome-do-agente
description: Quando usar esta skill e o que ela faz
---

# Conteúdo da skill (instruções, workflow, regras, memória)
```

---

## 🧪 Padrões de Teste

### Critérios de aprovação:
- **Quantidade:** 3 test cases por skill
- **Pass rate:** 2/3 aprovados (66%) é suficiente
- **Economia:** Testes enxutos para evitar consumo excessivo de tokens

### Como criar testes enxutos:
- **Prompts curtos:** 1-3 frases, não parágrafos longos
- **Outputs específicos:** Testar uma capacidade por vez, não projetos completos
- **Cenários realistas:** Casos que o agente realmente enfrentará
- **Evitar bloat:** Não pedir materiais de 50 páginas se 5 páginas validam o mesmo

### Exemplo de teste BOM (enxuto):
```
"Cria um outline de mentoria de 60 min sobre prompts.
Público intermediário. Inclui 1 exercício prático."
```

### Exemplo de teste RUIM (verboso demais):
```
"Preciso montar uma trilha completa de aprendizado de 12 semanas
com materiais detalhados para cada semana, incluindo slides,
exercícios, soluções, quizzes, recursos externos, templates,
cases de sucesso, métricas de avaliação..."
```
(Este teste gera 50k+ tokens desnecessariamente)

---

_Este arquivo é mantido atualizado pelo Agent Manager._
