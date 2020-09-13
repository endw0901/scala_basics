# 独自クラス

```scala
class Dollars(val amount: Int) extends AnyVal {
  override def toString() = "$" + amount
}

// 結果：$100　※Dollars型
val money = new Dollars(100)

// 結果：100  ※Int型
money.amount
```
