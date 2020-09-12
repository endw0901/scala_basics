# パラメータ無しメソッド
- height():Intとせず、括弧無し empty-paren method
- val height = contents.lengthとフィールドにしても同じだが、フィールドは容量を食うので
- 副作用無しの場合はvalよりも括弧無しのメソッドが推奨される
- 副作用アリで省略できない例：println()

```scala
  abstract class Element {
    def contents: Array[String]
    def height: Int = contents.length
    def width: Int = if (height == 0) 0 else contents(0).length    
  }
```  
