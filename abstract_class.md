# 抽象クラス

```scala
// 実装(定義)されていないメンバーを持つ(かもしれない)とき = abstract class
  abstract class Element {
    // メンバーを宣言するが定義はしていない
    def contents: Array[String]
  }
 
  // abstractクラスのインスタンス作成は不可
  new Element 
```  

## サブクラスの引数とスーパークラスの引数タイプが違う時

```scala
  abstract class Element {
    def contents: Array[String]
    def height: Int = contents.length
    def width: Int = if (height == 0) 0 else contents(0).length
  }

  // 抽象クラスを実装したスーパークラス
  class ArrayElement(conts: Array[String]) extends Element {
    def contents: Array[String] = conts
  }

  // サブクラス
  // 基本コンストラクトにarrayを渡す必要がある。サブクラスはStringのとき、arrayの引数で渡せばいい
  class LineElement(s: String) extends ArrayElement(Array(s)) {
    override def width = s.length
    override def height = 1
  }
```
  
## ファクトリーオブジェクトを使い、サブクラスを非公開とする例
- https://github.com/endw0901/scala_basics/blob/master/factory_object.md
