# threads-image-relay

Threads API へ投稿する画像の**受け渡し専用**の置き場。

Threads API は画像ファイルを直接受け取らず、
公開URLを Meta 側が cURL しに来る仕様のため、この置き場が要る。

> We will cURL your image using the URL provided so it must be on a public server.
> — [Threads Posts / Meta for Developers](https://developers.facebook.com/documentation/threads/posts)

## 決めごと

- **投稿に使う画像だけ**を、投稿の直前に置く。写真の保管庫やない（原本は別にある）
- 投稿が済んだら消す
- **販売前・未公開の物件は置かん**（ここは全世界から見える）

## 中身

| ファイル | 用途 |
|---|---|
| `test.png` / `test.jpg` | 疎通確認用の無地画像。物件の写真やない |
