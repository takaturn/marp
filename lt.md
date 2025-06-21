---
marp: true
theme: dracula
paginate: true
header: " "
footer: " "
---

<!--
_class: title
-->

# ![bg h:80%](https://cdn-ak.f.st-hatena.com/images/fotolife/n/nnc-k-takata/20250526/20250526233247.png)

---

## はじめに
<!--
headingDivider: 1

-->

- VS Codeの拡張機能「Dev Container」を使った効率的な開発環境の構築方法を紹介します
- この組み合わせにより、「どのマシンでも同じ環境で開発できる」という夢が現実になります

<img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEitaZecLs4auey-B5PGVO-m1q8E9D5s6PzmnjVkhkRKJgf0WsVN0OVzSgnJ59LsC4u0NXgY9pNZJQ6k-ca119t43a8bg-CzGDomh5Mh3GPqXlUsu5AzkyW0ilpzGWhyphenhyphenKIVauAkdf8TG5RWJ/s800/yume_man.png" style="display: block; margin: auto; width:200">

---

## もくじ

1. Dev Container とは？
1. なぜ Dev Container を使うのか？
1. Dev Container の構成要素
1. `devcontainer.json` の主要な設定
1. Dev Container Templates
1. Dev Container Features
1. VS Code Extensions との連携
1. Dev Container 専用ベースイメージ①
1. まとめ

---

## Dev Container とは？

- 🐳 **開発環境をコンテナ化する仕組み**
    - Docker コンテナ内で一貫した開発環境を提供
- 🔄 **VS Code (やその他の対応IDE) とシームレスに連携**
    - ローカルで開発しているかのような体験
- ✏️ **設定はコードで管理 (`devcontainer.json`)**
    - 再現性が高く、共有も容易
- ✂️ **プロジェクトごとに隔離された環境を簡単に構築可能**

---

## なぜ Dev Container を使うのか？

- **環境の一貫性**
    - 「私のマシンでは動くのに…」という問題から解放されます
- **素早いセットアップ**
    - 新しいメンバーが参加しても、すぐに開発を始められます
- **プロジェクト間の分離**
    - 異なるプロジェクトで異なるバージョンの言語やツールを使っても衝突しません
- **クリーンな環境**
    - ホストマシンを汚さずに開発できます

---

## Dev Container の構成要素

Dev Container は主に以下の要素で構成されます。

1. **`devcontainer.json` ファイル**
    - Dev Container の設定を記述するJSONファイル
2. **Dockerfile または Docker Image**
    - 開発環境のベースとなるコンテナイメージ
3. **(オプション) Docker Compose ファイル**
    - 複数のコンテナ (例: アプリケーション + データベース) を連携させる場合に使用

---

## `devcontainer.json` の主要な設定

```json
{
  "name": "My Project Dev Container", // コンテナの表示名
  "image": "mcr.microsoft.com/devcontainers/typescript-node:18", // コンテナイメージ
  "features": { // 追加ツールやランタイム定義
    "ghcr.io/devcontainers/features/git:1": {}
  },
  "customizations": {
    "vscode": {
      "extensions": [ // VS Code拡張機能
        "dbaeumer.vscode-eslint"
      ]
    }
  }
}
```

---

## Dev Container Templates

- 🌈 **さまざまな開発環境のための事前定義されたテンプレート**
    - 有志の方が作成した`devcontainer.json`をそのまま利用できます。
    - これらを利用して、開発環境を1から作るより断然簡単になります。
- 📚 **100以上のテンプレート**
    - Node.js、Python、Ruby、Go など、さまざまな言語やフレームワークに対応しています。
      [Available Dev Container Templates](https://containers.dev/templates)

---

## Dev Container Features

- 🛠 **ツール/ランタイム/ライブラリを開発環境に追加する仕組み**
    - `devcontainer.json`の`features`プロパティで指定することで、 Dev Containerイメージ作成時のセットアップ処理を自動的に追加してくれます
    - `Dockerfile`の`RUN`を作成していた手間を減らせます

---

## VS Code Extensions との連携

- **Dev Container コンテナ内に入れる VS Code拡張機能**
    - `devcontainer.json` の `customizations.vscode.extensions` で指定することでコンテナ内に自動でインストールしてくれます
- **Dev Container Features で入れたCLIとVS Codeを連携**
    - Features だけだとターミナル上でしかコマンド実行できません
    - （ Extensions と連携することで） VS Codeでファイルを開きながらCLI結果を表示できるなど利便性がさらに向上します

---

## Dev Container 専用ベースイメージ①

- 🐳 **よく使われるツール/ランタイム導入済みの専用イメージ**
    - 利用頻度が高い「 Dev Container Features 」インストール済みのイメージです
    - 利用している Dev Container Features が増えてくると、「Dockerイメージビルドが遅くなる」「Featuresの管理が煩雑化」など問題が出てくるかと思います
    - このイメージを使うことで、Dockerイメージビルドの時間短縮が見込めます

---

## Dev Container 専用ベースイメージ②

- 🔞 **18種類のイメージ**
    - OS/言語ごとでDockerイメージが用意されています。
      【参考URL】[Githubサイト(devcontainers)](https://github.com/devcontainers/images/tree/main/src)
    - 下記各イメージフォルダ内のリリースノートにインストール済一覧が掲載されています。
      【参考URL】[python用イメージのhistory](https://github.com/devcontainers/images/blob/main/src/python/history/0.201.4.md)

---

## まとめ

- **Dev Container は、一貫性があり再現性の高い開発環境を提供**
- **`devcontainer.json` で環境をコードとして定義・管理**
- **Templates と Features で環境構築を効率化**
    - Dev Container専用イメージもあるよ！
- **VS Code との強力な連携により、快適な開発体験を実現**

**ぜひ、あなたのプロジェクトでも Dev Container の導入を検討してみてください！**

---

## おわり

ご清聴ありがとうございました。

![bg fit right:40%](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjHtu3kBX8P39WYBBAjar9c8c1ladK2SYL6_gEMXFweQfauWVhSvCQP5KELsPX5KNL1uOddLLQ-aeMxv904OW_NFFfANhBYObfBV09KO2EXehrb9kMdCLZY1afsChib-7zIkBJbG6OrbJpM/s800/aisatsu_kodomo_boy.png)