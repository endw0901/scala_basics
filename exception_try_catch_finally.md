# 例外処理


## finally
- なにがあっても確実にファイルをクローズしたいときなど
```scala
import java.io.FileReader
val file = new FileReader("input.txt")
try{
//ファイル使う処理
} finally {
  file.close() //確実にファイルをクローズする
}
```
