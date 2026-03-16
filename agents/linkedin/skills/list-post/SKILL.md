---
name: linkedin-list
description: >
  Sub-skill do LinkedIn Agent para criar posts em formato de lista. Use when the content can be
  broken into enumerable items: tools, tips, mistakes, lessons, steps, or rankings.
  Examples: "5 tools I use daily", "3 mistakes to avoid", "my top AI workflows", "7 lessons from X".
  This skill is typically invoked by the linkedin orchestrator skill, not directly.
---

# Sub-skill: Post de Lista

## Quando usar
Conteúdo que se beneficia de enumeração: ferramentas, dicas, erros, rankings, etapas, recursos.
Lista funciona melhor quando cada item é independente e pode ser absorvido isoladamente.

---

## Estrutura obrigatória

```
[GANCHO — promessa clara do que a lista vai entregar]

[Item 1 — emoji + nome + explicação curta (1-2 linhas)]
[Item 2 — ...]
[Item N — ...]

[Bônus ou destaque — item extra que surpreende]

[Reflexão ou pergunta final]

[CTA]

[3-5 hashtags]
```

---

## Processo

### 1. Definir o tema e os itens
- **Quantidade ideal:** 3 a 7 itens (menos de 3 é fraco, mais de 7 cansa)
- **Critério de ordenação:** do mais impactante ao menos, ou ranking explícito (🥇🥈🥉), ou por etapa lógica
- **Cada item precisa de:** nome claro + contexto de 1-2 linhas explicando o porquê

### 2. Gerar 3 opções de gancho para lista

**Padrão A — Número + promessa:**
> "5 ferramentas de IA que uso todo dia (e que você provavelmente não conhece):"

**Padrão B — Erro + aprendizado:**
> "Cometi esses 4 erros criando agentes de IA. Não repita:"

**Padrão C — Ranking honesto:**
> "Testei 6 plataformas de automação em 2025. Ranking honesto:"

### 3. Escrever o post

- Use emoji no início de cada item para escaneabilidade visual
- Cada item: **1 linha de nome/título + 1-2 linhas de contexto**
- Não explique demais — listas funcionam pela densidade
- Inclua pelo menos 1 item "surpresa" que o leitor não esperava
- Feche com uma pergunta que convide o leitor a completar a lista

### 4. Revisão
- [ ] O gancho promete algo específico e valioso?
- [ ] Cada item é independente e faz sentido sozinho?
- [ ] Os emojis ajudam a escanear (não são decorativos)?
- [ ] Tem pelo menos 1 item surpreendente ou contraintuitivo?
- [ ] O CTA convida o leitor a contribuir com a lista?

---

## Exemplo de post de lista

```
Testei 7 ferramentas de automação com IA em 2025.

Aqui o ranking honesto:

🥇 n8n — melhor custo-benefício para self-hosted. Curva de aprendizado existe, mas vale.

🥈 Make — melhor para quem não quer código. Visual intuitivo, integra tudo.

🥉 Zapier — maior ecossistema de integrações. Caro, mas maduro.

4️⃣ Activepieces — open-source promissor. Ainda jovem, mas evoluindo rápido.

5️⃣ Pipedream — melhor para devs. Código primeiro, UI depois.

6️⃣ Pabbly — barato e funcional. Sem surpresas (boas ou ruins).

7️⃣ Integromat (versão legacy) — só se você já usa. Migre para o Make.

Qual está faltando na lista? 👇

#automação #n8n #IA #produtividade #ferramentas
```
