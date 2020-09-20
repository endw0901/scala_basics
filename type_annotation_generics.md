# 型アノテーション
- 変位指定(variant)：https://github.com/endw0901/scala_basics/blob/master/trait_type_constructor.md
- https://qiita.com/f81@github/items/7a664df8f4b87d86e5d8

## 型アノテーション（型パラメータ）
- ジェネリクス的にTとしておいて、使う時にStringやIntと宣言して使い分けることができる
```scala
object TypeParamSample {

  class TypeParam[T](val t: T) {
    def get: T = this.t
  }

  def main(args: Array[String]): Unit = {
    val stringTypeParam = new TypeParam[String]("test")
    println(stringTypeParam.get)

    val intTypeParam = new TypeParam[Int](1)
    println(intTypeParam.get)
  }

}
```

### Javaのジェネリクス型
```java
// 例えば、JavaのArrayListの定義を抜粋するとこんな感じです。
public class ArrayList<E> {...}
// <E>でジェネリックスだぜって言っておいて
// 実際に使うときは、
final List<String> arrays = new ArrayList<String>()
// として、EだったところにStringとして、ArrayListのインスタンスを生成します。
// これでこのListには、String型の要素しか入れれないぜ！てことができるんだ。
```



## Listの型アノテーション
```scala
  // 型推論ではリストの要素型は推論できないためアノテーションを省略できない　
  def flattendRight[T](xss: List[List[T]]) =
    // (xss :\ List())とするとエラーとなる
    (xss :\ List[T]()) (_ ::: _)
```
