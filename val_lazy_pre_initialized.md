# val_事前初期化済みフィールドと遅延評価
- 抽象メンバー https://github.com/endw0901/scala_basics/edit/master/val_var.md
- valとvar https://github.com/endw0901/scala_basics/blob/master/val_var.md

## 評価順の違い
```scala
  // 1.expr1,2の式を評価してから、その結果の値がRationalクラスの初期化に使われる
  new Rational(expr1, expr2)

  // 2.無名クラスのインスタンス生成
  // RationalTraitの後で初期化される
  new RationalTrait {
    val numerArg = expr1
    val denomArg = expr2
  }
```

### 評価順の違いによるエラー発生の例
- 後で評価されるものを使ったため、0となってしまいrequireでエラー
- assert, assume, require, ensuring https://github.com/endw0901/scala_basics/blob/master/assertion_test.md
```scala
  trait RationalTrait {
    val numerArg: Int
    val denomArg: Int
    require(denomArg != 0)
    private val g = gcd(numerArg, denomArg)
    val numer = numerArg / g
    val denom = denomArg / g
    private def gcd(a: Int, b: Int): Int =
      if (b == 0) a else gcd(b, a % b)
    override def toString = numer + "/" + denom
  }

  val x = 2
  // error発生（requireで)
  new RationalTrait {
    val numerArg = 1 * x
    val denomArg = 2 * x
  }
```
