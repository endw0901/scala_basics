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

## ワイルドカード

```scala
  // wild card(_) pattern
  expr match {
    case BinOp(op, left, right) =>
      println(expr + " is abinary operation")
    case _ => // default case
  }

  expr match {
    case BinOp(_, _, _) => println(expr + " is a binary operation")
    case _ => println("something else")
  }
```

## 定数パターンと変数パターン
- 変数はワイルドカードと同じだが、値を掴めるのでprint文字列にそのまま使える
- 小文字は変数、大文字は定数→下記は変数のため、case _ はとおらずすべてpiにつかまるため、コンパイルwarning発生
- バッククォートで小文字でも定数扱いできる
```scala
  // 定数パターン
  def describe(x: Any) = x match {
    case 5 => "five"
    case true => "truth"
    case "hello" => "hi"
    // Nilは空リストにだけマッチ
    case Nil =>  "empty list"
    case _ => "something else"
  }

  // 使い方
  describe(5)
  describe(true)
  describe("hello")
  describe(Nil)
  describe(List(1,2,3))

  // 変数はワイルドカードと同じだが、値を掴めるのでprint文字列にそのまま使える
  // 小文字は変数、大文字は定数→下記は変数のため、case _ はとおらずすべてpiにつかまるため、コンパイルwarning発生
  import math.{E, Pi}
  val pi = math.Pi
  E match {
    // piは変数
    case pi => "strange math? Pi = " + pi
    case _ => "ok"
  }

  // バッククオート使えば小文字でも定数と解釈される
  E match {
    case `pi` => "strange math? Pi = " + pi
    case _ => "ok"
  }

```

## コンストラクタパターン

```scala
 // コンストラクタパターン ※深いマッチ(BinOpか、0か・・まで)
  expr match {
    case BinOp("+", e, Number(0)) => println("a deep match")
    case _ =>
  }
```

## シーケンスパターン

```scala
  // シーケンスパターン => 3つ固定のリストかどうか（最初は0、あとはなんでも)
  expr match {
    case List(0, _, _) => println("found it")
    case _ =>
  }
  
  // 任意の長さ
  expr match {
    case List(0, _*) => println("found it")
    case _ => 
  }
```
