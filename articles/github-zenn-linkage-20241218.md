---
title: "Kotlin入門: 拡張関数やラムダ式を理解しよう"
emoji: "😽"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["kotlin", "programming", "java"]
published: false
---

# Kotlin入門: 拡張関数やラムダ式を理解しよう

## 目次
- [はじめに](#はじめに)
- [拡張関数とは？](#拡張関数とは)
- [ラムダ式の活用方法](#ラムダ式の活用方法)
- [高階関数の使い方](#高階関数の使い方)
- [まとめ](#まとめ)

## はじめに
前回はKotlinの基本文法について学びました。
前回の記事は以下からご覧いただけます。  
[前回の記事](https://zenn.dev/stakeuchi/articles/github-zenn-linkage-20241218)

今回は、Kotlinのモダンな特徴である拡張関数やラムダ式について学び、より高度な開発スキルを身につけましょう。

---

## 1. 拡張関数とは？
Kotlinでは、拡張関数を利用して既存のクラスに新しいメソッドを追加できますが、クラスそのものを修正する必要はありません。

```kotlin
fun String.addPrefix(prefix: String): String {
    return prefix + this
}

fun main() {
    println("World".addPrefix("Hello, ")) // 出力：Hello, World
}
```

### Javaとの比較
Javaでは拡張関数そのものは存在しないため、ユーティリティクラスを使って同じ効果を再現します。

```java
public class StringUtils {
    // Javaでは静的メソッドを作成する必要がある
    public static String addPrefix(String str, String prefix) {
        return prefix + str;
    }
}

public class Main {
    public static void main(String[] args) {
        System.out.println(StringUtils.addPrefix("World", "Hello, ")); // 出力：Hello, World
    }
}
```

### ポイント
Kotlinでは、メソッド呼び出しのように自然に拡張関数を利用できるため、**コードがより直感的**です。

---

## 2. ラムダ式の活用方法
Kotlinでは、ラムダ式を使うことでコードを簡潔に記述できます。例えば、リストのフィルタリングを行う場合：

```kotlin
val numbers = listOf(1, 2, 3, 4)
val evenNumbers = numbers.filter { it % 2 == 0 }
println(evenNumbers) // 出力：[2, 4]
```

### Javaとの比較
Java 8以降ではラムダ式がサポートされていますが、Stream APIを使用する必要があります。

```java
import java.util.*;
import java.util.stream.Collectors;

public class Main {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4);
        List<Integer> evenNumbers = numbers.stream()
                                           .filter(n -> n % 2 == 0)
                                           .collect(Collectors.toList());
        System.out.println(evenNumbers); // 出力：[2, 4]
    }
}
```

### ポイント
Kotlinは標準ライブラリにラムダ式を活用した便利な関数（`map`, `filter` など）が多く、より直感的に記述できます。

---

## 3. 高階関数の使い方
Kotlinでは、関数を引数として受け取る高階関数をサポートしています。

```kotlin
fun calculate(a: Int, b: Int, operation: (Int, Int) -> Int): Int {
    return operation(a, b)
}

fun main() {
    val result = calculate(3, 5) { x, y -> x + y }
    println(result) // 出力：8
}
```

### Javaとの比較
Javaでは、`BiFunction`や`Function`といったインターフェースを使用する必要があり、やや冗長です。

```java
import java.util.function.BiFunction;

public class Main {
    public static int calculate(int a, int b, BiFunction<Integer, Integer, Integer> operation) {
        return operation.apply(a, b);
    }

    public static void main(String[] args) {
        int result = calculate(3, 5, (x, y) -> x + y);
        System.out.println(result); // 出力：8
    }
}
```

### ポイント
Kotlinは高階関数を簡潔に記述でき、柔軟なコード設計が可能です。

#### 応用例: `apply` を使った初期化
```kotlin
data class User(var name: String, var age: Int)

fun main() {
    val user = User("Alice", 25).apply {
        name = "Bob"
        age = 30
    }
    println(user) // 出力：User(name=Bob, age=30)
}
```

---

## まとめ
Kotlinの拡張関数やラムダ式、高階関数を活用することで、より簡潔で直感的なコードを書くことができます。

- **拡張関数**: 既存クラスに新しいメソッドを追加できる。
- **ラムダ式**: 簡潔で直感的な処理を記述可能。
- **高階関数**: 柔軟なコード設計を実現。

次回は、Kotlinのオブジェクト指向について学びます。  
一緒にKotlinへの理解を深めていきましょう！
