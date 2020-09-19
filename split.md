# 文字列split
- タプル： https://github.com/endw0901/scala_basics/blob/master/tuple.md
- 文字列"The quick brownishorange fox"を半角スペースで分割
- 「"The quick brownishorange fox".split(" ")」

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
