---
title: "Kotlin入門：オブジェクト指向プログラミングの基本"
emoji: "🗂"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: []
published: false
---

# Kotlin入門：オブジェクト指向プログラミングの基本

## はじめに
前回はKotlinの拡張関数やラムダ式について学びました。
前回の記事は以下からご覧いただけます。  
[前回の記事](https://zenn.dev/stakeuchi/articles/github-zenn-linkage-20241218)

今回はKotlinを使用してのオブジェクト指向について学んでいこうと思います。

## オブジェクト指向プログラミングとは
オブジェクト指向プログラミング（OOP）は、プログラムをオブジェクト（データ）とその操作（メソッド）に分割するプログラミング手法です。  

Kotlinはオブジェクト指向プログラミング（OOP）をサポートしており、クラス、継承、ポリモーフィズム、抽象クラス、インターフェースなど、OOPの基本概念を簡潔かつ柔軟に利用できます。  

## 1. クラスの定義
Kolintでは、クラス定義を簡潔に書けます。
```kotlin
// クラス定義
class Person(val name: String, var age: Int)

fun main() {
    // インスタンス生成
    val person = Person("Alice", 20)
    // GetterやSetterを明示的に書かなくても、自動的に生成される
    println("Name: ${person.name}, Age: ${person.age}") // 出力: Name: Alice, Age: 20
}
```

Javaで同じコードを書いた場合は以下のようになります。
```java
// クラス定義
class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    public static void main(String[] args) {
        // インスタンス生成
        Person person = new Person("Alice", 20);
        System.out.println("Name: " + person.getName() + ", Age: " + person.getAge()); // 出力: Name: Alice, Age: 20
    }
}
```

## 2. 継承
### 基本継承
Kotlinでは、クラスはデフォルトでfinal（継承不可）です。  
継承を許可するには、クラスをopenで指定します。
```kotlin
// 親クラス
open class Animal {
    open fun sound() {
        println("Animal sound")
    }
}

// Animalクラスを継承した子クラス
class Dog : Animal() {
    // 親クラスのメソッドをオーバーライド
    override fun sound() {
        println("Bow-wow")
    }
}

fun main() {
    // インスタンス生成
    val dog = Dog()
    dog.sound() // 出力: Bow-wow
}
```

Javaで同じコードを書いた場合は以下のようになります。
```java
// 親クラス
class Animal {
    public void sound() {
        System.out.println("Animal sound");
    }
}

// Animalクラスを継承した子クラス
class Dog extends Animal {
    // 親クラスのメソッドをオーバーライド
    @Override
    public void sound() {
        System.out.println("Bow-wow");
    }
}

public class Main {
    public static void main(String[] args) {
        // インスタンス生成
        Dog dog = new Dog();
        dog.sound(); // 出力: Bow-wow
    }
}
```

## 3. 抽象クラス
抽象クラスは、共通の動作を持つが直接インスタンス化できないクラスを作るために使います。
```kotlin
// 抽象クラス
abstract class Vehicle {
    // 抽象メソッド
    abstract fun drive()
    fun stop() {
        println("Stopping the vehicle")
    }
}

// Vehicleクラスを継承した子クラス
class Car : Vehicle() {
    override fun drive() {
        println("Driving the car")
    }
}

fun main() {
    // インスタンス生成
    val car = Car()
    car.drive() // 出力: Driving the car
    car.stop() // 出力: Stopping the vehicle
}
```

Javaで同じコードを書いた場合は以下のようになります。
```java
// 抽象クラス
abstract class Vehicle {
    // 抽象メソッド
    abstract void drive();
    void stop() {
        System.out.println("Stopping the vehicle");
    }
}

// Vehicleクラスを継承した子クラス
class Car extends Vehicle {
    @Override
    void drive() {
        System.out.println("Driving the car");
    }
}

public class Main {
    public static void main(String[] args) {
        // インスタンス生成
        Car car = new Car();
        car.drive(); // 出力: Driving the car
        car.stop(); // 出力: Stopping the vehicle
    }
}
```

## 4. インターフェース
Kotlinのインターフェースは、抽象メソッドだけでなくデフォルト実装も持てます。
```kotlin
// インターフェース
interface Drivable {
    fun drive()
    // デフォルト実装
    fun honk() {
        println("Honking!")
    }
}

// Animalインターフェースを実装したクラス
class Truck : Drivable {
    override fun drive() {
        println("Driving a truck")
    }
}

fun main() {
    // インスタンス生成
    val truck = Truck()
    truck.drive() // 出力: Driving a truck
    truck.honk()  // 出力: Honking!
}
```

Javaで同じコードを書いた場合は以下のようになります。
```java
// インターフェース
interface Drivable {
    void drive();
    // デフォルト実装
    default void honk() {
        System.out.println("Honking!");
    }
}

// Drivableインターフェースを実装したクラス
class Truck implements Drivable {
    @Override
    void drive() {
        System.out.println("Driving a truck");
    }
}

public class Main {
    public static void main(String[] args) {
        // インスタンス生成
        Truck truck = new Truck();
        truck.drive(); // 出力: Driving a truck
        truck.honk();  // 出力: Honking!
    }
}
```

## 5. コンストラクタ
### プライマリコンストラクタ
Kotlinでは、クラス定義時に記述できます。
```kotlin
// クラス定義
class Person(val name: String, var age: Int)
```

Javaで同じコードを書いた場合は以下のようになります。
```java
// クラス定義
class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

### セカンダリコンストラクタ
複数のコンストラクタを持つ場合は、`constructor`キーワードを使用します。
```kotlin
// クラス定義
class Person(val name: String, var age: Int) {
    constructor(name: String) : this(name, 0) // デフォルトで年齢0
}
```

Javaで同じコードを書いた場合は以下のようになります。
```java
// クラス定義
class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public Person(String name) {
        this(name, 0); // デフォルトで年齢0
    }
}
```

## 6. データクラス
データクラスは、データを保持するためのクラスを簡潔に書けます。
以下の機能が自動生成されます。
- `equals()`
- `hashCode()`
- `toString()`
- `copy()`

```kotlin
// データクラス
data class User(val id: Int, val name: String)

