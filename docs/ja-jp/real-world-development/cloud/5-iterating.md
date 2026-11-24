---
title: "演習 5: GitHub Copilot の作業を反復改善する"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 前のレッスン: エージェントの管理][previous-lesson] |
|:--|

## 作業をレビューする

このラボでは、ユーザーエクスペリエンスと機能追加を目的とした複数のタスクで GitHub Copilot と協力しました。コードにドキュメントを追加し、デザインチーム向けの関連ゲーム機能を作成し、ハイコントラストモードとライトモードのトグルを含むアクセシビリティ機能を実装するよう依頼しました。コードの変更を確認し、必要に応じて Copilot にフィードバックして作業を改善します。

### シナリオ

繰り返し説明したように、生成 AI を導入しても、ソフトウェア設計と DevOps の基本原則は変わりません。生成されたコードは常にレビューし、通常の DevOps プロセスを通じて作業を進める必要があります。そのため、チームの残りのメンバー向けにレビューを有効にする前に、ドキュメント、関連ゲーム機能、アクセシビリティ機能に関する GitHub Copilot の提案を確認しましょう。
## セキュリティと GitHub Copilot cloud agent

Copilot cloud agent は監督なしで非同期にタスクを実行するため、安全性を維持するためのセキュリティ制約が設けられています。制約には次のものがあります。

- Copilot はリポジトリへの読み取り専用アクセス権を持ち、コードに使用するブランチに対してのみ書き込み権限を持ちます。
- cloud agent は GitHub Actions 内で動作し、作業用に独立した一時的な環境を作成します。
- GitHub Actions ワークフローを実行するには、すべて人間の承認が必要です。
- [外部リソースへのアクセスはデフォルトで制限][agent-firewall]され、MCP サーバーへのアクセスも含みます。
## 生成されたドキュメントをレビューする

まず、GitHub Copilot cloud agent が生成した最初の pull request（PR）、つまりコードへのドキュメント追加を確認します。このタスクは GitHub.com の標準的な PR インターフェースを使用して実行します。

> [!NOTE]
> PR を確認すると、GitHub Copilot がファイアウォールによってブロックされたという警告が表示される場合があります。これは**想定された動作**です。Copilot の外部リソースへのアクセスはデフォルトで制限されており、外部 MCP サーバーへの呼び出しも含まれます。必要に応じて、[Copilot cloud agent のファイアウォールをカスタマイズまたは無効化][agent-firewall]できます。

1. GitHub.com のリポジトリに戻ります。
2. **Pull Requests** を選択して pull request の一覧を開きます。
3. **Add missing documentation** またはより具体的な名前の pull request を開きます。

> [!NOTE]
> Copilot がまだタスクを処理中の場合、pull request に **[WIP]** フラグが表示されます。その場合は、Copilot が作業を完了するまで待ちます。数分かかる場合があります。休憩するか、ここまで学んだ内容を振り返ってください。

4. pull request の準備ができたら、**Files changed** タブを選択して変更を確認します。

    ![Files changed タブ](../../../_images/shared-pr-files-changed.png)

5. 新しく作成された TSDoc ドキュメントコメントやその他のドキュメントを含む、更新されたコードを確認します。正確な変更内容は異なる場合があります。

    変更を確認する際は、TSDoc ドキュメントコメント、TypeScript の規約、コメントヘッダーを探します。これらは演習 2 の冒頭で確認したカスタム指示ファイルから得られています。

6. 更新内容を確認し問題がなければ、**Conversation** タブに戻って下にスクロールします。
7. 一部のワークフローが承認待ちになっているインジケーターが表示されます。
8. ワークフローが承認待ちの場合は、**Approve and run workflows** を選択します。

   ![ワークフローを承認して実行](../../../_images/shared-approve-workflows.png)
9. ワークフローが pull request の checks セクションでキューに入ります。問題がなければ、単一の Astro アプリのプロジェクトチェックが成功します。完了まで数分かかる場合があります。

## GitHub Copilot に変更を依頼する

