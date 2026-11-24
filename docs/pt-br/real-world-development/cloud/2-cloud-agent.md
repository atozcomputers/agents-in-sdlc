---
title: "Exercício 2 - Agente de nuvem do GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lição anterior: Instruções personalizadas][previous-lesson] |
|:--|

Provavelmente, poucas organizações — ou nenhuma — não tenham dificuldade com dívidas técnicas. Isso pode incluir problemas de segurança não resolvidos, código legado que exige atualizações ou solicitações de funcionalidades que ficaram no backlog por falta de tempo para implementá-las. O agente de nuvem do GitHub Copilot foi criado para executar tarefas como atualizar código e adicionar funcionalidades de forma autônoma. Quando o agente conclui o trabalho, ele gera um PR em rascunho pronto para a revisão de um desenvolvedor humano. Isso permite delegar tarefas tediosas e acelerar o processo de desenvolvimento, além de liberar os desenvolvedores para se concentrar em questões mais amplas.

Você explorará os seguintes conceitos com o agente de nuvem do Copilot:

- personalizar o ambiente para gerar código;
- garantir que as operações sejam realizadas com segurança;
- compreender a importância de issues com escopo claramente definido;
- atribuir issues ao Copilot.

## Cenários

A Tailspin Toys precisa resolver parte de sua dívida técnica. Os contratados inicialmente contratados para criar a primeira versão do site deixaram a documentação em estado insatisfatório — e, como você verá, ela está totalmente ausente. Como primeiro passo, a equipe gostaria de adicionar comentários de documentação TSDoc a todas as funções exportadas do aplicativo.

Além disso, a equipe de design está pronta para melhorar a descoberta de jogos. A equipe deseja que a página de detalhes de cada jogo exiba jogos relacionados — outros títulos da mesma categoria — para que as pessoas possam continuar navegando. Ainda não é necessário implementar uma solução totalmente polida; a equipe quer algo utilizável para testar a experiência do usuário. Isso é um bloqueio atualmente, mas há outras issues com prioridade maior no momento.

Ambas são tarefas que podem acabar sendo adiadas e são excelentes candidatas para serem atribuídas ao agente de nuvem do Copilot. O agente de nuvem pode trabalhar nelas de forma assíncrona, permitindo que o desenvolvedor se concentre em outras tarefas e depois revise o trabalho do Copilot para garantir que tudo esteja conforme o esperado.

## Apresentando o agente de nuvem do GitHub Copilot

O [agente de nuvem do GitHub Copilot](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent) pode executar tarefas em segundo plano, da mesma forma que um desenvolvedor humano. Assim como no trabalho com uma pessoa, isso pode ser feito de várias maneiras, inclusive [atribuindo uma issue do GitHub ao Copilot](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions). Depois da atribuição, o Copilot cria um pull request em rascunho para acompanhar seu progresso, configura um ambiente e começa a trabalhar na tarefa. Você pode acompanhar a sessão do Copilot enquanto ela está em andamento ou depois da conclusão. Quando a solução proposta estiver pronta para revisão, o Copilot o marcará no pull request!

## A importância de instruções com escopo adequado

Não há mágica no GitHub Copilot — você não pode deixar de pensar. Mesmo operações aparentemente simples podem se tornar complexas ao examiná-las em detalhes. Por isso, [tenha cuidado ao definir o escopo das tarefas para o agente de nuvem do Copilot][cloud-agent-best-practices]. Trate-o como uma dupla de programação baseada em IA: trabalhe em etapas, aprenda, experimente e adapte-se conforme avança. Os fundamentos do desenvolvimento de software não mudam com a IA generativa.

## Instruções personalizadas neste repositório

Os exercícios anteriores apresentaram as instruções personalizadas e como elas orientam o Copilot. Se você já fez a prática de instruções personalizadas, viu o `.github/copilot-instructions.md` em ação; caso contrário, este é um bom momento para dar uma rápida olhada. Antes de atribuir trabalho ao agente de nuvem do Copilot, examine somente os arquivos de instruções já incluídos neste repositório para observar posteriormente seus efeitos.

Abra os arquivos a seguir na interface web do GitHub do repositório ou em um codespace, se já tiver um em execução:

