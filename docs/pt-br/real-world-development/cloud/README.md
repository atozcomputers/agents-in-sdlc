---
slug: pt-br/real-world-development/cloud
title: "Agente de nuvem do GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

O **[agente de nuvem do GitHub Copilot](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent)** permite que o GitHub Copilot trabalhe de forma assíncrona na nuvem. Você atribui trabalho no GitHub e o agente de nuvem o processa em segundo plano — explorando o repositório, fazendo alterações e abrindo um pull request — enquanto você fica livre para fazer outras coisas.

Ao longo destes exercícios, você adicionará instruções personalizadas que o agente de nuvem seguirá, atribuirá uma issue do GitHub e permitirá que ele implemente o trabalho. Você revisará os resultados e usará agentes personalizados para moldar sua abordagem, monitorará e orientará sessões no painel de agentes e finalizará revisando seus pull requests e iterando sobre os resultados.

## Exercícios

| Exercício | Tópico | Descrição |
|----------|-------|-------------|
| [0. Pré-requisitos][ex0] | Configuração | Crie seu repositório e seu codespace |
| [1. Instruções personalizadas][ex1] | Contexto | Adicione instruções personalizadas que o agente de nuvem seguirá |
| [2. Agente de nuvem][ex2] | Agente assíncrono | Atribua issues ao agente de nuvem do Copilot |
| [3. Agentes personalizados][ex3] | Agentes especializados | Revise e use agentes personalizados |
| [4. Gerenciamento de agentes][ex4] | Monitoramento | Monitore e oriente sessões de agentes |
| [5. Iteração][ex5] | Revisão | Revise PRs, itere sobre o trabalho do Copilot e escolha os próximos passos |

## Pré-requisitos

Antes de participar deste workshop, verifique se você possui:

- [ ] Uma conta do GitHub com um plano ativo **Copilot Student, Pro, Pro+, Business ou Enterprise**
- [ ] O agente de nuvem do Copilot habilitado para sua conta ou organização

> [!TIP]
> Não tem um plano pago? Estudantes verificados podem obter o GitHub Copilot gratuitamente pelo [GitHub Education][callout-student-plan-education]. O plano **Copilot Student** inclui o agente, MCP, revisão de código e recursos do Copilot CLI usados neste workshop — assim, você poderá concluir todo o treinamento com ele.

[callout-student-plan-education]: https://github.com/education/students

> [!NOTE]
> O agente de nuvem está disponível nos planos **Copilot Student, Pro, Pro+, Business e Enterprise** — todos, exceto o Copilot Free. No Copilot Business ou Enterprise, um administrador deve habilitá-lo para sua organização.

> [!NOTE]
> O MCP não é abordado neste treinamento. Para explorar o uso de servidores MCP com o Copilot, consulte o [treinamento de CLI](../cli/) ou o [treinamento de VS Code](../vscode/).

## Começar

**[Começar com o exercício 0: Pré-requisitos →][ex0]**

[ex0]: 0-prerequisites/
[ex1]: 1-custom-instructions/
[ex2]: 2-cloud-agent/
[ex3]: 3-custom-agents/
[ex4]: 4-managing-agents/
[ex5]: 5-iterating/
