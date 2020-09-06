# for反復処理

## generator( <- )
- ディレクトリ内のファイルリスト表示
- java.io.FileオブジェクトのlistFilesメソッド
```scala
object ScalaPlayground extends App {
  val filesHere = (new java.io.File(".")).listFiles
  for (file <- filesHere)
    println(file)
}
```

- if付き 
```scala
object ScalaPlayground extends App {
  val filesHere = (new java.io.File(".")).listFiles
  for (file <- filesHere)
    if (file.getName.endsWith(".scala"))
    println(file)
}
```

## Range型(x to x)

- x to y
```scala
for (i <- 1 to 4)
  println("iteration " + i)
```
- x until y
```scala
for (i <- 1 until 4)
  println("iteration " + i)
```

## 入れ子
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

```

## NG・使わない
- generator形式でcollectionを直接反復処理できるため、わざわざlengthは使わない
```scala
for (i < 0 to filesHere.length -1)
  println(filesHere(i))
```
