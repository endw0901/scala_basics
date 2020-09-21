# for式の変換

- forクエリ：https://github.com/endw0901/scala_basics/blob/master/for_query.md

## for式をmap/flatMapに置き換え
- map/flatMap: https://github.com/endw0901/scala_basics/blob/master/map_flatmap.md

### 1.for⇔map
```scala
  // 1.for⇔map
  for (x <- expr1) yield expr2

  expr1.map(x => expr2)
```

### 2.for⇔mapとフィルター
```scala
  // 2.for⇔mapとフィルター
  for (x <- expr1 if expr2) yield expr3
  
  for (x <- expr1 withFilter (x => expr2)) yield expr3
  
  expr1 withFilter (x => expr2) map (x => expr3)
```

### 3.2つのジェネレーター
```scala
  // 3.2つのジェネレーター
  for (x <- expr1; y <- expr2; seq) yield expr3
  
  expr1.flatMap(x => for (y <- expr2; seq) yield expr3)
```

### 4.forクエリ
```scala
// 4.forクエリ
  for (b1 <- books; b2 <- books if b1 != b2;
       a1 <- b1.authors; a2 <- b2.authors if a1 == a2)
    yield a1
  
  books flatMap (b1 =>
    books withFilter (b2 => b1 != b2) flatMap (b2 =>
    b1.authors flatMap (a1 =>
      b2.authors withFilter (a2 => a1 == a2) map (a2 =>
        a1))))
```

### 5.パターン

```scala
  // 5.パターン
  for ((x1, .., xn) <- expr1) yield expr2
  
  expr1.map { case (x1, ..., xn) => expr2}
  
  // 複雑なパターン
  for (pat <- expr1) yield expr2
  
  expr1 withFilter {
    case pat => true // パターンマッチしたものだけマッチング
    case _ => false
  } map {
    case pat => expr2
  }
```

## for => foreach変換

```scala
  // 1.例
  for (x <- expr1) body
  
  expr1 foreach (x => body)
```

- フィルター付き
```scala
  // 2.例 フィルターつき
  for (x <- expr1; if expr2; y <- expr3) body
  
  expr1 withFilter (x => expr2) foreach (x =>
    expr3 foreach (y => body))
  
  // 3.実例
  var sum = 0
  for (xs <- xss; x <- xs) sum += x
  
  var sum = 0
  xss foreach (xs =>
    xs foreach (x =>
      sum += x))
```


## map,flatMap, filterをfor式に変換
- p.450
```scala
  object Demo {
    def map[A, B](xs: List[A], f: A => B ): List[B] =
      for (x <- xs) yield f(x)
    def flatMap[A, B](xs: List[A], f: A => List[B]): List[B] =
      for (x <- xs; y <- f(x)) yield y
    def filter[A](xs: List[A], p: A => Boolean): List[A] =
      for (x <- xs if p(x)) yield x
  }
```
