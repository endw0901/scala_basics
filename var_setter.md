# varのセッター

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

  //
  val t = new Thermometer
  t.celsius = 100
  println(t)

  t.fahrenheit = -42
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
