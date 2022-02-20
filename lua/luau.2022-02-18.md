---
tags:
  - lua
---

# Luau

- Roblox Studio で使われている Lua方言
- パフォーマンス改善
- Lua 5.1 に後方互換性
- typed Lua
  - 型定義をできる

# install

```sh
brew install luau

luau
luau-analyze
```

# use Lua library

どうやら、普通のluaスクリプトを`require`できるらしい

```lua
local dkjson = require("path/to/dkjson")
```

拡張子なしのファイルパス指定する
(commonJSと同じような)
`LUA_PATH`, `LUA_CPATH` が使えるかは不明

# 仕組み
luau バイナリは JIT, Repl, Compiler を含む

バイナリ or text (アセンブリ) を生成する