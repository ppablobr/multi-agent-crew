# 📋 Protocolo de Handoff entre Agentes

## Propósito
Garantir que a passagem de contexto entre agentes seja clara, rastreável e eficiente.

---

## Quando usar handoff

Use o protocolo de handoff quando:
- Um agente precisa de **informação especializada** de outro agente para completar sua tarefa
- Um agente termina sua parte e precisa **passar o bastão** para outro continuar
- Uma tarefa requer **colaboração sequencial** entre múltiplos agentes

---

## Protocolo passo a passo

### Agente que entrega (origem):

1. **Escreva o handoff** em `shared/memory/handoff.md` usando o formato padrão
2. **Informe claramente** o que está pedindo e o formato esperado do output
3. **Indique a prioridade** (Alta / Normal / Baixa)
4. **Ative o agente destino** informando que há um handoff pendente

### Agente que recebe (destino):

1. **Leia** o handoff em `shared/memory/handoff.md`
2. **Confirme** que entendeu o que foi pedido
3. **Execute** a tarefa
4. **Escreva o resultado** em `shared/memory/handoff.md` na seção "Resultado"
5. **Marque como concluído** no histórico
6. **Notifique** que o handoff foi concluído

---

## Formato do handoff

```markdown
## Handoff: [Agente Origem] → [Agente Destino]
**Data:** YYYY-MM-DD
**Prioridade:** Alta / Normal / Baixa
**Status:** Pendente / Em andamento / Concluído

### Contexto
[O que o agente origem estava fazendo]

### Solicitação
[O que precisa do agente destino — seja específico]

### Inputs
- [Arquivo ou informação relevante 1]
- [Arquivo ou informação relevante 2]

### Output esperado
[Formato e conteúdo esperado como resposta]

### Resultado (preenchido pelo agente destino)
[Output produzido]
```

---

## Exemplo real de handoff

```markdown
## Handoff: Process Manager → n8n Agent
**Data:** 2026-03-12
**Prioridade:** Normal
**Status:** Pendente

### Contexto
Mapeei o processo de onboarding de novos clientes (AS-IS).
O processo tem 7 etapas manuais que podem ser automatizadas.

### Solicitação
Crie um workflow n8n que automatize as etapas 3 a 6 do processo
(envio de email de boas-vindas, criação de conta no sistema,
notificação do time de CS no Slack, e agendamento de call de onboarding).

### Inputs
- Processo documentado em: agents/process-manager/memory/processes.md
- Ferramentas disponíveis: Gmail, Slack, Google Calendar, CRM interno

### Output esperado
- Diagrama do workflow em texto
- Configurações de cada nó
- JSON do workflow para importar no n8n
```

---

## Regras do protocolo

1. **Nunca assuma** que o agente destino tem contexto — sempre escreva o handoff completo
2. **Seja específico** no output esperado — vago gera retrabalho
3. **Limpe handoffs antigos** — após concluído, mova para o histórico
4. **Máximo 3 handoffs simultâneos** — evita sobrecarga de contexto
