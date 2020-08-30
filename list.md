# リスト
- リスト = クラス
- クラスインスタンス生成 = クラスオブジェクト生成

- 配列：mutable ⇔ リスト・タプル：immutable
- リスト：同じ型 ⇔ タプル：異なる型を持てる


## リストのメソッド
- https://www.scala-lang.org/api/2.12.3/scala/collection/immutable/List.html

### 例
```
// 値＋リスト結合
val twoThree = List(2,3)
val oneThree = 1 :: threeFour

// 値＋リスト結合
val oneTwo = List(1,2)
val threeFour = List(3,4)
val oneFour = oneTwo ::: threeFour

// 一部出力
listdata(2)

// 最初の2つを削除
listdata.drop(2)

// その他
filter
map

// カンマ区切り＋空白で区切る
listdata.mkString(", ")

```

## appendとprepend
- p.66
- appendはデータ保持の問題で遅い。代わりに、prepend(先頭挿入) + reverseで逆転して最後のを最初に持ってくる
