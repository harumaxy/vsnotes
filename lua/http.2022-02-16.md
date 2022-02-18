---
tags:
  - lua
  - http
---


# Lua の HTTP Client Library

- `lua-http`
  - めっちゃ古いライブラリに依存してる
    - cqueues
      - OpenSSL の crypt.h, ssl.h を使ってビルドが必要
  - luarocks でのインストール時に、ビルドエラーが出る(make)
  - macOS だと使えない？

- `colo-http-luv`
  - https://github.com/squeek502/coro-http-luv
  - もともと coro-http というライブラリ
  - libuv という Node.js でも使われている非同期I/O実行プラットフォームに対応するため、リニューアルされた