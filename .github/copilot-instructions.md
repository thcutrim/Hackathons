# Hackathon Microsoft — Instruções Gerais do Workspace

## Contexto
Este é um workspace de hackathon presencial na sede da Microsoft.
O objetivo é resolver desafios propostos de forma rápida, iterativa e funcional.

## Prioridades
- **Velocidade de entrega** acima de perfeição arquitetural
- Soluções funcionais e demonstráveis ao final de cada desafio
- Código legível e documentado o suficiente para apresentação

## Fluxo de Trabalho Git
- Repositórios são hospedados no GitHub do usuário `thiagocutrim`
- Sempre inicialize com `git init` + `gh repo create` ou clone direto
- Use branches por desafio/feature: `desafio-01`, `feat/nome-da-feature`
- Commits descritivos em português ou inglês, prefixados com tipo: `feat:`, `fix:`, `chore:`

## Stack e Tecnologias
- Adapte conforme o desafio trazido
- Prefira soluções com SDKs oficiais Microsoft/Azure quando o desafio envolver cloud
- Para IA/ML: priorize Azure OpenAI, Azure AI Foundry ou Semantic Kernel quando disponível

## Convenções de Código
- Nomes de variáveis e funções em inglês
- Comentários e docstrings podem ser em português
- Testes automatizados quando o tempo permitir

## Agentes Disponíveis neste Workspace
- **Research Agent** (`.github/agents/research.agent.md`): pesquisa rápida de tecnologias e abordagens
- **Planner Agent** (`.github/agents/planner.agent.md`): planejamento de arquitetura de solução

## Skills Disponíveis
- **github-workflow** (`.github/skills/github-workflow/`): operações Git/GitHub (clone, push, PR)
