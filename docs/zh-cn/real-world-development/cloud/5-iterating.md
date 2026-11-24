---
title: "练习 5：迭代 GitHub Copilot 的工作"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 上一课：管理智能体][previous-lesson] |
|:--|

## 审查工作成果

在本实验中，已经与 GitHub Copilot 处理了多个旨在改善用户体验和添加功能的任务。已要求 Copilot 为代码添加文档，为设计团队构建可迭代的相关游戏功能，并实现包括高对比度模式和浅色模式切换在内的无障碍功能。接下来将探索代码更改，并在必要时向 Copilot 提供反馈以改进成果。

### 场景

前面已经多次强调，生成式 AI不会改变软件设计和 DevOps的基本原则。始终应审查生成的代码，并按照常规 DevOps流程处理。基于此，在向团队中的其他成员开放审查之前，应先审查 GitHub Copilot为文档、相关游戏功能和无障碍功能提出的建议。

## 安全与 GitHub Copilot 云智能体

由于 Copilot 云智能体异步且无人监督地执行任务，因此已设置特定安全限制以确保工作安全。包括：

- Copilot 对存储库只有读取权限，并且只能对用于编写代码的分支具有写入权限。
- 云智能体在 GitHub Actions 内运行，并会创建独立、临时的环境来执行工作。
- 任何 GitHub Actions 工作流都需要人工批准后才能运行。
- 默认情况下，[对外部资源的访问受到限制](https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall)，包括 MCP服务器。

## 审查生成的文档

先探索 GitHub Copilot 云智能体生成的第一个拉取请求（PR），即为代码添加文档。可使用 github.com上的标准 PR界面完成此任务。

> [!NOTE]
> 查看 PR时，可能会看到 GitHub Copilot 被防火墙阻止的警告。这是**预期行为**，因为 Copilot 默认对外部资源的访问受限，包括访问外部 MCP服务器。如有需要，可以[为 Copilot 云智能体自定义或禁用防火墙][agent-firewall]。

1. 返回存储库的 github.com页面。
2. 选择 **Pull Requests** 打开拉取请求列表。
3. 打开标题类似于 **Add missing documentation** 或更加具体的拉取请求。

> [!NOTE]
> 如果 Copilot仍在处理任务，拉取请求会包含 **[WIP]**标记。如遇此情况，请等待 Copilot完成工作。这可能需要几分钟；可以休息片刻或回顾迄今学到的内容。

4. 拉取请求准备就绪后，选择 **Files changed**选项卡并审查更改。

    ![Files changed选项卡](../../../_images/shared-pr-files-changed.png)

5. 浏览新更新的代码，其中包括新建的 TSDoc文档注释和其他文档。具体更改可能有所不同。

    查看更改时，请留意 TSDoc文档注释、TypeScript约定和注释头。这些内容来自练习 2 开始时审查的自定义说明文件。

6. 审查更新并确认无误后，返回 **Conversation**选项卡并向下滚动。
7. 应看到一些工作流正在等待批准的指示。
8. 如果工作流正在等待批准，请选择 **Approve and run workflows**。

   ![批准并运行工作流](../../../_images/shared-approve-workflows.png)

9. 应看到工作流已在拉取请求的检查部分排队。通常情况下，单个 Astro应用的项目检查会通过。此过程可能需要几分钟。

## 向 GitHub Copilot 请求更改

与拉取请求中的 Copilot协作不是单向流程。也可以在拉取请求的评论或代码行内评论中像提及其他团队成员一样提及 Copilot。Copilot 会看到这些评论，并启动另一个会话来处理。由于结果具有不确定性，无法提供固定措辞来规定应提出什么要求。以下是可要求 Copilot更新的示例：

- 在每个代码文件顶部添加简要说明用途的注释头。
- 为 TypeScript和 Astro文件添加 TSDoc文档注释。
- 创建 README，说明 Astro应用的结构。

1. 添加评论，请求对生成的文档进行更改，并像提及其他用户一样通过 **@copilot** 提及它。可使用上述建议之一，也可提出希望在代码库中看到的其他文档改进。
2. 选择 **View Session** 查看 Copilot执行工作。注意 Copilot如何启动新会话并进行更新。
3. 可以选择 **Back to pull request** 返回拉取请求。

    ![返回拉取请求](../../../_images/ex7-back-to-pr.png)

4. Copilot完成更改后，应看到拉取请求中出现新的提交。
5. 选择 **Files changed**选项卡以审查更改。

可以继续迭代，直到满意为止。满意后，可将 PR从草稿状态设为就绪，并合并到 main 分支。

![将 PR设为就绪](../../../_images/ex7-ready-for-review.png)

## 审查相关游戏功能

下面回到 Copilot为解决游戏详情页显示相关游戏的议题而生成的 PR。

1. 返回 github.com上的存储库。
2. 选择 **Pull Requests**选项卡。
3. 选择标题类似于 **Show related games on the game details page** 或更加具体的 PR。
4. 选择 **Files changed**选项卡以审查其生成的代码。
5. 审查更新并确认无误后，返回 **Conversation**选项卡并向下滚动。
6. 应看到一些工作流正在等待批准的指示。
7. 如果工作流正在等待批准，请选择 **Approve and run workflows**。

   ![批准并运行工作流](../../../_images/shared-approve-workflows.png)

