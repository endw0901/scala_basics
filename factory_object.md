# ファクトリーオブジェクト
- p.202

## newをファクトリーオブジェクトに改善
- newを使う例
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
    override def toString = contents mkString "\n"
  }
```

- ファクトリーメソッドを持つファクトリーオブジェクト
- オブジェクト生成を一元管理できる（多重定義）
- コードを破壊せずに実装を書き換えれる余地が増える
```scala
  // ファクトリーオブジェクト
  object Element {
    def elem(contents: Array[String]): Element =
      new ArrayElement(contents)
    def elem(chr: Char, width: Int, height: Int): Element =
      new UniformElement(chr, width, height)
    def elem(line: String): Element =
      new LineElement(line)
  }

  // ファクトリーオブジェクトを使ったオブジェクト生成(newの箇所を入れ替え)
  import Element.elem
  abstract class Element {
    def contents: Array[String]
    // height():Intとせず、括弧無し empty-paren method
    // val height = contents.lengthとフィールドにしても同じだが、フィールドは容量を食うので
    // 副作用無しの場合はvalよりも括弧無しのメソッドが推奨される(副作用アリで省略できない例：println()
    def width: Int =
      if (height == 0) 0 else contents(0).length
    def height: Int = contents.length
    def above(that: Element): Element =
      elem(this.contents ++ that.contents)
    def beside(that: Element): Element =
      elem(
        for (
          (line1, line2) <- this.contents zip that contents
        ) yield line1 + line2
      )

    override def toString = contents mkString "\n"
  }
```


## newをファクトリーオブジェクトに改善してサブクラス群を非公開にできる
- newを使う例
- サブクラスが公開されている
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
    override def toString = contents mkString "\n"
  }

  // サブクラス
  class ArrayElement(conts: Array[String]) extends Element {
    def contents: Array[String] = conts
  }

  // サブクラス
  class LineElement(s: String) extends ArrayElement(Array(s)) {
    override def width = s.length
    override def height = 1
  }

  // サブクラス　　
  class UniformElement(
                        ch: Char,
                        override val width: Int,
                        override val height: Int
                      ) extends Element {
    private val line = ch.toString * width
    def contents = Array.fill(height)(line)
  }

```

- ファクトリーオブジェクトを使い、サブクラスを非公開とする
- クライアントからサブクラスを直接使う必要がなくなったため

```scala
object ScalaPlayground extends App {

  object Element {

    private class ArrayElement(
      val contents: Array[String]
                              ) extends Element

    private class LineElement(s: String) extends Element {
      val contents = Array(s)
      override def width = s.length
      override def height = 1
    }

    private class UniformElement(
                          ch: Char,
                          override val width: Int,
                          override val height: Int
                        ) extends Element {
      private val line = ch.toString * width
      def contents = Array.fill(height)(line)
    }


    // ファクトリーメソッド（多重定義)
    def elem(contents: Array[String]): Element =
      new ArrayElement(contents)
    def elem(chr: Char, width: Int, height: Int): Element =
      new UniformElement(chr, width, height)
    def elem(line: String): Element =
      new LineElement(line)
  }

  import Element.elem
  abstract class Element {
    def contents: Array[String]
    // height():Intとせず、括弧無し empty-paren method
    // val height = contents.lengthとフィールドにしても同じだが、フィールドは容量を食うので
    // 副作用無しの場合はvalよりも括弧無しのメソッドが推奨される(副作用アリで省略できない例：println()
    def width: Int =
      if (height == 0) 0 else contents(0).length
    def height: Int = contents.length
    def above(that: Element): Element =
      elem(this.contents ++ that.contents)
    def beside(that: Element): Element =
      elem(
        for (
          (line1, line2) <- this.contents zip that.contents
        ) yield line1 + line2
      )

    override def toString = contents mkString "\n"
  }


}
```
