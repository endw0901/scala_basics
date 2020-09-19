# mapとflatMap

```scala
  // mapとflatmapの違い:flatmapは単一リストにする)
  val data4 = words map (_.toList)
  val data5 = words flatMap (_.toList)
  println(data4)
  println(data5)
```
