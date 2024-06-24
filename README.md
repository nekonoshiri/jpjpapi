# JPJPAPI

JPJPAPI (Japanese JSON POST API) は、

- 日本語
- JSON
- HTTP の POST メソッド

を用いた API 設計スタイルです。

## 注意

実験的な設計スタイルであり、実用性があるかどうかはわかっていません。

このスタイルを採用することで発生した問題についての責任は負いかねます。

## 全般

- 通信プロトコルは HTTP の バージョン 1.1 (HTTP/1.1) 以上を使用します（必要に応じて暗号化を行います）

## リクエスト

- HTTP メソッドは POST を使用します
- パスは、API の機能を表す日本語を使用します（必要に応じてパーセントエンコーディングを行います）
- パスパラメータ・クエリパラメータは使用しません
- リクエストボディは JSON 形式を使用します (`Content-Type: application/json`)

例：

```http
POST /%E3%83%A6%E3%83%BC%E3%82%B6%E3%83%BC%E7%99%BB%E9%8C%B2 HTTP/1.1
Content-Type: application/json

{
  "名前": "山田太郎",
  "メールアドレス": "taro@example.com"
}
```

Note. `%E3%83%A6%E3%83%BC%E3%82%B6%E3%83%BC%E7%99%BB%E9%8C%B2` は `ユーザー登録` のパーセントエンコーディング

## 正常レスポンス

- ステータスコードは 200 を使用します
- レスポンスボディは JSON 形式を使用します (`Content-Type: application/json`)

例：

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "ユーザーID": 10
}
```

## エラーレスポンス

- ステータスコードはクライアントエラーの場合は 400、サーバーエラーの場合は 500 を使用します
- レスポンスボディは JSON 形式を使用します (`Content-Type: application/json`)

例：

```http
HTTP/1.1 400 Bad Request
Content-Type: application/json

{
  "コード": "不正なメールアドレス",
  "メッセージ": "メールアドレスが不正です"
}
```
