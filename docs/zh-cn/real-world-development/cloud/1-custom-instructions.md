---
title: "练习 1 - 自定义说明（云智能体）"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 上一课：先决条件][previous-lesson] · [下一课：Copilot 云智能体 →][next-lesson]

使用生成式 AI 时，上下文至关重要。如果任务必须按特定方式完成，或者 Copilot 应了解某些背景信息，就需要确保这些上下文可供它访问。[说明文件][instruction-files]就是提供此类指导的方式，让 Copilot 不仅了解想让它做*什么*，也了解希望*如何*完成。

在本练习中，将：

- 探索项目上下文、编码指南和文档标准如何通过存储库自定义说明及限定路径的说明文件传递给 Copilot；
- 向 `.github/copilot-instructions.md` 添加一条新的存储库级标准。

> [!NOTE]
> 与 VS Code 和 CLI 工作坊不同，本练习不会执行*前后对比*提示——Copilot 云智能体在 GitHub议题上异步工作，因此很难实时并排展示效果。稍后审查云智能体生成的拉取请求时，将看到说明文件所产生的影响。

## 说明文件

### 场景

作为一家优秀的开发公司，Tailspin Toys 为开发实践制定了指南和要求，其中包括：

- 数据层始终需要单元测试。
- UI 应采用深色模式并具有现代感。
- 应在代码中以 TSDoc 文档注释的形式添加文档。
- 应在每个文件顶部添加注释块，说明该文件的作用。

通过说明文件，可以确保 Copilot 具备正确的信息，从而与上述实践保持一致。

### 自定义说明

自定义说明允许向 Copilot 提供上下文和偏好，使它更好地理解编码风格和要求。这是一项强大的功能，可以引导 Copilot 提供更相关的建议和代码片段。可以指定首选编码约定、库，甚至希望在代码中包含的注释类型。说明既可用于整个存储库，也可用于特定类型的文件以提供任务级上下文。

说明文件分为两种：

- `.github/copilot-instructions.md`：一个发送给 Copilot 的说明文件，适用于存储库中的**所有**请求。此文件应包含项目级信息——大多数发送给 Copilot 的聊天或 CLI 请求都相关的上下文，例如所采用的技术栈、构建目标概述、最佳实践和其他全局指南。
- `.github/instructions/*.instructions.md`：可针对特定任务或文件类型创建的说明文件。可用它们为特定语言（如 TypeScript 或 Astro）或任务（如创建 UI组件或一组新单元测试）提供指南。

> [!NOTE]
> 在 IDE中工作时，说明文件仅用于 Copilot Chat 的代码生成，不用于代码补全或后续编辑建议。
>
> Copilot Chat、Copilot CLI 和 Copilot 云智能体在生成代码时都会使用存储库级说明和带有 `applyTo` 前置元数据的 `*.instructions.md` 文件。
>
> 最后，Copilot[支持使用其他标准的说明文件][custom-instructions-support]，包括 AGENTS.md 和 CLAUDE.md 文件。

### 管理说明文件的最佳实践

创建说明文件的完整讨论超出了本工作坊的范围。不过，示例项目中的文件展示了一种代表性方法。总体而言：

- 将 `copilot-instructions.md` 中的说明集中于项目级指南，例如项目用途、项目结构和全局编码标准。
- 使用 `*.instructions.md` 文件，为文件类型（单元测试、Astro组件、数据层）或特定任务提供具体说明。
- 使用自然语言，保持指导清晰，并提供代码应采用及不应采用形式的示例。

说明文件的使用方式并非只有一种，就像使用 AI 也没有唯一标准。通过实验，可以确定最适合自己项目的方法。

> [!TIP]
> 每个使用 GitHub Copilot 的项目都应维护一套完善的说明文件。浏览此项目中的说明文件时，会发现其中包含面向多种任务的文件，例如 [UI更新][ui-instructions]和 [Astro][astro-instructions]。
>
> Copilot 也能帮助生成说明文件。各个使用界面提供方式不同（例如，在 VS Code 中选择 **Configure Chat → Generate Agent Instructions**，或在 Copilot CLI 中使用 `/init`）；相关界面的课程会在适当位置指出。
>
> 需要模板或起点？可浏览 [awesome-copilot][awesome-copilot]，其中包含说明文件、自定义智能体和其他资源。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## 浏览此项目中的自定义说明文件

