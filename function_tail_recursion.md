# 再帰末尾
- p.167

```scala
  def approximate(guess: Double): Double =
    if (isGoodEnough(guess)) guess
    else approximate(improve(guess))
```

## 最適化されない
- 最後に自分自身をcallしているように見えるが、関数オブジェクトを介在している場合は最適化されない

```scala
val funValue = nestedFun _

// 直接nestedFunをcallしていないので×
def nestedFun(x: Int):Unit = {
 if(x != 0){ println(x); funValue(x - 1) }
}
```
