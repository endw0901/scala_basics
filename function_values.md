# 値としての関数(function values)
- 関数値がオブジェクトとして存在する
- 関数を変数に格納できる

```scala
var increase = (x: Int) => x + 1
increase(10)
// 結果・・・Int = 11
```

- 複数の関数文を変数に格納する中括弧
```scala
increase = (x: Int) => {
  println("we")
  Println("do")
  x + 1
}

increase(10)
// 結果
// we
// do
// 11
```
