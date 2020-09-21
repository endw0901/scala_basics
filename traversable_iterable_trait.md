# Traversableトレイト、Iterableトレイト
- Iterableの上位がTraversable

## grouped / Iterable
```scala
  val xs = List(1,2,3,4,5)
  val git = xs grouped 3

  println(git.next()) // List(1, 2, 3)
  println(git.next()) // List(4, 5)
```

## sliding / Iterable

```scala
  val xs = List(1,2,3,4,5)
  val sit = xs sliding 3

  println(sit.next()) // List(1, 2, 3)
  println(sit.next()) // List(2, 3, 4)
```

## Traversableの方が効率がいい場合
- 100万要素の場合、Traversableのforeachなら200万ステップ、Iterableのiteratorなら2000万ステップになり大きな差が出る
```scala
  // Traversableで実装
  sealed abstract class Tree extends Traversable[Int] {
    def foreach[U](f: Int => U) = this match {
      case Node(elem) => f(elem)
      case Branch(l, r) => l foreach f; r foreach false
    }
  }
  
  // Iterableで実装
  sealed abstract class Tree extends Iterable[Int] {
    def iterator: Iterator[Int] = this match {
      case Node(elem) => Iterator.single(elem)
      // iteratorに辿りつくのに時間がかかる
      case Branch(l, r) => l.iterator ++ r.iterator
    }
  }
```
