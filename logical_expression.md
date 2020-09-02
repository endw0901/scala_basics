# AND OR演算子

## 省略する
- 先にfalseが来たら省略
```
def salt() = { println("salt"); false}
def pepper() = { println("pepper"); true}

// true => falseなので両方実行
pepper() && salt()
// false => trueなのでsaltで終わり
salt() && pepper()
```

## 省略せずに両方実行する AND OR
- 先にfalseが来ても省略しない
```
def salt() = { println("salt"); false}
def pepper() = { println("pepper"); true}

// true => falseなので両方実行
pepper() & salt()
// false => trueなのでsaltで終わり
salt() & pepper()
```

- AND,OR ・・・・ && ||
- AND,OR・・・・  &  | 
