# SOP: Verificação Diária de Cobranças de Parceiros

**Versão**: 1.0
**Data de Criação**: 2026-03-14
**Última Atualização**: 2026-03-14
**Autor**: Tech Docs Writer Agent
**Status**: Ativo
**Classificação**: Processo Operacional — Financeiro

---

## 📋 Sumário Executivo / TL;DR

Este SOP documenta o processo automatizado de verificação diária de cobranças de parceiros do ecommerce, garantindo que cada cobrança seja comunicada apenas uma vez (zero duplicatas) e que todas sejam registradas na tabela de controle.

**Frequência**: Diária, às 13h (automatizado via n8n)
**Tempo estimado**: 2-3 minutos (100% automatizado)
**Responsável principal**: Time Financeiro (monitoramento)
**Sistema**: Workflow n8n + Google Sheets + Slack

---

## 🎯 1. Objetivo

### Para que serve este procedimento

- **Garantir comunicação única**: Cada cobrança de parceiro é comunicada apenas uma vez, eliminando duplicatas
- **Controle centralizado**: Todos os registros de cobranças verificadas ficam na "tabela de check de cobrança"
- **Rastreabilidade completa**: Logs de execução permitem auditorias e troubleshooting
- **Operação sem falhas humanas**: Automação reduz erros de ~15-20% para <1%
- **Liberar tempo do time**: Time Financeiro foca em análise estratégica, não em verificação manual

### Benefícios esperados

- ⏱️ **Economia de tempo**: ~25 min/dia → ~9h/mês economizadas
- 💰 **Redução de custo**: ~R$ 450/mês (tempo operacional)
- 🎯 **Redução de duplicatas**: De 15-20% → <1%
- 📈 **Cobertura**: De 70% → 100% das cobranças verificadas
- ✅ **Confiança dos parceiros**: Zero reclamações por cobranças duplicadas

---

## 👥 2. Responsáveis (RACI)

| Atividade | Responsible (R) | Accountable (A) | Consulted (C) | Informed (I) |
|---|---|---|---|---|
| **Manutenção da planilha de cobranças** | Time Financeiro | Gestor Financeiro | - | Time Comercial |
| **Execução da automação** | Workflow n8n (automatizado) | Gestor de Automação | - | Time Financeiro |
| **Monitoramento de alertas Slack** | Time Financeiro | Gestor Financeiro | - | - |
| **Resolução de erros técnicos** | Time de Automação | Gestor de Automação | Time Financeiro | Gestor Comercial |
| **Validação mensal de KPIs** | Gestor Financeiro | Diretor Financeiro | Time Financeiro | Gestor de Automação |
| **Atualização deste SOP** | Gestor de Automação | Diretor de Processos | Time Financeiro | Todos os stakeholders |

### Quem faz o quê:

- **Time Financeiro**: Monitora notificações Slack, corrige dados incompletos na planilha, valida resultados semanalmente
- **Gestor Financeiro**: Aprovador final do processo, responde por KPIs e resultados
- **Time de Automação**: Mantém workflow funcionando, resolve erros técnicos, atualiza configurações
- **Gestor de Automação**: Responsável pela saúde técnica do workflow, SLA de resolução de incidentes

---

## ✅ 3. Pré-requisitos

Antes de usar este SOP, certifique-se de que:

### 3.1 Infraestrutura Técnica

