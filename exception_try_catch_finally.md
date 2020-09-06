# 例外処理


## finally
- なにがあっても確実にファイルをクローズしたいときなど
- 値を返したり、tryやcatchの結果を変更することはNG（書けばできてしまうがやらない)
```scala
import java.io.FileReader
val file = new FileReader("input.txt")
try{
//ファイル使う処理
} finally {
  file.close() //確実にファイルをクローズする
}
```

## try - catchの改善版エラーハンドリング
- https://www.udemy.com/course/rock-the-jvm-scala-for-beginners/learn/lecture
- 34.Handling Failure参照
- Try(unsafeMethod()).orElse(Try(backupMethod()))を使い、例外にはthrow new RuntimeException("エラーメッセージ")

```scala
package lectures.part3fp

import scala.util.{Random, Try, Failure, Success}

object HandlingFailure extends App {

  // create success and failure
  val aSuccess = Success(3)
  val aFailure = Failure(new RuntimeException("SUPER FAILURE"))

  println(aSuccess)
  println(aFailure)

  def unsafeMethod(): String = throw new RuntimeException("NO STRING FOR YOU BUSTER")

  // Try objects via the apply method
  val potentialFailure = Try(unsafeMethod())
  println(potentialFailure)

  // syntax sugar
  val anotherPotentialFailure = Try {
    // code that might throw
  }

  // utilities
  println(potentialFailure.isSuccess)

  // orElse
  def backupMethod(): String = "A valid result"
  val fallbackTry = Try(unsafeMethod()).orElse(Try(backupMethod()))
  println(fallbackTry)

  // IF you design the API
  def betterUnsafeMethod(): Try[String] = Failure(new RuntimeException)
  def betterBackupMethod(): Try[String] = Success("A valid result")
  val betterFallback = betterUnsafeMethod() orElse betterBackupMethod()

  // map, flatMap, filter
  println(aSuccess.map(_ * 2))
  println(aSuccess.flatMap(x => Success(x * 10)))
  println(aSuccess.filter(_ > 10))
  // => for-comprehensions

```
### 練習
- 処理の流れ

```
1.possibleHTMLは、①possibleConnectionを呼び出し、②connectionクラスのgetSafeをcall
①-1.possibleConnectionは、HttpServiceのgetSafeCnnectionを呼び出す
①-2.HttpServiceのgetSafeCnnectionは、HttpServiceのgetConnectionを呼び出しConnectionクラスを取得する
①-3.HttpServiceのgetConnectionで成功したらConnection、失敗したらerror
⇒Connectionクラスを取得

②connectionクラスのgetSafeをcall
②-1.ConnectionのgetSafeは、urlを引数にgetをcall
②-2.get関数は、成功したらhtml、失敗したらエラーを返す
⇒foreachで取得したhtmlまたはエラーを返す
```
```scala
  val host = "localhost"
  val port = "8080"
  def renderHTML(page: String) = println(page)

  // ランダムに成功・失敗する接続クラス
  class Connection {
    def get(url: String): String = {
      val random = new Random(System.nanoTime())
      if (random.nextBoolean()) "<html>...</html>"
      else throw new RuntimeException("Connection interrupted")
    }

    def getSafe(url: String): Try[String] = Try(get(url))
  }

  object HttpService {
    val random = new Random(System.nanoTime())

    def getConnection(host: String, port: String): Connection =
      if (random.nextBoolean()) new Connection
      else throw new RuntimeException("Someone else took the port")

    def getSafeConnection(host: String, port: String): Try[Connection] = Try(getConnection(host, port))
  }

  // if you get the html page from the connection, print it to the console i.e. call renderHTML
  val possibleConnection = HttpService.getSafeConnection(host, port)
  val possibleHTML = possibleConnection.flatMap(connection => connection.getSafe("/home"))
  possibleHTML.foreach(renderHTML)

  // shorthand version
  HttpService.getSafeConnection(host, port)
    .flatMap(connection => connection.getSafe("/home"))
    .foreach(renderHTML)

  // for-comprehension version
  for {
    connection <- HttpService.getSafeConnection(host, port)
    html <- connection.getSafe("/home")
  } renderHTML(html)

  /*
    try {
      connection = HttpService.getConnection(host, port)
      try {
        page = connection.get("/home")
        renderHTML(page)
      } catch (some other exception) {
      }
    } catch (exception) {
    }
   */

}
```
