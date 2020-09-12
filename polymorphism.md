# polymorphism

抽象クラスElement型の変数が、実装クラス ArrayElement型のオブジェクトを参照できる

```scala
  abstract class Element {
    def contents: Array[String]
    def height: Int = contents.length
    def width: Int = if (height == 0) 0 else contents(0).length
  }

  // 抽象クラスを実装
  class ArrayElement(conts: Array[String]) extends Element {
    def contents: Array[String] = conts
  }

  // polymorphism
　val e: Element = new ArrayElement(Array("hello"))

```


- 別例
```scala

  abstract class Element {
    def contents: Array[String]
    def height: Int = contents.length
    def width: Int = if (height == 0) 0 else contents(0).length
  }

  class UniformElement(
                      ch: Char,
                      override val width: Int,
                      override val height: Int
                      ) extends Element {
    private val line = ch.toString * width
    def contents = Array.fill(height)(line)
  }

```
