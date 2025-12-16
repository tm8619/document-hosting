# Usage Guide

Document Hosting の詳細な使用方法を説明します。

## ドキュメントの作成

### 新しいページの追加

1. `docs/` フォルダに新しい Markdown ファイルを作成

```bash
touch docs/new-page.md
```

2. `mkdocs.yml` のナビゲーションに追加

```yaml
nav:
  - Home: index.md
  - Getting Started: getting-started.md
  - Usage: usage.md
  - New Page: new-page.md # 追加
```

### Markdown の基本

#### 見出し

```markdown
# H1 見出し

## H2 見出し

### H3 見出し
```

#### リスト

```markdown
- アイテム 1
- アイテム 2
  - サブアイテム
```

#### コードブロック

````markdown
```python
def hello():
    print("Hello, World!")
```
````

#### リンク

```markdown
[リンクテキスト](https://example.com)
```

#### 画像

```markdown
![代替テキスト](images/example.png)
```

## 高度な機能

### アドモニション（警告ボックス）

!!! note "注意"
これは注意事項です。

!!! warning "警告"
重要な警告メッセージです。

!!! tip "ヒント"
便利なヒントです。

### コードのハイライト

```python
def calculate_sum(a: int, b: int) -> int:
    """2つの数値の合計を計算します。"""
    return a + b

result = calculate_sum(5, 3)
print(f"Result: {result}")
```

```javascript
function greet(name) {
  console.log(`Hello, ${name}!`);
}

greet('World');
```

### テーブル

| 機能               | 説明            | ステータス  |
| ------------------ | --------------- | ----------- |
| ドキュメント作成   | Markdown で記述 | ✅ 利用可能 |
| 検索機能           | 全文検索対応    | ✅ 利用可能 |
| テーマカスタマイズ | Material theme  | ✅ 利用可能 |

## ビルドとデプロイ

### ローカルビルド

```bash
mkdocs build
```

これにより `site/` フォルダに静的 HTML ファイルが生成されます。

### Cloudflare Pages へのデプロイ

詳細は README.md を参照してください。

## トラブルシューティング

### よくある問題

**Q: ページが表示されない**  
A: `mkdocs.yml` の `nav` セクションにページが追加されているか確認してください。

**Q: 画像が表示されない**  
A: 画像パスが正しいか、`docs/` フォルダ内に画像があるか確認してください。

**Q: スタイルが適用されない**  
A: `mkdocs serve` を再起動してみてください。

## さらに学ぶ

- [MkDocs 公式ドキュメント](https://www.mkdocs.org/)
- [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)
- [Markdown Guide](https://www.markdownguide.org/)

## Configuration

The MkDocs configuration is stored in `mkdocs.yml`. You can customize:

- Site name and description
- Navigation structure
- Theme settings
- Markdown extensions

## Deploying to GitHub Pages

To deploy the documentation to GitHub Pages, run:

```bash
mkdocs gh-deploy
```

This will build the documentation and push it to the `gh-pages` branch.

## Customizing the Theme

The project uses the Material theme. You can customize the theme by modifying the `theme` section in `mkdocs.yml`:

```yaml
theme:
  name: material
  palette:
    primary: indigo
    accent: indigo
```

See the [Material for MkDocs documentation](https://squidfunk.github.io/mkdocs-material/) for more customization options.
