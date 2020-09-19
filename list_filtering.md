# リストのフィルタリング
- 高階演算子 https://github.com/endw0901/scala_basics/blob/master/function_higher_order_list.md


## filter
- List + filter + [T => Boolean]型の術語関数
```scala
  val data = List(1,2,3,4,5) filter (_ % 2 == 0)
  // List(2,4)
  println(data)

  val words = List("the", "quick", "brown", "fox")
  val data2 = words filter (_.length == 3)
```

### find
- filterと同じだが最初の要素だけ返す
```scala
 　val data = List(1,2,3,4,5) find (_ % 2 == 0)
  
  // Some(2)
  println(data)

  val words = List("the", "quick", "brown", "fox")
  val data2 = words find (_.length == 3)
  // Some(the)
  println(data2)
```

## partition
- Someは値があることを示す
```scala
  // xs partition p equals (xs filter p, xs filter (!p(_)))
  // trueリスト + false リストにわける→ (List(2,4), List(1,3,5))
  List(1,2,3,4,5) partition (_ %  2 == 0)
```
