# 型コンストラクター
- 非公開クラスを持つコンパニオンオブジェクトでファクトリーメソッドを提供するtraitインターフェイスの例
- https://github.com/endw0901/scala_basics/blob/master/class_private.md

## ジェネリックトレイト
- QueueトレイトはQueue型の変数を作れないが、ジェネリックとしてQueue[Int]やQueue[String]など型パラメータを指定して型を作れる
- 型コンストラクター type constructor

```scala
def doesCompile(q: Queue[AnyRef]) = {}
```

## ジェネリックのサブ型(
- デフォルトでは非変nonvariantで厳格rigid

- 共変のサブ型 => Queue[String]をQueue[AnyRef]のサブ型とみなす
```scala
trait Queue[+T] {......}
```

### 型パラメータの変位指定(variant)：共変covariant、反変contravariant、非変nonvariant
- 変位指定アノテーション：+ -

```scala
// 非変nonvariant ※デフォルト状態
trait Queue[T] {....}

// 共変covariant
trait Queue[+T] {......}

// 反変contravariant
trait Queue[-T] {....}
```
