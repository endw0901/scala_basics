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

## NG・使わない
- generator形式でcollectionを直接反復処理できるため、わざわざlengthは使わない
```scala
for (i < 0 to filesHere.length -1)
  println(filesHere(i))
```
