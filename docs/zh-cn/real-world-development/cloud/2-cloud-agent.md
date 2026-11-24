---
title: "练习 2 - GitHub Copilot 云智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 上一课：自定义说明][previous-lesson] |
|:--|

很少有组织完全没有技术债务。这可能包括未解决的安全问题、需要更新的遗留代码，或因暂时没有时间实现而积压许久的功能请求。GitHub Copilot 云智能体适合执行更新代码、添加功能等任务，而且完全采用自主方式。智能体完成工作后，会生成可供开发人员审查的草稿拉取请求。这样可以卸载繁琐任务，加快开发进度，并让开发人员专注于更宏观的事项。

以下内容将通过 Copilot 云智能体进行探索：

- 自定义用于生成代码的环境。
- 确保操作安全执行。
- 明确界定议题范围的重要性。
- 将议题分配给 Copilot。

## 场景

Tailspin Toys 希望处理一些技术债务。最初受聘创建网站第一版的承包商留下的文档状态并不理想——更确切地说，文档几乎完全缺失。作为第一步，他们希望为应用程序中所有导出的函数添加 TSDoc文档注释。

此外，设计团队已准备改进游戏发现体验。他们希望在每款游戏的详情页展示相关游戏，即同一类别中的其他作品，以便用户继续浏览。暂时不需要精美实现，只需一个可用于UX验收测试的可用版本。此工作目前属于阻塞项，但还有优先级更高的议题。

这两个任务都很容易被延后处理，非常适合分配给 Copilot 云智能体。Copilot 云智能体会异步处理任务，让开发人员能够专注于其他工作，然后回来审查 Copilot 的成果并确认是否符合预期。

## 介绍 GitHub Copilot 云智能体

[GitHub Copilot 云智能体](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent) 可以在后台执行任务，方式与人类开发人员类似。就像与人类协作一样，它可以通过多种方式接收任务，包括[将 GitHub议题分配给 Copilot](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions)。分配后，Copilot 会创建草稿拉取请求以跟踪进度、设置环境并开始工作。可以在会话进行中或完成后查看会话内容。准备好审查建议方案时，Copilot 会在拉取请求中提及你！

## 明确界定说明范围的重要性

GitHub Copilot 中没有魔法，也不能跳过思考环节。即使看似简单的操作，在深入分析后也可能包含复杂内容，因此请[注意如何为 Copilot 云智能体界定任务范围][cloud-agent-best-practices]。可以把它当作 AI结对编程伙伴：分阶段工作、学习、实验并随时调整。生成式 AI 的加入不会改变软件开发的基本原则。

## 此存储库中的自定义说明

前面的练习介绍了自定义说明及其对 Copilot 的指导作用。如果已完成过自定义说明实践，就已在实际操作中看到 `.github/copilot-instructions.md`；如果没有，现在是快速查看它的好时机。在分配工作给 Copilot 云智能体之前，以只读方式查看存储库中已有的说明文件，以便稍后观察其效果。

在 GitHub Web界面或已运行的 codespace 中打开以下文件：

- `.github/copilot-instructions.md`——审查 **Code standards** 部分，尤其是 TypeScript约定和 TSDoc文档注释方面的要求。
- `.github/instructions/unit-tests.instructions.md`——注意 `applyTo` 前置元数据，它将这些说明限定到 `**/*.test.ts` 文件。

在下一节将 `Code lacks documentation`议题分配给云智能体后，可在生成的拉取请求中查看 TSDoc文档注释、TypeScript约定和注释头；这些内容都来自说明文件。稍后练习审查拉取请求时会再次指出这一点。

## 为 Copilot 云智能体设置开发环境

无论由谁参与，创建代码通常都需要特定环境，并运行一些设置脚本以确保环境处于可用状态。将任务分配给 Copilot 时也是如此，因为它也会像软件工程师那样执行任务。

执行任务时，云智能体使用 [GitHub Actions][github-actions] 作为运行环境。可以通过在 `.github/workflows/copilot-setup-steps.yml` 中配置的[专用设置工作流][setup-workflow]来自定义此环境；该工作流会在智能体开始工作前运行，使其能够访问所需的开发工具和依赖项。实验已预先配置此工作流，以确保流程顺畅并提供学习机会。工作流会确保 Copilot 能访问 Node.js、项目依赖项、用于端到端测试的浏览器二进制文件，以及用于单个 Astro应用的迁移并填充的 SQLite数据库：

```yaml
name: "Copilot Setup Steps"

# 允许在存储库的“Actions”选项卡中测试设置步骤
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # 将权限设置为运行步骤所需的最低权限。Copilot 将获得自己的令牌来执行操作。
    permissions:
      # 如果设置步骤需要克隆存储库（例如安装依赖项），则需授予 `contents: read` 权限。如果设置步骤不克隆存储库，Copilot 会在步骤完成后自动执行。
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # 前端 / 应用设置——Node.js（整个应用现在基于 Astro + Drizzle/libSQL）
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

      # 迁移并填充本地 SQLite 数据库，以便构建和测试拥有数据。
      - name: Set up the database
        run: npm run db:setup
```

