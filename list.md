# リスト
- リスト = クラス
- クラスインスタンス生成 = クラスオブジェクト生成

- 配列：mutable ⇔ リスト・タプル：immutable
- リスト：同じ型 ⇔ タプル：異なる型を持てる


## リストのメソッド
- https://www.scala-lang.org/api/2.12.3/scala/collection/immutable/List.html

### 例
```scala
// 値＋リスト結合
val twoThree = List(2,3)
val oneThree = 1 :: threeFour

// 値＋リスト結合
val oneTwo = List(1,2)
val threeFour = List(3,4)
val oneFour = oneTwo ::: threeFour

// 一部出力
listdata(2)

// 最初の2つを削除
listdata.drop(2)

// その他
filter
map

// カンマ区切り＋空白で区切る
listdata.mkString(", ")

```

## appendとprepend
- p.66
- appendはデータ保持の問題で遅い。代わりに、prepend(先頭挿入) + reverseで逆転して最後のを最初に持ってくる

## 基本メソッド
- p.296
```scala
 val fruit = List("apples","oranges","pears")
 val nums = List(1,2,3,4)
 val diag3 =
  List(
   List(1,0,0),
   List(0,1,0),
   List(0,0,1)
  )
 val empty = List()

 println(empty.isEmpty)
 println(fruit.isEmpty)
 println(fruit.head)
 // tail = 先頭を除くリストを返す
 println(fruit.tail)
 // tail.head = 先頭を除くリストの先頭(=元リストの2番目)を返す
 println(fruit.tail.head)
 println(diag3.head)
```
### 結合

```scala
 // Nilは空リスト
 val nums = 1 :: 2 :: 3 :: Nil
 // List(1,2,3)
 println(nums)

 // :::はリスト同士の結合
 // List(1,2,3,4,5)
 println(List(1,2) ::: List(3,4,5))

```

### headとtail, initとlast
- p.301
- initとlastはリスト全体をたどらないと操作できないため時間がかかる。
```scala
 val fruit = List("apples","oranges","pears")
 
 // head = 先頭の要素を返す 
 println(fruit.head)
 // tail = 先頭を除くリストを返す
 println(fruit.tail)

 // init = 最後の要素を除くリストを返す 
 println(fruit.init)
 // last = 最後の要素を返す
 println(fruit.last)
```

### 反転
- リストはimmutableなので、reverseは新しいリストを作る。元リストはそのまま
```scala
// List(e, d, c, b, a)
abcde.reverse

```

- reverseとhead-tail, init-last
```scala
// e,d,c,b
xs.reverse.init equals xs.tail.reverse
// d,c,b,a
xs.reverse.tail equals xs.init.reverse
// e
xs.reverse.head equals xs.last
// a
xs.reverse.last equals xs.head

```

#### :::を使ったreverse
```scala
def rev[T](xs: List[T]): List[T] = xs match {
  case List() => xs
  case x :: xs1 => rev(xs1) ::: List(x)
}
```

### drop, take, splitAt

```scala
val abcde = List('a','b','c','d','e')

  // List(a,b) 最初の2つを取る
 abcde take 2
 
 // List(c,d,e)  最初の2つ以外をとる
 abcde drop 2

 // (List(a,b), List(c,d,e))
 abcde splitAt 2
```

### リストのリストを単層にする：flatten
```scala
// List(1,2,3,4,5)
List(List(1,2),List(3,4,5)).flatten
```

### 添え字を返す:indices
```scala
val abcde = List('a','b','c','d','e')
// Range(0,1,2,3,4)
abcde.indices
```

### ペアを作るzip
```scala
 // ((0,a),(1,b),(2,c),(3,d),(4,e)
 abcde.indices zip abcde
 
 // こちらの方が簡単(index + valueのとき)
 abcde.zipWithIndex
 ```
- unzipでziplistを展開

### mkString
- pre + sep + post
```scala
// [a,b,c,d,e]
abcde mkString ("[", ",", "]")
```

### iterator
```scala
  val abcde = List('a','b','c','d','e')
// nextからaがとれる
 println(abcde.iterator.next)
```

### 位置を指定してcopy : copyToArray
```scala
// Array(0,0,0,0,0,0,0,0,0,0)
val arr = new Array[Int](10)
// Array(0,0,0,1,2,3,0,0,0,0)
List(1,2,3) copyToArray(arr,3)


```

### iterator, Array
```scala
// Array(a,b,c)
val arr = abc.toArray

// List(a,b,c)
arr.toList
```

### sortWith
```scala
List(1, -3, 4, 2, 6) sortWith (_ < _)
words sortWith (_.length > _.length)
```

## サンプル：ソートアルゴリズム
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

## 共変
- 共変covariantのためInt⇒Anyに格納できる
```scala
  // Listクラスの一部
  // abstract class List[+T]
  
  // 共変covariantのためInt⇒Anyに格納できる
  val xs = List(1,2,3)
  var ys: List[Any] = xs
```
