# 自己参照

- p.118
- numer * that.denom は、this.numer * that.denonの省略形

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
