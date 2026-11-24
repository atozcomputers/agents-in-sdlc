---
title: "Exercício 1 - Instruções personalizadas (Agente de nuvem)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lição anterior: Pré-requisitos][previous-lesson] · [Próxima lição: Agente de nuvem do Copilot →][next-lesson]

O contexto é essencial ao trabalhar com IA generativa. Se uma tarefa precisar ser executada de uma maneira específica — ou houver informações de contexto que o Copilot deva conhecer — você precisa garantir que esse contexto esteja acessível. Os [arquivos de instruções][instruction-files] são a forma de fornecer essa orientação, para que o Copilot entenda não apenas *o que* você deseja que ele faça, mas *como* deseja que seja feito.

Neste exercício, você irá:

- explorar como o contexto específico do projeto, as diretrizes de codificação e os padrões de documentação chegam ao Copilot por meio de instruções personalizadas do repositório e arquivos de instruções com escopo por caminho;
- adicionar um novo padrão global ao `.github/copilot-instructions.md`.

> [!NOTE]
> Diferentemente dos treinamentos de VS Code e CLI, aqui você não executará um prompt de *antes/depois* — o agente de nuvem do Copilot trabalha de forma assíncrona em issues do GitHub, portanto o impacto é mais difícil de demonstrar lado a lado em tempo real. Você verá a influência do arquivo de instruções mais adiante neste treinamento, ao revisar os pull requests produzidos pelo agente de nuvem.

## Arquivos de instruções

### Cenário

Como em qualquer boa empresa de desenvolvimento, a Tailspin Toys possui um conjunto de diretrizes e requisitos para práticas de desenvolvimento. Eles incluem:

- A camada de dados sempre precisa de testes de unidade.
- A interface deve usar o modo escuro e ter uma aparência moderna.
- A documentação deve ser adicionada ao código na forma de comentários de documentação TSDoc.
- Deve ser adicionado um bloco de comentários no início de cada arquivo descrevendo o que o arquivo faz.

Ao usar arquivos de instruções, você garantirá que o Copilot tenha as informações corretas para executar as tarefas alinhadas às práticas destacadas.

### Instruções personalizadas

As instruções personalizadas permitem fornecer contexto e preferências ao Copilot, para que ele compreenda melhor seu estilo de codificação e seus requisitos. Esse recurso poderoso pode ajudar a orientar o Copilot para obter sugestões e trechos de código mais relevantes. Você pode especificar convenções de código, bibliotecas e até os tipos de comentários que prefere incluir no código. É possível criar instruções para todo o repositório ou para tipos específicos de arquivos em contextos de tarefas.

Há dois tipos de arquivos de instruções:

- `.github/copilot-instructions.md`, um único arquivo de instruções enviado ao Copilot em **todas** as solicitações do repositório. Esse arquivo deve conter informações no nível do projeto — contexto relevante para a maioria das solicitações feitas ao Copilot no chat ou na CLI. Ele pode incluir a pilha tecnológica usada, uma visão geral do que está sendo criado, práticas recomendadas e outras orientações globais.
- Arquivos `.github/instructions/*.instructions.md` podem ser criados para tarefas ou tipos de arquivos específicos. Você pode usá-los para fornecer diretrizes para linguagens específicas (como TypeScript ou Astro) ou tarefas como criar um componente de interface ou um novo conjunto de testes de unidade.

> [!NOTE]
> Ao trabalhar no IDE, os arquivos de instruções são usados somente na geração de código no Copilot Chat — não em complementos de código ou sugestões de próxima edição.
>
> O Copilot Chat, o Copilot CLI e o agente de nuvem do Copilot usam tanto os arquivos no nível do repositório quanto os arquivos `*.instructions.md` (com frontmatter `applyTo`) ao gerar código.
>
> Por fim, o Copilot [aceita arquivos de instruções que usam outros padrões][custom-instructions-support], incluindo os arquivos AGENTS.md e CLAUDE.md.

### Práticas recomendadas para gerenciar arquivos de instruções

Uma conversa completa sobre como criar arquivos de instruções está além do escopo deste workshop. No entanto, os exemplos fornecidos no projeto de exemplo mostram uma abordagem representativa. Em linhas gerais:

- Mantenha as instruções em `copilot-instructions.md` focadas em orientações no nível do projeto, como uma descrição do que está sendo criado, a estrutura do projeto e padrões globais de codificação.
- Use arquivos `*.instructions.md` para fornecer instruções específicas a tipos de arquivos (testes de unidade, componentes Astro, camada de dados) ou a determinadas tarefas.
- Use linguagem natural. Mantenha as orientações claras. Forneça exemplos de como o código deve — e não deve — parecer.

Não existe uma única maneira correta de criar arquivos de instruções, assim como não existe uma única maneira correta de usar IA. A experimentação ajudará você a descobrir o que funciona melhor para seu projeto.

> [!TIP]
> Todo projeto que usa o GitHub Copilot deve ter uma coleção sólida de arquivos de instruções. Ao explorar os existentes neste projeto, você pode observar arquivos para vários tipos de tarefas, incluindo [atualizações da interface][ui-instructions] e [Astro][astro-instructions].
>
> O Copilot também pode ajudar você a gerar arquivos de instruções. Cada interface expõe esse recurso de modo diferente (por exemplo, **Configure Chat → Generate Agent Instructions** no VS Code ou `/init` no Copilot CLI); a lição correspondente apontará isso quando for relevante.
>
> Está procurando templates ou um ponto de partida? Explore o [awesome-copilot][awesome-copilot], um repositório cheio de arquivos de instruções, agentes personalizados e outros recursos.

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## Explore os arquivos de instruções personalizadas deste projeto

