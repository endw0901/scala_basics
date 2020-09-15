# 変数束縛パターン

- 2回続けて絶対値演算をしているものを探す
- UnOp()の結果をeに束縛
```scala
 expr match {
  case UnOp("abs", e @ UnOp("abs", _)) => e
  case _ =>
 }
```
