# 連続パラメータを受け取る関数 *
- p.165：パラメータの型の後ろに*を付ける
```scala
def echo(args: String*) =
  for (arg <- args) println(arg)
  
echo("hello", "world")
```

## 配列として個々の要素を連続パラメータとして渡す
- そのまま渡すのはエラー
```scala
val arr = Array("hello", "today", "world")
echo(arr)
```

- 配列を個々の要素として渡す　_*
```scala
val arr = Array("hello", "today", "world")
echo(arr: _*)
```
