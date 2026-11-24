---
title: "演習 0: 前提条件"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Copilot cloud agent の演習を始める前に、必要な準備をすべて整える必要があります。Tailspin Toys リポジトリの自分用コピーを作成し、指示ファイルを編集して cloud agent が生成した作業を確認できる [codespace][codespaces] を起動します。

## ラボ用リポジトリをセットアップする

作成するコード用のリポジトリのコピーを作成するために、[テンプレート][template-repository]からインスタンスを作成します。新しいインスタンスにはラボに必要なファイルがすべて含まれ、演習を進めながら使用します。

1. 新しいブラウザーウィンドウで [Tailspin Toys テンプレート][tailspin-template]を開きます。
2. ラボ用リポジトリのページで **Use this template** ボタンを選択して、自分用のリポジトリを作成します。続いて **Create a new repository** を選択します。

    ![Use this template ボタン](../../../_images/ex0-use-template.png)

3. GitHub または Microsoft が主催するイベントの一環としてワークショップを受講している場合は、メンターが提供する手順に従ってください。それ以外の場合は、GitHub Copilot にアクセスできる組織内に新しいリポジトリを作成できます。

    ![リポジトリテンプレートの設定を入力](../../../_images/ex0-repository-settings.png)

4. 作成したリポジトリのパス（**organization-or-user-name/repository-name**）をメモしてください。ラボを進める際にこのパスを参照します。
## codespace を作成する

次に、codespace を使用してラボの演習を完了します。

[GitHub Codespaces][codespaces] はクラウドベースの開発環境で、ブラウザー上でコードの記述、実行、デバッグを直接行えます。複数のプログラミング言語、拡張機能、ツールに対応した完全な IDE を利用できます。

1. 新しく作成したリポジトリに移動します。
2. 緑色の **Code** ボタンを選択します。

    ![Code ボタンを選択](../../../_images/ex0-code-button.png)

3. **Codespaces** タブを選択し、**+** ボタンを選択して新しい Codespace を作成します。

    ![新しい codespace を作成](../../../_images/ex0-create-codespace.png)

codespace の作成には数分かかりますが、すべてのサービスを手動でインストールする場合と比べると、はるかに短時間です。その間に、次に取り上げる GitHub Copilot の他の機能を確認できます。

> [!CAUTION]
> codespaceには今後の演習でも戻ります。今のところは、ブラウザーのタブを開いたままにしてください。

> [!NOTE]
> このワークショップは、codespace またはローカルの [dev container][dev-containers] 内で実行できるよう構成されています。どちらでも、スムーズに進められるよう必要な前提条件がすべてインストールされた環境になります。ローカルで実行する場合は、クローンしたリポジトリを VS Code で開き、表示されたら **Reopen in Container** を選択してください。VS Code が codespace と同じ dev container を構築します。

[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers
## まとめ

おめでとうございます。ラボ用リポジトリのコピーを作成し、Copilot cloud agent と共に作業するために使用する codespace の作成も開始できました。

## 次のステップ

cloud agent が従うカスタム指示を追加しましょう。[演習 1 - カスタム指示][next-lesson] に進みます。

## リソース

- [GitHub Codespaces の概要][codespaces]
- [テンプレートからリポジトリを作成する][template-repository]
- [Codespaces の概要][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[next-lesson]: ../1-custom-instructions/
