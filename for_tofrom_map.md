# for式の変換

- forクエリ：https://github.com/endw0901/scala_basics/blob/master/for_query.md

## for式をmap/flatMapに置き換え
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
