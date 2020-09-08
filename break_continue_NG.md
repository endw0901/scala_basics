# break continueのNG例と改善

## NG例：breakとcontinue
- Java
```java:qiita.rb
// 先頭がハイフンでなくて、.scalaで終わるものを探す
int i = 0;
boolean foundIt = false;
while ( i < args.length) {
  if (args[i].startsWith("-")) {
    i = i + 1;
    // 次のループに進む
    continue;
   }
   if (args[i].endsWith(".scala")) {
     foundIt = true;
     // ループを終了する
     break;
   }
   i = i + 1;
 }
```

## 普通例：breakとcontinueを使わないループ
- Java
```java:qiita.rb
// 先頭がハイフンでなくて、.scalaで終わるものを探す
int i = 0;
var foundIt = false;
// foundIt =false(まだ発見できていない間はループ)
while ( i < args.length && !foundIt) {
  if (!args(i).startsWith("-")) {
   if (args(i).endsWith(".scala"))
     foundIt = true;
   }
   i = i + 1;
 }
```


## 再帰関数例
- 条件に合致したindex i を返す
```scala:qiita.rb
def searchFrom(i: Int): Int =
 // 見つからず終了=> return -1
 if (i >= args.length) -1
 // 対象外 => i+1して再帰コール
 else if (args(i).startsWith("-")) searchFrom(i + 1)
 // 見つかったときのiの値を返す
 else if (args(i).endsWith(".scala")) i
 // 対象外 => i+1して再帰コール
 else searchFrom(i + 1)
var i = searchFrom(0)
```
