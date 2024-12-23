---
title: "Kotlin入門: バックエンド開発について理解する"
emoji: "😎"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Kotlin", "バックエンド", "Spring Boot", "Ktor"]
published: false
---

# Kotlin入門: バックエンド開発について理解する

## 1. はじめに
前回はAndroid開発について学びました。
- [Kotlin入門: Android開発について理解する](https://zenn.dev/techgym/articles/20241222-kotlin-android)

今回はバックエンド開発について学びます。

## 2. バックエンド開発とは
バックエンド開発とは、Webアプリケーションのサーバーサイドの開発を指します。  
Kotlin は Android 向けの開発に注目されがちですが、JVM 言語であるためにサーバサイド（バックエンド）開発でも非常に活用されています。

## 3. Kotlinでバックエンド開発をするメリット
### 1. Java との高い互換性
Kotlin は JVM 上で動作するため、Java の豊富なライブラリやフレームワークをそのまま利用できます。  
既存の Java コードと共存する形で徐々に Kotlin に移行できるのも強みです。

### 2. モダンな言語仕様
Null 安全や拡張関数、data class、Coroutine など、開発効率を高めるモダンな機能を標準でサポートしています。  
コードが簡潔になるので可読性が上がり、バグの原因となりがちな null 周りの問題を減らすこともできます。

### 3. 少ないボイラープレートコード
Kotlin ではクラス宣言や getter/setter などの**定型的に繰り返し書かざるを得ないコード**が減り、業務ロジックに集中しやすくなります。

### 4. Coroutines による非同期処理の簡潔化
Kotlin のコルーチン(Coroutines)は、軽量スレッドを使ってシンプルに非同期処理を実装できるため、高負荷環境でのパフォーマンス向上やコードの可読性改善に有効です。

## 4. 代表的なフレームワーク
### Spring Boot
#### 概要
Spring フレームワークをベースにした Java の定番フレームワークが「Spring Boot」です。  
Kotlin をサポートしており、チュートリアルやドキュメントも豊富なため、初学者から大規模開発まで幅広く利用されています。  
Spring Framework は Java で書かれた歴史が長いので「Spring = Java」というイメージが強いのは確かですが、近年は Kotlin に対しても公式にサポートが行われています。

#### 特徴
- 豊富な機能（DI/データベース連携/Web MVCなど）を備えたオールインワンフレームワークです。
- Kotlin でのサポートは公式にも手厚く、Kotlin 用のプロジェクトテンプレートを利用可能になります。
- 大規模システムにも適した構造です。

### サンプルコード
```kotlin
import org.springframework.boot.autoconfigure.SpringBootApplication
import org.springframework.boot.runApplication
import org.springframework.web.bind.annotation.GetMapping
import org.springframework.web.bind.annotation.RestController

@SpringBootApplication
class DemoApplication

fun main(args: Array<String>) {
    runApplication<DemoApplication>(*args)
}

@RestController
class HelloController {
    @GetMapping("/")
    fun hello(): String {
        return "Hello, Spring Boot!"
    }
}
```

### Ktor
#### 概要
JetBrains 製の Kotlin 向けフレームワーク。  
軽量で拡張性が高く、シンプルな設計が魅力です。マイクロサービスや小規模～中規模の API をサクッと作成したい場合に向いています。

#### 特徴
- 軽量で、必要な機能のみプラグインとして導入していく設計
- コルーチンとの親和性が高く、ノンブロッキング I/O を活かせる
- DSL を使ってルーティングなどを宣言的に書ける

### サンプルコード
```kotlin
import io.ktor.application.*
import io.ktor.http.*
import io.ktor.response.*
import io.ktor.routing.*
import io.ktor.server.engine.*
import io.ktor.server.netty.*
import io.ktor.features.*

// Ktor 2.x なら io.ktor.server.plugins.* になるなど、バージョンによってパッケージが異なります
fun main() {
    embeddedServer(Netty, port = 8080) {
        install(CallLogging)  // ログ機能追加（任意）
        routing {
            get("/") {
                call.respondText("Hello, Ktor!", ContentType.Text.Plain)
            }
        }
    }.start(wait = true)
}
```

## 5. データベース連携
Kotlin でのデータベース連携も Java と同じように行います。代表的な方法としては以下があります。 
### JPA/Hibernate
ORM（Object Relational Mapping）を使ってオブジェクトとテーブルをマッピング。Spring Data JPA などと組み合わせると生産性が高いです。

### Exposed
JetBrains 製の Kotlin 向けのデータベースフレームワーク。タイプセーフな DSL が特徴で、SQL を Kotlin で書きやすくしてくれます。

### MyBatis
Java でもおなじみの SQL マッピングフレームワーク。Kotlin 用プラグインも存在しており、XML ベースのマッピング管理にも対応しています。

## 6. 非同期処理（Coroutines）
Kotlin の強みのひとつであるコルーチンを利用することで、簡潔に非同期・並行処理を書くことができます。  
特に Ktor ではこのコルーチン機能を活かしたノンブロッキングな API サーバの実装が可能です。  
以下のようなメリットがあります。
- スレッドよりも軽量なコルーチンを多量に起動できるため、高スループットが期待できる
- async/await といったシンプルな構文で非同期処理を扱える
- サスペンド関数(suspend function)を使うことで、ノンブロッキング I/O を書きやすい

## 7. テスト・CI/CD・クラウド連携
バックエンド開発ではテストやデプロイ戦略も重要です。  
Kotlin でも JUnit や TestNG のほか、Kotest (旧 Spek) など Kotlin 向けのテスティングフレームワークが利用できます。  
また、GitHub Actions や Jenkins などの CI/CD パイプラインでビルド～テスト～デプロイを自動化することも可能です。  
クラウド連携においても Spring Boot や Ktor は人気が高く、Heroku や AWS、GCP へのデプロイ例は数多く紹介されています。

## 8. 学習リソース
- [Kotlin 公式ドキュメント](https://kotlinlang.org/docs/home.html)
- [Spring Boot 公式ドキュメント](https://spring.io/projects/spring-boot)
- [Ktor 公式ドキュメント](https://ktor.io/docs/)

## 9. まとめ
Kotlin は Android 開発はもちろん、サーバサイドでも高い生産性とモダンな設計を実現できる有力な選択肢です。  
既存の Java 環境を活かしながら Kotlin の新機能を取り入れることもできるため、段階的に導入するのもスムーズです。  
