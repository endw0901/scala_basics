# カリー化
- p.177

- カリーではない場合
```scala
def plainOldSum(x: Int, y: Int) = x + y
println(plainOldSum(1,2)
```

- カリー
```scala
def plainOldSum(x: Int)(y: Int) = x + y
println(plainOldSum(1)(2)
```

