# パッケージオブジェクト
- p.249
- パッケージ全体スコープに入れたいメソッドを格納

```scala
package object bobsdelights {
  def showFruit(fruit: Fruit) = {
     import fruit._
     println(name + "s are " + color)

```
