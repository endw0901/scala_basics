# タプル 
- タプル = クラス
- クラスインスタンス生成 = クラスオブジェクト生成

- 配列：mutable ⇔ リスト・タプル：immutable
- リスト：同じ型 ⇔ タプル：異なる型を持てる

## タプルにアクセス
- pari(0)ではない
- 0,1ではんく 1,2で
```scala
// タプルにアクセス _1

  val pair = (99, "tanaka")
  println(pair._1)
  println(pair._2)
```

### サンプル
```scala
  // 最も長い単語と添え字のタプル
  def longestWord(words: Array[String]) = {
    var word = words(0)
    var idx = 0
    for (i <- 1 until words.length)
      if (words(i).length > word.length) {
        word = words(i)
        idx = 1
      }

    // タプルをリターンする
    (word, idx)
  }

  val longest = longestWord("The quick brownishorange fox".split(" "))
  println("longest :" + longest)
  println(longest._1)
  println(longest._2)
```
