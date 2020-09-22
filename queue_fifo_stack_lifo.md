# FIFO LIFO

- キューはFIFO
- スタックはLIFO

## LIFO：immutable stack
- LIFO ・・・1,2,3と入ったら、3,2,1の順で取り出す


```scala
  val stack = scala.collection.immutable.Stack.empty

  val hasOne = stack.push(1)
  println(hasOne.top)
  println(hasOne.pop)
```

## FIFO：immutable Queue
- FIFO・・・1,2,3と入ったら、1,2,3の順で取り出す

### Queueに要素を追加
```scala
  val empty = scala.collection.immutable.Queue[Int]()
  
  // immutabel Queueに要素を追加
  val has1 = empty.enqueue(1)
  println(has1) // Queue(1)
  
  // 複数の要素を追加
  val has123 = has1.enqueue(List(2,3))
  println(has123) // Queue(1, 2, 3)
```

### 要素を削除
```scala
  // 先頭から要素を削除
  val (element, has23) = has123.dequeue
  println(element) // 1
  println((element, has23)) // (1,Queue(2, 3))
```