fun main() {
    // インスタンス生成
    val user1 = User(1, "Kotlin")
    val user2 = user1.copy(name = "Java")

    println(user1) // 出力: User(id=1, name=Kotlin)
    println(user2) // 出力: User(id=1, name=Java)
}
```

javaで同じコードを書いた場合は以下のようになります。
```java
// データクラス
class User {
    private int id;
    private String name;

    public User(int id, String name) {
        this.id = id;
        this.name = name;
    }

    public User copy(String name) {
        return new User(this.id, name);
    }

    @Override
    public String toString() {
        return "User(id=" + id + ", name=" + name + ")";
    }
}

public class Main {
    public static void main(String[] args) {
        // インスタンス生成
        User user1 = new User(1, "Kotlin");
        User user2 = user1.copy("Java");

        System.out.println(user1); // 出力: User(id=1, name=Kotlin)
        System.out.println(user2); // 出力: User(id=1, name=Java)
    }
}
```

## 7. オブジェクト宣言（シングルトン）
Kotlinはobjectキーワードを使ってシングルトンを簡単に実現します。
```kotlin
object Singleton {
    fun greet() {
        println("Hello, Singleton!")
    }
}

fun main() {
    Singleton.greet() // 出力: Hello, Singleton!
}
```

Javaで同じコードを書いた場合は以下のようになります。
```java
class Singleton {
    // シングルトンインスタンス
    private static final Singleton instance = new Singleton();

    private Singleton() {}

    // Getter
    public static Singleton getInstance() {
        return instance;
    }

    public void greet() {
        System.out.println("Hello, Singleton!");
    }
}

public class Main {
    public static void main(String[] args) {
        Singleton.getInstance().greet(); // 出力: Hello, Singleton!
    }
}
```

## 8. コンパニオンオブジェクト
Kotlinでは、クラス内に`companion object`を定義することで、静的メンバを持つことができます。
```kotlin
class MyClass {
    // 静的メンバ
    companion object {
        fun greet() {
            println("Hello, Companion!")
        }
    }
}

MyClass.greet() // 出力: Hello, Companion!
```

Javaで同じコードを書いた場合は以下のようになります。
```java
class MyClass {
    // 静的メンバ
    static void greet() {
        System.out.println("Hello, Companion!");
    }
}

public class Main {
    public static void main(String[] args) {
        MyClass.greet(); // 出力: Hello, Companion!
    }
}
```

## 9. 可視性修飾子
Kotlinでは、以下の可視性修飾子を使用できます。
- `public`（デフォルト）: どこからでもアクセス可能。
- `private`: 同じクラス内でのみアクセス可能。
- `protected`: クラスおよびそのサブクラスでアクセス可能。
- `internal`: 同じモジュール内でアクセス可能。（Kotlin特有）

```kotlin
class Example {
    private val privateProperty = "Private"
    internal val internalProperty = "Internal"
    val publicProperty = "Public" // public修飾子は省略可能
}

fun main() {
    val example = Example()
    println(example.publicProperty) // 出力: Public
    println(example.internalProperty) // 出力: Internal
    println(example.privateProperty) // エラー: privatePropertyはアクセスできません
}
```

Javaで同じコードを書いた場合は以下のようになります。
```java
class Example {
    private String privateProperty = "Private";
    String publicProperty = "Public";
    // internal修飾子はJavaには存在しない
}

public class Main {
    public static void main(String[] args) {
        Example example = new Example();
        System.out.println(example.publicProperty); // 出力: Public
        System.out.println(example.privateProperty); // エラー: privatePropertyはアクセスできません
    }
}
```

## 10. クラスのデリゲーション
Kotlinではクラスの機能を別のオブジェクトに委譲することが簡単にできます。
```kotlin
// Printableインターフェース
interface Printable {
    fun print()
}

// Printerクラス
class Printer : Printable {
    // Printableインターフェースの実装
    override fun print() {
        println("Printing...")
    }
}

// Documentクラス
class Document(private val printer: Printable) : Printable by printer

fun main() {
    // インスタンス生成
    val document = Document(Printer())
    document.print() // 出力: Printing...
}
```

Javaで同じコードを書いた場合は以下のようになります。
```java
// Printableインターフェース
interface Printable {
    void print();
}

// Printerクラス
class Printer implements Printable {
    // Printableインターフェースの実装
    @Override
    void print() {
        System.out.println("Printing...");
    }
}

// Documentクラス
class Document implements Printable {
    private Printable printer;

    public Document(Printable printer) {
        this.printer = printer;
    }

    // Printableインターフェースの実装
    @Override
    void print() {
        printer.print();
    }
}

public class Main {
    public static void main(String[] args) {
        // インスタンス生成
        Document document = new Document(new Printer());
        document.print(); // 出力: Printing...
    }
}
```

## まとめ
今回はKotlinを使用してオブジェクト指向プログラミングの基本を学びました。
KotlinはJavaと比べて、コードが簡潔で読みやすく、柔軟な記述が可能です。

次回は、課題に沿って実際にコードを書いていこうと思います。
