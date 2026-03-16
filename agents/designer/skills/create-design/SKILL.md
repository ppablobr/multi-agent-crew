---
name: create-design
description: >
  Skill orquestradora para criação de designs visuais, interfaces frontend e artefatos web.
  Use this skill whenever the user mentions: design, poster, banner, landing page, dashboard,
  interface, UI, visual, theme, style, artifact, component, website, or any request involving
  visual creation. Even if they don't explicitly say "design", use this skill when they want
  to create something visual like "make an image for my LinkedIn post", "build a page for my
  product", "create a dashboard", "style this component", or "make this look better". This skill
  orchestrates canvas-design (static art), frontend-design (web interfaces), theme-factory
  (applying themes), and web-artifacts-builder (complex React apps).
---

# Create Design Skill

Skill orquestradora para criação de designs visuais, interfaces frontend e artefatos web. Esta skill coordena o uso de quatro sub-skills especializadas: canvas-design, frontend-design, theme-factory e web-artifacts-builder.

## 📋 Quando usar

Use esta skill quando o usuário pedir:
- **Arte estática**: "Cria um pôster", "Desenha um banner", "Faz uma arte para Instagram"
- **Interfaces web**: "Cria uma landing page", "Desenha um dashboard", "Faz um componente React"
- **Aplicação de tema**: "Aplica o tema dark mode", "Usa a paleta azul/laranja"
- **Artefatos complexos**: "Cria um app multi-página", "Faz uma ferramenta interativa"

## 🔧 Skills disponíveis

### 1. canvas-design
**Usar para**: Designs estáticos (PNG/PDF) como pôsteres, arte para redes sociais, documentos visuais

**Características**:
- Output: Arquivo PNG ou PDF
- Design original (não copia artistas existentes)
- Filosofia de design aplicada
- Ideal para: Posts, banners, slides, documentos

**Exemplo de uso**:
> "Cria um pôster sobre IA Generativa com estilo minimalista e paleta azul/roxo"

### 2. frontend-design
**Usar para**: Interfaces web production-grade (componentes, páginas, layouts)

**Características**:
- Output: Código HTML/CSS/JS ou React
- Design distinto e polido (evita estética genérica de IA)
- Ideal para: Landing pages, componentes, dashboards, websites

**Exemplo de uso**:
> "Cria uma landing page para produto SaaS com seção hero, features e CTA"

### 3. theme-factory
**Usar para**: Aplicar temas visuais a artefatos existentes

**Características**:
- 10 temas pré-definidos com cores/fontes
- Pode gerar temas customizados
- Aplica a slides, docs, landing pages, etc.
- Ideal para: Estilizar artefatos já criados

**Exemplo de uso**:
> "Aplica o tema 'oceanic' no dashboard que acabei de criar"

### 4. web-artifacts-builder
**Usar para**: Artefatos React complexos com múltiplos componentes

**Características**:
- Usa React + Tailwind + shadcn/ui
- Suporta routing e state management
- Ideal para: Apps multi-página, ferramentas interativas complexas

**Exemplo de uso**:
> "Cria um gerenciador de tarefas com lista, filtros e modal de edição"

## 🎯 Fluxo de trabalho

### 0. Carregar contexto (SEMPRE executar antes de qualquer outra coisa)

Antes de clarificar requisitos ou iniciar qualquer criação, leia obrigatoriamente:

1. **`agents/designer/memory/design-library.md`** — designs já criados: paletas usadas, tipografias, decisões visuais. Mantenha consistência com o trabalho anterior.
2. **`agents/designer/memory/history.md`** — histórico de projetos e preferências do usuário sobre estilo visual.
3. **`shared/memory/world.md`** — contexto global: se há brand guidelines, projetos ativos com identidade visual definida.

**Com base no que leu**, adapte o processo:
- Se já existe identidade visual definida → use a paleta/tipografia estabelecida sem precisar perguntar
- Se o design é para suportar um post LinkedIn → consulte `agents/linkedin/memory/history.md` para entender o contexto do conteúdo

### 1. Clarificar requisitos
Sempre pergunte:
- **Contexto**: Para quê? Qual plataforma? Quem é o público?
- **Estilo**: Minimalista, colorido, profissional, criativo?
- **Conteúdo**: Que textos, imagens ou dados incluir?
- **Restrições**: Dimensões, cores obrigatórias, brand guidelines?

### 2. Escolher a skill certa
- Estático? → `canvas-design`
- Código frontend simples? → `frontend-design`
- React complexo? → `web-artifacts-builder`
- Só precisa mudar cores/tema? → `theme-factory`

### 3. Criar o design
Execute a skill apropriada com contexto completo.

### 4. Documentar na memória
Salve em `design-library.md`:
- Screenshot ou link do design
- Paleta de cores usada
- Tipografia escolhida
- Decisões importantes
- Reutilização possível

## 💡 Boas práticas

### Design principles
- **Hierarquia visual clara**: títulos > subtítulos > corpo
- **Whitespace generoso**: não encher todos os espaços
- **Consistência**: mesma paleta, tipografia, espaçamentos
- **Contraste adequado**: WCAG AA mínimo (4.5:1 para texto)
- **Mobile-first**: começar pelo layout mobile

### Performance
- Imagens otimizadas (WebP quando possível)
- CSS eficiente (evitar !important)
- Lazy loading para imagens below-the-fold
- Minificar CSS/JS em produção

### Acessibilidade
- Atributos `alt` descritivos em imagens
- Labels em campos de formulário
- Navegação por teclado funcional
- ARIA roles quando necessário
- Testes com screen readers

### Colaboração
- **LinkedIn Agent**: Pede briefing de tom e mensagem antes de criar arte
- **n8n Agent**: Entende estrutura de dados antes de criar interface
- **AI PM**: Alinha KPIs antes de criar dashboards
- **Process Manager**: Valida fluxo antes de criar diagramas

## 📊 Checklist de qualidade

Antes de entregar qualquer design:

- [ ] Atende aos requisitos do usuário
- [ ] Estilo visual consistente e profissional
- [ ] Responsivo (se aplicável)
- [ ] Contraste adequado (WCAG AA+)
- [ ] Performance otimizada
- [ ] Código limpo e comentado (se aplicável)
- [ ] Documentado em `design-library.md`
- [ ] Testado em viewport mobile (se web)
- [ ] Sem violações de copyright
- [ ] Preview mostrado ao usuário antes de finalizar

## 🔗 Recursos úteis

- Paletas de cores: Coolors, Adobe Color
- Tipografia: Google Fonts, Font Pair
- Ícones: Lucide, Heroicons, Feather
- Imagens: Unsplash, Pexels (com atribuição)
- Inspiração: Dribbble, Behance, Awwwards

---

**Lembre-se**: Design não é só estética, é resolver problemas de comunicação visual. Pergunte sempre "O que este design precisa comunicar?" antes de começar.

---

## Skills complementares

| Situação | Skill |
|---|---|
| Design é para um post LinkedIn (arte, carrossel visual) | **`linkedin`** → alinhe o conteúdo antes de criar o visual |
| Design é um dashboard de KPIs ou métricas de projeto | **`ai-pm`** → obtenha quais métricas e estrutura antes de criar |
| Design é um diagrama de processo | **`process-manager`** → obtenha o mapeamento AS-IS antes de criar o diagrama visual |
| Design precisa ser publicado ou anunciado | **`linkedin`** → criar post anunciando o novo design/interface |
