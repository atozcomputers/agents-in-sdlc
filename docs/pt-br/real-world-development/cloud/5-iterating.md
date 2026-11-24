---
title: "Exercício 5: Iterar sobre o trabalho do GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lição anterior: Gerenciar agentes][previous-lesson] |
|:--|

## Revisando o trabalho

Ao longo deste laboratório, você trabalhou com o GitHub Copilot em várias tarefas voltadas a melhorar a experiência do usuário e adicionar funcionalidades. Você pediu ao Copilot que adicionasse documentação ao código, criasse o recurso de jogos relacionados para a equipe de design iterar e implementasse recursos de acessibilidade, incluindo alternadores de modo de alto contraste e modo claro. Vamos explorar as alterações de código e, se necessário, fornecer feedback ao Copilot para melhorar o trabalho.

### Cenário

Como destacamos várias vezes, os fundamentos do design de software e de DevOps não mudam com a IA generativa. Sempre queremos revisar o código gerado e seguir nosso processo normal de DevOps. Com isso em mente, vamos revisar as sugestões do GitHub Copilot para criar a documentação, o recurso de jogos relacionados e os recursos de acessibilidade antes de ativar a revisão para o restante da equipe.

## Segurança e agente de nuvem do GitHub Copilot

Como o agente de nuvem do Copilot executa suas tarefas de forma assíncrona e sem supervisão, certas restrições de segurança foram adotadas para manter tudo seguro. Elas incluem:

- O Copilot tem acesso somente leitura ao repositório e acesso de gravação **somente** à branch que usará para o código.
- O agente de nuvem é executado no GitHub Actions, onde cria um ambiente separado e efêmero para trabalhar.
- Qualquer workflow do GitHub Actions exige aprovação humana antes de ser executado.
- [O acesso a recursos externos é limitado por padrão](https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall), inclusive a servidores MCP.

## Revisando a documentação gerada

Vamos começar explorando o primeiro pull request (PR) gerado pelo agente de nuvem do GitHub Copilot — a adição de documentação ao seu código. Você realizará esta tarefa usando a interface padrão de PR no GitHub.com.

> [!NOTE]
> Ao explorar o PR, talvez veja um aviso informando que o GitHub Copilot foi bloqueado por um firewall. Isso **é esperado**, pois o Copilot tem acesso limitado a recursos externos por padrão, inclusive a chamadas para servidores MCP externos. Se desejar, você pode [personalizar ou desativar o firewall do agente de nuvem do Copilot][agent-firewall].

1. Volte ao seu repositório em github.com.
2. Selecione **Pull Requests** para abrir a lista de pull requests.
3. Abra o pull request com título semelhante a **Add missing documentation** ou algo mais específico.

> [!NOTE]
> Se o Copilot ainda estiver trabalhando na tarefa, o pull request conterá o indicador **[WIP]**. Nesse caso, aguarde a conclusão do trabalho pelo Copilot. Isso pode levar alguns minutos; sinta-se à vontade para fazer uma pausa ou refletir sobre tudo o que aprendeu até agora.

4. Quando o pull request estiver pronto, selecione a guia **Files changed** e revise as alterações.

    ![Guia Files changed](../../../_images/shared-pr-files-changed.png)

5. Explore o código recém-atualizado, que inclui os novos comentários de documentação TSDoc e outras informações. As alterações exatas podem variar.

    Ao analisar as alterações, procure comentários de documentação TSDoc, convenções de TypeScript e cabeçalhos de comentário. Eles vêm dos arquivos de instruções personalizados revisados no início do Exercício 2.

6. Depois de revisar as atualizações e confirmar que está tudo certo, volte à guia **Conversation** e role até o final.
7. Você deverá ver um indicador informando que alguns workflows aguardam aprovação.
8. Se os workflows estiverem aguardando aprovação, selecione **Approve and run workflows**.

   ![Aprovar e executar workflows](../../../_images/shared-approve-workflows.png)

9. Os workflows serão colocados na fila na seção de verificações do pull request. Se tudo estiver correto, você verá as verificações do projeto passar no aplicativo Astro único. Isso pode levar alguns minutos.

## Solicitando alterações ao GitHub Copilot

