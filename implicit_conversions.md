# 暗黙の型変換
- p.413
- エラーになったときに変換（そのままで問題なければ暗黙の型変換はしない)
- 使われるのは下記3ケース


## 1.要求された型への暗黙の型変換

```scala
  // 精度が失われるのでDouble to Intはエラー
  // val i: Int = 3.5
  
  implicit def doubleToInt(x: Double) = x.toInt
  val i: Int = 3.5 // i: Int = 3 変換できる(エラーになったらimplicit conversionsを試す)
```

## 2.レシーバーの変換：暗黙のクラス
- 3 x で、intにはxのメソッドがない（レシーバーにメソッドがないとき) ⇒ implicitを探して def xを見つける
- 引数 width 関数x height ⇒ Rectangle(3,4)を生成
```scala
  case class Rectangle(width: Int, height: Int)
  
  implicit class RectangleMaker(width: Int) {
    def x(height: Int) = Rectangle(width, height)
  }
  
  val myRectangle = 3 x 4
```

## 暗黙のパラメーター
- p. 418
