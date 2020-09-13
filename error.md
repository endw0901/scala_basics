# Nothing型のerror

- 例外処理 https://github.com/endw0901/scala_basics/blob/master/exception_try_catch_finally.md

## Predefオブジェクトのerrorメソッド
- p.214
```scala
def error(message: String): Nothing =
  throw new RuntimeException(message)
```

- Predefで使えるerrorはNothing型を返し例外処理をthrowする
```scala
def divide(x: Int, y: Int): Int =
  if (y != 0) x / y
  else error("can't divide by zero")
```