Trabalhar com o Copilot em um pull request não é uma via de mão única. Você também pode marcar o Copilot em comentários — como faria com outros membros da equipe — no pull request ou em comentários inline no código. O Copilot verá esses comentários e iniciará outra sessão para resolvê-los. Como os resultados não são determinísticos, não podemos fornecer um texto prescritivo do que solicitar. Algumas ideias de alterações que você pode pedir ao Copilot incluem:

- Adicionar cabeçalhos de comentário no início de cada arquivo de código com uma breve descrição do que fazem.
- Adicionar comentários de documentação TSDoc aos arquivos TypeScript e Astro.
- Criar um README com uma descrição da estrutura do aplicativo Astro.

1. Adicione um comentário solicitando uma alteração na documentação gerada e marque **@copilot**, como faria com qualquer usuário. Use uma das ideias acima ou outra sugestão sobre a documentação que você gostaria de ver na base de código.
2. Selecione **View Session** para observar o Copilot executar o trabalho. Observe como o Copilot inicia uma nova sessão para aplicar as atualizações.
3. Você pode selecionar **Back to pull request** para retornar ao pull request.

    ![Voltar ao pull request](../../../_images/ex7-back-to-pr.png)

4. Depois que o Copilot concluir as alterações, você deverá ver um novo commit no pull request.
5. Selecione a guia **Files changed** para revisar as alterações.

Continue iterando até ficar satisfeito. Quando estiver satisfeito, converta o PR de rascunho para pronto e faça o merge na branch principal.

![Converter PR para pronto](../../../_images/ex7-ready-for-review.png)

## Revisar o recurso de jogos relacionados

Vamos voltar ao PR que o Copilot criou para resolver nossa issue sobre a exibição de jogos relacionados na página de detalhes do jogo.

1. Volte ao seu repositório no GitHub.com.
2. Selecione a guia **Pull Requests**.
3. Selecione o PR cujo título seja semelhante a **Show related games on the game details page** ou algo mais específico.
4. Selecione a guia **Files changed** para revisar o código gerado.
5. Depois de revisar as atualizações e confirmar que está tudo certo, volte à guia **Conversation** e role até o final.
6. Você deverá ver um indicador informando que alguns workflows aguardam aprovação.
7. Se os workflows estiverem aguardando aprovação, selecione **Approve and run workflows**.

   ![Aprovar e executar workflows](../../../_images/shared-approve-workflows.png)

8. Os workflows serão colocados na fila na seção de verificações do pull request. Se tudo estiver correto, você verá as verificações do projeto passar no aplicativo Astro único. Isso pode levar alguns minutos.
9. **Opcional:** você pode mudar para essa branch no Codespace e testar manualmente o recurso de jogos relacionados. Acesse seu Codespace, abra o terminal e execute os seguintes comandos (substitua `<branch-name>` pelo nome da branch criada pelo Copilot, por exemplo **copilot/fix-8**):

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

O Copilot criou o recurso de jogos relacionados! Como antes, você pode trabalhar de forma iterativa com o agente de nuvem do Copilot para solicitar atualizações. Por exemplo, você pode pedir ao Copilot que ajuste quantos jogos relacionados serão exibidos ou garanta que cabeçalhos de comentário e comentários de documentação TSDoc sejam adicionados (lembre-se de que essa tarefa foi atribuída **antes** de você atualizar as instruções personalizadas!). Como antes, você pode fazer essas solicitações adicionando um novo comentário na guia **Conversation**, que o Copilot verá e usará para iniciar uma nova sessão.

## Revisar os recursos de acessibilidade

Por fim, vamos revisar os recursos de acessibilidade implementados com o agente personalizado de acessibilidade. Este PR deve incluir tanto o modo de alto contraste atribuído no Exercício 3 quanto o modo claro solicitado no mission control no Exercício 4.

1. Volte ao seu repositório no GitHub.com.
2. Selecione a guia **Pull Requests**.
3. Selecione o PR cujo título seja semelhante a **Add high contrast mode to website** ou algo mais específico.

> [!NOTE]
> Se o Copilot ainda estiver trabalhando na tarefa, o pull request conterá o indicador **[WIP]**. Nesse caso, aguarde a conclusão do trabalho pelo Copilot. Isso pode levar alguns minutos.

