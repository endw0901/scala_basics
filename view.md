# ビュー

- トランスフォーマー・・・1のコレクションをレシーバーオブジェクトとして、結果値として別のコレクションを作るメソッド
- ビュー(view)・・・すべてのコレクションを遅延的にしたり、逆に正格(通常）にする系統だった方法
- force・・・遅延的から正格に戻すメソッド


## 中間コレクションを挟まず高速化
```scala
  // 1 + 1 = 2、  2 * 2 = 4の2つを中間コレクションなしで関数を繋げるので高速
  val v = Vector(1 to 10: _*)
  val v2 = v map (_ + 1) map (_ * 2)
  println(v2) //Vector(4, 6, 8, 10, 12, 14, 16, 18, 20, 22)
```

## Vector => view => 変換をviewに適用 => Vectorに戻す
- p.498

- 中間コレクションを挟まない場合(高速）
```scala
  val v = Vector(1 to 10: _*)
  println((v.view map (_ + 1) map (_ * 2)).force)
```

- 中間コレクションを挟む場合（確認用）
```scala
  val v = Vector(1 to 10: _*)
  val vv = v.view
  val vv2 = vv map (_ + 1)
  val vv3 = vv2 map (_ * 2)
  println(vv3.force)
```

## Viewで中間結果を回避して高速化

- viewなら100万個分の中間オブジェクトを作らなくてよくなる

```scala
  def isPalindrome(x: String) = x == x.reverse
  def findPalindrome(s: Seq[String]) = s find isPalindrome

 // 1)words = 長い文字列から100万取得して、関数に適用
  findPalindrome(words take 1000000)
  
  // 2)長い文字列の軽量なオブジェクト1個（view)作成して関数適用
  findPalindrome(words.view take 1000000)
```
