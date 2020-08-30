# 集合(SET)
- list:重複ok ⇔ set：重複NG

- setはimmutable、importでmutable
```
var aSet = Set("a","b")

// immutableだが、実際は新しい集合(set)を作って再代入している(+=メソッドをコールしているわけではなく省略記法)
aSet += "c"
```

```
import scala.collection.mutable
val bSet = mutable.Set("a","b")

// mutableなsetに挿入している(+=メソッドをコールしている)
bSet += "C"
```
