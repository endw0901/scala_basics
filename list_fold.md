# 畳み込み /: :\

```scala
  //left fold
  // (z /: List(a,b,c)) (op) equals op(op(op(z,a), b), c)
  ("" /: words) (_ + " " + _)

  (words.head /: words.tail) (_ + " " + _)

  // right fold
  // (List(a, b, c) :\ z) (op) equals op(a, op(b, op(c,z)))
  def flattendLeft[T](xss: List[List[T]]) =
    (List[T]() /: xss) (_ ::: _)

  // 型推論ではリストの要素型は推論できないためアノテーションを省略できない　
  def flattendRight[T](xss: List[List[T]]) =
    // (xss :\ List())とするとエラーとなる
    (xss :\ List[T]()) (_ ::: _)
```
