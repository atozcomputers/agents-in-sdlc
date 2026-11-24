---
title: "演習 4 - エージェントの監視と管理"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

直前の演習では、ユーザーエクスペリエンスと機能追加を目的とした3つのタスクを Copilot cloud agent に依頼しました。cloud agent は非同期かつ自律的に作業するよう設計されていますが、これらのタスクを監視できることも重要です。

GitHub.com の[エージェントページ][agents-page]など、cloud agent に割り当てたタスクを管理するためのツールが多数用意されています。この mission control から、open 状態の pull request（PR）があるすべてのエージェントタスクを確認できます。実行された操作を調べ、実行中のセッションを操作して作業をガイドできます。

このレッスンでは、次のことを行います。

- エージェントページを確認して cloud agent のタスクを監視します。
- 実行中のセッションを操作して追加機能を依頼します。

## シナリオ

ハイコントラストモードを作成するエージェントを割り当てた後、ライトモードの追加も適切なタイミングだとチームが判断しました。サイトのスタイル更新とトグル機能の追加はすでに進行中のため、ハイコントラストモードに加えてこの機能を含めるのが自然だと考えました。エージェントの作業を操作し、ハイコントラストモードに加えてライトモードも追加するよう依頼します。

## Copilot cloud agent のタスクを確認する

Copilot cloud agent に割り当てられたすべてのタスクの現在の状態を確認します。

1. [Copilot エージェントページ](https://github.com/copilot/agents)に移動します。
2. メインペインと左ペインのタスク一覧を確認します。割り当てたタスクが表示されます。たとえば、次のようなタスクがあります。
    - コードベースのドキュメント更新
    - ゲーム変更用 API の生成
    - Web サイトへのハイコントラストモードの追加
3. 実行中のタスクを1つ選択し、Copilot が実行したタスクを確認します。次のような操作が含まれる場合があります。
    - リポジトリからコードをチェックアウト
    - Copilot の作業環境を作成
    - MCP サーバーのセットアップ
    - 割り当てられたタスクを完了するための各種ステップ

> [!NOTE]
> 表示される正確なステップは、Copilot の作業状態や使用したアプローチによって異なります。

4. 右側に表示される pull request（PR）ペインにも注目してください。追加の監視に利用して、PRと変更されたファイルを確認できます。

## cloud agent を操作する

アクティブなタスクを確認できたので、ハイコントラストモードの作業中にライトモードのトグルも追加するよう Copilot に依頼します。

1. ハイコントラストモードの追加に関連するセッションを選択します。Copilot が使用する名前と作業の現在の状態によって、正確なタイトルは異なります。

    ![mission control のアクセシビリティセッション](../../../_images/ex6-accessibility-session.png)

2. セットアップが完了して作業を開始したことが表示されるまで、数分間セッションを確認します。次のようなメッセージが表示されれば開始されています。
3. **Steer active session while Copilot is working** ダイアログに次のプロンプトを追加します。

    ```plaintext
    While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
    ```

    ![操作ダイアログが強調表示された、エージェントページの cloud agent タスク画面](../../../_images/ex6-steer-cloud-agent-task.png)

4. <kbd>Enter</kbd> を押してプロンプトを送信します。
5. Copilot がプロンプトを認識し、処理フローに組み込む様子を確認します。

## Copilot に作業を任せる

前と同様に、Copilot が更新されたタスクに取り組みます。メッセージ送信時に Copilot が実行していたステップが完了した後、新しいリクエストを処理フローに組み込みます。

前回と同様に数分かかるため、ここまで学習し確認した内容を振り返るのに適したタイミングです。

## まとめと次のステップ

このレッスンでは、GitHub Copilot cloud agent タスクを監視およびガイドするための中央ハブである Copilot エージェントページについて確認しました。この mission control を使うと、実行中および完了済みのすべてのタスクを追跡し、実行中の作業をレビューし、実行中のタスクをリダイレクトしてスコープを調整したり追加のガイダンスを提供したりできます。

確認した概念は次のとおりです。

- mission control とエージェントページを確認して cloud agent のタスクを監視する方法
- 実行中のセッションをリダイレクトして追加機能を依頼する方法

Copilot がアクセシビリティ機能の作業を完了する間、Copilot が作成した[ pull request を反復改善][next-lesson]する作業に移ります。

## リソース

- [Copilot エージェントページ][agents-page]
- [カスタムエージェントについて][custom-agents]

---

| [← 前のレッスン: カスタムエージェント][previous-lesson] | [次のレッスン: Copilot の作業を反復改善 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
