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

#### ステップ 1: GitHub にプッシュ

```bash
git add .
git commit -m "Initial commit"
git push origin main
```

#### ステップ 2: Cloudflare Pages でプロジェクト作成

1. [Cloudflare Dashboard](https://dash.cloudflare.com/) にログイン
2. 左サイドバーから **Workers & Pages** をクリック
3. 右上の **Create application** ボタンをクリック
4. **Pages** タブを選択
5. **Connect to Git** をクリック

#### ステップ 3: リポジトリの選択

1. **GitHub** を選択（初回は GitHub との連携を許可）
2. リポジトリ一覧から `document-hosting` を選択
3. **Begin setup** をクリック

#### ステップ 4: ビルド設定（重要！）

**Set up builds and deployments** 画面で以下のように設定：

1. **Project name**: `document-hosting`（任意の名前で OK）

2. **Build command**:

   ```
   pip install -r requirements.txt && mkdocs build
   ```

3. **Deploy command**:

   - 空にできない場合は、以下を入力してください：

   ```
   echo "Build completed"
   ```

   - これは何もしないダミーコマンドです（Cloudflare が自動でデプロイ処理を行います）

4. **Framework preset** または **Build configuration** があれば:

   - `None` を選択（自動検出させない）

5. **Root directory (optional)**:

   - 空のままで OK（プロジェクトのルートを使用）

6. **Environment variables** を設定（重要）:
   - **Variable name**: `PYTHON_VERSION`
   - **Value**: `3.11`

**チェックボックス**:

- ✅ **Builds for non-production branches** - お好みでチェック

#### ステップ 5: デプロイ

1. **Save and Deploy** ボタンをクリック
2. ビルドが自動的に開始されます（数分かかります）
3. 完了すると `https://document-hosting-xxx.pages.dev` のような URL が発行されます

**もしビルドが失敗した場合**:

1. プロジェクトの **Settings** タブを開く
2. **Builds & deployments** を選択
3. **Build configuration** セクションで:
   - **Build output directory**: `site` を入力
4. **Retry deployment** をクリック

**"Hello World"や 404 エラーが表示される場合**:
これは Build output directory が設定されていないためです。以下の手順で修正：

1. Cloudflare Dashboard でプロジェクトを開く
2. **Settings** タブをクリック
3. 左サイドバーから **Builds & deployments** を選択
4. **Build configuration** セクションを探す
5. **Build output directory** の右にある **Edit** または **Configure** をクリック
6. **Build output directory** に `site` と入力
7. **Save** をクリック
8. **Deployments** タブに戻り、最新のデプロイメントの右側にある **...** メニューから **Retry deployment** を選択

これで MkDocs で生成された HTML が正しく表示されます！

#### ステップ 6: 以降の更新

コードを更新して `main` ブランチにプッシュすると、自動的に再デプロイされます：

```bash
git add .
git commit -m "Update documentation"
git push origin main
```

---

### 方法 2: Wrangler CLI を使用（直接デプロイ）

Git を使わず、ローカルから直接デプロイする方法です。

#### ステップ 1: 準備

```bash
# Node.js がインストールされていることを確認
node --version

# Wrangler をインストール（グローバル）
npm install -g wrangler

# Cloudflare にログイン
wrangler login
```

ブラウザが開くので、Cloudflare アカウントでログインして認証してください。

#### ステップ 2: ビルド

```bash
# MkDocs でサイトをビルド
mkdocs build
```

`site/` ディレクトリに HTML ファイルが生成されます。

#### ステップ 3: デプロイ

```bash
# プロジェクト名を指定してデプロイ（初回）
npx wrangler pages deploy site --project-name=document-hosting
```

**重要**:

- `site` はデプロイするディレクトリ名（mkdocs が生成したフォルダ）
- `--project-name=document-hosting` は Cloudflare 上のプロジェクト名（任意）

初回実行時に確認メッセージが表示されたら `y` を入力してください。

#### ステップ 4: 以降の更新

```bash
# ビルドしてデプロイ（1コマンドで）
mkdocs build && npx wrangler pages deploy site --project-name=document-hosting
```

---

### 方法 3: 手動アップロード（Git や CLI を使わない）

#### ステップ 1: ビルド

```bash
mkdocs build
```

#### ステップ 2: アップロード

1. [Cloudflare Dashboard](https://dash.cloudflare.com/) にログイン
2. **Workers & Pages** → **Create application**
3. **Pages** タブ → **Upload assets** を選択
4. プロジェクト名を入力（例: `document-hosting`）
5. `site/` フォルダ内のファイルをドラッグ&ドロップ
   - **注意**: `site` フォルダそのものではなく、`site` の中身をアップロード
6. **Deploy site** をクリック

---

## デプロイの確認

デプロイが完了すると、以下のような URL が発行されます：

```
https://document-hosting-xxx.pages.dev
```

ブラウザでアクセスして、サイトが表示されることを確認してください。

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
