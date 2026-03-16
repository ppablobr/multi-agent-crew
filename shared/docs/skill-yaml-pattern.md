# Padrão YAML para Skills

Este documento define o padrão YAML obrigatório para todas as skills do Multi-Agent Crew.

---

## 📋 Estrutura obrigatória

Toda skill MUST seguir este formato:

```yaml
---
name: skill-name
description: >
  Descrição completa da skill em inglês, explicando quando usar.
  Pode ser multi-linha usando o operador >.
  Inclui exemplos de uso e keywords relevantes.
---

# Título da Skill em Português

## Objetivo
[Objetivo da skill em português]

## Processo
[Conteúdo da skill em Markdown]
```

---

## 🔑 Componentes do frontmatter

### `name`
- **Tipo:** String
- **Obrigatório:** Sim
- **Formato:** kebab-case (ex: `n8n-workflow-patterns`, `create-design`)
- **Descrição:** Nome único da skill, usado pelo Claude Code para invocação

**Regras:**
- Deve ser único em todo o sistema
- Usar kebab-case (palavras separadas por hífen)
- Preferir nomes descritivos e específicos
- Evitar nomes genéricos como `skill1` ou `helper`

**Exemplos válidos:**
```yaml
name: linkedin
name: n8n-code-javascript
name: create-design
name: ai-pm
```

**Exemplos inválidos:**
```yaml
name: LinkedIn  # ❌ não usar CamelCase
name: create_post  # ❌ não usar snake_case
name: skill  # ❌ muito genérico
```

---

### `description`
- **Tipo:** String (multi-linha com `>`)
- **Obrigatório:** Sim
- **Idioma:** Inglês
- **Descrição:** Explica quando a skill deve ser usada, com exemplos e keywords

**Formato recomendado:**
```yaml
description: >
  Use when the user asks to [ação principal].
  Examples include "[exemplo 1]", "[exemplo 2]", "[exemplo 3]",
  or any request involving [keywords relacionados].
  Use this skill whenever the user mentions [triggers de ativação].
```

**Boas práticas:**
1. **Começar com "Use when"** - Indica claramente quando a skill é apropriada
2. **Incluir exemplos concretos** - Frases que ativariam a skill
3. **Listar keywords** - Termos-chave que indicam uso da skill
4. **Mencionar variações** - "or any request involving..."
5. **Finalizar com triggers** - "Use this skill whenever the user mentions..."

**Exemplo completo:**
```yaml
description: >
  Use when the user asks to create LinkedIn posts, write social media content about AI/automation/tech,
  develop LinkedIn strategy, or create professional content for social networks. Examples include
  "write a LinkedIn post about X", "create a carousel about Y", "draft content for announcing Z",
  or any request involving professional social media content, especially focused on AI, LLMs,
  automation, n8n, or tech topics. Use this skill whenever the user mentions LinkedIn, posts,
  social content, or wants to share professional insights.
```

---

## 📐 Exemplo completo

```yaml
---
name: n8n-workflow-patterns
description: >
  Proven workflow architectural patterns from real n8n workflows. Use when building new workflows,
  designing workflow structure, choosing workflow patterns, planning workflow architecture, or asking
  about webhook processing, HTTP API integration, database operations, AI agent workflows, or scheduled
  tasks. Use this skill whenever the user mentions workflow patterns, architecture, or best practices
  for n8n automation.
---

# n8n Workflow Patterns

Proven architectural patterns for building n8n workflows.

## The 5 Core Patterns

Based on analysis of real workflow usage:

1. **Webhook Processing** (Most Common)
   - Receive HTTP requests → Process → Output
   - Pattern: Webhook → Validate → Transform → Respond/Notify

[... resto do conteúdo em Markdown ...]
```

---

## ✅ Checklist de validação

Antes de criar ou atualizar uma skill, verifique:

