# クロージャー
- p.162, p.174

- 関数を階層化して共通化
- プレイスホルダー(_)を使って省略
- クロージャーを使ってさらに省略

## 処理の重複をクロージャーで除く
- 1.file / queryに重複がある
```scala 
object ScalaPlayground extends App {
  object FileMatcher {
    private def filesHere = (new java.io.File(".")).listFiles

    def filesEnding(query: String) =
      for (file <- filesHere; if file.getName.endsWith(query))
        yield file

    def filesContaining(query: String) =
      for (file <- filesHere; if file.getName.contains(query))
        yield file

    def filesRegex(query: String) =
      for (file <- filesHere; if file.getName.matches(query))
        yield file
  }
}
```

- _ _をmatcherのstring, stringとして渡してfileMatching箇所は共通化する。queryを渡す形で共通化
```scala 
object ScalaPlayground extends App {
  object FileMatcher {
    private def filesHere = (new java.io.File(".")).listFiles

    // 処理に重複のある上記を統合して最適化
    // メソッドを呼び出してくれる関数値を引き渡す（直接メソッド引き渡しはNG)
    def filesMatching(query: String,
                      matcher: (String, String) => Boolean) = {
      for (file <- filesHere; if matcher(file.getName, query))
        yield file
    }

    def filesEnding(query: String) =
      filesMatching(query, _.endsWith(_))
    def filesContaining(query: String) =
      filesMatching(query, _.contains(_))
    def filesRegex(query: String) =
      filesMatching(query, _.matches(_))

  }
}
```

- 引き渡すqueryは分かり切っているので省略（＝Closureを利用）

```scala
object ScalaPlayground extends App {
  object FileMatcher {
    private def filesHere = (new java.io.File(".")).listFiles

    // _をstringとして受けて、引き渡されたqueryとマッチする（queryは分かり切ってるので省略)
    private def filesMatching(matcher: String => Boolean) = {
      for (file <- filesHere; if matcher(file.getName))
        yield file
    }

    // queryは分かっている
    def filesEnding(query: String) =
      filesMatching(_.endsWith(query))
    def filesContaining(query: String) =
      filesMatching(_.contains(query))
    def filesRegex(query: String) =
      filesMatching(_.matches(query))

  }
}

```
