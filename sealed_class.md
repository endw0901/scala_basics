# シールドクラス

- sealedを付けることで、パターン漏れ定義でエラーが起こるようになる

```scala
sealed abstract class Expr
 case class Var(name: String) extends Expr
 case class Number(num: Double) extends Expr
 case class UnOp(operator: String, arg: Expr) extends Expr
 case class BinOp(operator: String,
                  left: Expr, right: Expr) extends Expr

 // UnOp, BinOpがチェックされていない、とエラーが起こる
 def describe(e: Expr): String = e match {
  case Number(_) => "a number"
  case Var(_)    => "a variable"
 
```

## sealed以外の方法：包括ケースでチェックする方法

```scala
 def describe(e: Expr): String = e match {
  case Number(_) => "a number"
  case Var(_)    => "a variable"
  case _ => throw new RuntimeException
 }
 ```


## sealed以外の方法：@unchecked アノテーションでチェックする方法

```scala
 def describe(e: Expr): String = (e: @unchecked) match {
  case Number(_) => "a number"
  case Var(_)    => "a variable"
 }
 ```
