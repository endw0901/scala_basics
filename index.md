# index

## index
- 1 + 5と同じようにindexOfが+のように解釈される
```
val s = "Hello, world"
println(s indexOf 'o')
println(s.indexOf('o'))

// 5(6文字目)から探索開始 => 2つ目のoの位置8
val s = "Hello, world"
s indexOf ('o', 5)
```
