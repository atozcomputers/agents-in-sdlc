---
title: "演習 1 - カスタム指示（Cloud agent）"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: 前提条件][previous-lesson] · [次のレッスン: Copilot cloud agent →][next-lesson]

生成 AI を使用する際、コンテキストが鍵になります。特定の方法でタスクを実行する必要がある場合や、Copilot が知るべき背景情報がある場合は、そのコンテキストに確実に到達できるようにします。[指示ファイル][instruction-files]がそのガイダンスを提供する手段であり、Copilot が単に何を実行すべきかだけでなく、どのように実行すべきかを理解できます。

この演習では、次のことを行います。

- プロジェクト固有のコンテキスト、コーディングガイドライン、ドキュメント規約が、リポジトリのカスタム指示とパススコープ付き指示ファイルによって Copilot にどのように届くかを確認します。
- `.github/copilot-instructions.md` に新しいリポジトリ全体の規定を追加します。

> [!NOTE]
> VS Code ハーネスや CLI ハーネスとは異なり、ここではプロンプトの使用前後の比較は行いません。Copilot cloud agent は GitHub Issue 上で非同期に動作するため、リアルタイムでその影響を並べて示すことは難しいためです。cloud agent が作成した pull request をこのハーネスでレビューするときに、指示ファイルが与える影響を確認します。

## 指示ファイル

### シナリオ

優れた開発チームと同様に、Tailspin Toys には開発プラクティスに関するガイドラインと要件があります。たとえば、次の内容があります。

- データレイヤーには常にユニットテストが必要です。
- UI はダークモードで、モダンな外観にします。
- コードには TSDoc ドキュメントコメントの形でドキュメントを追加します。
- 各ファイルの先頭には、そのファイルの目的を説明するコメントブロックを追加します。

指示ファイルを使用して、Copilot が上記のプラクティスに沿った作業を行うために必要な情報を確実に提供します。

### カスタム指示

カスタム指示を使うと、Copilot にコンテキストと設定を提供し、コーディングスタイルと要件をより正確に理解させることができます。この強力な機能を使うと、推奨するコーディング規約、ライブラリ、コード内に含めたいコメントの種類などを指定できます。リポジトリ全体または特定のファイルタイプに対して指示を作成し、タスクレベルのコンテキストを提供できます。

指示ファイルには次の2種類があります。

- `.github/copilot-instructions.md` は、リポジトリに対する Copilot の**すべての**リクエストに送信される単一の指示ファイルです。このファイルには、Copilot に送るチャットや CLI リクエストの大半に関係するプロジェクトレベルの情報を含めます。使用している技術スタック、構築中の対象の概要、ベストプラクティス、その他のグローバルガイダンスなどを記載できます。
- `.github/instructions/*.instructions.md` ファイルは、特定のタスクやファイルタイプ向けに作成できます。TypeScript や Astro など特定の言語、または UI コンポーネントの作成や新しいユニットテストの作成などのタスクに対するガイドラインを提供できます。

> [!NOTE]
> IDE で作業する場合、指示ファイルが使用されるのは Copilot Chat のコード生成時で、コード補完や次の編集候補には使用されません。
>
> Copilot Chat、Copilot CLI、Copilot cloud agent は、コード生成時にリポジトリレベルの指示と（`applyTo` フロントマターを含む）`*.instructions.md` ファイルの両方を使用します。
>
> 最後に、Copilot は [AGENTS.md や CLAUDE.md を含む他の規格を使用した指示ファイルもサポート][custom-instructions-support]しています。

### 指示ファイル管理のベストプラクティス

指示ファイルの作成方法に関する詳細な説明はワークショップの範囲外ですが、サンプルプロジェクトにある例は代表的なアプローチを示しています。概要は次のとおりです。

- `copilot-instructions.md` の指示は、構築中の対象の説明、プロジェクト構造、グローバルなコーディング規約など、プロジェクトレベルのガイダンスに絞ります。
- `*.instructions.md` ファイルは、ファイルタイプ（ユニットテスト、Astro コンポーネント、データレイヤー）や特定のタスクに固有の指示を提供するために使用します。
- 自然言語を使用します。ガイダンスを明確にし、コードがどのような場合に適切か、適切でない場合はどのような点を避けるべきかを例示します。

AI の使い方に唯一の正解がないのと同様に、指示ファイルの作成方法にも特定の方法はありません。実験を重ねて、プロジェクトに最適な方法を見つけてください。

> [!TIP]
> GitHub Copilot を使用するすべてのプロジェクトには、充実した指示ファイルのコレクションを用意してください。このプロジェクトの指示ファイルを確認すると、[UI 更新][ui-instructions]や [Astro][astro-instructions]など、さまざまなタスク向けのファイルがあることがわかります。
>
> Copilot は指示ファイルの生成も支援できます。各インターフェースでは使い方が異なります。たとえば、VS Code では **Configure Chat → Generate Agent Instructions**、Copilot CLI では `/init` を使用します。該当するインターフェース向けのレッスンでは、関連する箇所でこの方法を案内します。
>
> テンプレートや開始点を探していますか。[awesome-copilot][awesome-copilot]を参照してください。指示ファイル、カスタムエージェント、その他のリソースが集められています。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
## このプロジェクトのカスタム指示ファイルを確認する

