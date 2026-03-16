# 🎯 Matriz de Responsabilidades dos Agentes

**Última atualização:** 2026-03-15
**Status:** Approved

Este documento define claramente as responsabilidades de cada agente no Multi-Agent Crew, eliminando ambiguidades e garantindo que cada agente tenha um domínio bem definido.

---

## 📋 Matriz Completa de Responsabilidades

| Tipo de tarefa | Agente responsável | Quando colaborar |
|---|---|---|
| **Post no LinkedIn** | LinkedIn Agent | + Designer (imagem), + n8n (workflow de agendamento) |
| **Criar workflow/automação** | n8n Agent | + Process Manager (se precisa mapear processo antes) |
| **Mapear processo (AS-IS/TO-BE)** | Process Manager | + Tech Docs Writer (para SOP formal) |
| **Escrever SOP formal** | Tech Docs Writer | + Process Manager (para mapeamento) |
| **Definir estratégia de projeto** | AI PM Agent | + Tech Docs Writer (para documentar formalmente) |
| **Escrever PRD/Roadmap formal** | Tech Docs Writer | + AI PM (para estratégia e conteúdo) |
| **Fluxograma de processo** | Process Manager (Excalidraw) | + Designer (se precisa ser super polido) |
| **Diagrama visual sofisticado** | Designer Agent | — |
| **Dashboard funcional (análise)** | Data Analytics Agent | + Designer (se precisa ser polido) |
| **Dashboard visual (UI/UX)** | Designer Agent | + Data Analytics (para dados reais) |
| **Análise de ROI/dados** | Data Analytics Agent | — |
| **Criar novo agente** | Agent Manager | + AI PM (roadmap), + DevOps (estrutura) |
| **Material educacional** | Education Agent | + n8n (workflows de exemplo), + Designer (diagramas) |
| **Organizar arquivos do projeto** | DevOps Agent | — |
| **Escrever ADR/RFC** | Tech Docs Writer | + AI PM ou n8n Agent (contexto técnico) |
| **Interface web/landing page** | Designer Agent | — |
| **Arte estática (poster, banner)** | Designer Agent | — |

---

## 🔍 Áreas com Sobreposição Resolvida

### 1. 📝 SOPs (Standard Operating Procedures)

**Divisão clara:**
- **Process Manager** → Mapeia o processo (AS-IS/TO-BE), cria fluxogramas, identifica gargalos
- **Tech Docs Writer** → Escreve o documento SOP formal e estruturado

**Fluxo:**
```
User pede SOP
→ Process Manager mapeia processo + diagrama Excalidraw
→ Tech Docs Writer formaliza em documento SOP estruturado
```

---

### 2. 🎨 Diagramas e Fluxogramas

**Divisão clara:**
- **Process Manager** → Fluxogramas de processo (BPMN, swimlanes) usando Excalidraw — foco em clareza funcional
- **Designer Agent** → Diagramas visuais sofisticados (infográficos, wireframes, visualizações) — foco em estética

**Quando usar:**
- Mapear fluxo operacional/processo? → **Process Manager**
- Criar infográfico bonito para apresentação? → **Designer**
- Diagrama técnico simples? → **Process Manager (Excalidraw)**
- Wireframe/mockup de produto? → **Designer**

---

### 3. 📊 PRDs e Roadmaps

**Divisão clara:**
- **AI PM Agent** → Pensa o projeto (define escopo, prioriza, alinha stakeholders, decide KPIs)
- **Tech Docs Writer** → Documenta o projeto (escreve PRD formal, estrutura roadmap)

**Fluxo:**
```
User pede PRD
→ AI PM define escopo, KPIs, prioridades, personas
→ Tech Docs Writer cria documento PRD estruturado
```

---

### 4. 📈 Dashboards

**Divisão clara:**
- **Data Analytics Agent** → Dashboards funcionais com dados reais (Plotly standalone HTML) — foco em insights
- **Designer Agent** → Dashboards visuais e polidos (React/Tailwind, design system) — foco em estética

**Quando usar:**
- Dashboard rápido para análise? → **Data Analytics**
- Dashboard bonito integrado ao produto? → **Designer**
- **Colaboração:** Data Analytics gera insights → Designer cria interface polida

---

## 🎯 Resumo por Agente

### 🎨 Designer Agent
**Domínio:** Design visual, interfaces, artefatos web
**O que faz:**
- Arte estática (posters, banners, designs para redes sociais)
- Interfaces web production-ready (landing pages, dashboards UI)
- Artefatos React complexos (apps multi-página)
- Diagramas visuais sofisticados (infográficos, wireframes)

**O que NÃO faz:**
- Fluxogramas de processo simples (usa Process Manager)
- Análise de dados para dashboards (usa Data Analytics)

---

### 🔵 LinkedIn Agent
**Domínio:** Conteúdo e engajamento sobre IA no LinkedIn
**O que faz:**
- Posts narrativos, carrosséis, threads educativas
- Case studies de projetos de IA
- Comunicação técnica acessível

**O que NÃO faz:**
- Criar as artes/imagens (usa Designer)
- Construir workflows de agendamento (usa n8n)

