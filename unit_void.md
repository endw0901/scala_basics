# Unit型

- javaのvoidと異なり、Unit型は()という値を返す
- 意味のある結果を返さない手続きの定義の場合、Unit値の「()」を返す

## Unit値の()を返す例

- ()==greet()がtrueとなる
```scala
object ScalaPlayground extends App {
  def greet() = {println("hi")}
  println(()==greet())
}
```

- (line = readLine())のリターンは()なので、下記は無限ループになってしまう
```scala
var line = ""
while((line = readLine()) != "")
  println("Read: " + line)
```
