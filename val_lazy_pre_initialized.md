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

- thisでerrorとなる例
```scala
// errorとなる
new {
val numerArg = 1
val denomArg = this.numerArg * 2
} with RationalTrait
```


## 遅延評価val
- 1.通常の例
```scala
  // 1.通常の例
  object Demo {
    val x = { println("initializing x"); "done" }
  }
  
  Demo // オブジェクト参照した時点でxは初期化される
  Demo.x // String = done
```
- 2.遅延評価版
```scala
  // 2.遅延評価版
  object Demo {
    lazy val x = { println("initializing x"); "done"}
  }
  
  Demo   // Demoを初期化してもxは初期化されない。
  Demo.x // xが参照された時初めて初期化される String = done
  // 2回目以降のx参照は、格納済みのx値を参照するため初期化は1度だけ
```

### 遅延評価valによるtraitの初期化
- trait https://github.com/endw0901/scala_basics/edit/master/trait.md
- 遅延評価はオンデマンドで評価される。ソースコード上の記載順は関係ない
```scala
   trait LazyRationalTrait {
    val numerArg: Int
    val denomArg: Int
    lazy val numer = numerArg / g
    lazy val denom = denomArg / g
    override def toString = numer + "/" + denom
    private lazy val g = {
      require(denomArg != 0)
      gcd(numerArg, denomArg)
    }
    private def gcd(a: Int, b: Int): Int =
      if (b == 0) a else gcd(b, a % b)
      // (2,4) => gcd(4,2/4あまり2) => gcd(4,2) = > gcd(2, 4/2あまり0) => b==0なのでreturn a = 2 => g=2が返る
  }

  val x = 2
  val y = new LazyRationalTrait {
    val numerArg = 1 * x
    val denomArg = 2 * x
  }
  println(y)
```

1. LazyRationalTraitの新しいインスタンスが生成され、初期化コード実行 ※初期化されていない
1. 無名サブクラスの基本コンストラクター(new LazyRationalTrait)が実行され、numerArg = 2, denomArg= 4で初期化される
1. toStringが呼び出される numer / denom
1. ここでnumerが初めて参照され、初期化子が評価される(lazy val numer = numerArg / g) 
1. ここでgが参照され、private lazy val gが評価される ※requireの時点で、denomArg=4なのでエラーにはならない。ここでg = 2となり、numberArg = 2/2, denomArg = 4/2
1. toStringのnumerの次にdenomが評価されるが、既に初期化済みなのでskip
1. toStringのnumer / denomが　1/2と評価済みなので、1/2が表示される
