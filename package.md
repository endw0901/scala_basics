# パッケージ
- ネストしているときはpackageの外のShipにもそのままアクセス可能
```scala
  package bobsrockets {
    package navigation {
      class Navigator {
        val map = new StarMap
      }
      class StarMap
    }
    class Ship {
      val nav = new navigation.Navigator
    }
    package fleets {
      class Fleet {  
        // ネストしているときはpackageの外のShipにもそのままアクセス可能
        def addShip() = { new Ship }
      }
    }
  }
```

- ネストしていない時はNG
```scala
package bobsrockets {
  class Ship
}
package bobsrockets.fleets {
  class Fleet {
    def addShip() = { new Ship }
  }
}
```

## 外側のパッケージにrootからアクセス
```scala
  package launch {
    class Booster3
  }
  
  package bobsrockets {
    package navigation {
      package launch {
        class Booster1
      }
      
      class MissionControl {
        val booster1 = new launch.Booster1
        val booster2 = new bobsrockets.launch.Booster2
        val booster3 = new _root_.launch.Booster3
      }
    }
    package launch {
      class Booster2
    }
  }
```
