# for反復処理

## 改善前のforネストループ
- if fileでファイルを取得し、その中でlineをネストでループし、終わったら次のfile取得
- trimが毎回呼ばれることの改善案
```scala
object ScalaPlayground extends App {
  val filesHere = (new java.io.File(".")).listFiles
  for (file <- filesHere)
    println(file)

  def fileLines(file: java.io.File) =
    scala.io.Source.fromFile(file).getLines().toList

  def grep(pattern: String) =
    for(
      file <- filesHere
      if file.getName.endsWith(".iml");
      line <- fileLines(file)
      if line.trim.matches(pattern)
    ) println(file + ": " + line.trim)

  grep(".*src.*")
}

```

## 束縛変数を使った改善後
- trimが毎回呼ばれることの改善案 => line.trimを毎回計算するのではなく、束縛変数で結果を初期化することで計算を1度だけに制限している
- p.137 束縛変数・・・val省略可能、forの中だけで使われる
- https://kotsubu-chan.hatenadiary.org/entries/2000/07/01

```scala
object ScalaPlayground extends App {
  val filesHere = (new java.io.File(".")).listFiles
  for (file <- filesHere)
    println(file)

  def fileLines(file: java.io.File) =
    scala.io.Source.fromFile(file).getLines().toList

  def grep(pattern: String) =
    // 括弧ではなく中括弧
    for {
      file <- filesHere
      if file.getName.endsWith(".iml");
      line <- fileLines(file)
      // 束縛変数
      trimmed = line.trim
      if trimmed.matches(pattern)
    } println(file + ": " + trimmed)

  grep(".*src.*")
}

```
