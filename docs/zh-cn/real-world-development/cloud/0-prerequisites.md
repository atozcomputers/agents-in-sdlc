---
title: "练习 0：先决条件"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

开始 Copilot 云智能体练习前，需要准备好所有内容。将创建自己的 Tailspin Toys 存储库副本，并启动一个可用于编辑说明文件和审查云智能体工作成果的[codespace][codespaces]。

## 设置实验存储库

要为将创建的代码创建存储库副本，需要从[模板][template-repository]创建实例。新实例将包含实验所需的全部文件，并将在练习过程中使用。

1. 在新的浏览器窗口中，导航到 [Tailspin Toys 模板][tailspin-template]。
2. 在实验存储库页面选择 **Use this template** 按钮，创建自己的存储库副本；然后选择 **Create a new repository**。

    ![Use this template 按钮](../../../_images/ex0-use-template.png)

3. 如果正在参加由 GitHub 或 Microsoft 主持的研讨会，请按照导师提供的说明操作。否则，可以在有权访问 GitHub Copilot 的组织中创建新存储库。

    ![输入存储库模板设置](../../../_images/ex0-repository-settings.png)

4. 记下所创建的存储库路径（**组织或用户名/存储库名**），稍后练习中会用到。

## 创建 codespace

接下来，使用 codespace 完成本工作坊练习。

[GitHub Codespaces][codespaces]是一种基于云的开发环境，可直接在浏览器中编写、运行和调试代码。它提供功能完整的 IDE，并支持多种编程语言、扩展和工具。

1. 导航到新创建的存储库。
2. 选择绿色的 **Code** 按钮。

    ![选择 Code 按钮](../../../_images/ex0-code-button.png)

3. 选择 **Codespaces** 选项卡，然后选择 **+** 按钮创建新的 Codespace。

    ![创建新的 codespace](../../../_images/ex0-create-codespace.png)

创建 codespace 通常需要几分钟，但这仍比手动安装所有服务快得多！在等待期间，可以浏览 GitHub Copilot 的其他功能；下一步将介绍这些功能。

> [!CAUTION]
> 在后续练习中会返回此 codespace。暂时请将其保留在浏览器标签页中。

> [!NOTE]
> 本工作坊既可在 codespace 中运行，也可在本地 [dev container][dev-containers] 中运行。两者都能确保环境已安装顺畅体验所需的全部先决条件。如果希望在本地运行，请在 VS Code 中打开克隆的存储库，并在提示时选择 **Reopen in Container**；VS Code 将构建与 codespace 相同的 dev container。

[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers

## 总结

祝贺你创建了实验存储库副本！同时也已开始创建 codespace，后续将在其中与 Copilot 云智能体协作。

## 下一步

接下来添加云智能体要遵循的自定义说明。继续学习[练习 1 - 自定义说明][next-lesson]。

## 资源

- [GitHub Codespaces 概述][codespaces]
- [从模板创建存储库][template-repository]
- [Codespaces 入门][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[next-lesson]: ../1-custom-instructions/
