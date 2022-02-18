---
tags:
  - lua
---

# About Lua

- シンプルな構文
- 動的スクリプト言語で最速
- 関数型パラダイムをサポート
  - 末尾再帰最適化
- 組み込みしやすいランタイム

ゲーム開発に向く
ただしecosystemが完璧ではない
- IDE, ツールが少ない


# DevTools

## LuaRocks

- パッケージマネージャー
- バンドラー
- プロジェクトマネージャー

基本的に、ローカルファイル or 3rdパーティライブラリを利用するプログラムはこれがないと動かない

- `luarocks init`
  - `lua`, `luarocks` シェルスクリプトを生成
    - ローカルプロジェクトを利用して依存関係を読み込んでコマンド実行するスクリプト
  - `lua_modules`の初期化
  - `.rockspec`ファイルの初期化

### lua -e オプション

`lua -e 'key1=val1..key1;key2=val2..key2;'`

- `key` と `..key;` の間に書く
- 文字列値で`?`を使うとワイルドカード
- package.path : Luaパッケージをロードするパス(lua_modules, share など)
- package.cpath : C言語の共有ライブラリ (dylib, so, dll) のパス


## Lua Helper

- https://marketplace.visualstudio.com/items?itemName=yinfei.luahelper
- Tencent が開発するツール
  - 世界一のゲーム会社なので信頼性
- lint, intelisense, formatter などなど
- Golang 製
- LSP 準拠

更に、既存のLua拡張と比べ、

- Coroutine開発
- 大規模プロジェクトサポート
- エラー検出(文法, セマンティック)
- マルチファイル参照
- 省メモリ

