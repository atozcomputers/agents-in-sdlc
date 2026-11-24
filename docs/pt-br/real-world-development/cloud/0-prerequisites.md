---
title: "Exercício 0: Pré-requisitos"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Antes de iniciar os exercícios do agente de nuvem do Copilot, você precisa preparar tudo. Você criará sua própria cópia do repositório Tailspin Toys e iniciará um [codespace][codespaces] que poderá usar para editar arquivos de instruções e revisar o trabalho produzido pelo agente de nuvem.

## Configurando o repositório do laboratório

Para criar uma cópia do repositório para o código que você criará, você fará uma instância a partir do [template][template-repository]. A nova instância conterá todos os arquivos necessários para o laboratório, e você a usará durante os exercícios.

1. Em uma nova janela do navegador, acesse o [template do Tailspin Toys][tailspin-template].
2. Crie sua própria cópia do repositório selecionando o botão **Use this template** na página do repositório do laboratório. Em seguida, selecione **Create a new repository**.

    ![Botão Use this template](../../../_images/ex0-use-template.png)

3. Se estiver participando do workshop como parte de um evento conduzido pelo GitHub ou pela Microsoft, siga as instruções fornecidas pelos mentores. Caso contrário, você pode criar o novo repositório em uma organização na qual tenha acesso ao GitHub Copilot.

    ![Configurações do template do repositório](../../../_images/ex0-repository-settings.png)

4. Anote o caminho do repositório que você criou (**nome-da-organizacao-ou-do-usuario/nome-do-repositorio**), pois precisará dele posteriormente no laboratório.

## Criando um codespace

Em seguida, você usará um codespace para concluir os exercícios do laboratório.

O [GitHub Codespaces][codespaces] é um ambiente de desenvolvimento baseado em nuvem que permite escrever, executar e depurar código diretamente no navegador. Ele oferece um IDE completo com suporte a várias linguagens de programação, extensões e ferramentas.

1. Acesse o repositório recém-criado.
2. Selecione o botão verde **Code**.

    ![Selecionar o botão Code](../../../_images/ex0-code-button.png)

3. Selecione a guia **Codespaces** e selecione o botão **+** para criar um novo codespace.

    ![Criar um novo codespace](../../../_images/ex0-create-codespace.png)

A criação do codespace levará vários minutos, embora ainda seja muito mais rápido do que instalar manualmente todos os serviços! Aproveite esse tempo para explorar outros recursos do GitHub Copilot, aos quais voltaremos em seguida.

> [!CAUTION]
> Você retornará ao codespace em um exercício futuro. Por enquanto, deixe-o aberto em uma guia do navegador.

> [!NOTE]
> Este workshop foi criado para ser executado em um codespace ou em um [dev container][dev-containers] local. Ambos garantem que o ambiente tenha todos os pré-requisitos necessários instalados para uma experiência tranquila. Se preferir executar localmente, abra o repositório clonado no VS Code e selecione **Reopen in Container** quando solicitado — o VS Code criará o mesmo dev container usado pelo codespace.

[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers

## Resumo

Parabéns, você criou uma cópia do repositório do laboratório! Você também iniciou o processo de criação do codespace, que usará enquanto trabalha junto ao agente de nuvem do Copilot.

## Próximo passo

Vamos adicionar instruções personalizadas que o agente de nuvem seguirá. Continue para o [Exercício 1 - Instruções personalizadas][next-lesson].

## Recursos

- [Visão geral do GitHub Codespaces][codespaces]
- [Criar um repositório a partir de um template][template-repository]
- [Introdução aos Codespaces][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[next-lesson]: ../1-custom-instructions/
