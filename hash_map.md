# ハッシュテーブル
- p.487：ハッシュテーブルは、内部の配列に要素を格納する
- 要素の格納場所はハッシュコードで決まる
- 要素の追加は一定の時間

- mutable Setとmapのデフォルトはhash table

```scala
  val map = collection.mutable.HashMap.empty[Int, String]
  println(map) //HashMap()

  // map要素追加  
  map += (1 -> "make a web site")
  println(map) // HashMap(1 -> make a web site)

  map += (3 -> "profit!")
  println(map) //  HashMap(1 -> make a web site, 3 -> profit!)

  // key valueアクセス
  println(map(1)) //  make a web site
  
  // 存在チェック
  println(map contains 2) // false
```
