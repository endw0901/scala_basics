# Map
- list:重複ok ⇔ set：重複NG
- map:key-value

- mapはimmutable、importでmutable

## immutableなmap

```
// 引き渡す値で型が推論できるので型明示不要
val imMap = Map(1 -> "a", 2 -> "b", 3 -> "c")
println(imMap(1)) // a
println(imMap(2)) // b
```

## mutableなmap
```
  import scala.collection.mutable
  
  // 空map定義(型推論できないので型を明示
  val mMap = mutable.Map[Int, String]()
  
  // 値セット
  mMap += (1 -> "a a a")
  mMap += (2 -> "bbb")
  mMap += (3 -> "cc c")
  println(mMap(1))
  println(mMap(2))
  println(mMap(3))
```
