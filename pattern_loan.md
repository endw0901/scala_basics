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
