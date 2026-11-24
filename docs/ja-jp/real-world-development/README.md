---
title: "実際の開発"
slug: ja-jp/real-world-development
authors:
  - geektrainer
lastUpdated: 2026-09-16
---

現実的なシナリオ、完成されたアプリケーション、共有バックログを使って、ソフトウェア開発ライフサイクル全体で GitHub Copilot を体験します。計画、コード作成、動作テスト、pull request のレビュー、エージェントによる作業管理を反復的に行います。

## シナリオ

ボードゲーム向けクラウドファンディングを提供する架空の企業「Tailspin Toys」の新しい開発者になってください。チームのバックログはすでに GitHub Issue として登録されており、取り組む準備が整っています。フィルターやページネーションなどの機能改善に加え、アクセシビリティやコーディング規約などの品質向上項目も含まれています。

## 環境を選択

GitHub Copilot は、作業場所を問わず利用できます。作り方に合った環境を選択してください。各ワークショップは個別のセットアップから始まり、共通の Tailspin Toys シナリオを使用します。

### [GitHub Copilot CLI][cli]

ターミナルでエージェント型アシスタントを使用します。Plan モードと Autopilot モード、指示、スキル、カスタムエージェント、Playwright MCP、Agent Merge、実用的なスラッシュコマンドを扱います。

### [GitHub Copilot app][app]

並列エージェントセッションを実行し、セッションモードを切り替え、キャンバスで共同作業を行い、デスクトップアプリで GitHub Issue と pull request を管理します。

### [GitHub Copilot cloud agent][cloud]

非同期エージェントに GitHub Issue を割り当て、作業をガイドし、進行状況を監視し、作成された pull request をレビューします。

### [Visual Studio Code][vscode]

Visual Studio Code または GitHub Codespaces で GitHub Copilot を使用します。エディターを離れずに、Copilot Chat のエージェントモード、MCP サーバー、カスタムエージェントを利用します。

[cli]: cli/
[app]: app/
[cloud]: cloud/
[vscode]: vscode/
