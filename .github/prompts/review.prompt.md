---
description: "Review code from a hackathon challenge — check for bugs, security issues, and quick improvements before demo"
name: "Review Rápido"
argument-hint: "Arquivo ou trecho de código a revisar"
agent: "agent"
tools: [read, search]
---

Faça uma revisão rápida e focada do código fornecido, considerando o contexto de hackathon.

## Checar nesta ordem

1. **Bugs críticos**: Erros que vão quebrar a demo
2. **Segurança básica**: Credenciais expostas, injeção SQL, dados sensíveis em log
3. **Fluxo principal**: O caminho feliz funciona conforme esperado?
4. **Melhorias rápidas**: Só se levarem menos de 5 minutos para implementar

## Formato de resposta

### Crítico (corrigir antes da demo)
- {problema}: {sugestão de correção em 1 linha}

### Segurança
- {problema}: {sugestão de correção em 1 linha}

### Melhorias opcionais
- {sugestão}: {motivo}

### Aprovado
{lista do que está ok}

Seja direto. Não explique o óbvio. Foque no que importa para a demo funcionar.
