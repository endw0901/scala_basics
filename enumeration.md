# 列挙enumeration

```scala
object Direction extends Enumeration {
    val North = Value("North")
    val East = Value("East")
    val South = Value("South")
    val West = Value("West")
  }
  
  // valuesメソッドで列挙値をprint
  for (d <- Direction.values) print(d + " ")
  
  // 列挙値のidが分かる
  Direction.East.id // Int = 1
  Direction(1) // Direction.Value = East
  
  // importして使う
  import Dicrection._

```
