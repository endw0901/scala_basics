# ループ処理

https://github.com/rockthejvm/scala-beginners/tree/master/src

* 6.recursion

* ループ処理では、do whileはNG
* ループ処理・iteratorでは、tail-recursionを使う(stack-overflowを回避)
https://nrinaudo.github.io/scala-best-practices/unsafe/recursion.html

* 変数を蓄積せず、引き渡していき最後から最初に処理していく