- [ ] Frontmatter YAML presente (delimitado por `---`)
- [ ] Campo `name` definido em kebab-case
- [ ] Campo `description` presente e em inglês
- [ ] Description usa operador `>` para multi-linha
- [ ] Description inclui "Use when..."
- [ ] Description inclui exemplos ("Examples include...")
- [ ] Description lista keywords relevantes
- [ ] Description termina com "Use this skill whenever..."
- [ ] Conteúdo da skill em Markdown após o frontmatter
- [ ] Título da skill em português (se aplicável)

---

## 🚨 Erros comuns

### ❌ Falta de frontmatter
```markdown
# Skill: Criar Post para LinkedIn

## Objetivo
Criar posts de alto engajamento...
```

**Problema:** Sem frontmatter YAML, o Claude Code não consegue identificar e invocar a skill automaticamente.

**Correção:** Adicionar frontmatter no início do arquivo.

---

### ❌ Description em português
```yaml
---
name: linkedin
description: Usa quando o usuário pede para criar posts no LinkedIn
---
```

**Problema:** A description deve estar em inglês para ser processada corretamente pelo Claude Code.

**Correção:**
```yaml
---
name: linkedin
description: >
  Use when the user asks to create LinkedIn posts...
---
```

---

### ❌ Description sem exemplos
```yaml
---
name: linkedin
description: Creates LinkedIn posts
---
```

**Problema:** Muito vaga, não orienta quando usar a skill.

**Correção:** Adicionar "Use when...", exemplos concretos e keywords.

---

### ❌ Name em CamelCase ou com espaços
```yaml
---
name: LinkedInAgent  # ❌ CamelCase
name: linkedin agent  # ❌ com espaços
---
```

**Correção:**
```yaml
---
name: linkedin  # ✅ kebab-case
---
```

---

## 📂 Localização das skills

Skills devem estar organizadas em:

```
agents/
├── [agent-name]/
│   ├── skills/
│   │   ├── [skill-name]/
│   │   │   └── SKILL.md  ← Arquivo com frontmatter YAML
│   │   └── [outra-skill]/
│   │       └── SKILL.md
│   ├── memory/
│   └── AGENT.md
```

**Importante:** O Claude Code detecta automaticamente arquivos `SKILL.md` em qualquer diretório dentro de `agents/*/skills/`.

---

## 🔄 Como o Claude Code usa o frontmatter

1. **Detecção automática:** Claude Code escaneia todos os `SKILL.md` files
2. **Parsing do frontmatter:** Extrai `name` e `description`
3. **Matching semântico:** Quando o usuário faz uma pergunta, o Claude Code:
   - Analisa a intenção do usuário
   - Compara com as descriptions das skills disponíveis
   - Invoca automaticamente a skill mais adequada
4. **Contexto carregado:** Ao invocar a skill, carrega:
   - `agents/[agent]/AGENT.md` (persona do agente)
   - `agents/[agent]/memory/` (memória do agente)
   - `shared/memory/world.md` (contexto global)

---

## 🎯 Quando criar uma nova skill

Crie uma nova skill quando:

1. **Especialização necessária:** O agente precisa de um processo específico para um tipo de tarefa
2. **Reusabilidade:** O mesmo processo será usado múltiplas vezes
3. **Complexidade:** A tarefa tem múltiplos passos e decisões
4. **Clareza:** Separar a skill melhora a organização do agente

**Não crie** uma nova skill se:
- A tarefa é simples e única
- Já existe uma skill genérica que cobre o caso
- Criaria duplicação com skills existentes

---

## 📚 Referências

- **Skills com frontmatter YAML correto (exemplos):**
  - `agents/designer/skills/create-design/SKILL.md`
  - `agents/n8n/skills/n8n-workflow-patterns/SKILL.md`
  - `agents/education/skills/create-content/SKILL.md`

- **Documentação do Claude Code sobre skills:** Ver `.claude/skills/` (se disponível)

---

**Última atualização:** 2026-03-12
**Autor:** Multi-Agent Crew — Agent Manager
