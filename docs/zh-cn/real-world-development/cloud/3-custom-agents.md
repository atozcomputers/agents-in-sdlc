---
title: "练习 3 - 自定义智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## 什么是自定义智能体？

GitHub Copilot 中的[自定义智能体][custom-agents-concept]允许为开发工作流中的特定任务或领域创建专用 AI助手。通过在存储库的 `.github/agents` 文件夹中使用 markdown 文件定义智能体，可以向 Copilot 提供聚焦说明、最佳实践、编码模式和领域知识，引导它更高效地完成特定类型的工作。团队可以将专业知识固化为可复用智能体，例如强制遵循 [WCAG][wcag] 合规性的无障碍智能体、遵循安全编码实践的安全智能体，或维持一致测试模式的测试智能体。

自定义智能体由项目的 `.github/agents` 文件夹中的 markdown 文件定义，也可全局存放在 `~/.copilot/agents`。每个文件都具有至少包含 `name` 和 `description` 的 YAML前置元数据，后跟定义智能体行为、专业知识和说明的 markdown提示词。

### 自定义智能体与智能体技能的区别

自定义智能体与[智能体技能][agent-skills-concept]存在一定逻辑重叠。两者主要都通过 markdown 文件定义，并用于指导 AI 如何执行操作。区分它们最直接的方式是：**自定义智能体**是执行者，而**技能**是工具。

自定义智能体拥有自己的上下文窗口，并可在工作过程中编排技能乃至其他智能体。在本实验中，无障碍自定义智能体会根据无障碍指南审查并更新网站；工作中可以调用拉取请求工作流技能或运行并管理测试的技能。

> [!NOTE]
> 编写自定义智能体没有唯一“正确”的方式。与其他 AI应用一样，需要通过测试和迭代来确定其是否适合特定环境和场景。

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

以下内容将通过自定义智能体进行探索：

- 如何定义自定义智能体。
- 如何向自定义智能体分配任务。

## 场景

Tailspin Toys 致力于确保众筹平台对所有用户无障碍使用，无论用户的视觉能力或偏好如何。近期用户反馈显示，由于文本与背景之间的对比度不足，一些用户觉得当前深色主题难以阅读。为解决这一无障碍问题，设计团队要求实现用户可开关的高对比度模式。

无障碍是关键要求，因此希望尽快实现此功能。接下来将使用自定义智能体生成相应功能。

## 审查无障碍自定义智能体

实验已预先创建了无障碍自定义智能体。审查其内容，以了解它将如何指导 Copilot。

返回 codespace，然后审查无障碍自定义智能体文件：

1. 打开 `.github/agents/accessibility.md`。
2. 注意其中包含 `name` 和 `description` 字段的 YAML前置元数据。

> [!CAUTION]
> 自定义智能体必须包含带有 `name` 和 `description` 的前置元数据。

3. 然后浏览并审查以下章节：
   - 为无障碍网站生成代码时的核心职责。
   - 无障碍最佳实践。
   - HTML、CSS 和 JavaScript代码示例。
   - 常见陷阱和错误列表。

## 创建议题并分配任务

使命控制台是管理当前环境中所有智能体工作的中心位置。可将任务分配给 Copilot 云智能体、监控任务，甚至重定向任务并提供更多指导。现在开始分配创建高对比度模式的任务。

1. 导航到存储库。
2. 选择议题选项卡。
3. 选择 **New issue** 打开新议题对话框。
4. 选择 **Blank issue** 创建空白议题。
5. 将 **Title** 设置为 `Add high contrast mode to website`。
6. 将 **Description** 设置为：

    ```plaintext
    We need a high contrast mode for the site. There should be a toggle for high contrast which the user can set. It should store the setting in local storage on the browser.
    ```

7. 选择 **Create** 创建议题。
8. 在右侧选择 **Assign to Copilot** 打开分配对话框。
9. 从自定义智能体列表中选择 **Accessibility agent**。

    ![突出显示自定义智能体和无障碍智能体的云智能体分配截图](../../../_images/ex5-select-custom-agent.png)

10. 选择 **Assign**。
11. Copilot将在后台开始处理任务！

## 总结和后续步骤

本课探索了 GitHub Copilot 中的[自定义智能体][custom-agents]；它们是针对特定任务和领域量身定制的专用 AI助手。通过自定义智能体，可以将团队的专业知识和标准固化为可复用智能体，引导 Copilot 更高效地完成特定类型的工作。

已探索以下概念：

- 如何定义自定义智能体。
- 如何向自定义智能体分配任务。

Copilot 正在实现高对比度模式，接下来可在使命控制台中[监控并引导智能体会话][next-lesson]。

## 资源

- [关于自定义智能体][custom-agents]
- [在组织中准备使用自定义智能体][org-custom-agents]
- [在企业中准备使用自定义智能体][enterprise-custom-agents]

---

| [← 上一课：GitHub Copilot 云智能体][previous-lesson] | [下一课：监控和管理智能体 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