このリポジトリに含まれる指示ファイルを確認してください。コアとなる `copilot-instructions.md` と、さまざまなタスク向けの `*.instructions.md` ファイルのコレクションがあります。エディターまたは GitHub Web UI で開いてください。

1. `.github/copilot-instructions.md` を開きます。
2. プロジェクトの簡単な説明に加え、**Agent notes**、**Code standards**、**Scripts**、**Repository Structure**などのセクションを確認します。**Code standards** の下にある入れ子の **GitHub Actions Workflows** ガイダンスに注目してください。これは Copilotとのやり取りすべてに適用されます。
3. `.github/instructions` フォルダーを開いて確認します。Astro ファイル、Drizzle データレイヤー、テストなどの指示があることを確認してください。
4. `.github/instructions/unit-tests.instructions.md` を開きます。先頭にある `applyTo` フィールドに注目してください。リポジトリルートからの相対パスである glob を設定し、指示を適用するファイルを決定します。この例では、TypeScript テストファイル（たとえば `**/*.test.ts` に一致するファイル）が対象になります。
5. このプロジェクトのユニットテスト作成に固有の指示を確認します。
6. 最後に、`.github/instructions/drizzle.instructions.md` を開き、末尾までスクロールします。`unit-tests.instructions.md` やプロジェクト内の既存ファイルなど、他の指示ファイルへのリンクがあることを確認してください。これにより、大規模な指示セットを小さく再利用可能なファイルに分割し、Copilot がコード生成時に参照する例を指定できます（ここでのパスはリポジトリルートではなく指示ファイルからの相対パスです）。

> [!NOTE]
> `copilot-instructions.md` の **Code formatting requirements** セクションにはプロジェクトのコーディング規約が記載されていますが、コード内ドキュメントに関する要件はまだありません。次のステップで、TSDoc ドキュメントコメントとファイルコメントヘッダーのルールを追加します。
## 新しいリポジトリ規定を追加する

次のステップは、この演習で行う唯一の編集です。ドキュメントをコード内に TSDoc ドキュメントコメントとファイルレベルのコメントヘッダーとして記載することを、プロジェクト全体のルールとして追加します。このハーネスの後続の演習で割り当てる Issue を処理する際、Cloud agent がこのルールを参照します。

編集する前に、作業ブランチを作成します（cloud agent は Issue の対象ブランチから指示を読み取りますが、編集内容は確実にコミットします）。

1. codespace のターミナルで、新しいブランチを作成して切り替えます。

   ```bash
   git checkout -b custom-instructions-cloud
   ```

先ほど説明したように、`.github/copilot-instructions.md` は Copilot にプロジェクトレベルの情報を提供するように設計されています。リポジトリのコーディング規約を文書化して、コード候補の改善につなげましょう。

1. `.github/copilot-instructions.md` を再度開きます。
2. 通常27行付近にある **Code formatting requirements** セクションを探します。このセクションにはプロジェクトのコーディング規約が記載されていますが、コード内ドキュメントに関するルールはまだありません。これが生成されたヘルパーにドキュメントコメントがなかった理由です。
3. ファイルコメントヘッダーと TSDoc ドキュメントコメントを Copilot に追加するよう指示する、次の Markdown 行を既存の規約のすぐ下に追加します。

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. `copilot-instructions.md` を保存します。

> [!TIP]
> 前のレッスンで確認したように、リポジトリレベルの指示ファイル（`.github/copilot-instructions.md`）はグローバルガイダンスに、特定の言語、ファイルタイプ、タスク向けには `*.instructions.md` ファイルを作成できます。リポジトリレベルのファイルが、先ほど追加したドキュメントコメントルールなどのプロジェクト全体の規約に適した場所です。
## 指示の更新をコミット、プッシュ、マージする

cloud agent は Issue の対象ブランチから指示ファイルを読み取ります。次の演習で Issue を Copilot に割り当てると、Copilot は `main` からブランチを作成します。そのため、指示の変更を `main` に反映する必要があります。

1. ステージングしてコミットします。

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. ブランチをプッシュします。

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. github.com で `custom-instructions-cloud` から `main` への pull request を作成してマージします。これにより、cloud agent が次の演習で割り当てられた Issue を処理する際に、これらの指示を読み取れるようになります。

> [!TIP]
> このワークショップでは `main` で直接作業したい場合は、ブランチを作成せずに変更を直接 `main` にコミットできます。ブランチの手順は、実際のプロジェクトでの作業にワークショップを近づけるためのものです。

## まとめと次のステップ

Copilot がこのプロジェクトの指示ファイルからコンテキストを取得する仕組みを確認し、リポジトリ全体の新しい規定を `.github/copilot-instructions.md` に追加しました。このハーネスの残りの演習で cloud agent が生成する pull request に、この規定が反映されることを確認します。

次に、[Copilot cloud agent に最初の Issue を割り当てます][next-lesson]。

## リソース

- [GitHub Copilot カスタマイズのための指示ファイル][instruction-files]
- [カスタム指示を作成するためのベストプラクティス][instructions-best-practices]
- [Copilot のカスタム指示を改善するためのヒント 5選][copilot-instructions-five-tips]
- [Awesome Copilot - 指示ファイルやその他のリソースのコレクション][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
