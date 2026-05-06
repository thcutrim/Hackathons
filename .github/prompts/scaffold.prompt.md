---
description: "Scaffold a new project for a hackathon challenge — creates folder structure, README, .gitignore and initial files"
name: "Scaffold Projeto"
argument-hint: "Nome do projeto e linguagem/stack (ex: 'api-chatbot Python FastAPI')"
agent: "agent"
tools: [edit, search, execute]
---

Crie a estrutura inicial de um projeto de hackathon com base no nome e stack fornecidos.

## O que criar

1. **Estrutura de pastas** adequada para a stack escolhida
2. **README.md** com:
   - Nome do projeto
   - Descrição do desafio (placeholder)
   - Instruções de instalação e execução
   - Stack tecnológica utilizada
3. **.gitignore** adequado para a linguagem/framework
4. **Arquivo principal** de entrada (ex: `main.py`, `index.ts`, `app.js`)
5. **Dependências** (ex: `requirements.txt`, `package.json`) com dependências base

## Regras
- Mantenha simples: só o essencial para começar a codar
- Comente o arquivo principal com TODO markers onde o código principal deve ir
- Use o nome do projeto em snake_case para pastas e kebab-case para o repo

Após criar, liste os arquivos criados e o próximo passo para começar a desenvolver.
