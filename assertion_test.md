# アサーションテスト

- 引数のbooleanがfalseならerrorを返す。true(エラーではない)かどうかをチェックするテスト


## 例
- varも副作用も無し、関数型プログラミング

```
// この関数自体は何も出力しない。変数 + 改行区切り文字を返すのみ(副作用無し)⇒callすることで標準出力へ
def formatArgs(args: Array[String]) = args.mkString("\n")

// assertionテスト
val res = formatArgs(Array("a","b","c"))
assert(res == "a\nb\nc")
```

- this1.width == that1.widthかどうかのテスト
```scala
  def above(that: Element): Element = {
    val this1 = this widen that.width
    val that1 = that widen this.width
    assert(this1.width == that1.width)
    elem(this1.contents ++ that1.contents)
  }
```

## ensuring

```scala
 private def widen(w: Int): Element =
   if (w <= width)
     this
   else {
     val left = elem(' ', (w - width) / 2, height)
     val right = elem(' ', w - width - left.width, height)
     left beside this beside right
   // wは入力引数、_は結果のElementのプレースホルダー
   // w > widthの場合のelse処理の結果が w <= widthであることを保証するテスト
   //  満たさないときはAssertionErrorを投げる
   } ensuring (w <= _.width)
```
