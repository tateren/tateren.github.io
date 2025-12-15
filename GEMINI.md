# プロジェクト概要

このプロジェクトは、Reactベースの静的サイトジェネレーターである**Gatsby.js**を使用して構築された個人ブログ「tateren.github.io」です。

## 技術的特徴

- **コンテンツ管理**: ブログ記事は**Markdown**形式で記述され、`content/blog`ディレクトリに保存されます。
- **Gatsby.js**:
  - `gatsby-transformer-remark`を利用してMarkdownをHTMLに変換します。
  - `gatsby-remark-prismjs`により、コードブロックのシンタックスハイライト機能を提供します。
- **画像最適化**: `gatsby-plugin-image`や`gatsby-plugin-sharp`を用いて、画像の読み込み速度や表示を最適化します。
- **SEOとフィード**:
  - `gatsby-plugin-sitemap`でサイトマップを自動生成します。
  - `gatsby-plugin-google-analytics`を導入し、アクセス解析が可能です。
  - `gatsby-plugin-feed`により、RSSフィード (`/rss.xml`) を生成します。
- **デプロイ**: `package.json`のスクリプトから`gh-pages`ライブラリを使用していることが分かり、**GitHub Pages**にデプロイされる構成になっています。

---

ご要望に基づき、この概要は日本語で記述されています。