---

### ⚙️ n8n Agent
**Domínio:** Workflows, automações e integrações
**O que faz:**
- Criar/editar workflows via MCP tools
- Validar e testar automações
- Implementar AI Agents no n8n

**O que NÃO faz:**
- Mapear processos antes de automatizar (usa Process Manager)
- Criar interfaces para workflows (usa Designer)

---

### 🚀 AI Project Manager
**Domínio:** Gestão de projetos de IA
**O que faz:**
- Definir escopo e prioridades
- Criar roadmaps estratégicos
- Planejar sprints e definir KPIs
- Gerenciar riscos e stakeholders

**O que NÃO faz:**
- Escrever documentação formal de PRDs (usa Tech Docs Writer)
- Criar dashboards de métricas (usa Data Analytics ou Designer)

---

### 🗂️ Process Manager
**Domínio:** Desenho e documentação de processos
**O que faz:**
- Mapear processos AS-IS e TO-BE
- Criar fluxogramas com Excalidraw
- Identificar gargalos e oportunidades
- Definir RACI e KPIs de processo

**O que NÃO faz:**
- Escrever SOP formal final (usa Tech Docs Writer)
- Criar diagramas super polidos para apresentação (usa Designer)

---

### 🎓 Education Agent
**Domínio:** Materiais educacionais sobre IA e automação
**O que faz:**
- Criar trilhas de aprendizado
- Preparar mentorias e workshops
- Ensinar prompt engineering e criação de agentes
- Desenvolver exercícios práticos

**O que NÃO faz:**
- Criar os workflows de exemplo (usa n8n)
- Criar diagramas visuais (usa Designer ou Process Manager)

---

### 📊 Data Analytics Agent
**Domínio:** Análise de dados, ROI, insights
**O que faz:**
- EDA (Exploratory Data Analysis)
- Cálculos de ROI e métricas de impacto
- Dashboards funcionais com Plotly
- Testes estatísticos e storytelling com dados

**O que NÃO faz:**
- Criar dashboards visuais polidos (usa Designer)
- Definir quais métricas acompanhar (usa AI PM)

---

### 🔧 DevOps Agent
**Domínio:** Organização de projetos e estrutura
**O que faz:**
- Auditar estrutura de diretórios
- Mover arquivos para locais corretos
- Validar convenções de nomenclatura
- Limpar arquivos temporários

**O que NÃO faz:**
- Criar estrutura de novos agentes (usa Agent Manager)
- Reorganizar sem entender o contexto (sempre pergunta)

---

### 🧬 Agent Manager
**Domínio:** Criação e gestão de agentes
**O que faz:**
- Criar novos agentes via skill creator
- Auditar e evoluir agentes existentes
- Definir padrões do sistema
- Medir performance com evals

**O que NÃO faz:**
- Criar skills manualmente (SEMPRE usa skill creator)
- Aprovar agentes sem rodar casos de teste (mínimo 3)

---

### 📝 Tech Docs Writer
**Domínio:** Documentação técnica estruturada
**O que faz:**
- Escrever PRDs, ADRs, SOPs, RFCs
- Estruturar roadmaps e kanbans
- Criar user stories com critérios de aceite
- Documentar decisões arquiteturais

**O que NÃO faz:**
- Definir estratégia de projeto (usa AI PM)
- Mapear processos (usa Process Manager)
- Criar diagramas visuais (usa Designer ou Process Manager)

---

## 🔄 Fluxos de Colaboração Comuns

### Documentar um processo
```
1. Process Manager mapeia AS-IS/TO-BE + diagrama Excalidraw
2. Tech Docs Writer cria SOP formal estruturado
3. (Opcional) Education Agent cria material de treinamento
4. (Opcional) n8n Agent automatiza partes do processo
```

### Lançar uma feature
```
1. AI PM define escopo, KPIs, prioridades
2. Tech Docs Writer cria PRD formal
3. Designer cria mockups/interfaces
4. n8n Agent implementa automações
5. Data Analytics mede impacto pós-lançamento
6. LinkedIn Agent comunica o lançamento
```

### Criar dashboard de métricas
```
1. AI PM define quais métricas acompanhar
2. Data Analytics cria dashboard funcional (Plotly)
3. (Opcional) Designer polishes UI para integração no produto
```

### Criar novo agente
```
1. Agent Manager cria via skill creator + AGENT.md
2. DevOps valida estrutura de diretórios
3. AI PM integra ao roadmap (se aplicável)
4. LinkedIn Agent comunica novidade (se relevante)
```

---

## 📏 Regras Gerais

1. **Quando em dúvida, consulte esta matriz** antes de escolher o agente
2. **Cada agente tem um domínio claro** — evite invadir responsabilidades
3. **Colaboração > Sobreposição** — trabalhe junto quando a tarefa cruza domínios
4. **Sempre documente** decisões de responsabilidade em `shared/memory/world.md`
5. **Atualize este documento** se novas ambiguidades surgirem

---

_Documento criado em 2026-03-15 durante revisão de papéis dos agentes_
