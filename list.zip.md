# 複数リストをまとめて処理
- p.318

```scala
 // ((0,a),(1,b),(2,c),(3,d),(4,e)
 abcde.indices zip abcde
 
 // こちらの方が簡単(index + valueのとき)
 abcde.zipWithIndex
 ```
 
 ## zipped
- zipped : ペアで処理する
```scala
  // List(30,80) ※5は捨てられる
  val data1 = (List(10,20), List(3,4,5)).zipped.map(_ * _)
  println(data1)
```

  - zippedとforall / exists組み合わせ
  ```scala
  // true
  val data2 = (List("abc", "de"), List(3, 2)).zipped.forall(_.length == _)
  println(data2)

  // false
  val data3 = (List("abc", "de"), List(3,2)).zipped.exists(_.length != _)
  println(data3)
 ```
