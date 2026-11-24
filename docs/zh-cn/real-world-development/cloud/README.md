---
slug: zh-cn/real-world-development/cloud
title: "GitHub Copilot 云智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

**[GitHub Copilot 云智能体](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent)** 可以让 GitHub Copilot 在云端异步工作。你在 GitHub 上分配工作，云智能体将在后台接手：探索存储库、修改代码并创建拉取请求，而你可以继续处理其他事务。

在这些练习中，将为云智能体添加它要遵循的自定义说明，然后分配一个 GitHub议题，让它实现相应工作。还将审查并使用自定义智能体来调整其方法，在智能体仪表板中监控并引导会话，最后审查其拉取请求并迭代处理结果。

## 练习

| 练习 | 主题 | 说明 |
|----------|-------|-------------|
| [0. 先决条件][ex0] | 设置 | 创建存储库和 codespace |
| [1. 自定义说明][ex1] | 上下文 | 添加云智能体要遵循的自定义说明 |
| [2. 云智能体][ex2] | 异步智能体 | 将议题分配给 Copilot 云智能体 |
| [3. 自定义智能体][ex3] | 专用智能体 | 审查并使用自定义智能体 |
| [4. 管理智能体][ex4] | 监控 | 监控并引导智能体会话 |
| [5. 迭代][ex5] | 审查 | 审查拉取请求、迭代 Copilot 的工作并选择后续步骤 |

## 先决条件

参加本工作坊前，请确保已具备：

- [ ] 一个已启用 **Copilot Student、Pro、Pro+、Business 或 Enterprise** 付费计划的 GitHub账户
- [ ] 已为账户或组织启用 Copilot 云智能体

> [!TIP]
> 没有付费计划？已验证学生可通过 [GitHub Education][callout-student-plan-education] 免费使用 GitHub Copilot。**Copilot Student** 计划包含智能体、MCP、代码审查和 Copilot CLI 功能，因此可以完整完成本工作坊中的所有路径。

[callout-student-plan-education]: https://github.com/education/students

> [!NOTE]
> Cloud agent 适用于 **Copilot Student、Pro、Pro+、Business 和 Enterprise**；除了 Copilot Free，其他所有计划均可使用。对于 Copilot Business 或 Enterprise，管理员必须为组织启用它。

> [!NOTE]
> 本工作坊不涵盖 MCP。要了解如何将 MCP服务器用于 Copilot，请参阅 [CLI 工作坊](../cli/)或 [VS Code 工作坊](../vscode/)。

## 开始

**[从练习 0：先决条件开始 →][ex0]**

[ex0]: 0-prerequisites/
[ex1]: 1-custom-instructions/
[ex2]: 2-cloud-agent/
[ex3]: 3-custom-agents/
[ex4]: 4-managing-agents/
[ex5]: 5-iterating/
