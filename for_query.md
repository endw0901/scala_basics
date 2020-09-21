# for式クエリ
- クエリをかけるデータベース作成
- case classで定義したBook型のListのネスト
```scala
  case class Book(title: String, authors: String*)

  val books: List[Book] =
    List(
      Book(
        "aaaa",
        "ito", "tanaka"
      ),
      Book(
        "bbbb",
        "kunugi", "akari"
      ),
      Book(
        "cccc",
        "egg", "dreadnote","kunugi"
      )
    )
```

- 著者の名前からtitle名検索
```scala
  // 著者の名前からtitle名検索
  val findTitle = for (b <- books; a <- b.authors if a startsWith "i")
  yield b.title

  println(findTitle) // List(aaaa)
```

- タイトルから著者検索
```scala
  // タイトルから著者検索
  val findAuthor = for (b <- books if (b.title indexOf "cc") >= 0)
  yield b.title

  println(findAuthor)
```

- 2冊以上の著作を持っている ①本が違う組み合わせの中で、②著者が同じものを yield
```scala
  // 2冊以上の著作を持っている ①本が違う組み合わせの中で、②著者が同じものを yield
  val finnd2name = for (b1 <- books; b2 <- books if b1 != b2;
       a1 <- b1.authors; a2 <- b2.authors if a1 == a2)
    yield a1

  println(finnd2name)
```

- 重複排除
```scala
  def removeDuplicates[A](xs: List[A]): List[A] = {
    if (xs.isEmpty) xs
    else
      xs.head :: removeDuplicates(
        xs.tail filter (x => x != xs.head)
      )
  }

  removeDuplicates(finnd2name)
```

- 重複排除_for式
```scala
  def removeDuplicatesFor[A](xs: List[A]): List[A] = {
    if (xs.isEmpty) xs
    else
      xs.head :: removeDuplicatesFor(
        // xs.tail filter (x => x != xs.head)
        for (x <- xs.tail if x != xs.head) yield x
      )
  }

  removeDuplicatesFor(finnd2name)
```

## N女王問題

```scala
  // for_eight_queens
  def queens(n: Int): List[List[(Int, Int)]] = {
    def placeQueens(k: Int): List[List[(Int, Int)]] =
      if (k == 0)
        List(List())
      else
        for {
          queens <- placeQueens(k - 1)
          column <- 1 to n
          queen = (k, column)
          if isSafe(queen, queens)
        } yield queen :: queens
    // 関数呼び出し
    placeQueens(n)
  }
  
  def isSafe(queen: (Int, Int), queens: List[(Int, Int)]) =
    queens forall (q => !inCheck(queen, q))
  def inCheck(q1: (Int, Int), q2: (Int, Int)) =
    q1._1 == q2._1 || // 同じ段
    q1._2 == q2._2 || // 同じ行
      (q1._1 - q2._1).abs == (q1._2 - q2._2).abs // 対角線上
```
