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
