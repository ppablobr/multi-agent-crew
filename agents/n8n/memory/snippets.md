# Snippets n8n — Expressões e Padrões Úteis
> Trechos reutilizáveis coletados ao longo do uso.

## Expressões comuns
```javascript
// Data atual
{{ $now.toFormat('yyyy-MM-dd') }}

// Valor ou padrão
{{ $json.campo ?? 'padrão' }}

// Concatenar strings
{{ [$json.nome, $json.sobrenome].join(' ') }}
```

## Padrões de workflow frequentes
*A ser preenchido com uso*