它看起来与其他 GitHub工作流文件相同，但有几个关键点：

- 工作流只包含一个名为 `copilot-setup-steps` 的作业。Copilot 开始处理拉取请求前，此作业会在 GitHub Actions 中执行。
- 注意 `workflow_dispatch` 触发器，它允许在存储库的 **Actions**选项卡中手动运行工作流。此方式可用于测试工作流是否成功运行，而无需等待 Copilot 触发。

## 添加文档

虽然每个人都理解文档的重要性，但大多数项目要么文档已过时，要么完全缺失。这类技术债务常常得不到处理，不仅会降低生产力，还会使代码库更难维护，并增加新开发人员融入团队的难度。幸运的是，Copilot 擅长创建文档，这正是适合分配给 Copilot 云智能体的议题。它会在后台生成所需文档。在后续练习中，将回来审查成果。

1. 在新的浏览器标签页中导航到存储库的 github.com 页面。
2. 选择 **Issues**选项卡。
3. 选择 **New issue** 打开新议题对话框。
4. 选择 **Blank issue** 创建空白议题。
5. 将 **Title** 设置为 `Code lacks documentation`。
6. 将 **Description** 设置为：

    ```plaintext
    Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
    ```

7. 选择 **Create** 创建议题。
8. 在右侧选择 **Assign to Copilot** 打开分配对话框。

  ![将 Copilot 分配给议题](../../../_images/shared-assign-copilot.png)

9. 选择 **Assign**。

  ![Copilot 分配详细信息](../../../_images/ex4-assign-copilot-details.png)

10. 选择 **Pull Requests**选项卡。
11. 打开新生成的拉取请求；标题可能类似于 `[WIP]: Code lacks documentation`。如果列表中尚未出现，等待片刻并刷新浏览器。
12. 几分钟后，应看到 Copilot 已创建待办事项列表。

> [!NOTE]
> Copilot 在拉取请求中显示待办事项可能需要几分钟。Copilot 正在创建环境（运行前述工作流）、分析项目，并确定解决问题的最佳方案。

13. 查看列表和计划执行的任务。
14. 向下滚动拉取请求时间线，应看到 Copilot 已开始处理议题的更新。
15. 选择 **View session** 按钮。

  ![Copilot 会话视图](../../../_images/ex4-view-session.png)

> [!CAUTION]
> 如果看不到更新后的指示器，可能需要刷新窗口。

16. 注意可以在实时会话中向下滚动，了解 Copilot 如何解决问题，包括探索代码、理解状态、暂停思考并决定合适计划，以及创建代码。

这可能需要几分钟。Copilot 云智能体的主要目标之一，是让它异步执行任务，释放开发人员的时间处理其他工作。接下来将利用这一特性：向 Copilot 云智能体分配另一项任务，同时开始编写代码，为应用添加功能。

## 在游戏详情页添加相关游戏分区

正如前面所述，Copilot 云智能体的一大优势是能够分工：你专注于一组任务，而它专注于另一组任务。虽然为设计团队添加相关游戏分区可能用不了很长时间，但节省下来的时间仍可用于其他工作。接下来将议题分配给 Copilot 云智能体！

1. 返回 github.com 上的存储库。
2. 选择 **Issues**选项卡。
3. 选择 **New issue** 打开新议题对话框。
4. 选择 **Blank issue** 使用空白模板。
5. 将 **Title** 设置为：`Show related games on the game details page`
6. 将 **Description** 设置为：

    ```markdown
    We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
   ```

7. 选择 **Create** 创建议题。
8. 在右侧选择 **Assign to Copilot** 打开分配对话框。

  ![将 Copilot 分配给议题](../../../_images/shared-assign-copilot.png)

9. 选择 **Assign**。

不久后，第一个议题评论中会看到一组 👀，表示 Copilot 已开始工作！

![Copilot 使用眼睛表情表示正在处理议题](../../../_images/ex4-issue-eyes-emoji.png)

Copilot 现在正在认真处理第二项请求！Copilot 云智能体的工作方式与软件工程师类似，因此无需持续监控，只需在完成后审查即可。接下来将注意力转向创建和使用自定义智能体。

## 总结和后续步骤

本课探索了 [GitHub Copilot 云智能体][copilot-agents]。使用云智能体，可以将议题分配给 Copilot，使其异步执行工作。可以使用 Copilot 处理技术债务、创建新功能，或协助将代码从一个框架迁移到另一个框架。

已探索以下概念：

- 自定义用于生成代码的环境。
- 确保操作安全执行。
- 明确界定议题范围的重要性。
- 将议题分配给 Copilot。

Copilot 正在后台认真工作，接下来将关注创建和使用自定义智能体。[Copilot 云智能体也可以使用 MCP服务器][cloud-agent-mcp]，并可使用自定义说明；这些说明已在前面的模块中介绍。

## 资源

- [关于 Copilot 云智能体][copilot-agents]
- [将 GitHub议题分配给 Copilot][assign-issue]
- [Copilot 云智能体设置工作流最佳实践][cloud-agent-best-practices]

| [下一课：自定义智能体 →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
