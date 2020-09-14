# case class・パターンマッチ


## case class
- new Varを省略できる
- case classの引数は valフィールドとして管理される
```scala
  abstract class Expr
  case class Var(name: String) extends Expr
  case class Number(num: Double) extends Expr
  case class UnOp(operator: String, arg: Expr) extends Expr
  case class BinOp(operator: String, left: Expr, right: Expr) extends Expr

  // new Varを省略できる
  val v = Var("x")
  // case classの引数は valフィールドとして管理される
  v.name
```

# パターンマッチ
