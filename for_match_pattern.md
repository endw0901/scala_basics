# for式内のマッチパターン
- for内でマッチするパターンのみ取り出す
```scala
 // タプル「capitals」から、key-valueペアにマッチするもののみ取り出す
 for ((country, city) <- capitals)
  println("The capital of " + country + " ls " + city)

 // Listからパターンにマッチする要素のみ取り出す
 val results = List(Some("apple"), None, Some("orange"))
 // 結果apple orange
 for (Some(fruit) <- results) println(fruit)
 ```
