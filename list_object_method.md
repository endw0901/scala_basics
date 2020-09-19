# リストオブジェクトのメソッド

```scala
  // List(1,2,3,4) 5は含まない
  List.range(1,5)

  // List(1,3,5,7)
  List.range(1,9,2)

  // List(9,6,3)
  List(9,1, -3)

  // List(a,a,a,a,a)
  List.fill(5)('a')
  // List(hello, hello, hello)
  List.fill(3)("hello")

  // List(List(b,b,b), List(b,b,b))
  List.fill(2,3)('b')

  // 表作成
  // List(0, 1, 4, 9, 16)
    val squares = List.tabulate(5)(n => n * n)
  println(squares)

  //List(List(0, 0, 0, 0, 0), List(0, 1, 2, 3, 4), List(0, 2, 4, 6, 8), List(0, 3, 6, 9, 12), List(0, 4, 8, 12, 16))
  val multiplication = List.tabulate(5,5)(_ * _)
  println(multiplication)

  // List(b,c)
  List.concat(List(), List('b'), List('c'))

```
