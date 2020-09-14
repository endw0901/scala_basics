# シングルトンオブジェクト_コンパニオン

- object で宣言されたクラスからは、ひとつのインスタンスしか生成することができません。これを シングルトンオブジェクト といいます。
- https://qiita.com/kingzer0314/items/a6b82034f760f024fdfa
```scala
import scala.collection.mutable

// シングルトンオブジェクト＝クラスが同名のとき => コンパニオンクラス（お互いの非公開メンバーアクセス可能）
object ChecksumAccumulator {
　// cacheはmutableなMap
  private val cache = mutable.Map.empty[String, Int]
  
  def calculate(s:String): Int =
    // cacheが引数sをすでに持っているかどうかを調べる
    if (cache.contains(s))
      cache(s)
     else {
      // ChecksumAccumulatorクラスのインスタンスで初期化
      val acc = new ChecksumAccumulator
      for (c <- s)
      　// 引数sを1文字ずつバイト変換しacc -> cs -> cache
        acc.add(c.toByte)
       val cs = acc.checksum()
       // 引数sのキーと整数のチェックサムを対応させ、キーと値の対をcacheマップに追加
       cache += (s -> cs)
       // チェックサムがこのメソッドの結果となるよう(return省略なので最後がreturn)csと記載
       cs
     }
}

```

## コンパニオンオブジェクト

```scala
  class Rocket {
    import Rocket.fuel
    // Rocketオブジェクトからアクセス可能
    private def canGoHomeAgain = fuel > 20
  }
  // Rocketクラスのコンパニオン（同名のシングルトンオブジェクト(=objectで定義されるもの))
  object Rocket {
    // Rocketクラスからアクセス可能
    private def fuel = 10
    def chooseStrategy(rocket: Rocket) = {
      if (rocket.canGoHomeAgain)
        goHome()
      else
        pickAStar()
    }
    def goHome() = {}
    def pickAStar() = {}
  }
```
