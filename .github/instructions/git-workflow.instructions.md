---
description: "Use when cloning repositories, creating GitHub repos, pushing code, managing branches, or any Git/GitHub operations. Covers setup, clone, push, PRs and gh CLI usage."
---

# Git & GitHub Workflow

## Pré-requisitos
- `git` instalado e configurado (`git config --global user.name/user.email`)
- `gh` CLI autenticado (`gh auth login`)

## Criar novo repositório e subir código

```bash
# 1. Inicializar projeto local
git init
git add .
git commit -m "feat: initial commit"

# 2. Criar repositório no GitHub e fazer push
gh repo create thiagocutrim/<nome-do-repo> --public --source=. --remote=origin --push

# Ou: criar privado
gh repo create thiagocutrim/<nome-do-repo> --private --source=. --remote=origin --push
```

## Clonar repositório existente

```bash
gh repo clone thiagocutrim/<nome-do-repo>
# ou
git clone https://github.com/thiagocutrim/<nome-do-repo>.git
```

## Fluxo de trabalho por desafio

```bash
# Criar branch para o desafio
git checkout -b desafio-01

# Desenvolver... depois commitar
git add .
git commit -m "feat: solução do desafio 01"

# Subir branch
git push -u origin desafio-01

# Criar PR (opcional)
gh pr create --title "Desafio 01" --body "Solução do desafio 01"
```

## Convenções de Commit
- `feat:` nova funcionalidade
- `fix:` correção de bug
- `chore:` tarefas de manutenção / configuração
- `docs:` alterações em documentação
- `refactor:` refatoração sem mudança de comportamento

## Verificar autenticação gh CLI

```bash
gh auth status
# Se não autenticado:
gh auth login
```
