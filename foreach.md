# foreach
p.56

```
// 1.型明示
args.foreach((arg:String) => println(arg))

// 2.型省略
args.foreach(arg => println(arg))

// 3.省略形
args.foreach(println)

//
for (arg <- args)
    println(arg)

```

## varを取り除く関数型のメリット
- 大変なwhileの例
```
// while
def printArgs(args: Array[String]): Unit = {
  var i = 0
  while ( i < args.length) {
    println(arg(i))
    i += 1
  }
 }

```

- 関数型的なコーディング
```
// 変数初期化もカウントアップも不要なので簡易な記法になる
def printArgs(args: Array[String]): Unit = {
  for (arg <- args)
  println(arg)
}

// foreachでさらに簡易な記法へ
def printArgs(args: Array[String]): Unit = {
  args.foreach(println)
}
```


## Listからforeach
- p.156
```scala
val someNumbers = List(-11, 10, 0, 5, 10)
sumeNumbers.foreach((x: Int) => println(x))
```


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
