---
title: "演習 2 - GitHub Copilot cloud agent"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 前のレッスン: カスタム指示][previous-lesson] |
|:--|

技術的負債に苦慮していない組織はほとんどありません。未解決のセキュリティ問題、更新が必要なレガシーコード、実装する時間がないためにバックログで放置されている機能要望などが該当します。GitHub Copilot の cloud agent は、コードの更新や機能追加などのタスクを自律的に実行できます。作業が完了すると、人間の開発者がレビューできるドラフト PR を生成します。これにより、単調なタスクを任せられ、開発プロセスを加速できるため、開発者はより大きな課題に集中できます。

Copilot cloud agent では次のことを確認します。

- コード生成用の環境をカスタマイズする方法
- 操作を安全に実行する方法
- 明確にスコープを定めた Issue の重要性
- Issue を Copilot に割り当てる方法

## シナリオ

Tailspin Toys には解決したい技術的負債があります。最初のサイトを作成した請負業者がドキュメントを不十分な状態のままにしており、実際にはほとんど存在していません。最初のステップとして、アプリケーション内のすべてのエクスポートされた関数に TSDoc ドキュメントコメントを追加することを検討しています。

さらに、デザインチームはゲームの発見体験を改善する準備ができています。各ゲームの詳細ページに、同じカテゴリ内の他のタイトルである関連ゲームを表示し、ユーザーが閲覧を続けられるようにしたいと考えています。完成度の高い実装ではなく、UX の受け入れテストで使用できる実装を求めています。この機能は現在ブロッカーですが、他の Issue が優先度の高い課題です。

これらは、優先度を下げられがちなタスクの例であり、Copilot cloud agent に割り当てるのに適しています。Copilot cloud agent はこれらのタスクを非同期で処理するため、開発者は他の作業に集中し、後で Copilot の作業をレビューして期待通りか確認できます。
## GitHub Copilot cloud agent の概要

[GitHub Copilot cloud agent](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent) は、バックグラウンドで人間の開発者と同じようにタスクを実行できます。人間の開発者と協力する場合と同様に、[GitHub Issue を Copilot に割り当てる](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions)など、複数の方法で作業できます。割り当てられると、Copilot は進捗を追跡するドラフト pull request を作成し、環境をセットアップしてタスクの作業を開始します。セッションの実行中または完了後に、Copilot のセッションを確認できます。提案されたソリューションをレビューできる状態になると、pull request にレビュー担当者としてタグ付けします。
## スコープを明確にした指示の重要性

GitHub Copilot にも考えることは必要です。特別な魔法はありません。一見簡単な操作でも、詳細を調べると複雑になる可能性があります。[Copilot cloud agent のタスクスコープを慎重に定める][cloud-agent-best-practices]必要があります。AI ペアプログラマーとして扱い、段階的に作業し、学習、実験、適応を繰り返してください。生成 AI を追加しても、ソフトウェア開発の基本原則は変わりません。

## このリポジトリのカスタム指示

前の演習では、カスタム指示とその Copilot に対するガイダンスについて確認しました。カスタム指示のハンズオン演習を完了済みの場合は、`.github/copilot-instructions.md` の動作を確認済みです。まだの場合は、ここで簡単に確認してください。Copilot cloud agent に作業を割り当てる前に、このリポジトリに含まれる指示ファイルを読み取り専用で確認し、後でどのような影響があるかを把握します。

次のファイルをリポジトリの GitHub Web UI または、すでに実行している codespace で開いてください。

- `.github/copilot-instructions.md` - **Code standards** セクション、特に TypeScript の規約と TSDoc ドキュメントコメントに関する要件を確認します。
- `.github/instructions/unit-tests.instructions.md` - 指示の対象を `**/*.test.ts` ファイルに限定する `applyTo` フロントマターを確認します。

次のセクションで `Code lacks documentation` Issue を cloud agent に割り当てる際に、生成される pull request で TSDoc ドキュメントコメント、TypeScript の規約、コメントヘッダーを確認してください。これらは指示ファイルから得られます。後の演習で PR をレビューする際に、改めて説明します。

## Copilot cloud agent 用の開発環境をセットアップする

コードを作成するには、関係者や担当者に関係なく、通常は特定の環境とセットアップスクリプトが必要です。タスクを割り当てる Copilot でも同様です。Copilot は SWE と同様の方法でタスクを実行します。

cloud agent は作業時に環境として [GitHub Actions][github-actions] を使用します。[特別なセットアップワークフロー][setup-workflow]を作成することで、この環境をカスタマイズできます。セットアップワークフローは `.github/workflows/copilot-setup-steps.yml` ファイルで設定し、作業開始前に実行できます。これにより、必要な開発ツールと依存関係を利用できます。ラボ用にあらかじめ設定されているため、学習をスムーズに進められます。Copilot が Node.js、プロジェクトの依存関係、エンドツーエンドテスト用のブラウザーバイナリ、および単一の Astro アプリ用に移行済みでシードされた SQLite データベースにアクセスできるようになります。

```yaml
name: "Copilot Setup Steps"

# リポジトリの "Actions" タブからセットアップステップを実行できます
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # 各ステップに必要な最小限の権限を設定します。Copilotには操作用の独自トークンが付与されます。
    permissions:
      # セットアップステップでリポジトリをクローンする必要がある場合は、`contents: read` 権限が必要です。クローンしない場合は、ステップ完了後に Copilot が自動でクローンします。
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # フロントエンド / アプリのセットアップ - Node.js（アプリ全体が現在 Astro + Drizzle/libSQL）
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

      # ビルドとテストで使用するデータを用意するため、ローカルの SQLite データベースを移行してシードします。
      - name: Set up the database
        run: npm run db:setup
```

