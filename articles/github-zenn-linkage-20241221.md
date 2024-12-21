---
title: "Kotlin入門: Androidアプリ開発の基本"
emoji: "👏"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Kotlin", "Android", "アプリ開発", "Android Studio", "Java"]
published: false
---

# Kotlin入門: Androidアプリ開発の基本

## はじめに
前回はKotlinのオブジェクト指向プログラミングの応用について学びました。
前回の記事は以下からご覧いただけます。  
[前回の記事](https://zenn.dev/stakeuchi/articles/github-zenn-linkage-20241220)

今回はKotlinを使用してのAndroidアプリ開発の基本について学んでいきます。

## Androidアプリ開発とは
Androidアプリ開発は、スマートフォンやタブレットなどのAndroidデバイス向けにアプリケーションを開発することです。  
2017年にAndroid開発においてGoogleが公式にサポートするプログラミング言語であり、現在の主流の開発言語です。  

Jetpack ComposeはKotlinを使用してAndroidアプリのユーザーインターフェースを構築するためのツールキットです。

## Kotlinを使ったAndroid開発の基本構造
### プロジェクト構成
Android Studioで新規プロジェクトを作成すると、以下のような構成になります。
```
MyKotlinApp/
├── app/
│   ├── src/
│   │   ├── main/
│   │   │   ├── kotlin/  # Kotlinコードを配置
│   │   │   │   └── com/example/myapp/
│   │   │   │       └── MainActivity.kt
│   │   │   ├── res/     # リソース（XMLファイルなど）
│   │   │   │   ├── layout/
│   │   │   │   │   └── activity_main.xml
│   │   │   │   └── values/
│   │   │   │       └── strings.xml
│   │   │   └── AndroidManifest.xml
│   ├── build.gradle
└── build.gradle
```

## Kotlinの主要機能（Android開発向け）
### 1. 拡張関数
Kotlinでは、既存のクラスに新しいメソッドを追加する拡張関数を定義できます。
```kotlin
fun View.show() {
    this.visibility = View.VISIBLE
}

button.show() // ボタンを表示
```

### 2. データクラス
データクラスは、データを保持するためのクラスを簡潔に定義できます。
```kotlin
data class User(val name: String, val age: Int)
```

### 3. スコープ関数
スコープ関数は、オブジェクトのコンテキスト内でコードブロックを実行するための関数です。
```kotlin
val user = User("Alice", 25).apply {
    println("Name is $name and age is $age")
}
```

### 4. ラムダ式
ラムダ式は、無名関数を簡潔に記述するための構文です。
```kotlin
val sum = { x: Int, y: Int -> x + y }
```

### 5. 非同期処理
KotlinのCoroutinesは非同期処理を直線的に書けるため、可読性が高くなります。
```kotlin
suspend fun fetchData() {
    val result = withContext(Dispatchers.IO) {
        // 非同期処理
        "Data fetched"
    }
    println(result)
}
```

### 6. Jetpack Composeとの統合
KotlinはJetpack Compose（AndroidのモダンUIツールキット）を前提に設計されており、宣言型UI開発が容易。
```kotlin
@Composable
fun Greeting(name: String) {
    Text(text = "Hello, $name!")
}
```

## 基本例
```kotlin
// MainActivity.kt
package com.example.myapp

import android.os.Bundle
import android.widget.Button
import android.widget.Toast
import androidx.appcompat.app.AppCompatActivity

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val button: Button = findViewById(R.id.button)
        button.setOnClickListener {
            Toast.makeText(this, "Button clicked!", Toast.LENGTH_SHORT).show()
        }
    }
}
```

```xml
<!--  activity_main.xml -->
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
              android:layout_width="match_parent"
              android:layout_height="match_parent"
              android:orientation="vertical"
              android:gravity="center">

    <Button
            android:id="@+id/button"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Click Me" />
</LinearLayout>
```

## まとめ
Kotlinは、簡潔さ、安全性、非同期処理の簡単さなど、Javaの欠点を解消する設計がされています。  
特にAndroid開発ではGoogleが推奨する公式言語であり、今後さらに普及していくことが予想されます。
