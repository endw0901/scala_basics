# 括弧
- p.180

- curly braces{}は引数を1つしか取れない
- parentheses()は引数を複数取れる

```scala
val g = "abcde"

// NG
g.substring{2, 4}

// OK
g.substring(2, 4)
```

- ※substring(2, 4)は、頭の2文字を切り捨ててcde、5文字目以降のeを切り捨てて残りのcdが返る
- https://scalapedia.com/articles/53/substring%E3%81%A7String%E3%82%92%E5%88%87%E3%82%8A%E5%8F%96%E3%82%8A%E3%80%81%E9%83%A8%E5%88%86%E6%96%87%E5%AD%97%E5%88%97%E3%82%92%E6%8A%BD%E5%87%BA%E3%81%99%E3%82%8B%E6%96%B9%E6%B3%95
