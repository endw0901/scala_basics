# mapとflatMap

```scala
  // mapとflatmapの違い:flatmapは単一リストにする)
  val data4 = words map (_.toList)
  val data5 = words flatMap (_.toList)
  println(data4)
  println(data5)
```

## flatMapとfilterのサンプル => forで効率化
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
- list filtering https://github.com/endw0901/scala_basics/blob/master/list_filtering.md

### withFilterを使った効率化

```scala
  // 女性データを集めた中間データ構造の生成を回避でき、効率化できる
  val nameList2 = persons withFilter (p => !p.isMale) flatMap (p =>
    (p.children map (c => (p.name, c.name))))

  println(namelist)
```

### for式で分かりやすく
- for反復処理：https://github.com/endw0901/scala_basics/blob/master/for.md
```scala
  val nameList3 = for (p <- persons; if !p.isMale; c <- p.children)
    yield (p.name, c.name)

  println(nameList3)
```
