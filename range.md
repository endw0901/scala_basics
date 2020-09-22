# レンジ

- レンジ：等間隔で並べられたソート済みの整数シーケンス
- レンジ演算は高速

```scala
  // toは上限を含む
  val range1 = 1 to 3
  println(range1) // Range(1,2,3)

  // byでｘｘごと
  val range2 = 5 to 14 by 3
  println(range2) // Range(5,8,11,14)

  // untileは上限を含まない
  val range3 = 1 until 3
  println(range3) // Range(1,2)
```