- `.github/copilot-instructions.md` — revise a seção **Code standards**, especialmente as expectativas para convenções de TypeScript e comentários de documentação TSDoc.
- `.github/instructions/unit-tests.instructions.md` — observe o frontmatter `applyTo`, que limita estas instruções aos arquivos `**/*.test.ts`.

Ao atribuir a issue `Code lacks documentation` ao agente de nuvem na próxima seção, observe no pull request resultante os comentários de documentação TSDoc, as convenções de TypeScript e os cabeçalhos de comentários — eles vêm desses arquivos de instruções. Vamos destacar isso novamente ao revisar PRs em um exercício posterior.

## Configurando o ambiente de desenvolvimento para o agente de nuvem do Copilot

Criar código, independentemente de quem esteja envolvido, normalmente exige um ambiente específico e scripts de configuração que garantam que tudo esteja pronto. Isso também vale ao atribuir tarefas ao Copilot, que executa trabalhos de forma semelhante a um engenheiro de software.

O agente de nuvem usa o [GitHub Actions][github-actions] como ambiente de trabalho. Você pode personalizar esse ambiente criando um [workflow de configuração especial][setup-workflow], configurado no arquivo `.github/workflows/copilot-setup-steps.yml`, para executá-lo antes de o agente começar. Assim, ele terá acesso às ferramentas de desenvolvimento e às dependências necessárias. Isso já foi pré-configurado para o laboratório a fim de facilitar o fluxo e possibilitar esta oportunidade de aprendizado. Ele garante que o Copilot tenha acesso ao Node.js, às dependências do projeto, aos binários de navegador para testes ponta a ponta e ao banco SQLite migrado e populado para o aplicativo Astro único:

```yaml
name: "Copilot Setup Steps"

# Permite testar as etapas de configuração pela guia "Actions" do repositório
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # Define as menores permissões necessárias para suas etapas. O Copilot receberá seu próprio token para as operações.
    permissions:
      # Se você precisar clonar o repositório como parte das etapas de configuração, por exemplo, precisará da permissão `contents: read`. Caso contrário, o Copilot fará isso automaticamente depois que as etapas forem concluídas.
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # Configuração do frontend / aplicativo - agora o aplicativo é Astro + Drizzle/libSQL
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # Migra e popula o banco SQLite local para que builds e testes tenham dados.
      - name: Set up the database
        run: npm run db:setup
```

O arquivo parece qualquer outro workflow do GitHub, mas tem alguns pontos importantes:

- Ele contém um único job chamado `copilot-setup-steps`. Esse job é executado no GitHub Actions antes que o Copilot comece a trabalhar no pull request.
- Observe o gatilho `workflow_dispatch`, que permite executar o workflow manualmente pela guia **Actions** do repositório. Isso é útil para testar se o workflow é executado corretamente, em vez de esperar que o Copilot o execute.

## Adicionando documentação

Embora todos entendam a importância da documentação, a maioria dos projetos possui informações desatualizadas ou não possui documentação. Esse tipo de dívida técnica costuma ficar sem resolução, reduzindo a produtividade e dificultando a manutenção da base de código ou a integração de novos desenvolvedores à equipe. Felizmente, o Copilot é excelente em criar documentação, e esta é uma issue perfeita para atribuir ao agente de nuvem do Copilot. Ele trabalhará em segundo plano para gerar a documentação necessária. Em um exercício futuro, você revisará o trabalho.

1. Acesse seu repositório em github.com em uma nova guia do navegador.
2. Selecione a guia **Issues**.
3. Selecione **New issue** para abrir a caixa de criação da issue.
4. Selecione **Blank issue** para criar uma issue vazia.
5. Defina o **Title** como `Code lacks documentation`.
6. Defina a **Description** como:

    ```plaintext
    Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
    ```

7. Selecione **Create** para criar a issue.
8. À direita, selecione **Assign to Copilot** para abrir a caixa de atribuição.

  ![Atribuindo o Copilot a uma issue](../../../_images/shared-assign-copilot.png)

9. Selecione **Assign**.

  ![Detalhes da atribuição ao Copilot](../../../_images/ex4-assign-copilot-details.png)

10. Selecione a guia **Pull Requests**.
11. Abra o pull request recém-gerado (PR), cujo título será algo parecido com `[WIP]: Code lacks documentation`. Se o PR novo não aparecer na lista, aguarde um minuto ou dois e atualize a janela do navegador.
12. Depois de alguns minutos, você deverá ver que o Copilot criou uma lista de tarefas.

