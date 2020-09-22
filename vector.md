# ベクター
- リストは先頭アクセスが効率的、末尾はリストの要素分時間がかかる
- ベクターは先頭以外にも効率的にアクセスできる(実質一定）

```scala 
  val vec = scala.collection.immutable.Vector.empty
  val vec2 = vec :+ 1 :+ 2
  val vec3 = 100 +: vec2
  println(vec)     // Vector()
  println(vec2)    // Vector(1, 2)
  println(vec3)    // Vector(100, 1, 2)
  println(vec3(0)) // 100
```

## update
```scala
  // immutable だが、要素が異なるvectorを作れる(update)
  val vec4 = Vector(1,2,3)
  // index=2の位置なので3を4に変える
  val vec5 = vec4 updated (2,4)
  println(vec4) // Vector(1, 2, 3)
  println(vec5) // Vector(1, 2, 4)
```

## 高速アクセス
- ランダム選択が高速で、関数的更新も高速なのでimmutableな添え字付きシーケンスのデフォルトがvectorになっている

```scala
  // immutableな添え字付きシーケンスのデフォルトがvector
  println(collection.immutable.IndexedSeq(1,2,3)) // Vector(1, 2, 3)
```
