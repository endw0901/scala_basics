# 初期化if文

- varではなくvalをつかうことで、変数が変わっていないかチェックする手間を省ける

## 初期化 => 置き換え
- 初期化してから置き換え
- 置き換えるため、varを使う

```scala
var filename = "default.txt"
if (!args.isEmpty)
  filename = arg(0)
```

## 改善版
- valを使う
- if内で初期化する

```scala
val filename = 
  if (!args.isEmpty) args(0)
  else "defaut.txt"
```
