# 関数型待ち行列
- p.364
- 先頭に追加が速いのでそれをするには

- やりたいイメージ

```scala
  // function_enqueue
  val q = Queue(1,2,3)
  val q1 = q enqueue 4
  // q1のみに追加される。qは変化なし
  println("q" + q)
  println("q1" + q1)
```

## 基本形

```scala
  // 関数型待ち行列の基本形
  class Queue[T](
    // 非公開コンストラクター
    private val leading: List[T], // 1,2,3
    private val trailing: List[T] // 6,5,4 => reverse 4,5,6
                ){
    // ミラーリング：leadingが空なら、trailing全体を逆転してleadingにコピーする
    private def mirror =
      if (leading.isEmpty)
        new Queue(trailing.reverse, Nil)
      else
        this
    // leading:1,2,3の1 先頭はすぐ取り出せる
    def head = mirror.leading.head
    // leading 1,2,3の2,3 + trailing 6,5,4
    def tail = {
      val q = mirror
      new Queue(q.leading.tail, q.trailing)
    }
    // leading:1,2,3  trailing 6,5,4の先頭に追加するのですぐ追加できる（行列の末尾に)
    def enqueue(x: T) =
      new Queue(leading, x :: trailing)
  }
```

### 非公開コンストラクター
- クラス自体の内部とコンパニオンオブジェクトだけがアクセスできる
- 外部からはアクセスできない
```scala
// エラーとなる
new Queue(List(1,2), List(3))
```

