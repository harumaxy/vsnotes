---
tags:
  - glsl
  - shader-school
---

# How to use shader-school
お題の書かれたshaderファイル`.glsl`があるので、それを編集してお手本と違いがなくなればok
(下のスライダーでお手本と自分のシェーダーの画面比率を変更)

# Syntax
だいたいC言語と同じ

# Variable

## const
定数になる
再代入不可

## Precision specifiers
小数点の精度を指定するprefixをfloat型の前におく
GPUに変数表現で何ビット使うかを指定する
(ハードウェアによりサポートされない)

- lowp
- mediump
- highp

## global variable
関数の外で定義するとグローバル
使わぬほうが良い


# Function
```cpp
void main(
  mediump float v,
  out highp float result,
  inout highp float context){
  // code
  inout += v;
  result = 1.1 + inout;
}
```


## In, Out
C言語, C++, C# にもあるような、
ポインタを渡して関数内でデータを値の変更を関数外にも反映させるような仕組み

複数戻り値のような使い方をできる(モダンじゃないけど)。


- in
  - コピー渡し
  - 再代入可能だが、渡した引数の元は変更されない
- inout
  - 参照渡し
- out
  - 参照渡し
  - 初期化されていない前提なので、代入するまで使用できない。
- const
  - readonly

shader-school では、問題の関数を glslify で requireして、
それを使って比較描写してる。
コールバック的な使い方と言える

ので、`out` prefix で答えを提出する場面が多い

# Built-in

- radians(deg), degrees(rad)
  - rad, deg を相互変換
- sin, cos, tan, ...
- max, min, clamp, floor, ceil, round...


# Vector

## Vector boolean
vectorすべての要素を比較する関数
- lessThan(a,b)
- lessThanEqual(a,b)
- greaterThan(a,b)
- greaterThanEqual(a,b)
- equal(a,b)

a[i] == b[i] ?
して boolean vector を返す

## Vector boolean aggregation func
- any(v)
- all(v)

boolean vector を単一のbooleanにする

## Vector boolean logical ops
- &&
- ||
- not(b) = !b

これらはベクトル各要素を論理計算して boolean vector を返す


# Loop

for, while loop が C の文法で使える

## Loop の罠

C言語よろしく、forループの条件式には変数が使えない？(定数のみ)
(shader school だけかも)


# Matrix

`mat2`, `mat3`, `mat4` のコンストラクタで作れる
- mat + mat : ok
- 2.0 * mat : ok
- mat * mat : ng
- vec * mat : ok (transform)

matrix とスカラーの計算は普通の演算子でできる
matrix 同士の掛け算は関数を使う
`matrixCompMult()`関数
```c
matrixCompMult(m, w);
```


# Fragment vs Pixel

大きさ的には Fragment < Pixel(でかい)
アンチエイリアシングを使うと比率がでかくなる

.frag ファイルの main関数で gl_FragColor を書き換えることで
フラグメントシェーダーの操作を反映する

# gl_FragData[]
フラグメントシェーダーのデータ配列
基本的に、カラーアタッチメントが1つしかない場合は gl_FragData[0] だけが出力に使われる

大抵の場合、マクロでエイリアスが定義される
`gl_FragColor = gl_FragData[0]`


# discard statement
これを実行すると、シェーダー関数内で加えた変更をすべて取り消しつつ処理を中断する。

条件付きで元の入力をそのまま出したい場合に有効

# inTile(vec2, float): bool
```cpp
bool inTile(vec2 p,float tileSize){
  vec2 ptile=step(.5,fract(.5*p/tileSize));
  return ptile.x==ptile.y;
}
```

fract はタイリングなどの境界値判断に便利