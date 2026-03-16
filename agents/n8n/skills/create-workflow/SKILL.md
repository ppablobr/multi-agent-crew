---
name: n8n
description: >
  Use when the user asks to create workflows, build automations, integrate APIs, or work with n8n.
  Examples include "create a workflow for X", "automate Y process", "integrate Z with n8n",
  "build an AI agent in n8n", or any request involving automation, integrations, webhooks, APIs,
  or the n8n platform. Use this skill whenever the user mentions n8n, workflows, automations,
  integrations, or wants to connect different services/systems.
---

# Skill: n8n — Orquestrador de Automações

## Objetivo
Entender a necessidade, aplicar os padrões e sub-skills corretos, e entregar um workflow funcional e bem documentado.

---

## Processo

### 0. Carregar contexto (SEMPRE executar antes de qualquer outra coisa)

Antes de entender a necessidade ou desenhar qualquer workflow, leia obrigatoriamente:

1. **`agents/n8n/memory/history.md`** — workflows já criados. Verifique se existe um similar ou reutilizável como base.
2. **`agents/n8n/memory/snippets.md`** — padrões e trechos de código já validados para reutilizar.
3. **`shared/memory/world.md`** — contexto global: projetos ativos, integrações disponíveis e ferramentas configuradas.

**Com base no que leu**, adapte:
- Se já existe workflow parecido → proponha evoluí-lo ao invés de criar do zero
- Se há snippets reutilizáveis → use como ponto de partida
- Se o contexto global lista credenciais/serviços → inclua na proposta sem precisar perguntar

---

### 1. Entender a necessidade (pergunte se não souber)
- **Trigger:** O que inicia o workflow? (webhook, schedule, manual, evento)
- **Ação central:** O que o workflow faz?
- **Ferramentas envolvidas:** Quais sistemas são usados?
- **Resultado esperado:** O que acontece no final?
- **Edge cases:** O que acontece se algo der errado?

---

### 2. Acionar sub-skills conforme a necessidade

Durante a criação do workflow, use as sub-skills especializadas quando necessário:

| Quando | Sub-skill |
|---|---|
| Precisar de padrão arquitetural (webhook, schedule, HTTP, AI agent) | **`n8n-workflow-patterns`** → consultar padrões validados |
| Escrever código em um nó Code (JavaScript) | **`n8n-code-javascript`** → sintaxe correta de `$json`, `$input`, helpers |
| Escrever código em um nó Code (Python) | **`n8n-code-python`** → sintaxe correta de `_input`, `_json` |
| Escrever expressões `{{ }}` em campos de nós | **`n8n-expression-syntax`** → validar e corrigir expressões |
| Configurar nós específicos (propriedades, operações) | **`n8n-node-configuration`** → dependências e campos obrigatórios |
| Usar ferramentas MCP do n8n (criar, testar, buscar templates) | **`n8n-mcp-tools-expert`** → guia de uso das ferramentas MCP |
| Interpretar erros de validação do workflow | **`n8n-validation-expert`** → diagnóstico e correção |

---

### 3. Entregar nesta sequência

#### 3a. Diagrama em texto
```
[Trigger] → [Passo 1] → {Decisão?} → [Caminho A] → [Output]
                                   ↓
                              [Caminho B] → [Error handling]
```

#### 3b. Explicação de cada nó
| Nó | Tipo | Função | Notas |
|---|---|---|---|
| Webhook | Trigger | Recebe dados externos | POST /webhook/meu-workflow |

#### 3c. Configurações críticas
Lista dos campos que o usuário **precisa** configurar manualmente (credenciais, IDs, etc.)

#### 3d. Criar no n8n via MCP
Use **`n8n-mcp-tools-expert`** para criar o workflow diretamente na instância via `n8n_create_workflow`.

---

### 4. Padrões obrigatórios

**Nomenclatura de nós:**
- ✅ "Recebe Lead via Webhook" / "Valida se Email Existe no CRM"
- ❌ "Webhook1" / "HTTP Request2"

**Error handling obrigatório em workflows críticos:**
```
[Nó principal] → {Sucesso?} → [Continua]
                    ↓ Erro
              [Captura erro] → [Notifica no Slack] → [Para execução]
```

---

### 5. Revisão final
- [ ] Todo nó tem nome descritivo?
- [ ] Há error handling nos pontos críticos?
- [ ] As credenciais estão identificadas mas não expostas?
- [ ] O workflow escala para volume maior?
- [ ] Documentei os edge cases?

---

## Skills complementares

Após criar o workflow, considere:

| Situação | Skill |
|---|---|
| Workflow é relevante para virar conteúdo público | **`linkedin`** → post ou carrossel técnico |
| Workflow automatiza um processo mapeado | **`process-manager`** → atualizar o TO-BE do processo |
| Workflow precisa de documentação formal | **`tech-docs-writer`** → SOP ou ADR estruturado |
