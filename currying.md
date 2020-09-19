# カリー化
- p.177

- カリーではない場合
```scala
def plainOldSum(x: Int, y: Int) = x + y
println(plainOldSum(1,2)
```

- カリー
```scala
def plainOldSum(x: Int)(y: Int) = x + y
println(plainOldSum(1)(2)
```

## 関数を含む複数の引数を取るときの関数を{}に収めたいとき(分かりやすい記法）
- {}は複数の引数を取れない ⇔ （)は可能
- curryingで関数箇所を分けて、一つにしてから{}内に関数を収める

```scala
  def withPrintWriter(file: File)(op: PrintWriter => Unit) = {
    val writer = new PrintWriter(file)
    try{
      op(writer)
    } finally {
      writer.close()
    }
  }

  val file = new File("date.txt")
  withPrintWriter(file) { writer =>
    writer.println(new java.util.Date)
  }
 
```

## サンプル
- ソートマージ
- https://github.com/endw0901/scala_basics/blob/master/sort_merge.md
