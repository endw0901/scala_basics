# ストリーム
- p.477
- パフォーマンス性能はリストと同じ。遅延評価される点が違う
- Listは有限のimmutableシーケンスだが、Streamは無限に長くできる

```scala
  // 1,2,3を含むStream
  val str = 1 #:: 2 #:: 3 #:: Stream.empty

  // フィボナッチ数のStream
  def fibFrom(a: Int, b: Int): Stream[Int] =
    // ::だと無現再帰になるが、#::は遅延評価のため、take(7)で評価されて初めて計算される
    // そのため、Streamは無限に追加できるが、指定した7で止まる
    a #:: fibFrom(b, a + b)

  val fibs = fibFrom(1,1).take(7)
  println(fibs.toList) // List(1, 1, 2, 3, 5, 8, 13)
```
