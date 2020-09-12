# フィールド

- p.117
- add内で、別のRationalを引数で受けて、自分のフィールドと引数の別のクラスのフィールドを使って計算ができる
- n + that.nとはできない。フィールド上にそれぞれ保持しないといけない

```scala
object ScalaPlayground extends App {

  class Rational(n:Int, d:Int){
    require(d != 0)

    // フィールド
    val numer: Int = n
    val denom: Int = d

    override def toString = numer + "/" + denom

    def add(that: Rational): Rational =
      new Rational(
        numer * that.denom + that.numer * denom,
        denom * that.denom
      )
  }

  val oneHalf = new Rational(1,2)
  val twoThirds = new Rational(2,3)
  println("oneHalf :" + oneHalf)
  println("twoThird :" + twoThirds)

  println(oneHalf add twoThirds)

  // val twozero = new Rational(2,0)
  
  // フィールドにアクセス
  println("oneHalf.numer :" + oneHalf.numer)
}
```

## パラメータフィールド
- p.191

- 改善前：パラメータフィールド（引数）を受けてクラス内のフィールドに設定
```scala
  class ArrayElement(conts: Array[String]) extends Element {
    val contents: Array[String] = conts
  }
```

- 改善後：フィールドを引数に移す
- パラメータとフィールドに同名で定義するため、valを付与
```scala
  class ArrayElement(
    val contents: Array[String]
) extends Element
```

### field を引数に移す別例

```scala
class Tiger(param1: Boolean, param2: Int) extends Cat {
  override val dangerous = param1
  private var age = param2
}
```

```scala
class Tiger(
  override val dangerous: Boolean,
  private var age: Int
) extends Cat
```
