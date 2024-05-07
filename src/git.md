# Git ガイドライン

🔰 当ドキュメントは「[コーディングガイドライン](./index.md)」の一部です。
基本的なガイドライン・ルールについては先にそれから確認してください。

## 🔰 前提

### Gitの基礎知識

- [基礎講座（社内共有ドライブ内 Google スライド）](https://docs.google.com/presentation/d/1hsTsh2C3D1BUOHWsevkr1Xy2wR9RsZITp8DjLd281ac/)

### Gitクライアント

GUIのGitクライアントを利用して構いません。ターミナルから`git`コマンドを利用しても良いですし、[Visual Studio Code](https://azure.microsoft.com/ja-jp/products/visual-studio-code/)の機能を使っても良いです。

## 🚧 ブランチとデモサイト

- `dev`ブランチはプッシュするとデモサイトに同期される
- 本番と同じ状態のブランチは`main`ブランチとする

`dev`ブランチとデモサイトの連携はSlackから`@system`にリクエストしてください。

## 🎣 pre-commitフック

ソースコードの品質担保、そして修正忘れを防止するために`husky`と`lint-staged`による、**コミット直前のソースコードチェックを実行する仕組み**を導入してます。
コミットを行うと、先にコードチェックが実行され、もしも**コードに問題がある場合はコミットを強制的にキャンセル**します。リントエラーなどを修正しないとコミットできません。

::: warning
GUI(fork など)を使う場合、ホームディレクトリに `.huskyrc` ファイルが必要になります。ファイルがない場合、チェックされないままコミットできてしまうので注意が必要です。
:::

## 🔢 Git操作手順

### 初回リリースまで

- `main`ブランチは（まだ）利用しない。
- トピックブランチ他、ブランチの作成に制限は設けない（ただしプッシュし忘れ・マージし忘れなど注意）。
- コミットコメントは自由。可能であれば適切なコメントを入れる。空でも良い（リリース後はルールが変わる）。
- スピード重視で雑にコミットをしても構わない。

### 初回リリース時

1.  `dev`から`main`ブランチを切る。
2.  `yarn release` コマンドを実行し、ファイルをリリース可能状態にする。
3.  `main`ブランチをプッシュする。
4.  リリース作業者は`main`ブランチをプルし、その状態のファイル郡を本番データとして扱い以下のいずれかを行う。
    - 本番サーバーへアップロード。
    - 本番サーバーへデプロイ。
    - `htdocs`フォルダをZipして納品。
5.  リリースチェック・検品などが終わったら `releaseYYYYMMDD` の形式でタグを付けプッシュする。

::: danger 重要

リリース作業をパートナー企業が行う場合であっても、_1._ _2._ _3._ _5._ は **必ず社内の人間が責任をもって行うこと**。

:::