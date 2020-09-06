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
}
```

## パラメータフィールド
- p.191
