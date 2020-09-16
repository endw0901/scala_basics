# 部分適用された関数

```scala
def sum(a: Int, b:Int, c:Int) = a + b + c

// 引数が全部ある
sum(1,2,3) = 6
```

- 引数が足りないsum関数を変数aに格納し、aは引数を全部受けて6を返す
```scala
val a = sum _
a(1,2,3)
```

- 引数が足りないsum関数を変数bに格納し、bは引数を足りないところだけ受けて、1 + 2 + 3 = 6と計算する（部分適用された関数)
```scala
val b = sum(1, _: Int, 3)
b(2)
```

## _を省略できるとき、できないとき
- p.161 関数型が必須の時だけ省略ok
```scala
// okケース
sumeNumbers.foreach(println)

// okケース
val c = sum _

// NGケース
val c = sum
```

## ケースシーケンス・部分関数
- p.282
- マッチが網羅的でないケースシーケンス
- ::はリストの表記 ※(1,2,3)は 1 :: 2 :: 3とも書ける
```scala
// リストの2つめの要素を返す(関数型「List[Int] => Int」)
val second: List[Int] => Int = {
  case x :: y :: _ => y
}

// 結果：6
second(List(5, 6, 7))
// 結果 エラー
second(List())
```

### 部分関数のチェック
- isDefinedAtチェックがある前提で部分関数を利用する(Akkaなどで)
```scala
 // 部分関数型(空リストでエラーになるので網羅的ではない）
 val second: PartialFunction[List[Int], Int] = {
  case x :: y :: _ => y
 }
 
 // ture
 second.isDefinedAt(List(5,6,7))
 // false => このチェックがある前提で部分関数を利用する(Akkaなどで)
 second.isDefinedAt(List())
 ```