花一点时间阅读此存储库附带的说明文件：一个核心的 `copilot-instructions.md`，以及用于不同任务的一系列 `*.instructions.md` 文件。在编辑器或 GitHub Web界面中打开这些文件。

1. 打开 `.github/copilot-instructions.md`。
2. 浏览文件，注意项目简介以及 **Agent notes**、**Code standards**、**Scripts** 和 **Repository Structure** 等章节。在 **Code standards** 下方，请注意嵌套的 **GitHub Actions Workflows** 指导。这些内容适用于与 Copilot 的任何交互。
3. 打开 `.github/instructions` 文件夹并浏览。可注意到其中包含 Astro文件、Drizzle数据层、测试等方面的说明。
4. 打开 `.github/instructions/unit-tests.instructions.md`。注意顶部的 `applyTo` 字段——它设置了一个相对于存储库根目录的 glob，用于确定说明适用范围。此处，任何 TypeScript测试文件（例如匹配 `**/*.test.ts` 的文件）都会匹配。
5. 查看创建此项目单元测试时的具体说明。
6. 最后，打开 `.github/instructions/drizzle.instructions.md` 并滚动到底部。注意其中指向其他说明文件（如 `unit-tests.instructions.md`）和项目现有文件的链接。这样可以将大型说明集拆分为较小的可复用文件，并引导 Copilot 参考可遵循的示例。（其中的路径相对于说明文件，而不是存储库根目录。）

> [!NOTE]
> `copilot-instructions.md` 中的 **Code formatting requirements** 部分记录了项目的编码标准，但尚未要求在代码中添加文档。接下来的步骤中，将添加 TSDoc文档注释和文件注释头的规则。

## 添加新的存储库标准

接下来的唯一编辑工作是在此处添加一个项目级规则：文档应以 TSDoc文档注释和文件级注释头的形式保留在代码中。稍后在此工作坊中为议题分配云智能体时，它会读取并应用此规则。

编辑前，请先创建工作分支（云智能体会根据议题所针对的分支读取说明，但也仍会认真提交编辑）：

1. 在 codespace终端中创建并切换到新分支：

   ```bash
   git checkout -b custom-instructions-cloud
   ```

如前所述，`.github/copilot-instructions.md` 用于向 Copilot 提供项目级信息。现在确保已记录存储库编码标准，以改进代码建议。

1. 重新打开 `.github/copilot-instructions.md`。
2. 找到 **Code formatting requirements** 部分，通常位于第 27 行附近。注意它记录了项目的编码标准，但尚未包含代码内文档规则，这也是生成的辅助函数没有文档注释的原因。
3. 在现有标准下方添加以下 markdown 行，要求 Copilot 添加文件注释头和 TSDoc文档注释：

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. 保存 `copilot-instructions.md`。

> [!TIP]
> 正如上一课所示，可以在存储库级别（`.github/copilot-instructions.md`）创建说明以提供全局指导，也可以使用 `*.instructions.md` 文件为特定语言、文件类型或任务提供说明。对于刚添加的文档注释规则等项目级标准，存储库级文件是合适的位置。

## 提交、推送并合并说明更新

云智能体会从议题所针对的分支读取说明文件。分配议题给 Copilot 的下一练习中，Copilot 将从 `main` 创建分支，因此说明更改必须合并到 `main`，云智能体才能读取。

1. 暂存并提交：

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. 推送分支：

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. 在 github.com 上创建从 `custom-instructions-cloud` 到 `main` 的拉取请求并合并。此后，在下一练习中分配议题时，云智能体将读取这些说明。

> [!TIP]
> 如果希望在本工作坊中直接在 `main` 上操作，可以跳过分支步骤，直接提交到 `main`。保留分支步骤，是为了让工作坊模拟真实项目中的处理方式。

## 总结和后续步骤

已了解 Copilot 如何从说明文件获取上下文，并向 `.github/copilot-instructions.md` 添加了新的存储库级标准。之后云智能体创建的拉取请求将体现该标准。

接下来，将[为 Copilot 云智能体分配第一个议题][next-lesson]。

## 资源

- [GitHub Copilot 自定义说明文件][instruction-files]
- [创建自定义说明的最佳实践][instructions-best-practices]
- [编写更好的 Copilot 自定义说明的 5 个技巧][copilot-instructions-five-tips]
- [Awesome Copilot——说明文件、自定义智能体和其他资源的集合][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
