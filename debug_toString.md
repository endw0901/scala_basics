# デバッグ用のtoString

- 通常は、res0:xxxxxxのような表示のみ

## toStringをoverride
- デバッグ用のtoStringを上書きすることで、printlnも省略でき、余計なメッセージ表示が省略できる

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
