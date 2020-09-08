# メソッドとローカル関数
- p.152
- オブジェクトのメンバー = メソッド
- 機能ごとに関数を細分化→ヘルパー関数

```scala
object xxxx
   def xxxx
   
       AAAAA
   // ヘルパー関数
   private def AAAAA
```

## ローカル関数
- ネストすることで、privateが不要でスコープが明確な非公開メソッドとなる
- 上位の引数をそのまま引き継げる
```scala
object xxxx
   def xxxx
      def AAAAA
```