Copilot との pull request のやり取りは一方的ではありません。チームメンバーに対するときと同様に、pull request またはコードのインラインコメントで Copilot をタグ付けできます。Copilot はこれらのコメントを検出し、対応するための新しいセッションを開始します。結果は非決定的であるため、依頼するテキストは規定できません。Copilot に更新を依頼する例は次のとおりです。

- 各コードファイルの先頭に、ファイルの目的を簡潔に説明するコメントヘッダーを追加する。
- TypeScript ファイルと Astro ファイルに TSDoc ドキュメントコメントを追加する。
- Astro アプリの構造を説明する README を作成する。

1. 生成されたドキュメントの変更を依頼するコメントを追加し、ユーザーをタグ付けする場合と同じように **@copilot** をタグ付けします。上記の例を使用するか、コードベースで確認したいドキュメントに関する他の提案を利用してください。
2. **View Session** を選択して、Copilot が作業を行う様子を確認します。Copilot が更新のために新しいセッションを開始することを確認できます。
3. **Back to pull request** を選択して pull request に戻ることもできます。

    ![pull request に戻る](../../../_images/ex7-back-to-pr.png)

4. Copilot が変更を完了すると、pull request に新しいコミットが表示されます。
5. **Files changed** タブを選択して変更を確認します。

必要に応じて反復改善を続けてください。満足できる状態になったら、ドラフトから ready に変更し、`main` ブランチにマージします。

![PR を ready に変更](../../../_images/ex7-ready-for-review.png)

## 関連ゲーム機能をレビューする

ゲーム詳細ページに関連ゲームを表示する Issue を解決するため、Copilot が生成した PR に戻ります。

1. GitHub.com のリポジトリに戻ります。
2. **Pull Requests** タブを選択します。
3. **Show related games on the game details page** またはより具体的な名前の PR を選択します。
4. **Files changed** タブを選択して、生成されたコードを確認します。
5. 更新内容を確認し問題がなければ、**Conversation** タブに戻って下にスクロールします。
6. 一部のワークフローが承認待ちになっているインジケーターが表示されます。
7. ワークフローが承認待ちの場合は、**Approve and run workflows** を選択します。

   ![ワークフローを承認して実行](../../../_images/shared-approve-workflows.png)
