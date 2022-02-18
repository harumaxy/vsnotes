---
tags:
  - lua
  - teal
---

# Teal

型付き Lua の方言

- JS に対する TS のような存在
  - [teal-types](https://github.com/teal-language/teal-types) なるリポジトリがある
  - ただ、typescriptほどメジャーな存在にはなれていないようである...
- luarocks でインストール
- またはビルド済みのスタンドアロンファイル
- VSCode拡張も存在
  - コンパイラがLinterを兼ねる

# declaration file

`.d.tl`
型のないLuaモジュールに型付けを行おうという試み

- Lua と C モジュール両方で同じ拡張子
  - 元が `.lua` だろうと `.so` だろうと、`.d.tl`
- Luarocks のパッケージエントリと同じ命名規則にする

# Command
`.tlconfig` を用意して、プロジェクトビルド(バンドル)のようなこともできる

```sh
tl run main.tl
tl gen main.tl
tl build

```
