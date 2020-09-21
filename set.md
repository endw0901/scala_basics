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
'''

### 空のmutable集合を作る
```scala
  // 空のmutable集合を作る
  import scala.collection.mutable
  var words = mutable.Set.empty[String]
  println("words :" + words)
```

### 要素を足す、引く
```scala
  // 要素を足す、引く
  var words2 = words += "the"
  println(words2)

  var words3 = words2 -= "the"
  println(words3)

  // 複数の要素を足す、引く
  var words4 = words3 ++= List("do", "re", "mi")
  println(words4)
```

### HashSet
```scala
  // HashSet(do)
  var words5 = words4 --= List("re", "mi")
  println(words5)

  // HashSet()
  var words6 = words5.clear
  println("words5 :" + words5)
  // () ※空セット
  println("words6 :" + words6)
```

## apply
- applyメソッドのコレクションごとの違い
```scala
// 添え字で選択
Seq(1,2,3)(1) == 2
// 判定
Set('a','b','c')('b') == true
// keyで選択
Map('a' -> 1, 'b' -> 10, 'c' -> 100)('b') == 10
```

## mutableとimmutableの効率差
```scala
  // immutable Set : 要素4個までなら単一のオブジェクトで表現するコンパクト。それ以上はmutableが効率的
  var s = Set(1,2,3)
  s += 4; s-= 2
  println(s) // Set(1, 3, 4)
  
  // mutable
  val s2 = collection.mutable.Set(1,2,3)
  s2 += 4 // + ++より効率的
  s2 -= 2 // - --より効率的
  println(s2) // HashSet(1, 3, 4)
```

### 要素数が多い場合
```scala
  // immutable Set : 要素4個までなら単一のオブジェクトで表現するコンパクト。それ以上はmutableが効率的
  var s = Set(1,2,3,7,8,9)
  s += 4; s-= 2
  println(s) // HashSet(1, 9, 7, 3, 8, 4)

  // mutable
  val s2 = collection.mutable.Set(1,2,3,7,8,9)
  s2 += 4 // + ++より効率的
  s2 -= 2 // - --より効率的
  println(s2) // HashSet(1, 3, 4, 7, 8, 9)
```
