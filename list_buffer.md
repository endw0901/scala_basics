# ListBufferクラス

## 1.ListBufferもmapも使わないケース
- 欠点：末尾再帰でなく、スタックフレームオーバーフローが発生

```scala
  // Listの各要素に + 1
  // ::演算の中でスタックフレームが積み重なる
  def incAll(xs: List[Int]): List[Int] = xs match {
    case List() => List()
    case x :: xs1 => x + 1 :: incAll(xs1)
  }
```

## 2.ループを使用するケース
- ::: はリストの長さに応じて時間がかかるため非常に効率が悪い
```scala
  var result = List[Int]()
  for (x <- xs) result = result ::: List(x + 1)
  result
```


## 3.ListBufferを使う（効率よい)
- bufferに要素を1加算しつつ追加し、最後にリストに戻すのみ
```scala
  import scala.collection.mutable.ListBuffer
  val buf = new ListBuffer[Int]
  for (x <- xs) buf += x + 1
  
  buf.toList
```

## Listクラスmapメソッドの中身

```scala

  import scala.collection.mutable.ListBuffer
  final override def map[U](f: T => U): List[U] = {
    val b = new ListBuffer[U]
    var these = this
    while (!these.isEmpty) {
      b += f(these.head)
      these = these.tail
    }
    b.toList
  }
```
