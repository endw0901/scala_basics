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
