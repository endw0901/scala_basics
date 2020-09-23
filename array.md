# 配列
- 配列 = クラス
- クラスインスタンス生成 = クラスオブジェクト生成

- 配列：mutable ⇔ リスト：immutable

## 配列の新規作成
- 通常使う方法

```
  val names = Array("one","two","three")
  for(i <- 0 to 2)
    print(names(i))
    
```

### 面倒な方法
- 配列クラスオブジェクト作成⇒値を一個一個設定
```
val data = new Array[String](2)
  data(0) = "ito"
  data(1) = "tanaka"
  for(i <- 0 to 1)
    print(data(i))
```

## 配列の連結

- ++
```scala
  abstract class Element {
    def contents: Array[String]
    def height: Int = contents.length
    def width: Int = if (height == 0) 0 else contents(0).length
  }

  class ArrayElement(conts: Array[String]) extends Element {
    def contents: Array[String] = conts
  }
  
def above(that: Element): Element =
    new ArrayElement(this.contents ++ that.contents)  
```

## sequenceと互換性がある
- sequence演算をサポート

```scala
  val a1 = Array(1,2,3)
  println(a1) // Array(1,2,3)

  val a2 = a1 map (_ * 3)
  println(a2) // Array(3,6,9)

  val a3 = a2 filter (_ % 2 != 0)
  println(a3) // Array(3,9)

  println(a3.reverse) // Array(9,3)
```

### sequenceと互換性がある
```scala
  // sequenceと互換性がある
  val seq: Seq[Int] = a1
  println(seq) // WrappedArray(1,2,3)

  val a4: Array[Int]  =seq.toArray
  println(a4) // Array(1,2,3)

  a1 eq a4 // true

  val seq: Seq[Int] = a1
  println(seq) // WrappedArray(1,2,3)

  seq.reverse // WrappedArray(3,2,1)

  val ops: collection.mutable.ArrayOps[Int] = a1 // [I(1,2,3

  ops.reverse // Array(3,2,1)
```


## クラスタグ
- クラスタグがないとエラー
```scala
   def evenElems[T](xs: Vector[T]): Array[T] = {
      val arr = new Array[T]((xs.length + 1) / 2)
      for (i <- 0 until xs.length by 2)
        arr(i / 2) = xs(i)
      arr
    }
```

### クラスタグつき
```scala
  import scala.reflect.ClassTag
  def evenElems[T: ClassTag](xs: Vector[T]): Array[T] = {
    val arr = new Array[T]((xs.length + 1) / 2)
    for (i <- 0 until xs.length by 2)
      arr(i / 2) = xs(i)
    arr
  }

  evenElems(Vector(1,2,3,4,5))
  evenElems(Vector("this", "is", "a", "test"))

```

