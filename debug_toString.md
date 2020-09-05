# デバッグ用のtoString

- 通常は、res0:xxxxxxのような表示のみ

## toStringをoverride

```scala
// 結果：2/3
object ScalaPlayground extends App {
  class Rational(n:Int, d:Int){
    override def toString = n + "/" + d
  }
  val twoThird = new Rational(2,3)
  println(twoThird)
}
```
