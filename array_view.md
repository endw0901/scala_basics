# 配列のview
- view：https://github.com/endw0901/scala_basics/blob/master/view.md

- p.500
- ウィンドウ・・・・mutable sequenceのviewに適用できるtransofrmer関数の多くは元のsequenceの一部を覗くウィンドウを提供
- ウィンドウを使えば、sequenceの一部の要素を選択的に更新できる

```scala
 val arr = (0 to 9).toArray

  // 配列viewのsliceを作成すると、配列の一部だけのぞくサブウィンドウを作れる
  val subarr = arr.view.slice(3,6)

  def negate(xs: collection.mutable.Seq[Int]) =
    for (i <- 0 until xs.length) xs(i) = -xs(i)

  negate(arr.view.slice(3,6))
  println(arr)
```
