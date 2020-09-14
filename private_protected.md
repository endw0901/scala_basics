# private、protectedの範囲
- privateもprotectedも書いていなければpublic
```scala
  // privateの範囲
  class Outer {
    class Inner {
      private def f() = { println("f")}
      class InnerMost {
        f() //ok
      }
    }
    (new Inner).f() // error
  }
  
  // protectedの範囲・・・メンバーが定義されているクラスのサブクラスのみok
  package p {
    class Super {
      protected fef f() = { println("f") }
    }
    class Sub extends Super {
      f()
    }
    class Other {
      (new Super).f() //error 
    }
```

## 限定子付きアクセス修飾子
- p.246
- (1)privateだが、bobsrocketsに含まれるclass/objectすべてから見える
- (2)オブジェクト非公開(同じインスタンスからだけアクセス可能)
```scala
  package bobsrockets {
    package navigation {
      // (1)privateだが、bobsrocketsに含まれるclass/objectすべてから見える
      private[bobsrockets] class Navigator {
        protected[navigation] def useStarChart() = {}
        class LegOfJourney {
          private[Navigator] val distance = 100
        }
        // (2)オブジェクト非公開(同じインスタンスからだけアクセス可能)
        private[this] var speed = 200
      }
    }
    package launch {
      import navigation._
      object Vehicle {
        private[launch] val guide = new Navigator()
      }
    }
  }
  
  // (2)NG
  val other = new Navigator
  other.speed
```
