---
tags:
  - love2d
  - lua
---

# 準備

- lua-language-server
- love2d-support
  - 正直、補完は↑ので間に合ってるけど `cmd + L` でlove を起動するショートカットが便利

# Table pt.1

WTF
`table`組み込みモジュールの関数で色々便利できる

```lua
testScores = { 95, 87, 98 }
-- testScores[1] = 95
-- testScores[2] = 87
-- testScores[3] = 98
table.remove(testScores, 2)
table.insert(testScores, 2, 100) -- head, <inserts>, tail
table.insert(testScores, "last")

message = testScores[3]
```

# Table pt.2

table をループするには `for .. in iterator`
`table`モジュールに、キーバリューペアイテレーターを作り出す2つの関数がある
- `ipairs`: index, value
- `pairs`: key, value

多分、 .next の実装が違う
ipairs は 1... の整数値から始まり、インデックスの連番が途切れた瞬間終了
pairs は普通にすべてのキー
arrary として扱うなら ipairs
hash として扱うなら pairs
数値、文字列キーが混同していても使える

```lua
message = 0
testScores = { 95, 87, 98 }
testScores.subject = "sicence"

for i, s in ipairs(testScores) do
    message = message + s
end

function love.draw()
    love.graphics.setFont(love.graphics.newFont(50))
    love.graphics.print(message)
    love.graphics.print(testScores.subject)
end
```

# Syntax Station

http://syntaxstation.com/lua.html


# Lua ternary operator
三項演算子が無い
ただし、and, or の仕様が JS っぽいので、代わりに使うことで同じ結果を得る

