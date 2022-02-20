---
title: VSNotes と Zenn CLI でどこでも記事を書けるようにする
emoji: 📘
type: tech # tech: 技術記事 / idea: アイデア
topics: [zenn, vscode, vsnotes, markdown]
published: true
tags: []
---

# VSNotes の紹介

**VSNotes** は Markdownメモを管理するシンプルなVSCode拡張機能です。

VSCodeのコマンドパレットを介してメモの作成・編集を開始することができ、
メモの置き場を設定しておくことでどのワークスペースからでもアクセスすることができます。

自分はこの拡張機能を普段はちょっとしたメモを書くのに使っていますが、ちょっと応用したらZennの記事の編集をどこでもできるようになりました。

- [VSNotes の紹介](#vsnotes-の紹介)
- [インストール・設定](#インストール設定)
  - [Step0. VSCode 拡張機能 をインストール](#step0-vscode-拡張機能-をインストール)
  - [Step1. Zenn CLI のインストール](#step1-zenn-cli-のインストール)
  - [Step2. Zenn プロジェクトの初期化](#step2-zenn-プロジェクトの初期化)
  - [Step3. zenn コマンドの alias を設定](#step3-zenn-コマンドの-alias-を設定)
  - [Step4. VSNotes 拡張機能の設定](#step4-vsnotes-拡張機能の設定)
  - [Step5. テンプレートスニペットの作成](#step5-テンプレートスニペットの作成)
- [使ってみる](#使ってみる)
  - [メモ一覧](#メモ一覧)
  - [新規メモ作成](#新規メモ作成)
  - [記事プレビュー](#記事プレビュー)
  - [git commit & push](#git-commit--push)
  - [メモを削除する・移動する](#メモを削除する移動する)
- [終わり](#終わり)


# インストール・設定
## Step0. VSCode 拡張機能 をインストール

https://marketplace.visualstudio.com/items?itemName=patricklee.vsnotes

VSCode に上のリンクからVSNotes拡張機能をインストールしておきます


## Step1. Zenn CLI のインストール

グローバルにインストール
自信のある人はプロジェクトローカルでも可

```sh
npm i -g zenn-cli
```

## Step2. Zenn プロジェクトの初期化

ディレクトリの名前は何でも大丈夫です。
ここではホームに`.vsnotes`というディレクトリを作ります。


```sh
cd ~
mkdir .vsnotes && cd .vsnotes
git init
zenn init
```

## Step3. zenn コマンドの alias を設定

Zennプロジェクトへ移動してzennコマンドを実行するzshサブプロセスのaliasを、`.zshrc`に追加します。(bashとかfishの人は適宜読み替えてください)

これにより、どの場所でzennコマンドを実行しても`~/.vsnotes`ディレクトリに入ってるMarkdownをプレビューできるようになります。


```sh
cat << EOF >> ~/.zshrc
# zenn
VSNOTE_DIR="/Users/masaharuhosomichi/ghq/github.com/harumaxy/vsnotes"
alias zenn='(){zsh -c "cd $VSNOTE_DIR && zenn $@"}'
EOF
```

## Step4. VSNotes 拡張機能の設定

コマンドパレットから `Preferences: Open Settings(JSON)` を開いて設定
自分はファイル名の設定を変えてますがデフォルトでも全然問題ないと思います。
好みですね。


```json
{
  "vsnotes.defaultNotePath": "~/.vsnotes",
  "vsnotes.defaultNoteTitle": "{title}-{dt}.{ext}",
  "vsnotes.tokens": [
    {
      "type": "datetime",
      "token": "{dt}",
      "format": "YYYY-MM-DD",
      "description": "Insert formatted datetime."
    },
    {
      "type": "title",
      "token": "{title}",
      "description": "Insert note title from input box.",
      "format": "Untitled"
    },
    {
      "type": "extension",
      "token": "{ext}",
      "description": "Insert file vsnotes.",
      "format": "md"
    }
  ],
  "vsnotes.templates": ["default", "zenn"],
}
```


## Step5. テンプレートスニペットの作成
上の設定の`vsnotes.templates` という設定項目は、VSNotesでメモを新規作成するときのテンプレートですが、VSCodeのスニペット設定からを読み込んで使われます


コマンドパレットから `Preferences: Configure User Snippets > markdown.json` を選んで、下のように書きます。

※注意❗️: スニペット名に `vsnote_template_` が必要です！

```json
{
  // `vsnote_template_` という prefix が必要！
  "vsnote_template_zenn": {
    "prefix": "vsnote_template_zenn",
    "body": [
      "---",
      "title: ",
      "emoji: 🙌",
      "type: tech # tech: 技術記事 / idea: アイデア",
      "topics: []",
      "published: false",
      "tags: []",
      "---"
    ]
  }
}
```
フロントマターの `tags` っていうのは zenn の記事では無視されるんですが、VSNotesのタグ機能でまとめるのに使うのでテンプレートに足しときます。

これで準備はOK！

# 使ってみる

## メモ一覧

[![Image from Gyazo](https://i.gyazo.com/db5fd6cdf15aab0230333783de5ebd03.png)](https://gyazo.com/db5fd6cdf15aab0230333783de5ebd03)

**VSNotes** 拡張機能をインストールすると、左のツールバーに VSNotes アイコンが追加されるので、それをクリックすることでどのワークスペースからでもノートをまとめているディレクトリにアクセスすることができます。

## 新規メモ作成

[![Image from Gyazo](https://i.gyazo.com/aeeae34f675d7d050f7d14cefa830918.png)](https://gyazo.com/aeeae34f675d7d050f7d14cefa830918)

[![Image from Gyazo](https://i.gyazo.com/972f8d2db763bff475447d3f5673c224.png)](https://gyazo.com/972f8d2db763bff475447d3f5673c224)

`コマンドパレット > VSNotes: Create a New Note > zenn > articles/<記事名>` と入力することで、zennプロジェクトの`articles`ディレクトリに新しい記事が作成されます。

もしくは、zennコマンドがどのディレクトリから実行してもzennプロジェクトで実行されるようになってるので、以下のコマンドでもいいと思います。

```sh
zenn new:article
```

## 記事プレビュー

[![Image from Gyazo](https://i.gyazo.com/0614f8e7a16ddbce50035ec180f78e5c.png)](https://gyazo.com/0614f8e7a16ddbce50035ec180f78e5c)

VSCode のコンソールで `zenn preview` コマンドを打って、表示されるURLをブラウザで開く。

どのワークスペースからコマンドを打ってもプレビューできる。

```
zenn preview
# 👀 Preview: http://localhost:8000
```

## git commit & push

`コマンドパレット > VSNotes: Commit and Push` を実行するとできます。

いちいちメモのあるディレクトリを開かないで良いのが便利！

## メモを削除する・移動する

残念ながら、そういう操作はコマンドパレットから直接はできなさそう。

代わりに、`コマンドパレット > VSNotes: Open Note Folder` で **VSNotes** でメモを管理しているディレクトリを開けるので、そこから操作すると良いと思います！


# 終わり

VSCodeによりメモを管理すると同時に、VSCodeの豊富なMarkdown拡張機能による支援を受けられるので、ものすごく良い執筆体験ができそうな気がする。

あとユースケースとして、コード書いてるときにメモ書きたくなることあると思うんですが、ソースコメントに書くより全部のメモを一元管理しとくと見つけやすくなるので、そういう需要にフィットする拡張機能だと思います。

めっちゃ便利なので皆さん使ってみてください！

終わり