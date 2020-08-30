# 副作用もvarもない関数型コーディング

- p.73

## 1.varを取り除く

- 関数型的なコーディング
```
// 変数初期化もカウントアップも不要なので簡易な記法になる
def printArgs(args: Array[String]): Unit = {
  for (arg <- args)
  println(arg)
}

// foreachでさらに簡易な記法へ
def printArgs(args: Array[String]): Unit = {
  args.foreach(println)
}
```

## 2.副作用を取り除く
- Unit型を返す = 意味のある値を返さない関数である（副作用をもつ
- 副作用を持たない⇒別の作用を起こす必要がある

```
// この関数自体は何も出力しない。変数 + 改行区切り文字を返すのみ(副作用無し)⇒callすることで標準出力へ
def formatArgs(args: Array[String]) = args.mkString("\n")

// call
println(formatArgs(args))
```


## 参考

### foreachの省略形について
```
// 1.型明示
args.foreach((arg:String) => println(arg))

// 2.型省略
args.foreach(arg => println(arg))

// 3.省略形
args.foreach(println)

```


### 大変なwhileの例

```
// while
def printArgs(args: Array[String]): Unit = {
  var i = 0
  while ( i < args.length) {
    println(arg(i))
    i += 1
  }
 }

```
