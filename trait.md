# trait
- p.68
- javaはinterfaceのimplement、scalaはtraitのextend or mixin

- traitは引数を取れない
- 複数のミックスインは extends XXX with AAAA with BBB {}とwithを複数回入れることで可能
- ミックスインしたメソッドを継承し、オーバーライドも可能

## メリット
- traitはjavaのinterfaceと違って既に定義されているのでリッチにしやすい
- javaのinterfaceはrich interfaceならたくさん実装しないといけないので大変
- https://github.com/endw0901/scala_basics/blob/master/trait_stackable_modifications.md

## traitを使う時
- p.233
- 振る舞いが再利用されそうなとき→trait
- 再利用されそうにないとき→具象クラス
- どっちかはっきりしない→とりあえずtrait

## traitのミックスイン例
- Componentではなくtraitに共通化(座標情報)
- traitをミックスインしたオブジェクトを作成し、traitのメソッドを呼び出す
```scala
object ScalaPlayground extends App {

  class Point(val x: Int, val y: Int)

  // Componentではなくtraitに共通化(座標情報)
  trait Rectangular {
    def topLeft: Point
    def bottomRight: Point
    def left = topLeft.x
    def right = bottomRight.x
    def width = right -left
  }

  abstract class Component extends Rectangular{

  }

  class Rectangle(val topLeft: Point, val bottomRight: Point)
   extends Rectangular{

  }

  val rect = new Rectangle(new Point(1, 1), new Point(10,10))

  println(rect.left)
  println(rect.right)
  println(rect.width)
}
```
