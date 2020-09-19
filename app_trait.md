# Appトレイト
- http://takafumi-s.hatenablog.com/entry/2015/08/01/115927

- 通常Scalaアプリケーションはシングルトンオブジェクトのdef mainが実行される。

```scala
object Foo {
  def main(args: Array[string]):Unit = {
    // 処理
  }
}
```

- しかし、scala.Application(scala.App)トレイトを使うことで、def mainに入るコードを中括弧{}の間に書ける。
- ただしこの場合は、引数argsを使うことができない。
- ※ scala2.9以降では、Appトレイトが推奨されている。
```scala
object Bar extends App {
  // 処理
}
```

