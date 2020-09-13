# クラスへの積み重ね可能な変更(トレイトの用途）
- 用途①リッチインターフェイス化
- 用途②クラスへの積み重ね可能な変更

## 例
```scala
object ScalaPlayground extends App {

  // 抽象クラス
  abstract class IntQueue {
    def get(): Int
    def put(x: Int)
  }

  import scala.collection.mutable.ArrayBuffer
  // 実装
  class BasicIntQueue extends IntQueue {
    private val buf = new ArrayBuffer[Int]
    def get() = buf.remove(0)
    def put(x: Int) = { buf += x}
  }

  // 変更トレイト
  // extends指定 = IntQueure拡張クラスだけミックスインできるということ
  trait Incrementing extends IntQueue {
    abstract override def put(x: Int) = { super.put(x + 1) }
  }

  trait Filtering extends IntQueue {
    abstract override def put(x: Int) = {
      if (x >= 0) super.put(x)
    }
  }

  // ミックスイン(with)
  // withは後ろから適用される
  val queue = (new BasicIntQueue
    with Incrementing with Filtering)

  // -1はフィルターで除かれて、0,1は+1されて1,2でputされる
  queue.put(-1)
  queue.put(0);
  queue.put(1);

  println(queue.get())
  println(queue.get())

}
```
