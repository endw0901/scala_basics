# equal

- a == b => 値の等価性
- 参照の比較は？→xxxxxxxxxxxxxxxxあとで記載

## ==とeq
- javaでは x == yはfalse (scalaではオブジェクトが違っても、値が同じならtrue)
- javaの==に値するのがscalaのeq (値が同じでも、オブジェクトが別ならfalseとなる)
```scala
val x = new String("abc")
val y = new String("abc")

// true
x == y

// false
x eq y

// true
x ne y
``
