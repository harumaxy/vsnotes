---
tags:
  - lua
  - luarocks
---

# LuaRocks

パッケージマネージャー

# 使い方

```sh
luarocks init  # Lua プロジェクトを初期化
./luarocks install dkjson # ローカルインストール
./luarocks show dkjson # パッケージ詳細

```

## Rocks tree

- system: デフォルト
- user: 

## install した rocks パッケージを require するには

Lua システムがパスを知る必要がある
```lua
print(package.path)
print(package.cpath)
```


# Trouble shoot

### Header が無い

Lua はC言語の組み込みスクリプトとしてよく使われるという背景があり、LuaJITなどの実行環境でもC言語で書かれたライブラリをLuaでFFIするという光景がよくある。

Luarocks でパッケージをインストールするときも、C言語をビルドして.soオブジェクトをLuaでrequireするということがよくある

Macの場合、homebrew でインストールしたライブラリは
- `/usr/local/include`
- `/usr/include`
- `/include`

といったluarocksがデフォルトで探しに行く場所ではなく
- `/opt/homebrew/include` (ここにあるのはシンボリックリンク。`realpath`コマンドで実際のディレクトリを設定する必要がある)
- `/opt/homebrew/Cellar/libzip/1.8.0_1/include`
にある

インストールに失敗すると`*_DIR`, `*_INCDIR` 環境変数にディレクトリをセットしてもう一度やるパターンになるので、そのようにする
`*INCDIR` = `*_DIR/include`
```sh
You may have to install ZIP in your system and/or pass ZIP_DIR or ZIP_INCDIR to the luarocks command.
Example: luarocks install lua-zip ZIP_DIR=/usr/local
```