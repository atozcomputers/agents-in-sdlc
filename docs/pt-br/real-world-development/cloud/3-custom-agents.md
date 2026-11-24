---
title: "Exercício 3 - Agentes personalizados"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## O que são agentes personalizados?

[Agentes personalizados][custom-agents-concept] no GitHub Copilot permitem criar assistentes de IA especializados e adaptados a tarefas ou áreas específicas do fluxo de desenvolvimento. Ao definir agentes por meio de arquivos markdown na pasta `.github/agents` do repositório, você pode fornecer ao Copilot instruções direcionadas, práticas recomendadas, padrões de código e conhecimento específico do domínio que o orientem a executar determinados tipos de trabalho com mais eficácia. As equipes podem transformar sua experiência em agentes reutilizáveis — um agente de acessibilidade que aplica conformidade com a [WCAG][wcag], um agente de segurança que segue práticas de codificação segura ou um agente de testes que mantém padrões consistentes de teste.

Os agentes personalizados são definidos por arquivos markdown na pasta `.github/agents` do projeto ou globalmente em `~/.copilot/agents`. Cada arquivo possui frontmatter YAML com pelo menos os campos `name` e `description`, seguido de um prompt em markdown que define o comportamento, a experiência e as instruções do agente.

### Agentes personalizados comparados a skills de agente

Há alguma sobreposição lógica entre agentes personalizados e [skills de agente][agent-skills-concept]. Ambos são definidos principalmente por arquivos markdown e indicam à IA como executar operações. A separação mais clara é esta: um **agente personalizado** é o executor, e **skills** são ferramentas.

Os agentes personalizados têm a própria janela de contexto e foram criados para orquestrar skills (e até outros agentes) como parte de seu trabalho. Neste laboratório, o agente personalizado de acessibilidade revisa e atualiza o site de acordo com as diretrizes de acessibilidade; como parte desse trabalho, ele pode usar skills, como uma skill de fluxo de pull request ou outra que execute e gerencie testes.

> [!NOTE]
> Não existe uma maneira única "correta" de criar um agente personalizado. Como em tudo relacionado à IA, teste e itere para descobrir o que funciona melhor em seus ambientes e cenários.

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

Você explorará os seguintes conceitos com agentes personalizados:

- como os agentes personalizados são definidos;
- como atribuir uma tarefa a um agente personalizado.

## Cenário

A Tailspin Toys está comprometida em garantir que sua plataforma de financiamento coletivo seja acessível a todos os usuários, independentemente de suas capacidades ou preferências visuais. Comentários recentes de usuários destacaram que algumas pessoas consideram o tema escuro atual difícil de ler devido ao contraste insuficiente entre o texto e as cores de fundo. Para resolver essa questão de acessibilidade, a equipe de design solicitou a implementação de um modo de alto contraste que os usuários possam ativar e desativar.

Como a acessibilidade é crítica, você deseja garantir que essa funcionalidade seja implementada o mais rapidamente possível. Você usará um agente personalizado para gerar essa funcionalidade.

## Revisando o agente personalizado de acessibilidade

Já foi criado para você um agente personalizado de acessibilidade. Vamos revisar seu conteúdo para entender como ele orientará o Copilot.

Volte ao codespace e revise o arquivo do agente personalizado de acessibilidade:

1. Abra `.github/agents/accessibility.md`.
2. Observe o frontmatter YAML com os campos `name` e `description`.

> [!CAUTION]
> Os campos `name` e `description` no frontmatter são obrigatórios para agentes personalizados.

3. Em seguida, examine e revise as seções seguintes, que destacam:
   - Responsabilidades principais ao gerar código para um site acessível.
   - Práticas recomendadas de acessibilidade.
   - Exemplos de código em HTML, CSS e JavaScript.
   - Uma lista de armadilhas e erros comuns.

## Criar e atribuir uma issue

Mission control é o local central para trabalhar com todos os agentes do seu ambiente. Você pode atribuir tarefas ao agente de nuvem do Copilot, monitorar tarefas e até redirecioná-las e fornecer orientação adicional. Vamos começar atribuindo uma tarefa para criar o modo de alto contraste ao Copilot.

1. Acesse seu repositório.
2. Selecione a guia issues.
3. Selecione **New issue** para abrir a caixa de criação da issue.
4. Selecione **Blank issue** para criar uma issue vazia.
5. Defina o **Title** como `Add high contrast mode to website`.
6. Defina a **Description** como:

    ```plaintext
    We need a high contrast mode for the site. There should be a toggle for high contrast which the user can set. It should store the setting in local storage on the browser.
    ```

7. Selecione **Create** para criar a issue.
8. À direita, selecione **Assign to Copilot** para abrir a caixa de atribuição.
9. Selecione **Accessibility agent** na lista de agentes personalizados.

    ![Captura de tela da atribuição ao agente de nuvem, com o agente personalizado e Accessibility destacados](../../../_images/ex5-select-custom-agent.png)

10. Selecione **Assign**.
11. O Copilot começa a trabalhar na tarefa em segundo plano!

## Resumo e próximos passos

Esta lição apresentou os [agentes personalizados][custom-agents] no GitHub Copilot, assistentes de IA especializados adaptados a tarefas e domínios específicos. Com agentes personalizados, você pode transformar a experiência e os padrões da equipe em agentes reutilizáveis que orientam o Copilot a executar determinados tipos de trabalho com mais eficácia.

Você explorou estes conceitos:

- como os agentes personalizados são definidos;
- como atribuir uma tarefa a um agente personalizado.

Com o Copilot trabalhando na implementação do modo de alto contraste, podemos agora voltar nossa atenção ao [monitoramento e à orientação da sessão do agente][next-lesson] no mission control.

## Recursos

- [Sobre agentes personalizados][custom-agents]
- [Preparação para usar agentes personalizados na organização][org-custom-agents]
- [Preparação para usar agentes personalizados na empresa][enterprise-custom-agents]

---

| [← Lição anterior: Agente de nuvem do GitHub Copilot][previous-lesson] | [Próxima lição: Monitorar e gerenciar agentes →][next-lesson] |
|:--|--:|

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
