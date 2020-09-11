# collection型_List拡張のTraversableトレイト定義のループメソッド

- p.177
- 特殊な用途のループ実行用メソッドを使うと、コードを短くできることが多い

## 例 マイナスがあるかどうか
- 改善前
```scala
object ScalaPlayground extends App {
  def containsNeg(nums: List[Int]): Boolean = {
    var exists = false
    for (num <- nums)
      if (num < 0)
        exists = true
    exists
  }

  println(containsNeg(List(1,2,3,4)))
  println(containsNeg(List(1,2,-3,4)))
}
```

- Listメソッドのexistsを使った簡易版
```scala
object ScalaPlayground extends App {

// Listのメソッドexistsで、マイナスを探す
  def containsNeg2(nums: List[Int]) = nums.exists(_ < 0)

  println(containsNeg2(Nil))
  println(containsNeg2(List(0, -1,2)))
}
```

## 例 奇数があるかどうか
- 改善前
```scala
object ScalaPlayground extends App {
  def containsOdd(nums: List[Int]): Boolean = {
    var exists = false
    for (num <- nums)
      if (num % 2 == 1)
        exists = true
    exists
  }

  println(containsNeg(List(1,2,3,4)))
  println(containsNeg(List(2,4)))
}
```

- Listメソッドのexistsを使った簡易版
```scala
object ScalaPlayground extends App {

// Listのメソッドexistsで、奇数を探す
  def containsOdd2(nums: List[Int]) = nums.exists(_ % 2 == 1)

  println(containsNeg2(Nil))
  println(containsNeg(List(1,2,3,4)))
}
```
