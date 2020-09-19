# リストのフィルタリング
- List + filter + [T => Boolean]型の術語関数
- 高階演算子 https://github.com/endw0901/scala_basics/blob/master/function_higher_order_list.md


```scala
  val data = List(1,2,3,4,5) filter (_ % 2 == 0)
  // List(2,4)
  println(data)

  val words = List("the", "quick", "brown", "fox")
  val data2 = words filter (_.length == 3)
```
