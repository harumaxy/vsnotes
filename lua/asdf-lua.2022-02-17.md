---
tags:
  - lua
---

# asdf plugin での lua

```sh
asdf install lua 5.3.0
```

luarocks と lua が同時にインストールされる

なぜか、package.path などを指定しなくても global で使っている luarocks でインストールされたグローバルパッケージが使える

# 詳しく見る

```sh
which lua
# /Users/masaharuhosomichi/.asdf/shims/lua

cat $(which lua)
#!/usr/bin/env bash
# asdf-plugin: lua 5.4.3
# asdf-plugin: lua 5.3.0
# exec /opt/homebrew/opt/asdf/libexec/bin/asdf exec "lua" "$@"
```

`asdf exec` コマンド で `lua` を実行している
何らかの特殊な引数が指定されているのかも




