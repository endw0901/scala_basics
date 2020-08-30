# 集合(SET)
- list:重複ok ⇔ set：重複NG
- map:key-value

- setはimmutable、importでmutable
```
// immutableなsetに再代入するのでvarにする必要がある
var aSet = Set("a","b")

// immutableだが、実際は新しい集合(set)を作って再代入している(+=メソッドをコールしているわけではなく省略記法)
aSet += "c"
```

- valはfinal的、varは非final的

```
import scala.collection.mutable
// mutableなのでvalでいい
val bSet = mutable.Set("a","b")

// mutableなsetに挿入している(+=メソッドをコールしている)
bSet += "C"
```
