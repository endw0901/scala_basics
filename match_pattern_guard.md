# パターンガード

- (X + X) を (X * 2)に変更したいとき

- NG例
```scala
 def simplifyAdd(e: Expr) = e match {
  case BinOp("+", x, x) => BinOp("*", x, Number(2))
  case _ => e
 }
```

- OK例
- ガード(x == y)がtrueならマッチ
```scala
 def simplifyAdd(e: Expr) = e match {
  case BinOp("+", x, y) if x == y =>
     BinOp("*", x, Number(2))
  case _ => e
 }
```

## サンプル

```scala
  // 正の整数なら
  case n: Int if 0 < n =>
  
  // 先頭文字がaなら
 case s:String if s(0) == 'a' => ...
 ```
