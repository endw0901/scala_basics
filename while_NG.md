# whileループ
- whileループは使わない ⇒ foreach, for

## varを取り除く関数型のメリット
- 大変なwhileの例
```scala
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
```scala
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

## whileを関数型プログラムに改善する例
- 大変なwhileの例(varを使う)
```scala
object ScalaPlayground extends App {
  def gcdLoop(x: Long, y: Long): Long = {
    var a = x
    var b = y
    while ( a != 0) {
      val temp = a
      a = b % a
      b = temp
    }
    b
  }

  println(gcdLoop(66,42))
}

```
- 関数型プログラミングの例(変数は使わない、再帰)
```scala
object ScalaPlayground extends App {
  def gcd(x: Long, y: Long): Long =
    if (y == 0) x else gcd(y, x % y)

  println(gcd(66,42))
}
```
