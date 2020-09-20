# 抽象メンバー

```scala
  // 4種類の抽象メンバー
  trait Abstract {
    type T
    def transform(x: T): T
    val initial: T
    var current: T
  }

  // 具象実装
  class Concrete extends Abstract {
    type T = String
    def transform(x: String) = x + x
    val initial: "hi"
    var current = initial
  }
```

## defとvalの実装
```scala
  abstract class Fruit {
    val v: String
    def m: String
  }

  abstract class Apple extends Fruit {
    def v: String // error valをdefでoverrideは不可
    val m: String // ok    defをvalでoverride
  }
```

### 抽象valとvar
- https://github.com/endw0901/scala_basics/blob/master/val_var.md
