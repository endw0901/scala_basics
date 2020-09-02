# 文字列補間

## s文字列補間子：$計算式評価
```
s"The answer is ${6*7}."
```

## s文字列補間子：$変数評価 + toString
```
val name = "reader"
println(s"Hello, $name!")
```

## エスケープシーケンシーも表示
```
println(raw"No\\\\aaaa!")
```

## f補間子：フォーマット
- %があるときはフォーマット
- %がないときはs補間子と同じ
```
  val pi = "Pi"
  println(f"$pi is ${math.Pi}%.8f.")
```
