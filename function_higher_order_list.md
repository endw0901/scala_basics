# 高階メソッド

## List
```scala
  // 1足す：List(2,3,4)
  val data = List(1,2,3) map (_ + 1)
  println(data)

  // 文字列の長さ：List(3,5,5,3)
  val words = List("the", "quick", "brown", "fox")
  val data2 = words map (_.length)
  println(data2)

  // 文字列逆転　List(eht, kcuiq,,,,,)
  val data3 = words map (_.toList.reverse.mkString)
  println(data3)
```

### mapとflatMap
```scala
  // mapとflatmapの違い:flatmapは単一リストにする)
  val data4 = words map (_.toList)
  val data5 = words flatMap (_.toList)
  println(data4)
  println(data5)
```
