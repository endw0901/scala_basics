# 非公開クラス
- 非公開コンストラクターの例：https://github.com/endw0901/scala_basics/blob/master/function_enqueu.md

### 非公開コンストラクター
- クラス自体の内部とコンパニオンオブジェクトだけがアクセスできる
- 外部からはアクセスできない
```scala
// エラーとなる
new Queue(List(1,2), List(3))
```

## クラスの初期化と表現を隠ぺいする非公開クラス
- 個別のコンストラクターやメソッドを隠すのではなく、クラス全体を非公開にしてトレイトだけ公開インターフェイスとして提供
- クラスが非公開でも、コンパニオンオブジェクトを同じソースファイルに入れて、ファクトリーメソッドで新しいオブジェクトを作れる
- 非公開クラスは、コンパニオンオブジェクトの非公開内部クラスとする

```scala
// 公開インターフェイスとしてのトレイト
 trait Queue[T] {
   def head: T
   def tail: Queue[T]
   def enqueue(x: T): Queue[T]
 }

  // コンパニオンオブジェクト
  object Queue {
    // グローバルにアクセスできるファクトリーメソッド
    // 連続型パラメータT*を受けてtoListへ
    def apply[T](xs: T*): Queue[T] =
      new QueueImpl[T](xs.toList, Nil)
    private class QueueImpl[T](
                              private val leading: List[T], // 1,2,3
                              private val trailing: List[T] // 6,5,4 => reverse 4,5,6
                              ) extends Queue[T] {
      // ミラーリング：leadingが空なら、trailing全体を逆転してleadingにコピーする
      def mirror =
        if (leading.isEmpty)
          new QueueImpl(trailing.reverse, Nil)
        else
          this
      // leading:1,2,3の1 先頭はすぐ取り出せる
      def head: T = mirror.leading.head
      // leading 1,2,3の2,3 + trailing 6,5,4
      def tail: QueueImpl[T] = {
        val q = mirror
        new QueueImpl(q.leading.tail, q.trailing)
      }
      // leading:1,2,3  trailing 6,5,4の先頭に追加するのですぐ追加できる（行列の末尾に)
      def enqueue(x: T) =
        new QueueImpl(leading, x :: trailing)
    }
  }
```