> [!NOTE]
> Pode levar vários minutos para que a lista de tarefas do Copilot apareça no PR. O Copilot está criando seu ambiente (executando o workflow destacado anteriormente), analisando o projeto e determinando a melhor abordagem para resolver o problema.

13. Revise a lista e as tarefas que serão concluídas.
14. Role pela linha do tempo do pull request; você deverá ver uma atualização informando que o Copilot começou a trabalhar na issue.
15. Selecione o botão **View session**.

  ![Visualização da sessão do Copilot](../../../_images/ex4-view-session.png)

> [!CAUTION]
> Talvez seja necessário atualizar a janela para ver o indicador atualizado.

16. Observe que você pode percorrer a sessão ao vivo e ver como o Copilot resolve o problema. Isso inclui explorar o código e compreender seu estado, pausar para pensar e decidir sobre o plano adequado e, por fim, criar código.

Isso provavelmente levará vários minutos. Um dos principais objetivos do agente de nuvem do Copilot é permitir que ele execute tarefas de forma assíncrona, liberando-nos para realizar outras atividades. Vamos aproveitar esse recurso atribuindo outra tarefa ao agente de nuvem e, em seguida, voltando nossa atenção à adição de funcionalidades ao aplicativo.

## Adicionar uma seção de jogos relacionados à página de detalhes do jogo

Como destacamos, uma das grandes vantagens do agente de nuvem do Copilot é a capacidade de dividir o trabalho: você pode se concentrar em um conjunto de tarefas enquanto ele trabalha em outro. Embora a adição de uma seção de jogos relacionados para a equipe de design talvez não leve muito tempo, esse tempo poderia ser usado em outras tarefas. Vamos atribuí-la ao agente de nuvem do Copilot!

1. Volte ao seu repositório em github.com.
2. Selecione a guia **Issues**.
3. Selecione **New issue** para abrir a caixa de criação da issue.
4. Selecione **Blank issue** para usar o template vazio.
5. Defina o **Title** como: `Show related games on the game details page`
6. Defina a **Description** como:

    ```markdown
    We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
   ```

7. Selecione **Create** para criar a issue.
8. À direita, selecione **Assign to Copilot** para abrir a caixa de atribuição.

  ![Atribuindo o Copilot a uma issue](../../../_images/shared-assign-copilot.png)

9. Selecione **Assign**.

Pouco tempo depois, você deverá ver um conjunto de 👀 no primeiro comentário da issue, indicando que o Copilot está trabalhando nela!

![O Copilot usa o emoji de olhos para indicar que está trabalhando na issue](../../../_images/ex4-issue-eyes-emoji.png)

O Copilot agora está trabalhando diligentemente em sua segunda solicitação! O agente de nuvem do Copilot funciona de maneira semelhante a um engenheiro de software, portanto você não precisa monitorá-lo constantemente; basta revisar o resultado ao concluir. Vamos voltar nossa atenção à criação e ao uso de agentes personalizados.

## Resumo e próximos passos

Esta lição apresentou o [agente de nuvem do GitHub Copilot][copilot-agents]. Com o agente de nuvem, você pode atribuir issues ao Copilot para execução assíncrona. Você pode usar o Copilot para resolver dívidas técnicas, criar novos recursos ou migrar código de uma estrutura para outra.

Você explorou estes conceitos:

- personalizar o ambiente para gerar código;
- garantir que as operações sejam realizadas com segurança;
- compreender a importância de issues com escopo claro;
- atribuir issues ao Copilot.

Com o agente de nuvem trabalhando diligentemente em segundo plano, podemos agora voltar nossa atenção à criação e ao uso de agentes personalizados. [O agente de nuvem do Copilot também pode usar servidores MCP][cloud-agent-mcp] e tem instruções personalizadas disponíveis, recursos que exploramos em módulos anteriores.

## Recursos

- [Sobre o agente de nuvem do Copilot][copilot-agents]
- [Atribuir issues do GitHub ao Copilot][assign-issue]
- [Práticas recomendadas para o workflow de configuração do agente de nuvem do Copilot][cloud-agent-best-practices]

| [Próxima lição: Agentes personalizados →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
