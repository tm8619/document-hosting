# Document Hosting

MkDocs で構築されたドキュメントサイトです。Cloudflare Pages にデプロイして、高速なグローバル CDN 経由で配信できます。

## 機能

- 📝 Markdown ベースのドキュメント作成
- 🎨 Material for MkDocs テーマ
- 🚀 Cloudflare Pages への自動デプロイ
- 🔍 全文検索機能
- 📱 レスポンシブデザイン

## クイックスタート

### 1. 依存関係のインストール

```bash
pip install -r requirements.txt
```

### 2. 開発サーバーの起動

```bash
mkdocs serve
```

ブラウザで http://127.0.0.1:8000 を開いてください。

## ビルド

静的 HTML ファイルを生成するには：

```bash
mkdocs build
```

生成されたファイルは `site/` ディレクトリに保存されます。

## Cloudflare Pages へのデプロイ

### 方法 1: GitHub リポジトリと連携（推奨）

1. **GitHub にプッシュ**

   ```bash
   git add .
   git commit -m "Initial commit"
   git push origin main
   ```

2. **Cloudflare Pages でプロジェクト作成**

   - [Cloudflare Dashboard](https://dash.cloudflare.com/)にログイン
   - `Workers & Pages` → `Create application` → `Pages` → `Connect to Git`
   - GitHub リポジトリを選択

3. **ビルド設定**

   - **Build command**: `pip install -r requirements.txt && mkdocs build`
   - **Build output directory**: `site`
   - **Environment variables** (必要に応じて):
     - `PYTHON_VERSION`: `3.11`

4. **デプロイ**

   - `Save and Deploy` をクリック
   - 自動的にビルドとデプロイが開始されます

5. **自動デプロイ**
   - 以降、`main` ブランチへのプッシュで自動デプロイされます

### 方法 2: Wrangler を使用（CLI）

```bash
# Wranglerのインストール
npm install -g wrangler

# ビルド
mkdocs build

# デプロイ
npx wrangler pages deploy site --project-name=your-project-name
```

### 方法 3: 手動アップロード

1. `mkdocs build` でサイトをビルド
2. Cloudflare Dashboard で `Workers & Pages` → `Create application` → `Pages` → `Upload assets`
3. `site/` フォルダの内容をアップロード

## カスタムドメインの設定

Cloudflare Pages のプロジェクト設定から:

1. `Custom domains` タブを開く
2. `Set up a custom domain` をクリック
3. ドメイン名を入力して設定

## プロジェクト構造

```
document-hosting/
├── docs/               # ドキュメントファイル
│   ├── index.md       # トップページ
│   ├── getting-started.md
│   └── usage.md
├── mkdocs.yml         # MkDocs設定ファイル
├── requirements.txt   # Python依存パッケージ
├── .gitignore        # Git無視ファイル
├── .node-version     # Node.jsバージョン指定
└── README.md         # このファイル
```

## 設定のカスタマイズ

[mkdocs.yml](mkdocs.yml) を編集してサイトをカスタマイズできます：

- サイト名と説明
- ナビゲーション構造
- テーマ設定
- Markdown 拡張機能

## トラブルシューティング

### ビルドエラーが発生する場合

```bash
# 依存関係を再インストール
pip install --upgrade -r requirements.txt

# キャッシュをクリア
rm -rf site/
mkdocs build
```

### Cloudflare でビルドが失敗する場合

- ビルドコマンドを確認: `pip install -r requirements.txt && mkdocs build`
- 出力ディレクトリを確認: `site`
- Python 環境変数を設定: `PYTHON_VERSION=3.11`

## 参考リンク

- [MkDocs 公式ドキュメント](https://www.mkdocs.org/)
- [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)
- [Cloudflare Pages Docs](https://developers.cloudflare.com/pages/)

## ライセンス

MIT License
