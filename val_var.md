# valとvar
- valはfinal変数に似ている(変更不可)
- varは非finalに似ている（代入可能)

## scalaプログラミングの基本ルール
- varとwhileはなるべく避ける

## valのメリット
- varではなくvalをつかうことで、変数が変わっていないかチェックする手間を省ける

## 抽象メンバー
- https://github.com/endw0901/scala_basics/blob/master/abstract_members.md

## 暗黙のゲッター/セッター

```scala
  trait AbstractTime {
    var hour: Int
    var minute: Int
  }
  
  // 再代入可能なフィールドは作られない
  // クラス(抽象含む)のメンバーとしてvarを宣言すると、自動的に暗黙のゲッター・セッターが作られる
  trait AbstractTime {
    def hour: Int        // getter
    def hour_=(x: Int)   // setter
    
    def minute: Int      // getter
    def minute_=(x: Int) //setter
  }
```
