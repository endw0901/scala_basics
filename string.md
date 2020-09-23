# 文字列
- p.493

```scala
  val str = "hello"
  println(str)

  println(str.reverse) // olleh

  println(str.map(_.toUpper)) // HELLO
  println(str drop 3) // lo
  println(str slice (1,4)) // ell 0,1,2,3,4のうち、1～3
```
