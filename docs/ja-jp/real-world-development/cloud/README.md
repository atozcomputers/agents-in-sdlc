---
slug: ja-jp/real-world-development/cloud
title: "GitHub Copilot cloud agent"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

**[GitHub Copilot cloud agent](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent)** を使うと、GitHub Copilot がクラウド上で非同期に作業できます。GitHub 上で作業を割り当てると、cloud agent がバックグラウンドで作業を引き受けます。リポジトリを調査し、変更を加え、pull request を作成する間、他の作業に集中できます。

これらの演習では、cloud agent が従うカスタム指示を追加し、GitHub Issue を割り当てて実装させます。その後、カスタムエージェントを確認して使用し、作業の進め方を調整し、エージェントダッシュボードからセッションを監視して操作し、最後に pull request をレビューして結果を反復改善します。

## 演習

| 演習 | トピック | 説明 |
|----------|-------|-------------|
| [0. 前提条件][ex0] | セットアップ | リポジトリと codespace を作成します |
| [1. カスタム指示][ex1] | コンテキスト | cloud agent が従うカスタム指示を追加します |
| [2. Cloud Agent][ex2] | 非同期エージェント | Copilot cloud agent に Issue を割り当てます |
| [3. カスタムエージェント][ex3] | 専門エージェント | カスタムエージェントを確認して使用します |
| [4. エージェントの管理][ex4] | 監視 | エージェントセッションを監視して操作します |
| [5. 繰り返し改善][ex5] | レビュー | PR をレビューし、Copilot の作業を反復改善して次のステップを選択します |

## 前提条件

このワークショップに参加する前に、次の準備をしてください。

- [ ] 有効な **Copilot Student、Pro、Pro+、Business、Enterprise** のいずれかのプランが設定された GitHub アカウント
- [ ] アカウントまたは組織で Copilot cloud agent が有効になっていること

> [!TIP]
> 有料プランを利用していない場合、認証済みの学生は [GitHub Education][callout-student-plan-education] を通じて GitHub Copilot を無料で利用できます。**Copilot Student** プランには、このワークショップで使用するエージェント、MCP、コードレビュー、Copilot CLI の各機能が含まれているため、すべてのハーネスを完了できます。

[callout-student-plan-education]: https://github.com/education/students

> [!NOTE]
> cloud agent は **Copilot Student、Pro、Pro+、Business、Enterprise** で利用できます。Copilot Free を除くすべてのプランで利用できます。Copilot Business または Enterprise を使用する場合、管理者が組織で有効にする必要があります。

> [!NOTE]
> このハーネスでは MCP を扱いません。Copilot で MCP サーバーを使用する方法については、[CLI ハーネス](../cli/) または [VS Code ハーネス](../vscode/) を参照してください。

## はじめる

**[演習 0「前提条件」から始める →][ex0]**

[ex0]: 0-prerequisites/
[ex1]: 1-custom-instructions/
[ex2]: 2-cloud-agent/
[ex3]: 3-custom-agents/
[ex4]: 4-managing-agents/
[ex5]: 5-iterating/
