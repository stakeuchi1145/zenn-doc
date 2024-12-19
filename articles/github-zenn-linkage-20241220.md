---
title: "Kotlin入門：オブジェクト指向プログラミングの応用"
emoji: "😽"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Kotlin", "オブジェクト指向プログラミング", "oop", "Java"]
published: false
---

# Kotlin入門：オブジェクト指向プログラミングの応用

## はじめに
前回はKotlinのオブジェクト指向プログラミングの基本について学びました。
前回の記事は以下からご覧いただけます。  
[前回の記事](https://zenn.dev/stakeuchi/articles/github-zenn-linkage-20241219)

今回はKotlinを使用しての課題を解決していきます。

## 課題
以下の要件を満たす動物園の管理システムを作成してください
- 動物園には様々な動物がいます（犬、猫、鳥など）。
- すべての動物は「名前」と「鳴き声」を持ちます。
- 特定の動物（犬や鳥）は「飛ぶ」や「走る」など特定の動作を持つことができます。
- 管理者はすべての動物の情報を表示する機能を持っています。

## 実装
```kotlin
abstract class Animal(val name: String) {
    abstract fun cry(): String // 鳴き声（抽象メソッド）
    open fun move(): String = "歩く" // 共通の動作
}

// インターフェース: 特定の行動を表現
interface Flyable {
    fun fly(): String = "飛ぶ"
}

interface Runnnable {
    fun run(): String = "走る"
}

// サブクラス: 犬クラス (継承 + インターフェース実装)
class Dog(name: String) : Animal(name), Runnable {
    override fun cry() = "ワンワン"
    override fun move() = run() // move()を"走る"動作に上書き
}

// サブクラス: 鳥クラス (継承 + インターフェース実装)
class Bird(name: String) : Animal(name), Flyable {
    override fun cry() = "チュンチュン"
    override fun move() = fly() // move()を"飛ぶ"動作に上書き
}

// サブクラス: 猫クラス (単純な継承)
class Cat(name: String) : Animal(name) {
    override fun cry() = "ニャーニャー"
}

// 動物管理者: 動物を管理し表示
class ZooManager {
    private val animals = mutableListOf<Animal>()

    // 動物を追加
    fun addAnimal(animal: Animal) {
        animals.add(animal)
    }

    // 動物一覧を表示
    fun showAnimals() {
        for (animal in animals) {
            println("名前: ${animal.name}, 鳴き声: ${animal.cry()}, 移動方法: ${animal.move()}")
        }
    }
}

// メイン関数
fun main() {
    // 動物を作成
    val dog = Dog("ポチ")
    val bird = Bird("ピーちゃん")
    val cat = Cat("タマ")

    // 管理者による動物管理
    val zooManager = ZooManager()
    zooManager.addAnimal(dog)
    zooManager.addAnimal(bird)
    zooManager.addAnimal(cat)

    // 動物の情報を表示
    zooManager.showAnimals()
}
```

Javaで同じコードを書いた場合は以下のようになります。
```java
abstract class Animal {
    private String name;

    public Animal(String name) {
        this.name = name;
    }

    public abstract String cry(); // 鳴き声（抽象メソッド）

    public String move() {
        return "歩く"; // 共通の動作
    }
}

// インターフェース: 特定の行動を表現
interface Flyable {
    default String fly() {
        return "飛ぶ";
    }
}

interface Runnable {
    default String run() {
        return "走る";
    }
}

// サブクラス: 犬クラス (継承 + インターフェース実装)
class Dog extends Animal implements Runnable {
    public Dog(String name) {
        super(name);
    }

    @Override
    public String cry() {
        return "ワンワン";
    }

    @Override
    public String move() {
        return run(); // move()を"走る"動作に上書き
    }
}

// サブクラス: 鳥クラス (継承 + インターフェース実装)
class Bird extends Animal implements Flyable {
    public Bird(String name) {
        super(name);
    }

    @Override
    public String cry() {
        return "チュンチュン";
    }

    @Override
    public String move() {
        return fly(); // move()を"飛ぶ"動作に上書き
    }
}

// サブクラス: 猫クラス (単純な継承)
class Cat extends Animal {
    public Cat(String name) {
        super(name);
    }

    @Override
    public String cry() {
        return "ニャーニャー";
    }
}

// 動物管理者: 動物を管理し表示
class ZooManager {
    private List<Animal> animals = new ArrayList<>();

    // 動物を追加
    public void addAnimal(Animal animal) {
        animals.add(animal);
    }

    // 動物一覧を表示
    public void showAnimals() {
        for (Animal animal : animals) {
            System.out.println("名前: " + animal.getName() + ", 鳴き声: " + animal.cry() + ", 移動方法: " + animal.move());
        }
    }
}

// メイン関数
public class Main {
    public static void main(String[] args) {
        // 動物を作成
        Dog dog = new Dog("ポチ");
        Bird bird = new Bird("ピーちゃん");
        Cat cat = new Cat("タマ");

        // 管理者による動物管理
        ZooManager zooManager = new ZooManager();
        zooManager.addAnimal(dog);
        zooManager.addAnimal(bird);
        zooManager.addAnimal(cat);

        // 動物の情報を表示
        zooManager.showAnimals();
    }
}
```

## 実行結果
```shell
名前: ポチ, 鳴き声: ワンワン, 移動方法: 走る
名前: ピーちゃん, 鳴き声: チュンチュン, 移動方法: 飛ぶ
名前: タマ, 鳴き声: ニャーニャー, 移動方法: 歩く
```

## コード解説
### 1. 抽象クラス:
- Animalクラスはすべての動物の共通要素を定義。
- 鳴き声は動物ごとに異なるため、cry()メソッドは抽象メソッドとしてサブクラスで実装。

### 2. インターフェース:
- 特定の動作（FlyableやRunnable）を独立した形で実装可能。
- これにより、異なる動物が複数の特性を持つ設計が可能に。

### 3. 継承とオーバーライド:
- 各動物クラス（Dog, Bird, Cat）はAnimalクラスを継承し、それぞれ異なる動作を持つ。

### 4. ポリモーフィズム:
- ZooManagerはリストにAnimal型のオブジェクトを保持。
- 実際のオブジェクト（犬、鳥、猫）ごとに適切な動作を実行。

### 5. カプセル化:
- ZooManagerが動物の追加や表示を一元管理。

### 6. デリゲーション:
- DogとBirdのmove()メソッドは、それぞれRunnableやFlyableインターフェースに動作を委譲。

## まとめ
Kotlinのオブジェクト指向プログラミングの応用について学びました。
抽象クラスやインターフェースを使うことで、柔軟な設計が可能になります。
これらの機能を活用して、より効率的なコードを書いていけそうです。

次回は、KotlinのAndroidアプリ開発について学んでいきます。
