# private、protectedの範囲

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