8. 应看到工作流已在拉取请求的检查部分排队。通常情况下，单个 Astro应用的项目检查会通过。此过程可能需要几分钟。
9. **可选：** 可以在 Codespace中切换到此分支，对相关游戏功能进行手动测试。导航到 Codespace，打开终端并运行以下命令（将 `<branch-name>`替换为 Copilot创建的分支名，例如 **copilot/fix-8**）：

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

Copilot已构建相关游戏功能！与之前一样，可以通过迭代与 Copilot 云智能体协作，请求更新。例如，可以要求 Copilot调整相关游戏的显示数量，或确保添加注释头和 TSDoc文档注释（请记住，此任务是在更新自定义说明**之前**分配的！）与之前一样，可在 **Conversation**选项卡中添加新评论提出这些请求；Copilot 会看到评论并启动新会话。

## 审查无障碍功能

最后，审查由自定义无障碍智能体实现的无障碍功能。此 PR应同时包含练习 3 中分配的高对比度模式，以及练习 4 中在使命控制台中请求的浅色模式。

1. 返回 github.com上的存储库。
2. 选择 **Pull Requests**选项卡。
3. 选择标题类似于 **Add high contrast mode to website** 或更加具体的 PR。

> [!NOTE]
> 如果 Copilot 仍在处理任务，拉取请求会包含 **[WIP]** 标记。如遇此情况，请等待 Copilot 完成工作。这可能需要几分钟。

4. 选择 **Files changed**选项卡以审查其生成的代码。
5. 审查实现，尤其注意：
   - 用于在模式间切换的切换界面组件
   - 使用本地存储持久保存用户偏好
   - 高对比度和浅色模式的 CSS或样式更改
   - 无障碍属性（ARIA标签、键盘导航等）
   - 管理模式切换的 JavaScript/TypeScript代码

6. 审查更新并确认无误后，返回 **Conversation**选项卡并向下滚动。
7. 应看到一些工作流正在等待批准的指示。
8. 如果工作流正在等待批准，请选择 **Approve and run workflows**。

   ![批准并运行工作流](../../../_images/shared-approve-workflows.png)

9. 应看到工作流已在拉取请求的检查部分排队。通常情况下，单个 Astro应用的项目检查会通过。此过程可能需要几分钟。
10. **可选：** 可以在 Codespace中切换到此分支，手动测试无障碍功能。导航到 Codespace，打开终端并运行以下命令（将 `<branch-name>`替换为 Copilot创建的分支名）：

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

    然后启动应用，并在浏览器中测试高对比度模式和浅色模式切换，以确认它们按预期工作，并可在页面重新加载后继续生效。

注意自定义无障碍智能体如何引导 Copilot按照无障碍最佳实践实现这些功能。如果发现无障碍问题或改进点，可以像前几个 PR一样，在评论中通过 **@copilot** 请求更新。

## 可选练习——继续委派

将真实积压工作交给云智能体并腾出时间处理其他事务时，效果最佳。养成此习惯，可以在存储库中再提交几个议题并分配给 Copilot。示例包括：

- 在游戏详情页创建资助者兴趣表。
- 在游戏列表页实现分页。
- 为数据访问辅助函数添加输入验证和错误处理。

## 总结

已完成 Cloud agent工作坊。在这些课程中：

- **检查了此存储库附带的自定义说明文件**，以便观察它们在云智能体输出中的作用。
- **将议题分配给 Copilot 云智能体**，并查看其设置环境、规划和异步执行的过程。
- **创建并使用自定义无障碍智能体**，添加高对比度模式和浅色模式切换。
- **将 Copilot智能体页面用作使命控制台**，在会话进行中监控并引导无障碍会话。
- **审查并迭代云智能体的拉取请求**，通过提及 `@copilot`请求更改并批准工作流。

## 审查和后续步骤

已完成 Cloud agent工作坊。如果希望继续探索，其他工作坊可以补充此处的实践：

- 🖥️ **[VS Code 工作坊](../../vscode/)**——直接在 IDE中通过 Copilot Chat智能体模式和 MCP集成进行探索。
- 💻 **[CLI 工作坊](../../cli/)**——在终端中交付两个经过审查的更改，使用计划和自动驾驶模式、智能体技能、自定义 QA智能体、Playwright MCP、Agent Merge，以及可选的 `/delegate`桥接回云智能体。

在自己的存储库中，可尝试以下后续操作：

- 将重构或测试覆盖率议题分配给云智能体。
- 为其他领域创建自定义智能体。
- 为其他技术栈设置 `copilot-setup-steps.yml`。

## 资源

- [GitHub Copilot][github-copilot]
- [关于 Copilot智能体][copilot-agents]
- [将 GitHub议题分配给 Copilot][assign-issue]
- [Copilot 云智能体设置工作流最佳实践][cloud-agent-best-practices]
- [配置 Copilot 云智能体防火墙][agent-firewall]

---

| [← 上一课：管理智能体][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall

[previous-lesson]: ../4-managing-agents/
