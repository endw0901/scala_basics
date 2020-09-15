# 型消去
- 型引数の情報は保持しない
- Intかどうかチェックしてるのに、Stringでもtrueになる
```scala
def isIntMap(x:Any) = x match {
  case m: Map[Int, Int] => true
  case _ => false
}

// これもtrueとなる
isIntIntMap(Map("abc" -> "abc"))
```

## リストは型消去の例外
- Stringかどうかチェック→Listの要素がIntなのでfalseと正常に判定される
```scala
 def isStringArray(x:Any) = x match {
  case a: Array[String] => "yes"
  case _ => "no"
 }
 
 val ai = Array(1,2,3)
 // false ※型消去されない
 isStringArray(ai)
```
