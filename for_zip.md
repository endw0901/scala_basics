# forループでzipで文字列連結
- for https://github.com/endw0901/scala_basics/blob/master/for.md
```scala
object ScalaPlayground extends App {
  val filesHere = (new java.io.File(".")).listFiles
  for (file <- filesHere)
    println(file)
}
```

- forループで文字配列を連結(zip未使用)
```scala
  abstract class Element {
    def contents: Array[String]
    def width: Int =
      if (height == 0) 0 else contents(0).length
    def height: Int = contents.length
    def above(that: Element): Element =
      new ArrayElement(this.contents ++ that.contents)

    def beside(that: Element): Element = {
      val contents = new Array[String](this.contents.length)
      for (i <- 0 until this.contents.length)
        contents(i) = this.contents(i) + that.contents(i)
      new ArrayElement(contents)
    }
  }
```

- 改善例

```scala
  abstract class Element {
    def contents: Array[String]
    def width: Int =
      if (height == 0) 0 else contents(0).length
    def height: Int = contents.length
    def above(that: Element): Element =
      new ArrayElement(this.contents ++ that.contents)

    def beside(that: Element): Element =
      new ArrayElement(
        for (
          (line1, line2) <- this.contents zip that contents
        ) yield line1 + line2                
      )
  }
```
