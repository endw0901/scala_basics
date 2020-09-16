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

## ケースシーケンス
- p.282
```scala
val second: List[Int] => Int = {
  case x :: y :: _ => y
}
```
