# 型コンストラクター
- 非公開クラスを持つコンパニオンオブジェクトでファクトリーメソッドを提供するtraitインターフェイスの例
- https://github.com/endw0901/scala_basics/blob/master/class_private.md

## ジェネリックトレイト
- QueueトレイトはQueue型の変数を作れないが、ジェネリックとしてQueue[Int]やQueue[String]など型パラメータを指定して型を作れる
- 型コンストラクター type constructor

```scala
def doesCompile(q: Queue[AnyRef]) = {}
```

## ジェネリックのサブ型(
- デフォルトでは非変nonvariantで厳格rigid

- 共変のサブ型 => Queue[String]をQueue[AnyRef]のサブ型とみなす
```scala
trait Queue[+T] {......}
```

### 型パラメータの変位指定(variant)：共変covariant、反変contravariant、非変nonvariant
- 変位指定アノテーション：+ -

```scala
// 非変nonvariant ※デフォルト状態
trait Queue[T] {....}

// 共変covariant
trait Queue[+T] {......}

// 反変contravariant
trait Queue[-T] {....}
```

## 関数型の関数トレイトへの展開と変位指定(variant)
- 関数型「S => T」を使うと関数トレイトに展開される
- 引数は反変の-S、結果は共変の+T
```scala
// 関数トレイト
trait Function1[-S, +T] {
  def apply(x: S): T
}
```

### 関数型パラメータの変位指定サンプル
- p.376

- 「サブBook => スーパーAnyRef」を、「スーパーPublication => サブString」として扱う（-S反変、+T共変)
- PublicationのメソッドはサブクラスBookでもすべて使えるので反変（サブをスーパーとして扱う)
- StringだけでなくAnyRefのサブクラスどれを使っても満たせるので共変(スーパーをサブとして扱う)

```scala
 class Publication(val title: String)
 class Book(title: String) extends Publication(title)
  
 object Library {
   val books: Set[Book] =
     Set(
       new Book("Programming in Scala"),
       new Book("Walden")
     )
   // 関数型:サブBookに引き渡しをスーパーPublicationとして引き渡し（反変）、結果のサブStringをAnyRefに(共変）
   def printBookList(info: Book => AnyRef) = {
     for (book <- books) println(info(book))
   }
 }
 object Customer extends App{
    def getTitle(p: Publication): String = p.title
    // getTitle関数を「関数型Book => AnyRef」に渡す
    Library.printBookList(getTitle)
 }
```

## 境界
- lower bounds : https://github.com/endw0901/scala_basics/blob/master/class_private.md
- upper bounds

```scala
  // Orderdトレイトをミックスインしているリストを引数にOrderedの抽象メソッドcompareを実装すれば <>演算子で比較できる
  class Person(val firstName: String, val lastName: String) extends Ordered[Person] {
    def compare(that: Person) = {
      val lastNameComparison = lastName.compareToIgnoreCase(that.lastName)
      if (lastNameComparison != 0)
        lastNameComparison
      else
        firstName.compareToIgnoreCase(that.firstName)
    }
    override def toString = firstName + " " + lastName
  }

  // 比較実行
  val robert = new Person("Robert", "Jones")
  val sally = new Person("Sally", "Smith")
  // compareメソッドを実装しているので演算子でインスタンス比較ができる
  println(robert < sally)


  // 上限境界upper bounds
  def orderedMergeSort[T <: Ordered[T]](xs: List[T]): List[T] = {
    def merge(xs: List[T], ys: List[T]): List[T] =
      (xs, ys) match {
        case (Nil, _) => ys
        case (_, Nil) => xs
        case (x :: xs1, y :: ys1) =>
          if (x < y) x :: merge(xs1, ys)
          else y :: merge(xs, ys1)
      }
    val n = xs.length / 2
    if (n == 0) xs
    else {
      val (ys, zs) = xs splitAt n
      merge(orderedMergeSort(ys), orderedMergeSort(zs))
    }
  }

  val people = List(
    new Person("Larry", "Wall"),
    new Person("Anders", "Herberg"),
    new Person("Guido", "van Rossum"),
    new Person("Alan", "Kay"),
    new Person("Yukihiro", "Matsumoto"),
  )

  // Orderedのサブ型の要素のみ渡せる
  val sortedPeople = orderedMergeSort(people)
  println(sortedPeople) // List(Anders Herberg, Alan Kay, Yukihiro Matsumoto, Guido van Rossum, Larry Wall)

  // エラーとなる : List要素がIntで、IntはOrderedのサブ型ではないので
  // val wontCompile = orderedMergeSort(List(3,2,1))
```
