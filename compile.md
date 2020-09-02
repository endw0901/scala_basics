# コンパイル
- p.87
- 結果式で終わらない、定義式で終わるファイルのコンパイル => scalac or fsc
- xxx.scalaファイルを、コンパイルで生成されるクラスファイル「xxx.class」を実行する必要がある


## 例

```
package test1

class ChecksumAccumulator {
  private var sum = 0
  def add(b: Byte): Unit = { sum += b }
  def checksum(): Int = ~(sum & 0xFF) + 1

}

// コンパイル
scalac ChecksumAccumulator.scala
```
