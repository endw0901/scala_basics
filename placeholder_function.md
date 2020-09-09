# プレースホルダー構文（省略形）
p.157

- ルール・・・同じ_は一度しか使えない（再利用不可)
- 引数１の_、引数２の_という複数使い分けは可能。同じものを複数回使うことはできない

## 例
- Listのうち、正の値のみ抽出
```scala
val someNumbers = List(-11, 10, 0, 5, 10)
sumeNumbers.filter((x: Int) => x > 0)
// 結果・・・List[Int] = List(5, 10)
```

- 省略形(推論による型付け：target typing)
```scala
val someNumbers = List(-11, 10, 0, 5, 10)
sumeNumbers.filter(x => x > 0)
// 結果・・・List[Int] = List(5, 10)
```

- さらに省略形_プレースホルダー構文
```scala
val someNumbers = List(-11, 10, 0, 5, 10)
sumeNumbers.filter(_ > 0)
// 結果・・・List[Int] = List(5, 10)
```

## 型が不明確なときの明記

```scala
// 順番に引数１＋引数２
var f = (_: Int) + (_: Int)

f(5, 10)
// 結果・・・Int = 15

```

## （）も省略するパターン

- 省略前
```scala
sumeNumbers.foreach(x => println(x))
```

- 省略形
```scala
sumeNumbers.foreach(println _)
```


- さらに省略形 p.160
- foreachが関数を要求しているので省略可能
```scala
sumeNumbers.foreach(println)
```
