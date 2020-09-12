# 名前渡しパラメータ

- 括弧の中に関数コードを渡さないようにする

## 関数を引数に含むパターン
- {}は複数の引数を取れない ⇔ （)は可能
- curryingで関数箇所を分けて、一つにしてから{}内に関数を収める

```scala
  def withPrintWriter(file: File)(op: PrintWriter => Unit) = {
    val writer = new PrintWriter(file)
    try{
      op(writer)
    } finally {
      writer.close()
    }
  }

  val file = new File("date.txt")
  withPrintWriter(file) { writer =>
    writer.println(new java.util.Date)
  }
 
```

## 関数を引数に含まないパターン
- 関数が使いづらい
```scala
  var assertionEnabled = true
  def myAssert(predicate: () => Boolean) =
    if(assertionEnabled && !predicate())
      throw new AssertionError

  myAssert(() => 5 > 3 
```

## ()=>ではなく =>で関数型を定義
- 関数型 => を引き渡すため、引き渡す前には評価されない（副作用無し）
- Boolean形の引き渡しには副作用が発生（引き渡す前に評価されてしまう)

```scala
  var assertionEnabled = true

  def byNameAssert(predicate: => Boolean) =
    if (assertionEnabled && !predicate)
      throw new AssertionError
  
  // 関数型を引き渡すので、assertionEnabledがfalseなら実行されない（副作用無し)
  byNameAssert(5 > 3)
```

```scala
  var assertionEnabled = true

  def boolAssert(predicate: Boolean) =
    if(assertionEnabled && !predicate)
      throw new AssertionError

  // 関数は引き渡しの前に評価され(副作用あり)、bool型を引き渡す
  // assertionEnabledがfalseでも関数が実行されるという副作用あり
  boolAssert( 5 > 3)
```
