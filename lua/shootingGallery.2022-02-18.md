---
tags:
  - love2d
  - udemy
---

# Shooting Gallery

## initial 3 functions

- love.load()
- love.update(dt)
- love.draw()

この３つの関数が基本のコード
load: 初期化、ファイルなどのロード
update: 状態の更新、物理
draw: 描画

# Draw Shapes

基本的に `love.graphics` モジュールの関数を使う
love.draw() コールバックの中で行う

```lua
function love.draw()
    love.graphics.print(time)
    love.graphics.setColor(0, 1, 0)
    love.graphics.rectangle("line", 200, 250, 200, 100)
    love.graphics.setColor(204 / 255, 102 / 255, 1)
    love.graphics.circle("fill", 300, 200, 100)
end
```
後に描写したものが上に来る
z-index などのプロパティで制御することが重要