# val_事前初期化済みフィールドと遅延評価
- 抽象メンバー https://github.com/endw0901/scala_basics/edit/master/val_var.md
- valとvar https://github.com/endw0901/scala_basics/blob/master/val_var.md

## 評価順の違い
- １）クラスパラメーターは、クラスコンストラクターに渡される前に評価される（名前渡しパラメータの場合を除く）
- ２）サブクラスでのval定義は、スーパークラスが初期化された後で初めて評価される
```scala
  // １）expr1,2の式を評価してから、その結果の値がRationalクラスの初期化に使われる
  new Rational(expr1, expr2)

  // ２）無名クラスのインスタンス生成
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

## 事前初期化済みフィールド
- １）クラスパラメーターは、クラスコンストラクターに渡される前に評価される（名前渡しパラメータの場合を除く）
- ２）サブクラスでのval定義は、スーパークラスが初期化された後で初めて評価される

- 事前初期化済みフィールド：スーパークラスが呼び出される前にサブクラスのフィールドを初期化できるようにするもの

```scala
  // 無名クラス式に含まれる事前初期化済みフィールド
  new {
    val numerArg = 1 * x
    val denomArg = 2 * x
  } with RationalTrait

  // オブジェクト定義に含まれる事前初期化済みフィールド
  object twoThirds extends {
    val numerArg = 2
    val denomArg = 2
  } with RationalTrait

  // クラス定義に含まれる事前初期化済みフィールド
  // スーパートレイトの初期化としてクラスパラメーターを使うのは一般的
  class RationalClass(n: Int, d: Int) extends {
    val numerArg = n
    val denomArg = d
  } with RationalTrait {
    def + (that: RationalClass) = new RationalClass(
      numer * that.denom + that.numer * denomArg
      denom * that.denom
    )
  }
```

### 事前初期化済みフィールドは構築中オブジェクトを参照できない
- スーパークラスのコンストラクターが呼び出される前に初期化されるため、事前初期化済みフィールドは構築中オブジェクトを参照できない

```scala
// errorとなる
new {
val numerArg = 1
val denomArg = this.numerArg * 2
} with RationalTrait
```
