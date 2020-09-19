# マージソート
```scala
  def msort[T](less: (T,T) => Boolean)
              (xs: List[T]): List[T] ={
    def merge(xs: List[T], ys: List[T]): List[T] =
      (xs, ys) match {
        case (Nil, _) => ys
        case (_, Nil) => xs
        // 小さいものを先頭にしてマージしていく
        case (x :: xs1, y :: ys1) =>
          if (less(x,y)) x :: merge(xs1, ys)
          else y :: merge(xs, ys1)
      }
    // 半分で分割
    val n = xs.length / 2
    if (n == 0) xs
    else {
      val (ys, zs) = xs splitAt n
      // ソートマージ
      merge(msort(less)(ys), msort(less)(zs))
    }
  }
```

- 実行
```scala
  println(msort((x: Int, y: Int) => x < y)(List(5,7,1,3)))
```

## カリー化を利用したソート
- カリー化について：https://github.com/endw0901/scala_basics/blob/master/currying.md

```scala
  // まずlessの定義だけ入れて欠けた引数を後から引き渡す
  val mixedInts = List(4,1,0,9,5,8,3,6)
  
  // 昇順
  val intSort = msort((x: Int, y: Int) => x < y) _
  println(intSort(mixedInts))
  
  // 降順
  val reverseIntSort = msort((x: Int, y: Int) => x > y) _
  println(reverseIntSort(mixedInts))
```

