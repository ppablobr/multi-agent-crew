---
name: linkedin
description: >
  Use when the user asks to create LinkedIn posts, write social media content about AI/automation/tech,
  develop LinkedIn strategy, or create professional content for social networks. Examples include
  "write a LinkedIn post about X", "create a carousel about Y", "draft content for announcing Z",
  or any request involving professional social media content, especially focused on AI, LLMs,
  automation, n8n, or tech topics. Use this skill whenever the user mentions LinkedIn, posts,
  social content, or wants to share professional insights.
---

# Skill: LinkedIn — Orquestrador de Conteúdo

## Objetivo
Identificar o formato ideal de post e rotear para a sub-skill especializada correta.

---

## Processo

### 0. Carregar contexto (SEMPRE executar antes de qualquer outra coisa)

Antes de coletar insumos ou criar qualquer conteúdo, leia obrigatoriamente:

1. **`agents/linkedin/memory/history.md`** — posts já criados, temas usados, formatos que funcionaram. Evite repetir temas ou ganchos recentes.
2. **`agents/linkedin/memory/style-guide.md`** — preferências de estilo, tom e hashtags já validadas.
3. **`agents/n8n/memory/history.md`** — se o post envolve automação ou n8n, verifique workflows já criados que podem enriquecer o conteúdo com exemplos reais.
4. **`shared/memory/world.md`** — contexto global do projeto, temas em andamento e projetos ativos que podem ser fonte de conteúdo.

**Com base no que leu**, adapte:
- Se já foi criado um post sobre o mesmo tema → sugira um ângulo diferente ou complementar
- Se há um workflow n8n relevante no histórico → proponha usá-lo como base técnica do post
- Se o style-guide tem preferências definidas → aplique sem precisar perguntar

---

### 1. Coletar insumos mínimos (pergunte apenas o que não conseguir inferir)

- **Tema central:** Sobre o que é o post?
- **Ângulo/história:** Tem uma experiência pessoal, dado ou resultado por trás?
- **Público-alvo:** Técnico (devs, engenheiros) ou executivo/negócio?
- **CTA desejado:** Comentar, salvar, seguir, acessar algo?

---

### 2. Identificar o formato e rotear para a sub-skill correta

Com base no tema e insumos, determine o formato:

| Situação | Formato | Sub-skill |
|---|---|---|
| Há uma história pessoal, lição aprendida ou jornada | Narrativa | **`linkedin-narrative`** |
| Tema pode ser quebrado em itens enumerados (ferramentas, dicas, erros) | Lista | **`linkedin-list`** |
| Tema educativo com múltiplos conceitos para explicar visualmente | Carrossel | **`linkedin-carousel`** |

**Se o usuário não especificou o formato**, sugira o mais adequado e confirme antes de prosseguir.

**Ao rotear, informe o usuário qual sub-skill será usada:**
> "Vou usar a estrutura de **post narrativo** para este tema. Seguindo..."

---

### 3. Após criar o conteúdo — oferecer complementos

Ao concluir o post, sempre ofereça:

- **Imagem ou arte visual?** → Use a skill **`designer`** (sub-skill `canvas-design`) para criar um visual impactante para o post
- **Agendar publicação automaticamente?** → Use a skill **`n8n`** para criar um workflow de agendamento via LinkedIn API ou buffer

---

### 4. Salvar post na Google Sheets

Após o post ser aprovado pelo usuário, salve na planilha de controle via webhook do n8n:

1. Leia a **Webhook URL** em `agents/linkedin/memory/google-sheets-config.md`
2. Use o Bash tool para enviar um POST request com os dados do post:

```bash
curl -X POST https://your-n8n-instance.example.com/webhook/linkedin-post \
  -H "Content-Type: application/json" \
  -d '{
    "data": "YYYY-MM-DD",
    "formato": "Narrativa|Lista|Carrossel",
    "tema": "Título curto do post",
    "hook": "Primeira linha do post",
    "texto": "Corpo completo do post",
    "hashtags": "#tag1 #tag2 #tag3",
    "publico": "Técnico|Executivo|Misto",
    "status": "Rascunho|Aprovado|Publicado"
  }'
```

> Se o webhook retornar erro, verifique se o workflow está ativo em https://your-n8n-instance.example.com/workflow/your-workflow-id

---

### 5. Atualizar memória

Após entregar o post final, registre em **`agents/linkedin/memory/history.md`**:

```markdown
## YYYY-MM-DD — [Título/tema do post]
- **Formato:** Narrativa / Lista / Carrossel
- **Gancho usado:** [primeira linha do post]
- **Hashtags:** #tag1 #tag2
- **Google Sheets:** ✅ Salvo na planilha
- **Engajamento:** (preencher após publicar)
```
