# 抽象型
- 抽象メンバー：https://github.com/endw0901/scala_basics/blob/master/abstract_members.md

## タイプミスマッチ
- コンパイルエラーとなる例（タイプミスマッチ)
```scala
  class Food
  abstract class Animal {
    def eat(food: Food)
  }

  class Grass extends Food
  class Cow extends Animal {
    // Animalのeatの型Foodと、Cowのeatの型Grassが異なるのでコンパイルエラー発生
    // これがとおると、CowがFishを食べることも許可されることになる
    override def eat(food: Grass) = {}
  }
  
  // class Fish extends Food
  // val bessy: Animal = new Cow
  // bessy eat (new Fish)
```

- コンパイルが通る例
```scala
  class Food
  abstract class Animal {
    type SuitableFood <: Food // 上限境界 左辺はFoodのサブクラスでないといけない
    // Animalの実装クラスは、自分に適したFoodだけを食べれるようにするという意図
    def eat(food: SuitableFood)
  }

  class Grass extends Food
  class Cow extends Animal {
    type SuitableFood = Grass
    override def eat(food: Grass) = {}
  }

  class Fish extends Food
  val bessy: Animal = new Cow
  bessy eat (new Fish) // typeミスマッチエラー発生
```
