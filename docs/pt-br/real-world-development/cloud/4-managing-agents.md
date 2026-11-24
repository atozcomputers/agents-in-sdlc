---
title: "Exercício 4 - Monitorar e gerenciar agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Nos últimos exercícios, você pediu ao agente de nuvem do Copilot que assumisse três tarefas separadas voltadas a melhorar a experiência do usuário e adicionar funcionalidades. Embora o agente de nuvem tenha sido criado para operar de forma assíncrona e autônoma, a capacidade de monitorar essas tarefas continua sendo importante.

Há várias ferramentas disponíveis para gerenciar tarefas atribuídas ao agente de nuvem, incluindo a [página de agentes][agents-page] no GitHub.com. Nesse mission control, você pode ver todas as tarefas de agentes com pull requests (PRs) abertos. É possível explorar as operações realizadas e até orientar uma sessão em andamento para ajudar a direcioná-la.

Nesta lição, você irá:

- explorar a página de agentes para monitorar tarefas do agente de nuvem;
- orientar uma sessão em andamento para solicitar funcionalidades adicionais.

## Cenário

Depois de atribuir ao agente a criação de um modo de alto contraste, a equipe percebeu que seria interessante adicionar também um modo claro. Como o trabalho já estava sendo realizado para atualizar o estilo do site e adicionar a funcionalidade de alternância, parecia lógico incluir essa funcionalidade. Você deseja orientar o trabalho do agente para garantir que ele adicione o modo claro e o modo de alto contraste.

## Revisar tarefas do agente de nuvem do Copilot

Vamos verificar o status atual de todas as tarefas atribuídas ao agente de nuvem do Copilot.

1. Acesse a [página de agentes do Copilot](https://github.com/copilot/agents).
2. Observe a lista de tarefas, no painel principal e no painel esquerdo. Você deverá ver as tarefas que atribuiu ao Copilot, incluindo:
    - atualização da documentação da base de código;
    - geração de APIs para modificar jogos;
    - adição de um modo de alto contraste ao site.
3. Selecione uma das tarefas em execução. Revise as tarefas realizadas pelo Copilot. Elas podem incluir:
    - clonar o código do repositório;
    - criar o ambiente do Copilot;
    - configurar servidores MCP;
    - executar várias etapas para concluir a tarefa atribuída.

> [!NOTE]
> As etapas exatas exibidas variam conforme o estado do trabalho do Copilot e a abordagem adotada.

4. Observe também o painel de pull requests (PR) exibido à direita. Ele permite ver o PR e os arquivos alterados para um monitoramento adicional.

## Orientar o agente de nuvem

Agora que você viu as tarefas ativas, vamos pedir ao Copilot que inclua a opção de modo claro enquanto trabalha no modo de alto contraste.

1. Selecione a sessão referente à adição do modo de alto contraste. O título exato varia conforme o nome usado pelo Copilot e o estado atual do trabalho.

    ![Sessão de acessibilidade no mission control](../../../_images/ex6-accessibility-session.png)

2. Observe a sessão por alguns minutos, até indicar que concluiu a configuração e iniciou o trabalho. Isso ocorrerá quando começarem a aparecer mensagens semelhantes às exibidas abaixo.
3. Na caixa de diálogo **Steer active session while Copilot is working**, adicione o seguinte prompt:

    ```plaintext
    While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
    ```

    ![Captura de tela da tarefa do agente de nuvem na página de agentes, com a caixa de diálogo Steer active session while copilot is working destacada](../../../_images/ex6-steer-cloud-agent-task.png)

4. Pressione <kbd>Enter</kbd> para enviar o prompt.
5. Observe como o Copilot reconhece o prompt e o incorpora ao fluxo.

## Deixe o Copilot trabalhar

Assim como antes, o Copilot começará a trabalhar na tarefa atualizada! Ele incorporará a nova solicitação ao fluxo depois de concluir a etapa específica em que estava trabalhando quando você enviou a mensagem.

Como antes, isso levará vários minutos; é um bom momento para pausar e refletir sobre tudo o que você aprendeu e explorou até agora.

## Resumo e próximos passos

Esta lição apresentou a página de agentes do Copilot, seu hub central para monitorar e orientar tarefas do agente de nuvem do GitHub Copilot. Neste mission control, você pode acompanhar todas as tarefas ativas e concluídas, revisar o trabalho realizado e até redirecionar tarefas em andamento para ajustar o escopo ou fornecer orientação adicional.

Você explorou estes conceitos:

- explorar o mission control e a página de agentes para monitorar tarefas do agente de nuvem;
- redirecionar uma sessão em andamento para solicitar funcionalidades adicionais.

Com o Copilot concluindo o trabalho nas funcionalidades de acessibilidade, podemos agora voltar nossa atenção à [iteração nos pull requests criados pelo Copilot][next-lesson].

## Recursos

- [Página de agentes do Copilot][agents-page]
- [Sobre agentes personalizados][custom-agents]

---

| [← Lição anterior: Agentes personalizados][previous-lesson] | [Próxima lição: Iterar sobre o trabalho do Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
