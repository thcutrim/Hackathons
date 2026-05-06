---
name: github-workflow
description: "Git and GitHub operations for hackathon projects. Use when cloning repos, creating GitHub repositories, pushing code, managing branches, or running gh CLI commands. Covers full workflow from init to PR creation."
argument-hint: "Descreva a operação Git/GitHub desejada"
---

# GitHub Workflow para Hackathon

## Quando Usar
- Criar novo repositório no GitHub (`thiagocutrim`)
- Clonar repositório existente
- Fazer push de código
- Criar branches por desafio
- Abrir Pull Requests

## Pré-requisitos

Verificar antes de qualquer operação:

```bash
# Checar autenticação gh CLI
gh auth status

# Se necessário autenticar:
gh auth login

# Checar identidade git
git config --global user.name
git config --global user.email
```

## Procedimentos

### 1. Novo Projeto do Zero

```bash
cd /Users/thiagocutrim/PROJETOS/HACKATONS/Microsoft

# Criar pasta e inicializar
mkdir <nome-do-projeto> && cd <nome-do-projeto>
git init

# Adicionar código e commitar
git add .
git commit -m "feat: initial commit"

# Criar repo no GitHub e subir
gh repo create thiagocutrim/<nome-do-projeto> --public --source=. --remote=origin --push
```

### 2. Clonar Repositório Existente

```bash
cd /Users/thiagocutrim/PROJETOS/HACKATONS/Microsoft
gh repo clone thiagocutrim/<nome-do-repo>
```

### 3. Push de Atualizações

```bash
git add .
git commit -m "feat: <descrição da mudança>"
git push
```

### 4. Trabalhar com Branch por Desafio

```bash
# Criar e trocar para branch do desafio
git checkout -b desafio-01

# Após desenvolvimento, subir
git push -u origin desafio-01

# Criar PR
gh pr create --title "Desafio 01 — <título>" --body "## Solução\n<descrição>"
```

### 5. Listar Repositórios do Usuário

```bash
gh repo list thiagocutrim --limit 20
```

## Convenções de Commit
- `feat:` nova funcionalidade
- `fix:` correção de bug  
- `chore:` configuração/manutenção
- `docs:` documentação

## Solução de Problemas

| Problema | Solução |
|---|---|
| `gh: command not found` | `brew install gh` |
| `Permission denied (publickey)` | `gh auth login` para re-autenticar |
| `remote origin already exists` | `git remote set-url origin <url>` |
| `Updates were rejected` | `git pull --rebase origin main` antes do push |
