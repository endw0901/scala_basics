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
