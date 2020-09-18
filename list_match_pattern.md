# リストパターン

```scala
 val fruit = List("apples","oranges","pears")
 // restはList(pears)
 val List(a,b,c) = fruit
 val a :: b :: rest = fruit
 ```
 
## リストパターンを使わないソートアルゴリズム１
```scala
 // ソートアルゴリズム
 def isort(xs: List[Int]): List[Int] =
  if(xs.isEmpty) Nil
  else insert(xs.head, isort(xs.tail))
 def insert(x: Int, xs: List[Int]) : List[Int] =
  if(xs.isEmpty || x <= xs.head) x :: xs
  else xs.head :: insert(x, xs.tail)

 val sortedList = isort(List(5,4,3))
 println(sortedList)

 // insert(5,(4,3))
 // insert(4,3) => 3,4でリターン
 // insert(5,(4,3)) => insert(5,(3,4)) => (3,insert(5,4))をリターン
 // insert(5,4) => (4,5)をリターン
 // (3,insert(5,4)) => (3,4,5)をリターン
```
 
## リストパターンマッチを使ったソートアルゴリズム２
```scala
 def isort(xs: List[Int]): List[Int] = xs match {
  // isEmptyの代わりにcase List()でパターンマッチ
  case List() => List()
  // xs1はxを除く残りのリスト(headを除くtail)
  case x :: xs1 => insert(x, isort(xs1))
 }
 def insert(x: Int, xs: List[Int]): List[Int] = xs match {
  case List() => List(x)
  case y :: ys => if (x <= y) x :: xs
  else y :: insert(x, ys)
 }
```
