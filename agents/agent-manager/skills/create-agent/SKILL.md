---
name: agent-manager
description: >
  Ative o **Agent Manager**. Use when the user asks to create new agents, evolve existing agents,
  manage the multi-agent ecosystem, or design agent collaboration patterns. Examples include
  "create a new agent for X", "improve the Y agent", "manage agent interactions", or any request
  involving agent creation, evolution, or orchestration. Note: Agent Manager is invoked via
  /agent-manager slash command, but this skill documents the process.
---

# Skill: Criar Novo Agente

## Objetivo
Criar um agente novo completo — persona, especialidades, memória e integrações com o sistema.

## Processo

### 0. Carregar contexto (SEMPRE executar antes de qualquer outra coisa)

Antes de definir ou criar qualquer agente, leia obrigatoriamente:

1. **`agents/agent-manager/memory/ecosystem-map.md`** — mapa completo de agentes existentes com especialidades. Garanta que o novo agente não duplica responsabilidade de outro.
2. **`agents/agent-manager/memory/standards.md`** — padrões e convenções estabelecidos para criação de agentes (nomenclatura, estrutura de arquivos, regras mínimas).
3. **`agents/agent-manager/memory/history.md`** — agentes criados, decisões de design tomadas, lições aprendidas.
4. **`shared/memory/world.md`** — contexto global: gaps identificados no ecossistema, projetos que demandam novos agentes.

**Com base no que leu**, adapte o processo:
- Se já existe agente com especialidade similar → proponha evoluir o existente ao invés de criar um novo
- Se o ecosystem-map tem gaps identificados → priorize cobrir esses gaps
- Se os standards têm convenções definidas → aplique automaticamente sem precisar perguntar ao usuário

### 1. Definir o agente (pergunte se não souber)
- **Nome:** Como o agente será chamado?
- **Problema que resolve:** Qual necessidade esse agente atende?
- **Público:** Quem vai interagir com ele?
- **Especialidades principais:** O que ele faz melhor?
- **Limites:** O que ele NÃO faz?
- **Colaborações:** Com quais outros agentes vai interagir?

### 2. Checklist antes de criar
- [ ] O agente não duplica responsabilidade de outro agente existente?
- [ ] A especialidade é suficientemente específica para justificar um agente separado?
- [ ] Já sei quais skills iniciais ele terá?
- [ ] Sei o padrão de colaboração com outros agentes?

### 3. Criar os arquivos do agente

#### 3a. Diretório
```bash
mkdir -p agents/[nome-do-agente]/{skills,memory}
```

#### 3b. AGENT.md
Use o template padrão (ver `agents/agent-manager/AGENT.md` seção "Template de novo agente")

Seções obrigatórias:
- Persona (quem é, mentalidade)
- Especialidades (o que faz, casos de uso)
- Como colaborar com outros agentes (tabela)
- Memória do agente (arquivos)
- Regras do agente (mínimo 5 regras)

#### 3c. Slash command
Criar em `.claude/commands/[nome].md`:
```markdown
Ative o **[Nome] Agent**.

Siga estes passos:
1. Leia o arquivo `agents/[nome]/AGENT.md`
2. Leia `agents/[nome]/memory/history.md` (se existir)
3. Leia `shared/memory/world.md`
4. Assuma completamente a persona do agente
5. Execute a tarefa abaixo

Ao final:
- Atualize `agents/[nome]/memory/history.md`
- Se relevante, atualize `shared/memory/world.md`

**Tarefa:** $ARGUMENTS
```

#### 3d. Arquivos de memória iniciais
```bash
touch agents/[nome]/memory/history.md
```

Com conteúdo inicial:
```markdown
# Histórico: [Nome] Agent
*Sem histórico ainda — agente criado em YYYY-MM-DD*
```

#### 3e. Skill inicial (opcional mas recomendado)
Crie ao menos uma skill em `agents/[nome]/skills/SKILL-[funcao-principal].md`

### 4. Atualizar o ecossistema

Após criar o agente:
1. **Atualizar** `shared/memory/world.md` — adicionar na tabela de agentes ativos
2. **Atualizar** `agents/agent-manager/memory/ecosystem-map.md` — adicionar o novo agente
3. **Atualizar** `agents/agent-manager/memory/history.md` — registrar a criação
4. **Notificar** outros agentes relevantes (via handoff se necessário)

### 5. Checklist de agente completo
- [ ] AGENT.md criado com todas as seções
- [ ] Slash command criado em `.claude/commands/`
- [ ] Arquivos de memória inicializados
- [ ] Pelo menos uma skill criada
- [ ] Adicionado em `shared/memory/world.md`
- [ ] Ecosystem map atualizado
- [ ] Colaborações com outros agentes documentadas nos AGENT.md correspondentes

### 6. Teste de sanidade
Antes de declarar o agente pronto, faça uma tarefa de teste simples:
- Execute `/[nome-do-agente] [tarefa simples de teste]`
- Verifique se a persona está coerente
- Verifique se o agente sabe quando colaborar com outros

---

## Skills complementares

Durante e após a criação do agente:

| Situação | Skill |
|---|---|
| Criar ou otimizar a skill do novo agente | **`skill-creator`** → OBRIGATÓRIO para toda criação de skill |
| Novo agente precisa de documentação formal (ADR, spec) | **`tech-docs-writer`** → gerar ADR da decisão de criar o agente |
| Novo agente faz parte de um projeto de IA maior | **`ai-pm`** → integrar ao roadmap do projeto |
| Comunicar publicamente o novo agente ou capacidade | **`linkedin`** → criar post sobre o novo agente/automação |
