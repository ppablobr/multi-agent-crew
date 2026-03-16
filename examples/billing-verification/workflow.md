# Workflow n8n: Verificação Diária de Cobranças - Parceiros

**ID do Workflow**: `your-workflow-id`
**URL**: [Abrir no n8n](https://your-n8n-instance.example.com/workflow/your-workflow-id)
**Status**: Criado (aguardando configuração de credenciais)
**Timezone**: America/Sao_Paulo

---

## 📋 Visão Geral

Este workflow automatiza a verificação diária de cobranças de parceiros do ecommerce, garantindo que:
- ✅ Cada cobrança seja comunicada apenas uma vez (zero duplicatas)
- ✅ Todas as cobranças sejam verificadas diariamente às 13h
- ✅ Dados incompletos sejam alertados ao Time Financeiro
- ✅ Rastreabilidade completa com logs de execução

---

## 🔧 Configuração Necessária

### Passo 1: Credenciais Google Sheets

1. Acesse o workflow no n8n: https://your-n8n-instance.example.com/workflow/your-workflow-id
2. Clique no node "**Ler Planilha de Cobranças**"
3. Em "Credential to connect with", clique em "Create New"
4. Selecione "Google Sheets OAuth2 API"
5. Siga o fluxo de autenticação do Google
6. **Repita o processo** para o node "**Inserir na Tabela de Check**" (pode reutilizar a mesma credencial)

### Passo 2: Configurar Planilha de Cobranças

No node "**Ler Planilha de Cobranças**":
1. **Document**: Selecione a planilha de cobranças na lista
2. **Sheet**: Selecione a aba que contém as cobranças
3. **Range** (se necessário): Deixe vazio para ler todas as linhas ou especifique (ex: `A2:H`)

**Colunas esperadas na planilha:**
- `data de análise`
- `NF` (número da nota fiscal)
- `valor`
- `parceiro`
- `data de emissão`
- `data de vencimento`
- `boleto url`
- `slack_message_id` (indica se já foi comunicada - vazio = não enviada)

### Passo 3: Configurar Tabela de Check

No node "**Inserir na Tabela de Check**":
1. **Document**: Selecione a planilha de destino (tabela de check)
2. **Sheet**: Selecione a aba de destino
3. **Columns to Match On**: Deixe vazio (sempre adiciona nova linha)

**Colunas criadas na tabela de check:**
- `NF`, `valor`, `parceiro`, `data_analise`, `data_emissao`, `data_vencimento`, `boleto_url`, `timestamp_verificacao`

### Passo 4: Credenciais Slack

1. Clique no node "**Alerta - Dados Incompletos**"
2. Em "Credential to connect with", clique em "Create New"
3. Selecione "Slack API"
4. Insira o token do Slack (você pode obter em https://api.slack.com/apps)
5. Salve a credencial
6. **Repita** para o node "**Notificar Novas Cobranças**" (pode reutilizar a mesma credencial)

### Passo 5: Configurar Canais Slack

**No node "Alerta - Dados Incompletos":**
- **Channel**: Selecione o canal onde os alertas de dados incompletos devem ser enviados (ex: `#financeiro`)

**No node "Notificar Novas Cobranças":**
- **Channel**: Selecione o canal onde as notificações de sucesso devem ser enviadas (ex: `#financeiro` ou `#cobrancas`)

---

## 📊 Arquitetura do Workflow

### Nodes e Fluxo

```
1. Schedule Trigger - 13h (⏰ Trigger)
   ↓
2. Ler Planilha de Cobranças (📖 Google Sheets)
   ↓
3. Filtrar slack_message_id Vazio (🔍 Filter)
   ↓
4. Validar Dados Obrigatórios (✓ IF)
   ├─ FALSE → 5. Alerta - Dados Incompletos (⚠️ Slack)
   └─ TRUE → 6. Inserir na Tabela de Check (💾 Google Sheets)
                ↓
             7. Registrar Log de Execução (📊 Set)
                ↓
             8. Verificar Novas Cobranças (? IF)
                └─ TRUE → 9. Notificar Novas Cobranças (📧 Slack)
```

### Detalhamento dos Nodes

#### 1️⃣ **Schedule Trigger - 13h**
- **Tipo**: Schedule Trigger
- **Função**: Dispara o workflow automaticamente todos os dias às 13h
- **Configuração**: Cron expression `0 13 * * *` (timezone: America/Sao_Paulo)
- **Não requer configuração adicional**

#### 2️⃣ **Ler Planilha de Cobranças**
- **Tipo**: Google Sheets
- **Operação**: Read (ler dados)
- **Função**: Lê todas as linhas da planilha de cobranças
- **Output**: Array de objetos com todas as cobranças
- **⚠️ REQUER**: Credencial Google Sheets + Document ID + Sheet Name

#### 3️⃣ **Filtrar slack_message_id Vazio**
- **Tipo**: Filter
- **Função**: Filtra apenas cobranças onde `slack_message_id` está vazio (não comunicadas)
- **Condição**: `$json.slack_message_id` is empty
- **Output**: Apenas cobranças não comunicadas

#### 4️⃣ **Validar Dados Obrigatórios**
- **Tipo**: IF
- **Função**: Verifica se campos obrigatórios estão preenchidos
- **Condições**:
  - `$json.NF` não está vazio
  - `$json.valor` não está vazio
  - `$json.parceiro` não está vazio
- **Output TRUE**: Dados completos → continua para inserir na tabela
- **Output FALSE**: Dados incompletos → envia alerta Slack

#### 5️⃣ **Alerta - Dados Incompletos**
- **Tipo**: Slack
- **Função**: Envia alerta ao Time Financeiro sobre cobranças com dados incompletos
- **Mensagem**:
  ```
  ⚠️ Cobrança com dados incompletos detectada

  NF: [valor ou N/A]
  Parceiro: [valor ou N/A]
  Valor: [valor ou N/A]

  Por favor, revisar a planilha de cobranças.
  ```
- **⚠️ REQUER**: Credencial Slack + Canal configurado

#### 6️⃣ **Inserir na Tabela de Check**
- **Tipo**: Google Sheets
- **Operação**: Append (adicionar linha)
- **Função**: Insere as cobranças válidas na tabela de check para evitar duplicatas futuras
- **Dados inseridos**:
  - NF, valor, parceiro
  - data_analise, data_emissao, data_vencimento
  - boleto_url
  - timestamp_verificacao (timestamp atual)
- **⚠️ REQUER**: Credencial Google Sheets + Document ID + Sheet Name

#### 7️⃣ **Registrar Log de Execução**
- **Tipo**: Set
- **Função**: Cria um registro de log com métricas da execução
- **Campos criados**:
  - `total_verificadas`: Total de cobranças na planilha original
  - `novas_cobrancas`: Quantidade de cobranças sem slack_message_id
  - `timestamp_execucao`: Timestamp da execução
  - `status`: "sucesso"

#### 8️⃣ **Verificar Novas Cobranças**
- **Tipo**: IF
- **Função**: Verifica se há novas cobranças identificadas
- **Condição**: `$json.novas_cobrancas > 0`
- **Output TRUE**: Há novas cobranças → envia notificação Slack
- **Output FALSE**: Nenhuma nova cobrança → workflow termina

#### 9️⃣ **Notificar Novas Cobranças**
- **Tipo**: Slack
- **Função**: Envia notificação de sucesso ao Time Financeiro
- **Mensagem**:
  ```
  ✅ Verificação de Cobranças Concluída

  📊 Resumo:
  • Total verificadas: [X]
  • Novas cobranças identificadas: [Y]
  • Horário: [timestamp]

  As novas cobranças foram registradas na tabela de check.
  ```
- **⚠️ REQUER**: Credencial Slack + Canal configurado

---

## 🧪 Como Testar

### Teste Manual (antes de ativar o schedule)

1. **Acesse o workflow**: https://your-n8n-instance.example.com/workflow/your-workflow-id
2. **Clique em "Execute Workflow"** (botão no canto superior direito)
3. **Acompanhe a execução**:
   - ✅ Verde = Node executado com sucesso
   - ❌ Vermelho = Erro no node
4. **Clique em cada node** para ver os dados que passaram por ele
5. **Verifique**:
   - Se a planilha foi lida corretamente
   - Se o filtro funcionou (apenas slack_message_id vazios)
   - Se os dados foram inseridos na tabela de check
   - Se as notificações Slack foram enviadas

### Cenários de Teste

**Cenário 1: Cobranças válidas não comunicadas**
- Adicione uma linha na planilha com todos os campos preenchidos, EXCETO `slack_message_id`
- Execute o workflow
- ✅ Esperado: Cobrança inserida na tabela de check + notificação Slack enviada

**Cenário 2: Cobranças com dados incompletos**
- Adicione uma linha com `slack_message_id` vazio E algum campo obrigatório vazio (NF, valor ou parceiro)
- Execute o workflow
- ✅ Esperado: Alerta Slack enviado sobre dados incompletos

**Cenário 3: Nenhuma nova cobrança**
- Todas as linhas da planilha têm `slack_message_id` preenchido
- Execute o workflow
- ✅ Esperado: Workflow termina sem enviar notificações

---

## 🚀 Ativação

Após testar com sucesso:

1. **Ative o workflow**:
   - Clique no botão "Active" no canto superior direito
   - O status mudará para "Active"
2. **Confirme o schedule**:
   - Verifique que o trigger está configurado para 13h (America/Sao_Paulo)
3. **Monitore a primeira execução automática**:
   - Acompanhe no dia seguinte às 13h
   - Verifique os logs em "Executions" (menu lateral esquerdo)

---

## 🔍 Troubleshooting

### Erro: "Range is required for read operation"
**Causa**: O node Google Sheets precisa de um range especificado
**Solução**:
1. Abra o node "Ler Planilha de Cobranças"
2. Em "Options", adicione o campo "Range"
3. Deixe vazio para ler todas as linhas ou especifique (ex: `A2:H`)

### Erro: "Invalid credentials"
**Causa**: Credenciais Google Sheets ou Slack não configuradas ou expiradas
**Solução**:
1. Abra o node com erro
2. Clique em "Credential to connect with"
3. Teste a conexão ("Test Connection")
4. Se falhar, recrie a credencial

### Erro: "Channel not found"
**Causa**: Canal Slack não selecionado ou ID inválido
**Solução**:
1. Abra o node Slack
2. Certifique-se de que "Send Message To" está como "Channel"
3. Selecione o canal correto na lista

### Workflow não executa às 13h
**Causa**: Timezone incorreto ou workflow inativo
**Solução**:
1. Verifique que o workflow está "Active"
2. Abra "Schedule Trigger - 13h"
3. Confirme timezone: America/Sao_Paulo
4. Confirme cron: `0 13 * * *`

### Dados não estão sendo filtrados corretamente
**Causa**: Nome da coluna diferente na planilha
**Solução**:
1. Verifique que a coluna na planilha é exatamente `slack_message_id`
2. Se for diferente, atualize o node "Filtrar slack_message_id Vazio"
3. Altere a expressão para o nome correto: `{{ $json.nome_correto_da_coluna }}`

### Set node mostra "empty items"
**Causa**: Expressões do Set node não estão acessando os dados corretamente
**Solução**:
1. Verifique que os nodes anteriores estão retornando dados
2. Ajuste as expressões para usar `$('Nome do Node').item.json.campo`

---

## 📈 Monitoramento e KPIs

### Logs de Execução

Acesse **Executions** no menu lateral do n8n para ver:
- Histórico de execuções (sucesso/falha)
- Duração de cada execução
- Dados processados em cada node

### KPIs para Acompanhar

| KPI | Onde encontrar | Meta |
|---|---|---|
| Taxa de sucesso | Executions > Success rate | >99% |
| Cobranças duplicadas | Tabela de check (verificar duplicatas de NF) | 0/mês |
| Tempo de execução | Executions > Duration | <5 min |
| Alertas de dados incompletos | Canal Slack | <5% das cobranças |

### Dashboard Sugerido

Crie um dashboard (Google Sheets ou outra ferramenta) para monitorar:
- Total de cobranças verificadas por dia
- Novas cobranças identificadas por dia
- Taxa de dados incompletos
- Tempo médio de execução

---

## 🔄 Manutenção

### Semanal
- Revisar logs de execução
- Verificar alertas de dados incompletos
- Confirmar que tabela de check está sendo preenchida

### Mensal
- Analisar KPIs (duplicatas, tempo de execução, taxa de erro)
- Revisar mensagens Slack (ajustar formatação se necessário)
- Verificar se credenciais precisam ser renovadas

### Quando alterar a estrutura da planilha
1. **Pause o workflow** (desative temporariamente)
2. **Atualize os nodes** que referenciam as colunas alteradas
3. **Teste manualmente** antes de reativar
4. **Reative o workflow**

---

## 📚 Recursos Adicionais

- **Documentação n8n**: https://docs.n8n.io
- **Node Google Sheets**: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.googlesheets/
- **Node Slack**: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.slack/
- **Expressões n8n**: https://docs.n8n.io/code-examples/expressions/

---

## ✅ Checklist de Configuração

Use este checklist antes de ativar o workflow:

- [ ] Credencial Google Sheets criada e testada
- [ ] Credencial Slack criada e testada
- [ ] Node "Ler Planilha de Cobranças" configurado (Document + Sheet)
- [ ] Node "Inserir na Tabela de Check" configurado (Document + Sheet)
- [ ] Node "Alerta - Dados Incompletos" configurado (Canal Slack)
- [ ] Node "Notificar Novas Cobranças" configurado (Canal Slack)
- [ ] Workflow testado manualmente com sucesso
- [ ] Tabela de check recebeu dados de teste corretamente
- [ ] Notificações Slack foram recebidas
- [ ] Workflow ativado
- [ ] Primeira execução automática monitorada

---

**Criado em**: 2026-03-13
**Última atualização**: 2026-03-13
**Versão**: 1.0
