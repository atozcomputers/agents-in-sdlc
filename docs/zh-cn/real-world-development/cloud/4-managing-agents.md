---
title: "练习 4 - 监控和管理智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

在前几项练习中，已要求 Copilot 云智能体分别处理三项任务，以改善用户体验并添加功能。虽然云智能体本来就用于异步和自主运行，但监控这些任务仍然非常重要。

GitHub.com 上的[智能体页面][agents-page]等工具可用于管理分配给云智能体的任务。在此使命控制台中，可以看到所有包含未合并拉取请求（PR）的智能体任务，查看已执行的操作，甚至引导进行中的会话以提供指导。

本课将：

- 浏览智能体页面以监控云智能体任务。
- 引导进行中的会话，以请求额外功能。

## 场景

分配智能体创建高对比度模式后，团队认为此时也应添加浅色模式。既然已经在更新网站样式并添加切换功能，把此功能一并纳入会更加合理。因此，需要引导智能体的工作，确保它同时添加浅色模式和高对比度模式。

## 审查 Copilot 云智能体任务

现在查看分配给 Copilot 云智能体的全部任务当前状态。

1. 导航到 [Copilot 智能体页面](https://github.com/copilot/agents)。
2. 注意主窗格和左侧窗格中的任务列表。应能看到已分配给 Copilot 的任务，包括：
    - 更新代码库文档。
    - 生成用于修改游戏的 API。
    - 为网站添加高对比度模式。
3. 选择一个正在运行的任务，审查 Copilot 已执行的任务，可能包括：
    - 从存储库检出代码。
    - 为 Copilot 创建运行环境。
    - 设置 MCP服务器。
    - 执行各种步骤以完成分配的任务。

> [!NOTE]
> 列出的具体步骤会因 Copilot 工作状态和所采用方案而有所不同。

4. 同时注意右侧显示的拉取请求（PR）窗格。可借此查看 PR及所更改的文件，以便进一步监控。

## 引导云智能体

现在已查看活跃任务，接下来在 Copilot处理高对比度模式时，请求它包含浅色模式切换。

1. 选择与添加高对比度模式相关的会话。具体标题会因 Copilot 使用的名称及当前工作状态而有所不同。

    ![使命控制台中的无障碍会话](../../../_images/ex6-accessibility-session.png)

2. 持续查看几分钟，直到会话显示已完成设置并开始工作。开始看到与下面类似的消息时，即表示它已进入此状态。
3. 在 **Steer active session while Copilot is working** 对话框中添加以下提示：

    ```plaintext
    While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
    ```

    ![智能体页面中突出显示引导工作中会话对话框的云智能体任务截图](../../../_images/ex6-steer-cloud-agent-task.png)

4. 按 <kbd>Enter</kbd>发送提示。
5. 注意 Copilot 如何确认提示并将其纳入工作流程。

## 让 Copilot 完成工作

与之前一样，Copilot 将开始处理更新后的任务！它会在完成发送消息时正在执行的步骤后，将新请求纳入工作流程。

与之前一样，此过程也需要几分钟；现在正适合暂停片刻，回顾迄今学到和探索的内容。

## 总结和后续步骤

本课探索了 Copilot 智能体页面，即监控和引导 GitHub Copilot 云智能体任务的中央枢纽。通过此使命控制台，可以跟踪所有活跃和已完成的任务、审查正在执行的工作，甚至重定向进行中的任务以调整范围或提供更多指导。

已探索以下概念：

- 浏览使命控制台和智能体页面以监控云智能体任务。
- 重定向进行中的会话，以请求额外功能。

随着 Copilot 完成无障碍功能的工作，现在可以转向[迭代 Copilot 创建的拉取请求][next-lesson]。

## 资源

- [Copilot 智能体页面][agents-page]
- [关于自定义智能体][custom-agents]

---

| [← 上一课：自定义智能体][previous-lesson] | [下一课：迭代 Copilot 的工作 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
