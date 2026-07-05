# NAMASTE TOOLS

インド駐在者とその家族のための便利Webアプリ集ポートフォリオサイトです。
すべて静的な1枚の `index.html` で構成されており、ビルド不要でそのまま GitHub Pages に公開できます。

**公開URL:** https://narindia.github.io/namaste-tools/

## 構成

```
.
├── index.html   ページ本体(HTML / CSS / JS すべて含む)
├── img/         写真素材(hero, contact, about, 各アプリのキャプチャ写真)
└── README.md    このファイル
```

### img/ フォルダの内訳

| ファイル               | 用途                                   |
|------------------------|----------------------------------------|
| `hero.jpg`             | トップのヒーロー画像(アディヨギ像)     |
| `contact.jpg`          | 一番下の CONTACT セクション背景         |
| `about.jpg`            | ABOUT セクションの写真                  |
| `app-money.jpg`        | 「INR⇔JPY 為替換算」の背景写真          |
| `app-language.jpg`     | 「カンナダ語学習アプリ」の背景写真       |
| `app-health.jpg`       | 「病院サポートアプリ」の背景写真         |

## ローカルでの確認方法

```bash
python3 -m http.server 8000
# http://localhost:8000 をブラウザで開く
```

## メンテナンス手順

### 1. アプリを追加する

`index.html` 内の `<script>` にある `apps` 配列に、オブジェクトを1つ追加するだけです。

```js
const apps = [
  {
    category: "MONEY",           // カテゴリ名(英字・大文字)
    title: "INR⇔JPY 為替換算",     // アプリ名
    desc: "説明文...",            // 紹介文
    url: "https://narindia.github.io/inr-jpy", // リンク先(未公開なら "#")
    caption: "PAYING BY UPI — FISH MARKET, BENGALURU", // 背景写真の英字キャプション
    isNew: false,                 // true にすると「NEW」バッジが付く
    image: "img/app-money.jpg",   // 背景写真のパス(空文字ならプレースホルダー)
    thumb: ""                     // アプリのスクリーンショット(任意、img/に配置してパス指定)
  },
  // ↓ここに新しいオブジェクトを追加
];
```

配列に追加するだけで、トップページの APPS セクションに自動的にバンドが1つ増えます。

### 2. 写真を差し替える・追加する

1. 新しい写真を `img/` フォルダに追加する(ファイル名は `わかりやすい英語名.jpg` 推奨)
2. `index.html` 内の該当箇所(`--hero-img`、`--contact-img`、`<img src="img/about.jpg">`、または `apps` 配列の `image` / `thumb`)のパスを新しいファイル名に書き換える

**注意:** 写真は base64 埋め込みにせず、必ず `img/` フォルダに画像ファイルとして置き、`index.html` からは相対パスで参照すること。HTML ファイルが肥大化するのを防ぐため。

### 3. 公開(デプロイ)

`main` ブランチに push するだけで、GitHub Pages が自動的に再ビルド・公開します(Settings → Pages で `main` ブランチ / ルートディレクトリを Source に設定している場合)。

```bash
git add .
git commit -m "変更内容"
git push origin main
```

### 4. 新しい単体アプリ(サブアプリ)を追加する場合

`inr-jpy` のような個別アプリは別リポジトリ(例: `narindia/inr-jpy`)として作成し、GitHub Pages で `https://narindia.github.io/<リポジトリ名>` に公開した上で、このサイトの `apps` 配列の `url` にリンクを追加してください。
