# Type

```
// Int
val dec1 = 31

// Long 
val tower = 35L

// Float
val little = 1.2345F
```

## e
- AAAeB aaa × 10のb乗

```
// 1.2345 * 10の2乗 = 123.45
1.2345e2
```

## 文字
- 'A'・・・文字リテラル
- "hello"・・・文字「列」リテラル

## 特殊文字ok

- """ 以外のなんでも受け入れok (""とかなんでも
```
// なんでもokなのでスペースがそのままでてしまう
println(""" Welcom to 
      Type "HELP" for help """)
      
// スペースなくす(各行の最初に|と、stripMargin
println("""|Welcom to 
      |Type "HELP" for help """.stripMargin)

```
