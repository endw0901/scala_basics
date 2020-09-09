# 名前付き引数
- p.166

```scala
def speed(distance: Float, time: Float): Float =
  distance / time
  
// 順番に引き渡す => 100/10
speed(100, 10)

// 順番がばらばらでも、名前付き引数なら => 100/10 同じ結果になる
speed(time = 10, distance = 100)
```