- [ ] **Workflow n8n criado e ativo**
  - ID do Workflow: `your-workflow-id`
  - URL: [https://your-n8n-instance.example.com/workflow/your-workflow-id](https://your-n8n-instance.example.com/workflow/your-workflow-id)
  - Status: Ativo

- [ ] **Credenciais configuradas**
  - Google Sheets OAuth2 (para leitura e escrita)
  - Slack API (para notificações)

- [ ] **Google Sheets estruturada**
  - Planilha de cobranças com colunas:
    - `data de análise`, `NF`, `valor`, `parceiro`, `data de emissão`, `data de vencimento`, `boleto url`, `slack_message_id`
  - Tabela de check de cobrança (destino dos registros)

- [ ] **Canais Slack configurados**
  - Canal para alertas de dados incompletos (ex: `#financeiro`)
  - Canal para notificações de sucesso (ex: `#cobrancas`)

### 3.2 Acesso e Permissões

- [ ] Time Financeiro tem acesso à planilha de cobranças (Google Sheets)
- [ ] Time Financeiro está no canal Slack de notificações
- [ ] Time de Automação tem acesso ao n8n (https://your-n8n-instance.example.com)
- [ ] Gestor Financeiro tem acesso à tabela de check de cobrança

### 3.3 Conhecimento Necessário

- Time Financeiro deve saber:
  - Como interpretar notificações Slack
  - Como corrigir dados incompletos na planilha
  - Como escalar problemas para Time de Automação

- Time de Automação deve saber:
  - Como acessar e editar workflows no n8n
  - Como verificar logs de execução
  - Como resolver erros técnicos (ver seção 7 deste SOP)

---

## 🔄 4. Procedimento Passo a Passo

### 4.1 Configuração Inicial (apenas primeira vez)

Se o workflow ainda não foi configurado, siga este checklist (geralmente executado pelo Time de Automação):

#### Passo 1: Configurar Credenciais Google Sheets

1. Acesse o workflow: [https://your-n8n-instance.example.com/workflow/your-workflow-id](https://your-n8n-instance.example.com/workflow/your-workflow-id)
2. Clique no node "**Ler Planilha de Cobranças**"
3. Em "Credential to connect with", clique em "Create New"
4. Selecione "Google Sheets OAuth2 API"
5. Siga o fluxo de autenticação do Google
6. **Repita** para o node "**Inserir na Tabela de Check**" (pode reutilizar a mesma credencial)

#### Passo 2: Configurar Planilha de Cobranças

No node "**Ler Planilha de Cobranças**":

1. **Document**: Selecione a planilha de cobranças na lista
2. **Sheet**: Selecione a aba que contém as cobranças
3. **Range**: Deixe vazio para ler todas as linhas ou especifique (ex: `A2:H`)

**Validação**: Execute manualmente (botão "Execute Workflow") e verifique se as cobranças aparecem no node

#### Passo 3: Configurar Tabela de Check

No node "**Inserir na Tabela de Check**":

1. **Document**: Selecione a planilha de destino (tabela de check)
2. **Sheet**: Selecione a aba de destino
3. **Columns to Match On**: Deixe vazio (sempre adiciona nova linha)

**Validação**: Execute manualmente e verifique se uma linha foi inserida na tabela de check

#### Passo 4: Configurar Notificações Slack

**No node "Alerta - Dados Incompletos":**

1. Clique no node
2. Em "Credential to connect with", clique em "Create New"
3. Selecione "Slack API"
4. Insira o token do Slack
5. Em "Channel", selecione o canal de alertas (ex: `#financeiro`)

**No node "Notificar Novas Cobranças":**

1. Repita o processo (pode reutilizar a mesma credencial)
2. Selecione o canal de notificações de sucesso (ex: `#cobrancas`)

**Validação**: Execute manualmente e verifique se as mensagens chegaram no Slack

#### Passo 5: Teste Completo Antes de Ativar

Antes de ativar o schedule diário, execute estes testes:

**Cenário 1: Cobranças válidas não comunicadas**

1. Adicione uma linha de teste na planilha:
   - Preencha todos os campos obrigatórios (NF, valor, parceiro, datas, boleto url)
   - Deixe `slack_message_id` **vazio**
2. Execute o workflow manualmente (botão "Execute Workflow")
3. ✅ **Esperado**:
   - Cobrança inserida na tabela de check
   - Notificação Slack recebida no canal de sucesso
   - Todos os nodes verdes (sem erros)

**Cenário 2: Cobranças com dados incompletos**

1. Adicione uma linha de teste com `slack_message_id` vazio E algum campo obrigatório vazio (ex: NF ou valor)
2. Execute o workflow
3. ✅ **Esperado**:
   - Alerta Slack enviado no canal de alertas
   - Cobrança NÃO inserida na tabela de check

**Cenário 3: Nenhuma nova cobrança**

1. Preencha `slack_message_id` em todas as linhas da planilha
2. Execute o workflow
3. ✅ **Esperado**:
   - Workflow termina sem enviar notificações
   - Nenhum erro exibido

#### Passo 6: Ativar o Workflow

Após todos os testes passarem:

1. Clique no botão "**Active**" no canto superior direito do workflow
2. Status mudará para "Active" (verde)
3. Confirme que o schedule está configurado para **13h (America/Sao_Paulo)**

---

### 4.2 Monitoramento Diário (Operação Rotineira)

A partir daqui, o workflow roda automaticamente todos os dias às 13h. O Time Financeiro deve:

#### Segunda a Sexta, às 13h05 (logo após a execução)

1. **Verifique o canal Slack de notificações** (ex: `#cobrancas`)

   - **Se receber notificação de sucesso** (✅ Verificação de Cobranças Concluída):
     - ✅ Processo executou com sucesso
     - Anote a quantidade de novas cobranças identificadas
     - Nenhuma ação necessária

   - **Se NÃO receber notificação**:
     - ⚠️ Pode ser que não havia cobranças novas (normal)
     - OU pode ser um problema técnico
     - **Ação**: Acesse os logs de execução (ver seção 4.3) para confirmar

2. **Verifique o canal Slack de alertas** (ex: `#financeiro`)

   - **Se receber alerta de dados incompletos** (⚠️):
     - Abra a planilha de cobranças
     - Localize a cobrança mencionada no alerta (NF, parceiro)
     - Corrija os campos vazios (NF, valor, parceiro)
     - **Nota**: Na próxima execução (dia seguinte às 13h), a cobrança será processada corretamente

#### Uma vez por semana (sexta-feira, fim do dia)

1. **Valide a tabela de check de cobrança**:
   - Abra a tabela de check
   - Confirme que há registros novos da semana
   - Verifique se não há duplicatas (mesma NF registrada 2x)

   ✅ **Esperado**: Novos registros diários, sem duplicatas

2. **Revise os alertas da semana**:
   - Revise mensagens de alertas no Slack
   - Confirme que dados incompletos foram corrigidos
   - Se houver alertas recorrentes → escalar para Gestor Financeiro

---

### 4.3 Como Verificar Logs de Execução (quando necessário)

Se você precisa investigar se o workflow rodou ou se houve algum erro:

1. Acesse o n8n: [https://your-n8n-instance.example.com](https://your-n8n-instance.example.com)
2. No menu lateral esquerdo, clique em "**Executions**"
3. Localize a execução do workflow "Verificação Diária de Cobranças"
   - **Data/hora**: Deve mostrar execuções às 13h
   - **Status**:
     - ✅ **Verde (Success)**: Executou sem erros
     - ❌ **Vermelho (Error)**: Houve um erro técnico → escalar para Time de Automação
     - ⏸️ **Cinza (Waiting)**: Aguardando algo (não deve acontecer neste workflow)
4. Clique na execução para ver detalhes:
   - Cada node mostra quantos itens processou
   - Se houver erro, o node vermelho mostra a mensagem de erro
5. **Se encontrar erro**: Tire um print da tela e envie para Time de Automação

---

### 4.4 Como Agir Quando Receber Alertas Slack

#### Alerta: "Cobrança com dados incompletos detectada"

**O que significa**: O workflow encontrou uma cobrança na planilha com campos obrigatórios vazios.

**O que fazer**:

1. Abra a planilha de cobranças
2. Localize a linha mencionada no alerta:
   - **NF**: [número da nota fiscal, se disponível]
   - **Parceiro**: [nome do parceiro, se disponível]
   - **Valor**: [valor, se disponível]
3. Preencha os campos que estão vazios:
   - Se NF está vazio → consulte a nota fiscal e preencha
   - Se valor está vazio → consulte o valor correto e preencha
   - Se parceiro está vazio → identifique o parceiro e preencha
4. Salve a planilha
5. **Nota**: Na próxima execução (dia seguinte às 13h), a cobrança será processada automaticamente

**Quando escalar**: Se você não tem as informações necessárias para preencher → escalar para Gestor Financeiro

---

#### Alerta: "Erro no workflow" (mensagem de erro técnico)

**O que significa**: Houve uma falha técnica no workflow (ex: credenciais expiradas, Google Sheets indisponível).

**O que fazer**:

1. **NÃO tente consertar você mesmo** (a menos que você seja do Time de Automação)
2. Tire um print da mensagem de erro
3. Envie para o Time de Automação via Slack, e-mail ou sistema de tickets
4. **Informe**:
   - Data e hora do erro
   - Print da mensagem
   - O que você estava fazendo (se aplicável)
5. Time de Automação irá investigar e resolver

**SLA de resposta**: Time de Automação deve responder em até 2 horas úteis

---

### 4.5 Como Resolver Problemas Comuns (Time Financeiro)

#### Problema: "Recebi a notificação de sucesso, mas a tabela de check não foi atualizada"

**Diagnóstico**:
1. Verifique se você está olhando a **planilha correta** (tabela de check, não a planilha de cobranças)
2. Verifique se está na **aba correta** da planilha
3. Recarregue a página (Ctrl+R ou Cmd+R)

**Solução**: Se ainda não aparecer → escalar para Time de Automação

---

#### Problema: "Não recebi nenhuma notificação hoje às 13h"

**Diagnóstico**:
1. Pode ser que não havia cobranças novas (normal)
2. OU o workflow pode não ter executado

**Solução**:
1. Verifique os logs de execução (ver seção 4.3)
2. Se não houver execução às 13h de hoje → escalar para Time de Automação

---

#### Problema: "Recebi alerta de dados incompletos, mas a linha parece completa"

**Diagnóstico**:
1. Verifique se os campos **NF**, **valor** e **parceiro** estão preenchidos (são os únicos obrigatórios)
2. Pode haver um espaço vazio ou caractere invisível

**Solução**:
1. Copie o valor da célula e cole novamente (remove caracteres invisíveis)
2. Salve a planilha
3. Se persistir → escalar para Time de Automação

---

## ✅ 5. Checklist de Verificação

### 5.1 Checklist Diário (Time Financeiro)

Execute todos os dias, logo após 13h05:

- [ ] Verificar canal Slack de notificações (ex: `#cobrancas`)
  - [ ] Se houver notificação de sucesso → anotar quantidade de novas cobranças
  - [ ] Se não houver notificação → verificar logs de execução

- [ ] Verificar canal Slack de alertas (ex: `#financeiro`)
  - [ ] Se houver alerta de dados incompletos → corrigir na planilha
  - [ ] Se houver alerta de erro técnico → escalar para Time de Automação

**Tempo estimado**: 2-3 minutos/dia

---

### 5.2 Checklist Semanal (Time Financeiro)

Execute toda sexta-feira, fim do dia:

- [ ] Abrir tabela de check de cobrança
- [ ] Validar que há novos registros da semana (segunda a sexta)
- [ ] Verificar se não há duplicatas (mesma NF registrada 2x)
- [ ] Revisar alertas de dados incompletos da semana
  - [ ] Confirmar que foram corrigidos
  - [ ] Se houver alertas recorrentes → escalar para Gestor Financeiro
- [ ] (Opcional) Anotar insights ou padrões observados

**Tempo estimado**: 10-15 minutos/semana

---

### 5.3 Checklist Mensal (Gestor Financeiro)

Execute no último dia útil de cada mês:

- [ ] Revisar KPIs do mês (ver seção 6)
- [ ] Validar que não houve cobranças duplicadas
- [ ] Revisar taxa de alertas de dados incompletos
  - [ ] Se >5% → investigar causa raiz e ajustar processo de entrada de dados
- [ ] Verificar tempo médio de execução do workflow
  - [ ] Se >5 min → escalar para Time de Automação para otimizar
- [ ] Verificar taxa de sucesso do workflow
  - [ ] Se <99% → reunir com Time de Automação para entender falhas
- [ ] (Opcional) Atualizar este SOP se houver mudanças no processo

**Tempo estimado**: 30-45 minutos/mês

---

## 📊 6. KPIs para Acompanhar

### 6.1 KPIs Principais

| KPI | Meta | Como Medir | Frequência | Responsável |
|---|---|---|---|---|
| **Cobranças duplicadas** | 0/mês | Verificar duplicatas de NF na tabela de check | Mensal | Gestor Financeiro |
| **Taxa de sucesso do workflow** | >99% | Logs de execução no n8n (Success/Error ratio) | Mensal | Time de Automação |
| **Tempo de execução** | <5 min | Duração média nas execuções do n8n | Mensal | Time de Automação |
| **Taxa de alertas de dados incompletos** | <5% | (Alertas / Total de cobranças) × 100 | Mensal | Gestor Financeiro |
| **Cobertura de verificação** | 100% | Todas as cobranças verificadas diariamente | Semanal | Time Financeiro |

### 6.2 Como Acessar os Dados para KPIs

#### 6.2.1 Cobranças Duplicadas

1. Abra a tabela de check de cobrança
2. Use a função do Google Sheets para encontrar duplicatas:
   - Selecione a coluna `NF`
   - Menu: Dados → Formatar como tabela → Filtrar
   - Ordene por NF e procure valores repetidos
3. **Meta**: 0 duplicatas/mês

#### 6.2.2 Taxa de Sucesso do Workflow

1. Acesse o n8n: [https://your-n8n-instance.example.com](https://your-n8n-instance.example.com)
2. Menu lateral: **Executions**
3. Filtre pelo workflow "Verificação Diária de Cobranças"
4. Conte:
   - **Total de execuções no mês** (deve ser ~22-23, considerando dias úteis)
   - **Execuções com sucesso** (verde)
   - **Execuções com erro** (vermelho)
5. **Fórmula**: (Sucesso / Total) × 100
6. **Meta**: >99%

#### 6.2.3 Tempo de Execução

1. No n8n, em **Executions**, clique em uma execução
2. Veja "Duration" no topo da tela
3. Anote a duração de 5-10 execuções do mês
4. Calcule a média
5. **Meta**: <5 min

#### 6.2.4 Taxa de Alertas de Dados Incompletos

1. No canal Slack de alertas (ex: `#financeiro`), conte os alertas de "dados incompletos" no mês
2. Na tabela de check, conte o total de cobranças verificadas no mês
3. **Fórmula**: (Alertas / Total de cobranças) × 100
4. **Meta**: <5%

---

### 6.3 Dashboard Sugerido (opcional, mas recomendado)

Crie uma planilha de KPIs mensais para acompanhamento:

| Mês | Cobranças Verificadas | Cobranças Duplicadas | Taxa de Sucesso | Tempo Médio | Alertas de Dados Incompletos | Taxa de Alertas |
|---|---|---|---|---|---|---|
| Jan/2026 | 450 | 0 | 100% | 2.5 min | 15 | 3.3% |
| Fev/2026 | 480 | 0 | 99.5% | 2.8 min | 20 | 4.2% |
| Mar/2026 | ... | ... | ... | ... | ... | ... |

**Benefício**: Visualizar tendências e identificar degradações antes que se tornem problemas críticos.

---

## 🚨 7. Contatos e Escalação

### 7.1 Quem Contatar para Cada Situação

| Problema | Quem Contatar | Como Contatar | SLA de Resposta |
|---|---|---|---|
| **Dados incompletos na planilha** | Time Financeiro | Interno (Slack #financeiro) | Imediato |
| **Erro técnico no workflow** | Time de Automação | Slack #automacao ou ticket | 2 horas úteis |
| **KPIs fora da meta** | Gestor Financeiro | E-mail ou reunião | 1 dia útil |
| **Necessidade de atualizar SOP** | Gestor de Automação | E-mail ou Slack | 3 dias úteis |
| **Incidente crítico** (workflow parado >1 dia) | Gestor de Automação + Diretor Financeiro | Telefone + Slack | Imediato |

### 7.2 Matriz de Escalação

**Nível 1** (Time Financeiro):
- Corrige dados incompletos
- Monitora notificações Slack
- Valida resultados semanalmente

**Nível 2** (Gestor Financeiro):
- Investiga alertas recorrentes
- Analisa KPIs mensais
- Aprova mudanças no processo

**Nível 3** (Time de Automação):
- Resolve erros técnicos
- Otimiza performance do workflow
- Atualiza configurações no n8n

**Nível 4** (Gestor de Automação):
- Resolve incidentes críticos
- Aprova mudanças estruturais no workflow
- Garante SLA de disponibilidade

**Nível 5** (Diretor Financeiro + Diretor de Processos):
- Aprovam mudanças estratégicas no processo
- Tomam decisões sobre investimentos em melhorias

---

## 📎 8. Anexos

### 8.1 Links Úteis

- **Workflow n8n**: [https://your-n8n-instance.example.com/workflow/your-workflow-id](https://your-n8n-instance.example.com/workflow/your-workflow-id)
- **Documentação do Workflow**: `/shared/workflows/verificacao-cobrancas-workflow.md`
- **Documentação do Processo (AS-IS → TO-BE)**: `/shared/processes/cobranca-parceiros-ecommerce.md`
- **Documentação n8n (oficial)**: [https://docs.n8n.io](https://docs.n8n.io)

### 8.2 Arquivos Relacionados

- **Fluxograma AS-IS**: (a ser criado via excalidraw-diagram)
- **Fluxograma TO-BE**: (a ser criado via excalidraw-diagram)
- **Planilha de cobranças**: (Google Sheets — link a ser adicionado)
- **Tabela de check de cobrança**: (Google Sheets — link a ser adicionado)

### 8.3 Glossário

- **NF**: Nota Fiscal
- **slack_message_id**: Campo na planilha que indica se a cobrança já foi comunicada ao parceiro (se vazio = não comunicada)
- **Tabela de check**: Planilha de destino onde ficam registradas todas as cobranças verificadas
- **Node**: Componente individual do workflow n8n (ex: "Ler Planilha", "Enviar Slack")
- **Execution**: Uma execução completa do workflow (acontece diariamente às 13h)
- **Workflow**: Conjunto de nodes que automatiza o processo de verificação

---

## 🔄 9. Histórico de Versões

| Versão | Data | Autor | Mudanças |
|---|---|---|---|
| 1.0 | 2026-03-14 | Tech Docs Writer Agent | SOP criado com base no processo TO-BE e workflow n8n documentado |

---

## 📝 10. Aprovação

| Papel | Nome | Assinatura | Data |
|---|---|---|---|
| **Elaborador** | Tech Docs Writer Agent | (assinatura digital) | 2026-03-14 |
| **Revisor** | Gestor Financeiro | (pendente) | (pendente) |
| **Revisor** | Gestor de Automação | (pendente) | (pendente) |
| **Aprovador** | Diretor Financeiro | (pendente) | (pendente) |

---

**Próxima revisão programada**: 2026-06-14 (3 meses após criação)

---

## 📞 Suporte

Para dúvidas sobre este SOP:
- **Time Financeiro**: Consultar Gestor Financeiro
- **Time de Automação**: Consultar Gestor de Automação
- **Sugestões de melhoria**: Enviar para Gestor de Automação via Slack #automacao
