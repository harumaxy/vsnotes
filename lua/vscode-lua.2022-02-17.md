---
tags:
  - lua
  - vscode
---

# VSCode-Lua

by sumneko

https://github.com/sumneko/lua-language-server

lua-language-server 機能を使う

`brew` でバイナリをインストールできるが、VSCode Extension でインストールすると一緒にDLされるので必要なし
(Vimとかで使うときにいるかも)
現状これしかまともなのがない

gmod, roblox, fivem などの Lua方言はそれ専用の拡張機能を使ったほうが良いかも

# Settings

1. VSCode の場合 : `settings.json`
2. その他 : `.luarc.json`, lua設定ファイル

VSCode で使う限り、基本1の方法でいい

# 3rd party library の completion

なんと、設定ファイルでライブラリの場所を指定しないと読み込んでくれない(クソ)

```json
{
  "Lua.workspace.library": [
    "/Users/masaharuhosomichi/.asdf/installs/lua/5.3.0/luarocks"
  ],
  "Lua.workspace.userThirdParty": [
    "./lua_modules/share/5.3/lua"
  ]
}
```

`luarocks install` コマンドで表示される場所を指定してあげる
`userThirdParty` はローカルパッケージ用？

# Lua.diagnotics.global

実行環境により、グローバル変数が利用できるパターンについては VSCode 拡張設定JSON で指定しておくことでプリセットの補完が利用できる

(OpenResty, Love, ...)

```json
{
  "Lua.workspace.library": [
    "/Users/masaharuhosomichi/.asdf/installs/lua/5.3.0/luarocks",
    "${3rd}/OpenResty/library"
  ],
  "Lua.runtime.version": "LuaJIT",
  "Lua.diagnostics.globals": ["ngx"],
  "Lua.workspace.checkThirdParty": true
}
```

検知されるとワークスペース用の設定が書き換わる


# 3rd party diagnotics

有名なやつだけ、拡張機能によるグローバル変数の保管ができる

`$3rd` = `$HOME/.vscode/extensions/sumneko.lua-2.6.4/server/meta/3rd`

- Cocos4.0
- OpenResty
- love2d
- skynet
- Jass
- example
- lovr

見た感じ、`$3rd`にあるディレクトリと同じフォーマットを用意すれば自分でも作れそう

# その他おすすめ拡張

- sumneko.lua
- rog2.luacheck
- JohnnyMorganz.stylua
- tomblind.local-lua-debugger-vscode