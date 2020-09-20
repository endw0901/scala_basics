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

- 連続型パラメータ： https://github.com/endw0901/scala_basics/blob/master/function_multiple_args.md

## 最適化された関数型待ち行列
- 変位指定 https://github.com/endw0901/scala_basics/blob/master/trait_type_constructor.md
- headを連続してcallするとmirrorがtrailingをleadingに繰り返しコピーする問題を改善
- Queue[+T]は共変
```scala
  // 変位指定(variant)：共変covariant 
  class Queue[+T] private (
                          private[this] var leading: List[T], // private[this]を外すとエラーになる(varは変位指定の規則違反だが非公開ならok)
                          private[this] var trailing: List[T]
                          ){
    private def mirror() =
      // 初回だけ
      if (leading.isEmpty) {
        while (!trailing.isEmpty) {
          leading = trailing.head :: leading
          trailing = trailing.tail
        }
      }
    def head: T = {
      // 連続でheadをcallしても、既にleadingに要素があれば毎回trailingからcopyは起こらない
      mirror()
      leading.head
    }
    def tail: Queue[T] = {
      mirror()
      new Queue(leading.tail, trailing)
    }
    // UはサブTのスーパー型Uでなければならない　※下限境界 lower bounds
    def enqueue[U >: T](x: U) =
      // 初回はleading(空), x :: trailing(空)で、leadingにはxの先頭、trailingには残りがmirrorでセットされる
      new Queue[U](leading, x :: trailing)
  }
```

- UはサブTのスーパー型Uでなければならない　※下限境界 lower bounds
- Queue[+T]共変なので、スーパーUのサブ型として使える Queue[AnyRef]はQueue[Int]やQueue[String]として扱える
