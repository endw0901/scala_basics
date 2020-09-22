# 配列バッファー
- mutable
- 配列：https://github.com/endw0901/scala_basics/blob/master/array.md

- 末尾に効率よくデータを追加できる（先頭に効率がいいのはリスト）
- 配列と配列バッファーは同じ速さで実行できる

```scala
  val buf = collection.mutable.ArrayBuffer.empty[Int]
  println(buf) //ArrayBuffer()

  buf += 1
  println(buf) // ArrayBuffer(1)

  buf += 10
  println(buf) // ArrayBuffer(1, 10)

  var array2 = buf.toArray
  println(array2) // Array(1,10)

```