Reserve um momento para ler os arquivos de instruções fornecidos por este repositório — há um `copilot-instructions.md` central e uma coleção de arquivos `*.instructions.md` para diferentes tarefas. Abra-os no editor ou na interface web do GitHub.

1. Abra `.github/copilot-instructions.md`.
2. Explore o arquivo, observando a breve descrição do projeto e seções como **Agent notes**, **Code standards**, **Scripts** e **Repository Structure**. Em **Code standards**, observe as orientações aninhadas de **GitHub Actions Workflows**. Elas se aplicam a todas as interações que você tiver com o Copilot.
3. Abra a pasta `.github/instructions` e examine-a. Observe que há instruções para arquivos Astro, a camada de dados Drizzle, testes e muito mais.
4. Abra `.github/instructions/unit-tests.instructions.md`. Observe o campo `applyTo` no início — ele define um glob (relativo à raiz do repositório) que determina quais arquivos recebem as instruções. Aqui, qualquer arquivo de teste TypeScript (por exemplo, um que corresponda a `**/*.test.ts`) será incluído.
5. Observe as instruções específicas para criar testes de unidade neste projeto.
6. Por fim, abra `.github/instructions/drizzle.instructions.md` e role até o final. Observe os links para outros arquivos de instruções (como `unit-tests.instructions.md`) e arquivos existentes no projeto. Isso permite dividir conjuntos maiores de instruções em arquivos menores e reutilizáveis e indicar ao Copilot exemplos a seguir ao gerar código. (Os caminhos são relativos ao arquivo de instruções, não à raiz do repositório.)

> [!NOTE]
> A seção **Code formatting requirements** em `copilot-instructions.md` documenta os padrões de codificação do projeto, mas ainda não exige documentação no código. Nas próximas etapas, você adicionará regras para comentários de documentação TSDoc e cabeçalhos de comentários de arquivo.

## Adicione um novo padrão ao repositório

O próximo passo é a única edição que você fará aqui: adicione uma regra global segundo a qual a documentação deve ficar no código, como comentários de documentação TSDoc e um cabeçalho de comentário no nível do arquivo. O agente de nuvem a considerará ao trabalhar nas issues que você atribuir a ele mais adiante neste treinamento.

Antes de editar, configure uma branch para trabalhar (o agente de nuvem lerá suas instruções da branch que a issue direcionar, mas você ainda fará os commits de forma organizada):

1. No terminal do codespace, crie e mude para uma nova branch:

   ```bash
   git checkout -b custom-instructions-cloud
   ```

Como destacamos anteriormente, `.github/copilot-instructions.md` foi criado para fornecer informações no nível do projeto ao Copilot. Vamos garantir que os padrões de codificação do repositório estejam documentados para melhorar as sugestões de código.

1. Abra novamente `.github/copilot-instructions.md`.
2. Localize a seção **Code formatting requirements**, que deve estar próxima da linha 27. Observe que ela documenta os padrões de codificação do projeto — mas ainda não contém uma regra para documentação no código, motivo pelo qual o helper gerado não tinha comentários de documentação.
3. Adicione as seguintes linhas de markdown logo abaixo dos padrões existentes para instruir o Copilot a adicionar cabeçalhos de comentário e comentários de documentação TSDoc:

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. Salve `copilot-instructions.md`.

> [!TIP]
> Como você viu na lição anterior, os arquivos de instruções podem ser criados no nível do repositório (`.github/copilot-instructions.md`) para orientação global ou como arquivos `*.instructions.md` para linguagens, tipos de arquivo ou tarefas específicas. O arquivo no nível do repositório é o local adequado para padrões globais do projeto, como a regra de comentários de documentação que você acabou de adicionar.

## Commit, push e merge da atualização das instruções

O agente de nuvem lê os arquivos de instruções da branch direcionada pela issue. Ao atribuir uma issue ao Copilot no próximo exercício, o Copilot criará uma branch a partir de `main` — portanto, suas alterações nas instruções precisam chegar a `main` para que o agente de nuvem as considere.

1. Prepare e faça o commit:

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. Faça o push da branch:

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. Abra um pull request de `custom-instructions-cloud` para `main` em github.com e faça o merge. O agente de nuvem lerá essas instruções ao trabalhar nas issues atribuídas no próximo exercício.

> [!TIP]
> Se preferir trabalhar diretamente em `main` neste workshop, você pode ignorar a branch e fazer o commit diretamente em `main`. A etapa da branch está aqui para que o workshop reflita a forma de trabalho em um projeto real.

## Resumo e próximos passos

Você explorou como o Copilot obtém contexto dos arquivos de instruções deste projeto e adicionou um novo padrão global ao `.github/copilot-instructions.md`. Você verá esse padrão aplicado nos pull requests gerados pelo agente de nuvem ao longo deste treinamento.

Em seguida, você [atribuirá sua primeira issue ao agente de nuvem do Copilot][next-lesson].

## Recursos

- [Arquivos de instruções para personalização do GitHub Copilot][instruction-files]
- [Práticas recomendadas para criar instruções personalizadas][instructions-best-practices]
- [5 dicas para escrever instruções personalizadas melhores para o Copilot][copilot-instructions-five-tips]
- [Awesome Copilot — uma coleção de arquivos de instruções e outros recursos][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
