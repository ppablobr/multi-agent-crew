# 🔄 Handoff — Passagem de contexto entre agentes

> Este arquivo é usado para **passar contexto de um agente para outro**.
> O agente que entrega escreve aqui. O agente que recebe lê e apaga após processar.

---

## Formato de handoff

```markdown
## Handoff: [Agente Origem] → [Agente Destino]
**Data:** YYYY-MM-DD HH:MM
**Prioridade:** Alta / Normal / Baixa

### Contexto
[O que estava sendo feito]

### O que preciso de você
[Tarefa específica para o agente destino]

### Inputs disponíveis
[Arquivos, dados, informações relevantes]

### Output esperado
[O que o agente destino deve entregar]

### Após concluir
[O que fazer com o resultado — retornar para quem, atualizar qual arquivo]
```

---

## Handoffs pendentes

*Nenhum handoff pendente no momento.*

---

## Histórico de handoffs

| Data | Origem | Destino | Assunto | Status |
|---|---|---|---|---|
| — | — | — | Sistema inicializado | — |
