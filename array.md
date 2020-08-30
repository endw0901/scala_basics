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
