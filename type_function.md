# 関数の型
- p.179

- op:Double => Double 関数の型
```scala
object ScalaPlayground extends App {

  def once(op:Double => Double, x: Double) = op(x)
  println(once(_ +1, 5))

  def twice(op:Double => Double, x: Double) = op(op(x))
  println(twice(_ +1, 5))
}
```
