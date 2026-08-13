# threads-image-relay

Threads へ投稿する画像の**受け渡し専用**の置き場。
[threads-auto](https://github.com/kawaichika-tech/threads-auto) が自動で出し入れする。

## なんでこれが要るんか

Threads API は画像ファイルを受け取ってくれへん。
**公開URLを渡すと、Meta 側がそこへ取りに来る**という仕様やから、
「Meta から見える場所」が1個だけ要る。

> We will cURL your image using the URL provided so it must be on a public server.
> — [Threads Posts / Meta for Developers](https://developers.facebook.com/documentation/threads/posts)

## 実測でわかったこと（2026-08-13）

同じ画像でも、**どう配られとるか**で通ったり弾かれたりする。

| 置き場 | Content-Type | 結果 |
|---|---|---|
| Chatwork の署名付きURL | **(無し)** + `attachment` + `.dat` | ❌ 400 `error_subcode 2207052` |
| **GitHub (raw)** | **`image/jpeg`** | ✅ `FINISHED` |

中身は同じJPEGでも、**Meta は札（Content-Type）を見て門前払いする**。
せやから Google Drive・Chatwork・その手の「人がダウンロードするための置き場」は使えん。

## 決めごと

- **投稿に使う画像だけ**を、投稿の直前に置く。**写真の保管庫やない**
  （原本は Google 共有ドライブの `◎分譲（RASHIE ）/インスタ用写真`）
- 投稿が済んだら**消す**
- 🔴 **販売前・未公開の物件は置かん。** ここは全世界から見える
- JPEG / PNG のみ・8MB まで（Threads 側の制限）