4. Selecione a guia **Files changed** para revisar o código gerado.
5. Revise a implementação, prestando atenção especial a:
   - os componentes de interface que alternam entre os modos;
   - o uso de armazenamento local para persistir as preferências do usuário;
   - as alterações de CSS ou estilo para os modos de alto contraste e claro;
   - os atributos de acessibilidade (rótulos ARIA, navegação pelo teclado etc.);
   - qualquer código JavaScript/TypeScript que gerencie a troca de modos.

6. Depois de revisar as atualizações e confirmar que está tudo certo, volte à guia **Conversation** e role até o final.
7. Você deverá ver um indicador informando que alguns workflows aguardam aprovação.
8. Se os workflows estiverem aguardando aprovação, selecione **Approve and run workflows**.

   ![Aprovar e executar workflows](../../../_images/shared-approve-workflows.png)

9. Os workflows serão colocados na fila na seção de verificações do pull request. Se tudo estiver correto, você verá as verificações do projeto passar no aplicativo Astro único. Isso pode levar alguns minutos.
10. **Opcional:** você pode mudar para essa branch no Codespace para testar manualmente os recursos de acessibilidade. Acesse seu Codespace, abra o terminal e execute os seguintes comandos (substitua `<branch-name>` pelo nome da branch criada pelo Copilot):

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

    Em seguida, inicie o aplicativo e teste no navegador os alternadores de modo de alto contraste e modo claro para garantir que funcionem como esperado e permaneçam ativos após recarregar a página.

Observe como o agente personalizado de acessibilidade ajudou a orientar o Copilot na implementação desses recursos de acordo com as melhores práticas de acessibilidade. Se identificar algum problema ou oportunidade de melhoria de acessibilidade, marque **@copilot** em um comentário para solicitar atualizações, como fez nos PRs anteriores.

## Exercício opcional — continue delegando

O agente de nuvem funciona melhor quando você pode entregar itens reais do backlog e voltar sua atenção para outros assuntos. Para criar o hábito, registre mais algumas issues no repositório e atribua-as ao Copilot. Algumas ideias:

- Criar um formulário de interesse de apoiadores na página de detalhes do jogo.
- Implementar paginação na lista de jogos.
- Adicionar validação de entrada e tratamento de erros aos helpers da camada de acesso a dados.

## Resumo

Você concluiu o treinamento do agente de nuvem. Ao longo destas lições, você:

- **inspecionou os arquivos de instruções personalizados fornecidos por este repositório** para observar posteriormente seu efeito no resultado do agente de nuvem;
- **atribuiu issues ao agente de nuvem do Copilot** e viu-o configurar o ambiente, planejar e executar de forma assíncrona;
- **criou e usou um agente personalizado** para acessibilidade, adicionando alternadores de modos de alto contraste e claro;
- **usou a página de agentes do Copilot como mission control** para monitorar e orientar a sessão de acessibilidade em andamento;
- **revisou e iterou sobre os pull requests do agente de nuvem**, marcando `@copilot` para solicitar alterações e aprovando workflows.

## Revisão e próximos passos

Você concluiu o treinamento do agente de nuvem. Se quiser continuar explorando, os outros treinamentos complementam o que você praticou aqui:

- 🖥️ **[Treinamento de VS Code](../../vscode/)** — explore o modo agente do Copilot Chat e a integração com MCP diretamente no IDE.
- 💻 **[Treinamento de CLI](../../cli/)** — entregue duas alterações revisadas pelo terminal com os modos Plan e Autopilot, skills de agente, um agente personalizado de QA, Playwright MCP, Agent Merge e uma ponte opcional `/delegate` para o agente de nuvem.

Em seu próprio repositório, experimente estas ideias de acompanhamento:

- Atribua ao agente de nuvem uma issue de refatoração ou cobertura de testes.
- Crie um agente personalizado para outra área.
- Configure `copilot-setup-steps.yml` para uma pilha diferente.

## Recursos

- [GitHub Copilot][github-copilot]
- [Sobre agentes do Copilot][copilot-agents]
- [Atribuir issues do GitHub ao Copilot][assign-issue]
- [Práticas recomendadas para o workflow de configuração do agente de nuvem do Copilot][cloud-agent-best-practices]
- [Configurar o firewall do agente de nuvem do Copilot][agent-firewall]

---

| [← Lição anterior: Gerenciar agentes][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall

[previous-lesson]: ../4-managing-agents/
