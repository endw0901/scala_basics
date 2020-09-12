# 配列
- 配列 = クラス
- クラスインスタンス生成 = クラスオブジェクト生成

- 配列：mutable ⇔ リスト：immutable

## 配列の新規作成
- 通常使う方法

```
  val names = Array("one","two","three")
  for(i <- 0 to 2)
    print(names(i))
    
```

### 面倒な方法
- 配列クラスオブジェクト作成⇒値を一個一個設定
```
val data = new Array[String](2)
  data(0) = "ito"
  data(1) = "tanaka"
  for(i <- 0 to 1)
    print(data(i))
```

## 配列の連結

- ++
```scala
  abstract class Element {
    def contents: Array[String]
    def height: Int = contents.length
    def width: Int = if (height == 0) 0 else contents(0).length
  }

  class ArrayElement(conts: Array[String]) extends Element {
    def contents: Array[String] = conts
  }
  
def above(that: Element): Element =
    new ArrayElement(this.contents ++ that.contents)  
```
