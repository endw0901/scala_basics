# valとvar
- valはfinal変数に似ている(変更不可)
- varは非finalに似ている（代入可能)

## scalaプログラミングの基本ルール
- varとwhileはなるべく避ける

## valのメリット
- varではなくvalをつかうことで、変数が変わっていないかチェックする手間を省ける

## 抽象メンバー
- https://github.com/endw0901/scala_basics/blob/master/abstract_members.md

## 暗黙のゲッター/セッター
- クラス(抽象含む)のメンバーとしてvarを宣言すると、自動的に暗黙のゲッター・セッターが作られる
- https://github.com/endw0901/scala_basics/blob/master/var_setter.md

## traitの中の抽象val実装
 
```scala
  // traitの中の抽象val
  trait RationalTrait {
    val numerArg: Int
    val denomArg: Int
  }
  
  // 実装 
  new RationalTrait {
    val numerArg = 1
    val denomArg = 2
  }
```

### 事前初期化済みフィールドと遅延評価
- https://github.com/endw0901/scala_basics/blob/master/val_lazy_pre_initialized.md
