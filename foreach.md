# foreach
p.56

```
// 1.型明示
args.foreach((arg:String) => println(arg))

// 2.型省略
args.foreach(arg => println(arg))

// 3.省略形
args.foreach(println)

//
for (arg <- args)
    println(arg)

```
