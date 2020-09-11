# デフォルト値付き引数

```scala
def printTime2(out: java.io.PrintStream = Console.out,divisor: Int = 1) = 
  out.println("time = " + System.currentTimeMills()/divisor

// 指定なしはデフォルト値を使う
printTime2()

// 一部指定して置き換え
printTime2(out = Console.err)
printTime2(divisor = 1000)
```
