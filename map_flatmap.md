# mapとflatMap

```scala
  // mapとflatmapの違い:flatmapは単一リストにする)
  val data4 = words map (_.toList)
  val data5 = words flatMap (_.toList)
  println(data4)
  println(data5)
```

## flatMapとfilterのサンプル
- リストから母と子のペアを取って名前を表示する
```scala
  case class Person(name: String,
                    isMale: Boolean,
                    children: Person*)

  val lara = Person("Lara", false)
  val bob = Person("Bob", true)
  val julie = Person("Julie", false, lara, bob)
  val persons = List(lara, bob, julie)

  // リストから母と子のペアを取って名前を表示する
  val namelist = persons filter (p => !p.isMale) flatMap (p =>
    (p.children map (c => (p.name, c.name))))

  // List((Julie,Lara), (Julie,Bob))
  println(namelist)
```