8. ワークフローが pull request の checks セクションでキューに入ります。問題がなければ、単一の Astro アプリのプロジェクトチェックが成功します。完了まで数分かかる場合があります。
9. **任意:** Codespace でこのブランチに切り替え、関連ゲーム機能を手動テストできます。Codespace に移動し、ターミナルを開いて次のコマンドを実行します（`<branch-name>` は Copilot が作成したブランチ名（例: **copilot/fix-8**）に置き換えてください）。

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```
   
Copilot が関連ゲーム機能を構築しました。前と同様に、Copilot cloud agent と反復的に連携して更新を依頼できます。たとえば、表示する関連ゲームの数を変更するよう依頼したり、コメントヘッダーと TSDoc ドキュメントコメントの追加を依頼したりできます（これは、カスタム指示の更新を行う**前**に割り当てたタスクであることを忘れないでください）。前と同様に、**Conversation** タブに新しいコメントを追加して依頼すると、Copilot が新しいセッションを開始します。

## アクセシビリティ機能をレビューする

最後に、カスタムアクセシビリティエージェントを使用して実装されたアクセシビリティ機能を確認します。この PR には、演習 3 で割り当てたハイコントラストモードと、演習 4 の mission control で依頼したライトモードの両方が含まれるはずです。

1. GitHub.com のリポジトリに戻ります。
2. **Pull Requests** タブを選択します。
3. **Add high contrast mode to website** またはより具体的な名前の PR を選択します。

> [!NOTE]
> Copilot がまだタスクを処理中の場合、pull request に **[WIP]** フラグが表示されます。その場合は、Copilot が作業を完了するまで待ちます。数分かかる場合があります。

4. **Files changed** タブを選択して、生成されたコードを確認します。
5. 実装をレビューし、特に次の点に注目します。
   - モードを切り替えるトグル UI コンポーネント
   - ユーザー設定を保持するローカルストレージの使用
   - ハイコントラストモードとライトモードの CSS またはスタイル変更
   - アクセシビリティ属性（ARIA ラベル、キーボードナビゲーションなど）
   - モード切り替えを管理する JavaScript/TypeScript コード

6. 更新内容を確認し問題がなければ、**Conversation** タブに戻って下にスクロールします。
7. 一部のワークフローが承認待ちになっているインジケーターが表示されます。
8. ワークフローが承認待ちの場合は、**Approve and run workflows** を選択します。

   ![ワークフローを承認して実行](../../../_images/shared-approve-workflows.png)
9. ワークフローが pull request の checks セクションでキューに入ります。問題がなければ、単一の Astro アプリのプロジェクトチェックが成功します。完了まで数分かかる場合があります。
10. **任意:** Codespace でこのブランチに切り替え、アクセシビリティ機能を手動テストできます。Codespace に移動し、ターミナルを開いて次のコマンドを実行します（`<branch-name>` は Copilot が作成したブランチ名に置き換えてください）。

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

    アプリケーションを起動し、ブラウザーでハイコントラストモードとライトモードのトグルをテストして、期待通りに動作し、ページの再読み込み後も設定が保持されることを確認します。

カスタムアクセシビリティエージェントが、アクセシビリティのベストプラクティスに沿った機能の実装を Copilot にガイドする様子を確認してください。アクセシビリティ上の懸念や改善点があれば、前の PR と同様にコメントで **@copilot** をタグ付けして更新を依頼できます。

## 任意の演習 - 委任を続ける

cloud agent は、リポジトリの実際のバックログ項目を任せて他の作業に集中できる場合に最も効果を発揮します。この習慣を身につけるため、リポジトリにいくつかの Issue を登録し、Copilot に割り当ててください。例は次のとおりです。

- ゲーム詳細ページに支援者向けの関心登録フォームを作成する。
- ゲーム一覧ページにページネーションを実装する。
- データアクセスヘルパーに入力検証とエラー処理を追加する。

## まとめ

Cloud agent ハーネスを完了しました。これらのレッスン全体で、次のことを行いました。

- **このリポジトリに含まれるカスタム指示ファイルを確認**し、後で cloud agent の出力に与える影響を確認しました。
- **Issue を Copilot cloud agent に割り当て**、環境のセットアップ、計画、非同期実行の様子を確認しました。
- アクセシビリティ用の**カスタムエージェントを作成して使用**し、ハイコントラストモードとライトモードのトグルを追加しました。
- **Copilot エージェントページを mission control として使用**し、アクセシビリティセッションを実行中に監視・操作しました。
- **cloud agent の pull request をレビューして反復改善**し、`@copilot` をタグ付けして変更を依頼し、ワークフローを承認しました。

## レビューと次のステップ

Cloud agent ハーネスを完了しました。さらに確認したい場合は、他のハーネスがここで学んだ内容を補完します。

- 🖥️ **[VS Code ハーネス](../../vscode/)** - IDE から直接、Copilot Chat のエージェントモードと MCP 統合を確認します。
- 💻 **[CLI ハーネス](../../cli/)** - ターミナルからレビュー済みの変更を2つ提供し、Plan モードと Autopilot モード、エージェントスキル、カスタム QA エージェント、Playwright MCP、Agent Merge、任意の `/delegate` ブリッジを cloud agent に利用します。

自分のリポジトリで、次のアイデアを試してください。

- リファクタリングやテストカバレッジに関する Issue を cloud agent に割り当てます。
- 別の領域向けのカスタムエージェントを作成します。
- 別のスタック向けに `copilot-setup-steps.yml` をセットアップします。

## リソース

- [GitHub Copilot][github-copilot]
- [Copilot エージェントについて][copilot-agents]
- [GitHub Issue を Copilot に割り当てる][assign-issue]
- [Copilot cloud agent セットアップワークフローのベストプラクティス][cloud-agent-best-practices]
- [Copilot cloud agent ファイアウォールの設定][agent-firewall]

---

| [← 前のレッスン: エージェントの管理][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall

[previous-lesson]: ../4-managing-agents/
