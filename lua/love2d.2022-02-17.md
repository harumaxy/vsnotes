---
tags:
  - lua
  - love
---


# love2d

luajit 環境で動作する


# user love as Lua module

https://love2d.org/forums/viewtopic.php?t=86145

love の機能は so ファイルとして存在するらしい
コピーして require すると動くっぽい
(`liblove`から取ってくる)

filesystem, window, graphics など単体で抜き出して使えるものも多い

