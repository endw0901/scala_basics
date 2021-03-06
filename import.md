# import
- importはどこにでも書ける
- パッケージだけでなく、オブジェクトも参照できる

## アクセス方法
```scala
  package bobsdelights
  abstract class Fruit (
                       val name: String,
                       val color: String
                       )
  object Fruits {
    object Apple extends Fruit("apple", "red")
    object Orange extends Fruit("orange", "orange")
    val menu = List(Apple, Orange)
      }

  import bobsdelights.Fruit
  import bobsdelights._
  // Fruitの全てのメソッドへ簡単にアクセスできる
  import bobsdelights.Fruit._
 
```

- 引数の変数経由で、型のFruitをimportする方法
```scala
   // 引数の変数経由で、型のFruitをimportする方法
  def showFruit(fruit: Fruit) = {
    import fruit._
    println(name + "s are " + color)
  }
  
  // java.util.regex.Patternにアクセスする方法
  import java.util.regex
  class AstarB {
    val pat = regex.Pattern.compile("a*b")
  }
```

- 配下のメソッドにアクセスする方法
```scala
  // java.util.regex.Patternにアクセスする方法
  import java.util.regex
  class AstarB {
    val pat = regex.Pattern.compile("a*b")
  }
```

## 部分的にimport
``` scala
import Fruits.{Apple, Orange}
```

## リネームしてインポート
``` scala
import Fruits.{Apple => McIntosh, Orange}

// java.sql.Dateを、「S.Date」と書けるようになる
import java.{sql => S}
```

## リネーム＆全てのメンバをインポート
``` scala
import Fruits.{Apple => McIntosh, _}
```

## 指定したメンバ以外をインポート
``` scala
import Fruits.{Pear => _, _}
```
