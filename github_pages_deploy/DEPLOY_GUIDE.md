# GitHub Pagesデプロイ手順書

このガイドでは、ビルド済みのプロジェクトをGitHub Pagesで公開する手順を説明します。

## プロジェクト概要

このプロジェクトは、React + Vite + TypeScript + Tailwind CSSで構築されたWebサイトです。すでにビルド済みの静的ファイルが含まれており、GitHub Pagesで直接公開できる状態になっています。

## 含まれるファイル

```
github_pages_deploy/
├── .git/                    # Gitリポジトリ（初期化済み）
├── .nojekyll               # GitHub PagesでJekyll処理を無効化
├── index.html              # メインHTMLファイル
├── robots.txt              # 検索エンジン向けの設定
├── placeholder.svg         # プレースホルダー画像
└── assets/                 # 静的アセット（CSS、JS、画像）
    ├── index-BNmvFIjK.css
    ├── index-C1q9DHAL.js
    ├── contact-Cf7fxVmI.jpg
    ├── hero-home-pSaeqfyS.jpg
    ├── office-overview-BeoKtHr9.jpg
    ├── pricing-CxYns8Ue.jpg
    ├── representative-CD5DxqLg.jpg
    ├── service-icon-1-DGLtSfZV.jpg
    ├── service-icon-2-CdBZQeIx.jpg
    ├── service-icon-3-DLxVbQ3N.jpg
    └── services-C4selua5.jpg
```

## デプロイ手順

### 1. GitHubでリポジトリを作成

1. [GitHub](https://github.com)にログイン
2. 右上の「+」ボタンから「New repository」を選択
3. リポジトリ名を入力（例：`my-website`）
4. 「Public」を選択（GitHub Pagesは無料プランではPublicリポジトリのみ対応）
5. **「Initialize this repository with a README」はチェックしない**
6. 「Create repository」をクリック

### 2. ローカルリポジトリをGitHubにプッシュ

ターミナルで以下のコマンドを実行します：

```bash
# デプロイ用ディレクトリに移動
cd github_pages_deploy

# GitHubリポジトリをリモートとして追加（YOUR_USERNAMEとREPO_NAMEを置き換える）
git remote add origin https://github.com/YOUR_USERNAME/REPO_NAME.git

# mainブランチにプッシュ
git push -u origin main
```

**注意**: `YOUR_USERNAME`はあなたのGitHubユーザー名、`REPO_NAME`は作成したリポジトリ名に置き換えてください。

### 3. GitHub Pagesを有効化

1. GitHubのリポジトリページに移動
2. 「Settings」タブをクリック
3. 左サイドバーの「Pages」をクリック
4. 「Source」セクションで以下を設定：
   - **Branch**: `main`
   - **Folder**: `/ (root)`
5. 「Save」をクリック

### 4. デプロイ完了を確認

数分後、GitHub Pagesのセクションに以下のようなメッセージが表示されます：

```
Your site is live at https://YOUR_USERNAME.github.io/REPO_NAME/
```

このURLをクリックして、サイトが正しく表示されることを確認してください。

## トラブルシューティング

### 404エラーが表示される

- GitHub Pagesの設定が正しいか確認
- ブランチが`main`で、フォルダが`/ (root)`になっているか確認
- 数分待ってから再度アクセス

### CSSやJavaScriptが読み込まれない

- `.nojekyll`ファイルが含まれているか確認
- ブラウザのキャッシュをクリアして再読み込み

### カスタムドメインを使用したい

1. GitHub Pagesの設定ページで「Custom domain」にドメイン名を入力
2. DNSプロバイダーでCNAMEレコードを設定
3. 詳細は[GitHub公式ドキュメント](https://docs.github.com/ja/pages/configuring-a-custom-domain-for-your-github-pages-site)を参照

## 更新方法

サイトを更新する場合は、元のプロジェクトを再ビルドして、以下の手順で更新します：

```bash
# 元のプロジェクトでビルド
cd lovable-project
pnpm install
pnpm build

# ビルド結果をデプロイディレクトリにコピー
rm -rf ../github_pages_deploy/assets
cp -r dist/* ../github_pages_deploy/

# 変更をコミットしてプッシュ
cd ../github_pages_deploy
git add .
git commit -m "Update site"
git push
```

## 参考リンク

- [GitHub Pages公式ドキュメント](https://docs.github.com/ja/pages)
- [Viteデプロイガイド](https://vitejs.dev/guide/static-deploy.html)
- [React Router on GitHub Pages](https://create-react-app.dev/docs/deployment/#github-pages)

---

**作成日**: 2025年11月14日
