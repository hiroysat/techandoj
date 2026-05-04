# Tech and Doj — ブログ管理引き継ぎ

## 概要

- **サイト**: https://hiroysat.github.io/techandoj/
- **構成**: Hugo + GitHub Pages（テーマ: PaperMod）
- **デプロイ**: `main` ブランチへのpushで GitHub Actions が自動ビルド・公開

---

## ディレクトリ構成（重要ファイル）

```
techandoj/
├── hugo.toml                          # サイト設定・ナビメニュー
├── content/posts/                     # 記事ファイル
│   ├── black-company-to-it-01.md     # 公開済み（1記事目）
│   └── black-company-to-it-02.md     # 公開済み（2記事目）
├── layouts/partials/extend_head.html  # GoatCounter解析タグ
└── .github/workflows/deploy.yml       # GitHub Actionsデプロイ設定
```

---

## 記事の公開フロー

1. 下書きは `draft: true` のまま `content/posts/` に作成・編集する
2. 公開前にレビューを行い、承認を得てから `draft: false` に変更する
3. コミット＆pushすれば GitHub Actions が自動デプロイ（約30秒）
4. 公開済み記事は変更しない

### 記事ファイルの命名規則

```
content/posts/<シリーズ名>-<連番>.md
例: black-company-to-it-03.md
```

### 公開後URL

```
https://hiroysat.github.io/techandoj/posts/<ファイル名（.md除く）>/
例: https://hiroysat.github.io/techandoj/posts/black-company-to-it-02/
```

---

## 記事作成ルール

### 書く前のチェック
「この記事を読んだ人は何を得られるか？」を一文で言えるか確認する。言えなければ切り口を変える。

### 表現
- 具体的な表現を使う（固有名詞、数字、エピソード）
- 個人が特定される情報はNG（実名、第三者が特定できる会社名など）

### 所属企業の扱い
- **Informatica社** → 「2社目の外資系IT企業」
- **Snowflake社（現在）** → 「現在の外資系IT企業」
- 日本オラクルは実名で記載可
- テコンドーの道場名は現時点では伏せる

### 記事構成
- 途中はある程度生々しい表現でよい（読者に刺さるリアリティを優先）
- 締めは箇条書きで「この経験から言えること」として学びを提示する

### タイトル
- 読み手が検索しそうなキーワードを含める
- 「自分の話」ではなく「読み手の疑問・状況」に答える形にする

---

## サイト設定の変更（hugo.toml）

| 項目 | 変更箇所 |
|------|----------|
| トップページの紹介文 | `params.homeInfoParams.Content` |
| ナビゲーションメニュー | `[[menu.main]]` ブロックを追加・削除 |
| サイト説明文（SEO） | `params.description` |

現在のナビメニュー: **キャリア**（weight=10）、**テコンドー**（weight=20）

---

## アクセス解析

- **GoatCounter**: https://techandoj.goatcounter.com/
- ローカル開発サーバー起動時（`hugo server`）はタグが挿入されない（`layouts/partials/extend_head.html` で制御）

---

## 過去のトラブルと対処

### Hugo v0.158.0以降の破壊的変更
- `.Site.IsServer` → `hugo.IsServer` に変更済み（`extend_head.html`）
- `languageCode` → `locale` への移行警告が出るが現時点では動作に影響なし

---

## 下書きファイルの保管場所

```
~/claude-code-projects/blog_drafts/
```

記事を書くときはここに下書きを置き、レビュー後に `content/posts/` へ反映する。
