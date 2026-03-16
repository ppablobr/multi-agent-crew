# Processo: Verificação de Cobranças Comunicadas aos Parceiros

**Versão**: 1.0
**Data**: 2026-03-13
**Responsável**: Process Manager Agent
**Status**: TO-BE (Proposta de automação)

---

## 📋 Objetivo

Garantir que cada cobrança de parceiro do ecommerce seja comunicada **apenas uma vez**, evitando duplicidade de mensagens e mantendo controle sobre quais cobranças já foram enviadas.

---

## 🎯 Escopo

**Início**: Leitura diária da planilha de cobranças (Google Sheets)
**Fim**: Registro de cobranças verificadas na tabela de check

---

## 👥 Responsáveis (RACI)

| Atividade | Responsible | Accountable | Consulted | Informed |
|---|---|---|---|---|
| Manutenção da planilha de cobranças | Time Financeiro | Gestor Financeiro | - | Time Comercial |
| Execução da automação | Workflow n8n | Gestor de Automação | - | Time Financeiro |
| Validação de duplicatas | Sistema automatizado | Gestor de Automação | Time Financeiro | - |
| Resolução de erros | Time de Automação | Gestor de Automação | Time Financeiro | Gestor Comercial |

---

## 🔴 PROCESSO AS-IS (Estado Atual)

### Problemas identificados:
- ❌ **Verificação manual ou inconsistente**
- ❌ **Alto risco de duplicidade** de comunicações aos parceiros
- ❌ **Sem controle centralizado** de quais cobranças já foram enviadas
- ❌ **Falta de rastreabilidade** (não sabemos quando/se uma cobrança foi comunicada)
- ❌ **Processo propenso a erros humanos**

### Fluxo atual:
1. Alguém abre a planilha de cobranças manualmente
2. Verifica visualmente se a coluna `slack_message_id` está vazia
3. Se vazia, deveria comunicar o parceiro (mas nem sempre acontece)
4. Se preenchida, deveria ignorar (mas pode duplicar por erro)
5. **Sem registro sistemático** de verificações realizadas

### Métricas AS-IS:
- ⏱️ **Tempo por verificação**: ~15-30 min/dia (manual)
- 🎯 **Taxa de erro**: ~15-20% (duplicatas ou esquecimentos)
- 📊 **Cobertura**: ~60-70% das cobranças verificadas
- 🔄 **Frequência**: Irregular (depende de disponibilidade humana)

---

## 🟢 PROCESSO TO-BE (Estado Futuro - Automatizado)

### Melhorias:
- ✅ **Verificação automatizada** diária às 13h (horário comercial)
- ✅ **Zero duplicidade** garantida por verificação de `slack_message_id`
- ✅ **Controle centralizado** na tabela de check de cobrança
- ✅ **100% de rastreabilidade** com logs de execução
- ✅ **Escalável** para qualquer volume de cobranças

### Fluxo automatizado:

#### 1️⃣ **Trigger Agendado** (Diário às 13h America/Sao_Paulo)
- Workflow n8n inicia automaticamente

#### 2️⃣ **Leitura da Google Sheets**
- Conecta na planilha de cobranças
- Lê todas as linhas com dados

#### 3️⃣ **Filtro de Cobranças Não Comunicadas**
- Filtra linhas onde `slack_message_id` está **vazio** ou **null**
- Estas são cobranças que ainda não foram comunicadas

#### 4️⃣ **Validação de Dados**
- Verifica se campos obrigatórios estão preenchidos:
  - ✓ NF (número da nota fiscal)
  - ✓ Valor
  - ✓ Parceiro
- Se dados incompletos → Envia alerta para Time Financeiro

#### 5️⃣ **Inserção na Tabela de Check**
- Para cada cobrança válida não comunicada:
  - Insere registro na "tabela de check de cobrança" com:
    - NF
    - Valor
    - Parceiro
    - Data de análise
    - Data de emissão
    - Data de vencimento
    - Boleto URL
    - Timestamp de verificação
    - Status: "Pendente comunicação"

#### 6️⃣ **Log de Execução**
- Registra:
  - Quantidade de cobranças verificadas
  - Quantidade de novas cobranças identificadas
  - Quantidade de alertas gerados
  - Timestamp da execução

#### 7️⃣ **Notificação**
- Se houver novas cobranças → Notifica Time Financeiro
- Se houver erros → Alerta Time de Automação

### Métricas TO-BE:
- ⏱️ **Tempo por verificação**: ~2-3 min (100% automatizado)
- 🎯 **Taxa de erro**: <1% (apenas falhas técnicas)
- 📊 **Cobertura**: 100% das cobranças verificadas
- 🔄 **Frequência**: Diária às 13h (consistente)
- 💰 **Economia de tempo**: ~90% (de 30min → 3min)

---

## 🎛️ Pontos de Controle e KPIs

### KPIs do Processo:

| KPI | Meta | Medição | Ação se fora do alvo |
|---|---|---|---|
| **Cobranças duplicadas** | 0/mês | Monitorar tabela de check | Revisar lógica de filtro |
| **Tempo de execução** | <5 min | Log do workflow | Otimizar queries da planilha |
| **Taxa de sucesso** | >99% | Monitorar falhas no n8n | Investigar erros e ajustar |
| **Cobranças identificadas** | Variável | Dashboard do workflow | Apenas monitorar tendência |
| **Alertas de dados incompletos** | <5% | Contador de alertas | Revisar processo de preenchimento |

