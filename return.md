# return
p.81

- return省略時は、メソッド内の最後の値を返す
```
def checksum(): Int = { return ~(sum & 0xFF) +1}

// 
def checksum(): Int = ~(sum & 0xFF) +1
```
