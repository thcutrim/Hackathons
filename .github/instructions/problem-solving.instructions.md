---
description: "Use when starting a new challenge, breaking down a problem, designing a technical solution, or choosing the right tech stack for a hackathon challenge. Covers analysis, prioritization and rapid prototyping approach."
---

# Abordagem de Resolução de Desafios — Hackathon

## Framework Rápido (máx. 5 min antes de codificar)

1. **Entender o problema**: Qual é o input? Qual é o output esperado? Quais são as restrições?
2. **Identificar componentes**: Quais partes independentes precisam ser construídas?
3. **Definir MVP**: O mínimo para funcionar e demonstrar valor
4. **Escolher stack**: Menor fricção para o time — prefira o que já conhece
5. **Dividir tarefas**: Se houver time, quem faz o quê?

## Critérios de Escolha de Stack

| Necessidade | Opção Rápida |
|---|---|
| Backend API | Python (FastAPI) ou Node.js (Express) |
| Frontend | Next.js, React ou HTML/JS puro |
| IA/LLM | Azure OpenAI via SDK Python ou JS |
| Banco de dados | SQLite (local) ou Azure SQL |
| Deploy rápido | Azure Container Apps, Azure App Service |

## Priorização no Hackathon

1. **Funciona** > bonito
2. **Demo funcional** > cobertura de testes
3. **Entrega parcial** > não entrega nada
4. Documentar o que não teve tempo de implementar

## Estrutura de Projeto Sugerida

```
projeto/
├── README.md           # Descrever problema, solução e como rodar
├── src/                # Código-fonte principal
├── tests/              # Testes (quando der tempo)
├── docs/               # Diagramas, decisões de design
└── .github/            # CI/CD, instruções
```
