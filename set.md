# 集合(SET)
- list:重複ok ⇔ set：重複NG
- map:key-value

- setはimmutable、importでmutable
```
// immutableなsetに再代入するのでvarにする必要がある
var aSet = Set("a","b")

// immutableだが、実際は新しい集合(set)を作って再代入している(+=メソッドをコールしているわけではなく省略記法)
aSet += "c"
```

- valはfinal的、varは非final的

```
import scala.collection.mutable
// mutableなのでvalでいい
val bSet = mutable.Set("a","b")

// mutableなsetに挿入している(+=メソッドをコールしている)
bSet += "C"
```

## Setの一般的な操作

```scala
  val nums = Set(1,2,3)

  val nums2 = nums + 5
  println(nums2)

  val nums3 = nums2 - 3
  println(nums3)

  val nums4 = nums3 ++ List(6,7)
  println(nums4)

  val nums5 = nums4 -- List(1,2)
  println(nums5)

  println(nums5.size)
  println(nums5.contains(3))


  // 空のmutable集合を作る
  import scala.collection.mutable
  var words = mutable.Set.empty[String]
  println("words :" + words)

  // 要素を足す、引く
  var words2 = words += "the"
  println(words2)

  var words3 = words2 -= "the"
  println(words3)

  // 複数の要素を足す、引く
  var words4 = words3 ++= List("do", "re", "mi")
  println(words4)

  // HashSet(do)
  var words5 = words4 --= List("re", "mi")
  println(words5)

  // HashSet()
  var words6 = words5.clear
  println("words5 :" + words5)
  // () ※空セット
  println("words6 :" + words6)
```
