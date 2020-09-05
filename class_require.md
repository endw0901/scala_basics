# クラス生成条件require

- 0で割るときはclassを生成しない、などの条件をつけたい

```scala
object ScalaPlayground extends App {

  class Rational(n:Int, d:Int){
    require(d != 0)
    override def toString = n + "/" + d
  }

  val twoThird = new Rational(2,3)
  println(twoThird)
  
  val twozero = new Rational(2,0)
}

```
