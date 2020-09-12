# ローンパターン
-p.179

- PrintWriterをop関数に貸し出し（loan)、op関数がクローズする

```scala
  def withPrintWriter(file: File, op: PrintWriter => Unit) = {
    val writer = new PrintWriter(file)
    try{
      op(writer)
    } finally {
      writer.close()
    }
  }
  
  withPrintWriter(
    new File("data.txt"),
    writer => writer.println(new java.util.Date)
  )
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
- ※括弧の中に関数コードを渡さない方法については、function_by_name_parameter参照