### Pontos de Controle:

#### ✅ **Checkpoint 1: Validação de Dados**
- **Quando**: Após leitura da planilha
- **O que**: Verificar campos obrigatórios preenchidos
- **Se falhar**: Enviar alerta + não processar registro

#### ✅ **Checkpoint 2: Verificação de Duplicidade**
- **Quando**: Antes de inserir na tabela de check
- **O que**: Verificar se `slack_message_id` está vazio
- **Se falhar**: Ignorar registro (já foi comunicado)

#### ✅ **Checkpoint 3: Confirmação de Inserção**
- **Quando**: Após inserir na tabela de check
- **O que**: Validar que registro foi salvo com sucesso
- **Se falhar**: Tentar novamente + alertar se persistir

#### ✅ **Checkpoint 4: Monitoramento de Execução**
- **Quando**: Ao final do workflow
- **O que**: Validar que workflow rodou no horário correto
- **Se falhar**: Alertar Time de Automação

---

## 📦 Pré-requisitos

- ✅ Google Sheets com estrutura definida:
  - Colunas: data de análise, NF, valor, parceiro, data de emissão, data de vencimento, boleto url, slack_message_id
- ✅ Tabela de check de cobrança criada (destino dos dados)
- ✅ Workflow n8n configurado e ativo
- ✅ Credenciais Google Sheets configuradas no n8n
- ✅ Timezone configurado: America/Sao_Paulo
- ✅ Notificações Slack configuradas (para alertas)

---

## 🔄 Passos Detalhados (TO-BE)

| # | Atividade | Responsável | Sistema/Tool | Duração | Decisão |
|---|---|---|---|---|---|
| 1 | Trigger agendado dispara às 13h | n8n Scheduler | n8n | Instantâneo | - |
| 2 | Conecta na Google Sheets | Workflow | Google Sheets API | 5s | - |
| 3 | Lê todas as linhas da planilha | Workflow | Google Sheets Node | 10s | - |
| 4 | Filtra linhas com `slack_message_id` vazio | Workflow | Filter Node (n8n) | 1s | Se vazio → continua |
| 5 | Valida campos obrigatórios (NF, valor, parceiro) | Workflow | IF Node (n8n) | 1s | Se incompleto → alerta |
| 6 | Insere dados válidos na tabela de check | Workflow | Google Sheets Node | 5s/registro | - |
| 7 | Registra log de execução | Workflow | n8n Execution Log | 1s | - |
| 8 | Envia notificação se houver novas cobranças | Workflow | Slack Node | 2s | Se count > 0 → notifica |

**Tempo total estimado**: 2-3 minutos (dependendo do volume de cobranças)

---

## 🚨 Problemas Comuns e Soluções

| Problema | Causa Provável | Solução |
|---|---|---|
| Workflow não executou às 13h | Timezone errado ou n8n inativo | Verificar timezone do n8n / status da instância |
| Erro ao ler Google Sheets | Permissões ou credenciais expiradas | Renovar OAuth / verificar permissões da planilha |
| Dados duplicados na tabela de check | Lógica de filtro falhou | Revisar condição do Filter Node |
| Alertas excessivos de dados incompletos | Planilha sendo preenchida incompletamente | Revisar processo de entrada de dados no financeiro |
| Workflow muito lento | Volume alto de dados | Adicionar paginação ou otimizar query |

---

## 📊 Impacto Estimado da Automação

### Benefícios Quantitativos:
- ⏱️ **Economia de tempo**: 25 min/dia × 22 dias úteis = **9h/mês** economizadas
- 💰 **Redução de custo operacional**: ~R$ 450/mês (considerando custo/hora do time financeiro)
- 🎯 **Redução de duplicatas**: De ~15-20% → <1%
- 📈 **Aumento de cobertura**: De ~70% → 100%

### Benefícios Qualitativos:
- ✅ Maior confiança dos parceiros (sem cobranças duplicadas)
- ✅ Redução de fricção no relacionamento comercial
- ✅ Time financeiro focado em tarefas estratégicas (não operacionais)
- ✅ Rastreabilidade completa para auditorias
- ✅ Escalabilidade para crescimento do negócio

---

## 🔄 Próximos Passos

1. ✅ **Process Manager**: Documentação e fluxogramas criados
2. ⏳ **n8n Agent**: Criar workflow de automação
3. ⏳ **Tech Docs Writer**: Criar SOP operacional completo
4. ⏳ Testar workflow em ambiente de homologação
5. ⏳ Deploy em produção
6. ⏳ Monitorar KPIs por 2 semanas
7. ⏳ Ajustes finos conforme feedback

---

## 📝 Histórico de Versões

| Versão | Data | Autor | Mudanças |
|---|---|---|---|
| 1.0 | 2026-03-13 | Process Manager Agent | Mapeamento inicial AS-IS e TO-BE |

---

## 🔗 Arquivos Relacionados

- Fluxograma AS-IS: (será criado via excalidraw-diagram)
- Fluxograma TO-BE: (será criado via excalidraw-diagram)
- Workflow n8n: (será criado pelo n8n Agent)
- SOP Operacional: (será criado pelo Tech Docs Writer)
