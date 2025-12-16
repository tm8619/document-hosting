# Getting Started

このガイドでは、Document Hosting プロジェクトの始め方を説明します。

## 前提条件

始める前に、以下のツールがインストールされていることを確認してください：

- Python 3.8 以上
- pip（Python パッケージマネージャー）
- Git
- テキストエディタ（VS Code 推奨）

## インストール

### 1. リポジトリのクローン

```bash
git clone https://github.com/tm8619/document-hosting.git
cd document-hosting
```

### 2. 依存パッケージのインストール

```bash
pip install -r requirements.txt
```

### 3. ローカルサーバーの起動

```bash
mkdocs serve
```

ブラウザで `http://127.0.0.1:8000` にアクセスすると、ドキュメントサイトが表示されます。

## プロジェクト構造

```
document-hosting/
├── docs/               # ドキュメントファイル
│   ├── index.md       # トップページ
│   ├── getting-started.md
│   └── usage.md
├── mkdocs.yml         # MkDocs設定ファイル
├── requirements.txt   # Python依存パッケージ
└── README.md         # プロジェクト概要
```

## ドキュメントの編集

1. `docs/` フォルダ内の Markdown ファイルを編集
2. 保存すると自動的にブラウザが更新されます（開発サーバー起動時）
3. 新しいページを追加する場合は `mkdocs.yml` の `nav` セクションを更新

## 次のステップ

- [Usage](usage.md) - 詳細な使用方法を確認
- ドキュメントをカスタマイズ
- Cloudflare Pages へのデプロイ

## Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/tm8619/document-hosting.git
   cd document-hosting
   ```

2. Install the dependencies:

   ```bash
   pip install -r requirements.txt
   ```

## Running Locally

To preview the documentation locally, run:

```bash
mkdocs serve
```

Then open your browser and navigate to `http://127.0.0.1:8000`.

## Building the Documentation

To build the static site, run:

```bash
mkdocs build
```

This will create a `site/` directory containing the static HTML files.

## Next Steps

- Read the [Usage](usage.md) guide for more detailed information
