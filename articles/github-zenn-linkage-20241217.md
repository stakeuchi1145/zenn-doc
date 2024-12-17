---
title: "Kotlin入門: 基本文法をマスターしよう"
emoji: "🐈"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["kotlin", "programming", "java"]
published: false
---

# Kotlin入門: 基本文法をマスターしよう

## はじめに
前回はKotlinの特徴と採用事例について紹介しました。
前回の記事は以下からご覧いただけます。  
[前回の記事](https://zenn.dev/stakeuchi/articles/github-zenn-linkage-20241215)

今回は、Kotlinの基本文法について学び、開発の第一歩を踏み出しましょう。

## Kotlinの基本文法
### 1. 変数宣言
Kotlinでは変数の再代入の可否に応じて、以下の2種類のキーワードを使います。

- `val`（再代入不可）
- `var`（再代入可能）

以下のコード例を見てみましょう。

```kotlin
val name: String = "Kotlin"  // 再代入不可
var age: Int = 25           // 再代入可能

// エラー例
name = "Java" // エラー: valは再代入できません
age = 30      // OK: varは再代入できます
```
型推論も可能です。
```kotlin
val message = "Hello, Kotlin!" // String型と推論
var count = 10                 // Int型と推論
```

### 2. 関数
この章では、Kotlinで関数を定義する方法とシンプルに記述するコツを学びます。

Kotlinではfunキーワードを使って関数を定義します。
```kotlin
fun greet(name: String): String {
    return "Hello, $name!"
}
println(greet("Kotlin")) // 出力: Hello, Kotlin!
```

単一式の関数では、returnを省略できます。

```kotlin
fun add(a: Int, b: Int) = a + b
println(add(2, 3)) // 出力: 5
```

### 3. 条件分岐
Kotlinのif文は、条件に応じた処理だけでなく、値を返す「式」としても利用できます。
```kotlin
val number = 10
val result = if (number % 2 == 0) "Even" else "Odd"
println(result) // 出力: Even
```

### 4. ループ
Kotlinでは、forループとwhileループをサポートしています。

**forループ**: コレクションや範囲を反復処理します。
```kotlin
for (i in 1..5) {
    println(i) // 出力: 1, 2, 3, 4, 5
}
```

**whileループ**: 条件がtrueの間、繰り返し処理を行います。
```kotlin
var i = 1
while (i <= 5) {
    println(i) // 出力: 1, 2, 3, 4, 5
    i++
}
```

### 5. null安全
Kotlinでは、nullを明示的に許容する型を指定する必要があります。  
?.や?:を利用することで安全にnullを扱えます。
```kotlin
var name: String? = null // null許容型
name = "Kotlin"

// null安全にアクセスする例
println(name?.length) // ?.はnull安全呼び出しで、変数がnullでない場合のみ実行されます。
println(name?.length ?: 0) // ?:（エルビス演算子）は、nullの場合にデフォルト値(0)を提供します。
```

### 6. クラスとオブジェクト
Kotlinではシンプルにクラスを定義できます。
```kotlin
class Person(val name: String, var age: Int)

val person = Person("Kotlin", 25)
println(person.name) // 出力: Kotlin
person.age = 26
println(person.age)  // 出力: 26

```

**データクラス**: データクラスは、データを保持するためのクラスです。toStringやequalsが自動生成されます。
```kotlin
data class User(val id: Int, val name: String)

val user = User(1, "Kotlin")
println(user) // 出力: User(id=1, name=Kotlin)
```

### 7. コレクション操作
強力なコレクション操作機能を提供します。
```kotlin
val numbers = listOf(1, 2, 3, 4, 5)

// フィルタリング
val evenNumbers = numbers.filter { it % 2 == 0 }
println(evenNumbers) // 出力: [2, 4]

// マッピング
val doubled = numbers.map { it * 2 }
println(doubled) // 出力: [2, 4, 6, 8, 10]
```
## 8. まとめ
Kotlinの基本文法を理解することで、シンプルかつ効率的にコードを記述できるようになります。  
これらの基礎を踏まえ、次のステップではKotlinのモダンな特徴である拡張関数やラムダ式を学びましょう！  
Kotlinの強力な機能を活用して、一緒にレベルアップしたコーディングスキルを身につけていきましょう。

