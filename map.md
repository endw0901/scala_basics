# Map
- list:重複ok ⇔ set：重複NG
- map:key-value

## mutableとimmutable
- mapはimmutable、importでmutable

### メモリ効率
- immutableは16-40バイト、参照追加のみなのでポインタ分のみ
- mutableは80バイト、追加するたびに16バイトずつ増える

## immutableなmap

```
// 引き渡す値で型が推論できるので型明示不要
val imMap = Map(1 -> "a", 2 -> "b", 3 -> "c")
println(imMap(1)) // a
println(imMap(2)) // b
```

## mutableなmap
```
  import scala.collection.mutable
  
  // 空map定義(型推論できないので型を明示
  val mMap = mutable.Map[Int, String]()
  
  // 値セット
  mMap += (1 -> "a a a")
  mMap += (2 -> "bbb")
  mMap += (3 -> "cc c")
  println(mMap(1))
  println(mMap(2))
  println(mMap(3))
```

- 空マップ作成の別の方法
```scala
val map = mutable.Map.empty[String, Int]
```

## Mapの一般的な操作

```scala
  // immutable Map作成
  val nums = Map("i" -> 1, "ii" -> 2)
  println(nums)

  // Mapの要素ペアを追加
  val nums2 = nums + ("vi" -> 6)
  println(nums2)

  // Map(i -> 1, vi -> 6)
  val nums3 = nums2 - "ii"
  println(nums3)

  println(nums3.size)
  println(nums.contains("ii"))

  // keyを返す
  println("key" + nums2.keys)
  println("keySet" + nums2.keySet)
  println("value" + nums2.values)
  println("isEmpty" + nums2.isEmpty)

  // 空のmutable Map作成
  import scala.collection.mutable
  val words = mutable.Map.empty[String, Int]

  // oneを1にマッピングしてwordsにエントリー追加する
  val words2 = words += ("one" -> 1)
  println(words2)

  // keyだけ指定してマッチするmapエントリーを削除
  val words3 = words2 -= "one"
  println(words3)

  // Listを使って複数のkey-valueペアをmap要素に追加
  val words4 = words3 ++= List("one" -> 1, "two" -> 2, "three" -> 3)
  println(words4)

  // 複数のペアを削除
  val words5 = words4 --= List("one", "two")
  println(words5)
```

- 文字ごとのカウント
```scala
  import scala.collection.mutable

  // textに含まれる文字列ごとに出現回数をカウントする
  def countWords(text: String) = {
    // 空のmutableマップ「counts」作成
    val counts = mutable.Map.empty[String, Int]
    for (rawWord <- text.split("[ ,!.]+")) {
      val word = rawWord.toLowerCase
      // countsマップの(word)をkeyに、valueであるIntを取得しoldCountに格納する(初出なら0)
      val oldCount =
        if (counts.contains(word)) counts(word)
        else 0
      // key:wordに対応するvalue:oldCountをマッピング（+1)して、マップ「counts」の要素として追加する
      counts += (word -> (oldCount + 1))
    }
    counts
  }

  val result = countWords("See Spot run! Run, Spot. Run!")
  // HashMap(see -> 1, spot -> 2, run -> 3)
  println("result" + result)
```
