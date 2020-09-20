# varのセッター
- p.344 
- p.114 toStringメソッドのオーバーライド
```scala
  // サンプル
  class Thermometer {
    // 初期化　※ var celsious: Floatだけだと抽象変数の宣言のみ
    var celsius: Float = _
    def fahrenheit = celsius * 9 / 5 + 32
    // セッター
    def fahrenheit_= (f: Float) = {
      celsius = (f - 32) * 5 / 9
    }
    override def toString = fahrenheit + "F/" + celsius + "C"
  }

  //　使い方
  val t = new Thermometer
  
  t.celsius = 100
  // 212.0F/100.0C
  println(t)

  t.fahrenheit = -42
  // -42.0F/-41.11111C
println(t)
```

- 別サンプル
```scala
 // var セッター ゲッター
  class Time {
    private[this] var h = 12
    private[this] var m = 0
    def hour: Int = h
    // reassignable variablesの暗黙のセッター 「hour_=」
    def hour_=(x: Int) = { h = x }
    def minute: Int = m
    def minute_=(x: Int) = { m = x }
  }
```

## 抽象クラスも
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