これは一般的な GitHub workflow ファイルに見えますが、重要なポイントがいくつかあります。

- `copilot-setup-steps` という単一のジョブが含まれています。このジョブは、Copilot が pull request の作業を開始する前に GitHub Actions 内で実行されます。
- **Actions** タブからワークフローを手動で実行できる `workflow_dispatch` トリガーがあります。これは、Copilot の実行を待たずにワークフローが正常に実行されるかテストするのに便利です。

## ドキュメントを追加する

ドキュメントの重要性は誰もが理解していますが、多くのプロジェクトでは情報が古くなっているか、ドキュメントそのものが存在しません。この種の技術的負債は放置されがちで、生産性を低下させ、コードベースの保守や新しい開発者のチーム参加を困難にします。幸い、Copilot はドキュメント作成を得意としており、これは Copilot cloud agent に割り当てるのに適した Issue です。バックグラウンドで必要なドキュメントを生成します。後の演習で作業をレビューします。

1. 新しいブラウザータブで github.com のリポジトリに移動します。
2. **Issues** タブを選択します。
3. **New issue** を選択して、新しい Issue ダイアログを開きます。
4. **Blank issue** を選択して、新しい Issue を作成します。
5. **Title** を `Code lacks documentation` に設定します。
6. **Description** を次のように設定します。

    ```plaintext
    Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
    ```

7. **Create** を選択して Issue を作成します。
8. 右側で **Assign to Copilot** を選択して割り当てダイアログを開きます。

  ![Issue に Copilot を割り当てる](../../../_images/shared-assign-copilot.png)

9. **Assign** を選択します。

  ![Copilot の割り当て詳細](../../../_images/ex4-assign-copilot-details.png)

10. **Pull Requests** タブを選択します。
11. 新しく生成された pull request を開きます。タイトルは `[WIP]: Code lacks documentation` などです。一覧に新しい PR が表示されない場合は、しばらく待ってブラウザーウィンドウを更新してください。
12. 数分後、Copilot が todo リストを作成したことがわかります。

> [!NOTE]
> Copilot の todo リストが PR に表示されるまで数分かかる場合があります。Copilot は環境を作成し（前述のワークフローを実行）、プロジェクトを分析し、問題への最適なアプローチを決定しています。

13. リストと実行予定のタスクを確認します。
14. pull request のタイムラインを下にスクロールすると、Copilot が作業を開始したという更新が表示されます。
15. **View session** ボタンを選択します。

  ![Copilot セッションビュー](../../../_images/ex4-view-session.png)

> [!CAUTION]
> 更新されたインジケーターが表示されるまでウィンドウを更新する必要がある場合があります。

16. ライブセッションをスクロールして、Copilot が問題をどのように解決しているか確認します。コードを調査して状態を理解し、適切な計画を検討して判断し、コードを作成する様子がわかります。

これには通常数分かかります。Copilot cloud agent の主な目的の1つは、タスクを非同期で実行し、他の作業に集中できるようにすることです。その機能を活用するため、もう1つのタスクを Copilot cloud agent に割り当て、アプリケーションに機能を追加するコード作成に移ります。

## ゲーム詳細ページに関連ゲームセクションを追加する

前述のとおり、Copilot cloud agent の大きな利点は作業を分担できることです。デザインチーム向けに関連ゲームセクションを追加する作業は時間がかからない場合でも、その時間を他のタスクに使えるかもしれません。Copilot cloud agent に割り当てましょう。

1. github.com のリポジトリに戻ります。
2. **Issues** タブを選択します。
3. **New issue** を選択して、新しい Issue ダイアログを開きます。
4. **Blank issue** を選択して空のテンプレートを使用します。
5. **Title** を `Show related games on the game details page` に設定します。
6. **Description** を次のように設定します。

    ```markdown
    We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
   ```

7. **Create** を選択して Issue を作成します。
8. 右側で **Assign to Copilot** を選択して割り当てダイアログを開きます。

  ![Issue に Copilot を割り当てる](../../../_images/shared-assign-copilot.png)

9. **Assign** を選択します。

しばらくすると、最初のコメントに Copilot が作業中であることを示す 👀 が表示されます。

![Copilot が作業中であることを示す eyes 絵文字](../../../_images/ex4-issue-eyes-emoji.png)

Copilot が2つ目のリクエストに取り組んでいます。Copilot cloud agent は SWE と同様の方法で作業するため、積極的に監視する必要はありません。完了後にレビューできます。それでは、カスタムエージェントの作成と使用に移ります。

## まとめと次のステップ

このレッスンでは [GitHub Copilot cloud agent][copilot-agents]について確認しました。cloud agent を使うと、Issue を Copilot に割り当てて非同期に処理できます。技術的負債の解消、新機能の作成、あるフレームワークから別のフレームワークへの移行支援などに利用できます。

確認した概念は次のとおりです。

- コード生成用の環境をカスタマイズする方法
- 操作を安全に実行する方法
- 明確にスコープを定めた Issue の重要性
- Issue を Copilot に割り当てる方法

cloud agent がバックグラウンドで作業する間、カスタムエージェントの作成と使用に注目を移せます。[Copilot cloud agent は MCP サーバーも使用][cloud-agent-mcp]でき、カスタム指示も利用できます。これは前のモジュールで確認しました。

## リソース

- [Copilot cloud agentについて][copilot-agents]
- [GitHub Issue を Copilot に割り当てる][assign-issue]
- [Copilot cloud agent セットアップワークフローのベストプラクティス][cloud-agent-best-practices]

| [次のレッスン: カスタムエージェント →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
