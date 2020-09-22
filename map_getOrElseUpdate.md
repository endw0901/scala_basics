# mutableマップのgetOrElseUpdate
- キャッシュにないときだけ値設定する

```scala

  def f(x: String) = {
    println("taking my time."); Thread.sleep(100)
    x.reverse }

  val cache = collection.mutable.Map[String, String]()

  // cacheにあればsでmap keyでget、cacheになければf(s)適用してsleep時間かけてreverseでcache反転設定
  def cachedF(s: String) = cache.getOrElseUpdate(s, f(s))
  // 上のdefを起動
  cachedF("abc")

  // 上記を別のコードの冗長な方法で
  def cachedF(arg: String) = cache get arg match {
    case Some(result) => result
    case None =>
      val result = f(arg)
      cache(arg) = result
      result
  }     
```

## getOrElse
- ms getOrElse (k, d) ： マップmsでキーkに対応する値を返す。値がないときはデフォルト値dを返す

## その他のmap演算・操作
- p.475：Mapトレイトの演算・操作
- p.476：mutable.Mapトレイトの演算・操作
