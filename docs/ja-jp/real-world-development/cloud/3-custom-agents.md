---
title: "演習 3 - カスタムエージェント"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## カスタムエージェントとは

GitHub Copilot の[カスタムエージェント][custom-agents-concept]を使用すると、開発ワークフロー内の特定のタスクや領域に合わせた専門 AI アシスタントを作成できます。リポジトリの `.github/agents` フォルダーに Markdown ファイルでエージェントを定義し、特定の作業を効果的に実行するための、絞り込まれた指示、ベストプラクティス、コーディングパターン、ドメイン固有の知識を Copilot に提供できます。チームは専門知識を再利用可能なエージェントとしてコード化できます。たとえば、[WCAG][wcag]準拠を強制するアクセシビリティエージェント、セキュアコーディングプラクティスに従うセキュリティエージェント、一貫したテストパターンを維持するテストエージェントなどです。

カスタムエージェントは、プロジェクトの `.github/agents` フォルダーまたはグローバルな `~/.copilot/agents` にある Markdown ファイルで定義します。各ファイルには、少なくとも `name` と `description` を含む YAML フロントマターがあり、続いてエージェントの動作、専門知識、指示を定義する Markdown プロンプトがあります。

### カスタムエージェントとエージェントスキルの比較

カスタムエージェントと[エージェントスキル][agent-skills-concept]には一定の重複があります。どちらも主に Markdown ファイルで定義され、AI に操作方法を指示します。両者を区別する最も簡単な方法は、**カスタムエージェント**が作業者であり、**スキル**がツールだと考えることです。

カスタムエージェントには独自のコンテキストウィンドウがあり、スキル（場合によっては他のエージェント）をオーケストレーションして作業を実行するために構築されています。このラボでは、アクセシビリティカスタムエージェントがアクセシビリティガイドラインに照らしてサイトを確認し、更新します。この作業では、pull request ワークフロースキルやテストの実行と管理を行うスキルなどを呼び出せます。

> [!NOTE]
> カスタムエージェントを作成する唯一の正解はありません。AI の他の用途と同様に、テストと反復により環境やシナリオに最適な方法を見つけてください。

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/
次のカスタムエージェントについて確認します。

- カスタムエージェントを定義する方法
- カスタムエージェントにタスクを割り当てる方法

## シナリオ

Tailspin Toys は、視覚的な能力や設定に関係なく、クラウドファンディングプラットフォームがすべてのユーザーにとってアクセシブルであることを目指しています。最近のユーザーフィードバックでは、テキストと背景色のコントラストが不足しているため、一部のユーザーが現在のダークテーマを読みづらいと感じています。このアクセシビリティ上の問題に対応するため、デザインチームはユーザーがオンとオフを切り替えられるハイコントラストモードの実装を依頼しました。

アクセシビリティは重要なため、可能な限り迅速に実装できるようにしたいと考えています。カスタムエージェントを使用して機能を生成します。
## アクセシビリティカスタムエージェントを確認する

アクセシビリティ用のカスタムエージェントがすでに作成されています。内容を確認して、Copilot のガイド方法を理解しましょう。

codespace に戻り、アクセシビリティカスタムエージェントのファイルを確認してください。

1. `.github/agents/accessibility.md` を開きます。
2. `name` と `description` フィールドを含む YAML フロントマターを確認します。

> [!CAUTION]
> カスタムエージェントには、`name` と `description` を含むフロントマターが必要です。

3. 続いて、次の内容を示すセクションを確認します。
   - アクセシブルな Web サイトのコード生成時の主要な責務
   - アクセシビリティのベストプラクティス
   - HTML、CSS、JavaScript のコード例
   - よくある落とし穴とエラーの一覧
## Issue を作成して割り当てる

Mission control は、環境内のすべてのエージェントを操作するための中央拠点です。Copilot cloud agent にタスクを割り当て、タスクを監視し、作業をリダイレクトして追加のガイダンスを提供できます。ハイコントラストモードを作成するタスクを割り当てることから始めましょう。

1. リポジトリに移動します。
2. issues タブを選択します。
3. **New issue** を選択して、新しい Issue ダイアログを開きます。
4. **Blank issue** を選択して、新しい Issue を作成します。
5. **Title** を `Add high contrast mode to website` に設定します。
6. **Description** を次のように設定します。

    ```plaintext
    We need a high contrast mode for the site. There should be a toggle for high contrast which the user can set. It should store the setting in local storage on the browser.
    ```

7. **Create** を選択して Issue を作成します。
8. 右側で **Assign to Copilot** を選択して割り当てダイアログを開きます。
9. カスタムエージェントの一覧から **Accessibility agent** を選択します。

    ![カスタムエージェントとアクセシビリティを強調表示した cloud agent の割り当て画面](../../../_images/ex5-select-custom-agent.png)

10. **Assign** を選択します。
11. Copilot がバックグラウンドでタスクに取り組みます。

## まとめと次のステップ

このレッスンでは、特定のタスクや領域に合わせた専門 AI アシスタントである GitHub Copilot の[カスタムエージェント][custom-agents]について確認しました。カスタムエージェントを使用すると、チームの専門知識と規約を再利用可能なエージェントとしてコード化し、Copilot が特定の作業をより効果的に実行できるようにできます。

確認した概念は次のとおりです。

- カスタムエージェントを定義する方法
- カスタムエージェントにタスクを割り当てる方法

Copilot がハイコントラストモードの実装を進めている間、mission control から[エージェントセッションの監視と操作][next-lesson]に注目を移せます。

## リソース

- [カスタムエージェントについて][custom-agents]
- [組織でカスタムエージェントを使用する準備][org-custom-agents]
- [エンタープライズでカスタムエージェントを使用する準備][enterprise-custom-agents]

---

| [← 前のレッスン: GitHub Copilot cloud agent][previous-lesson] | [次のレッスン: エージェントの監視と管理 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
