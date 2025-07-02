# LiveTable API 仕様書

LiveTable API サーバーの OpenAPI 3.0 仕様書です。

## 概要

LiveTable は YouTube ライブ配信タイムテーブルアプリケーションのポリレポ構成です：

- **フロントエンド**: Next.js アプリケーション（別リポジトリ）
- **バックエンド**: API サーバー（別リポジトリ）
- **API 仕様**: このリポジトリ - 共有仕様書

## API 仕様書

LiveTable API サーバーの全エンドポイント、リクエスト/レスポンススキーマ、認証要件を OpenAPI 3.0 形式で定義しています。

### 主な機能

- NextAuth による JWT Bearer トークン認証
- Google OAuth 連携によるユーザー管理
- YouTube チャンネル購読管理
- ライブ配信・動画データエンドポイント
- 包括的なエラーハンドリング

### エンドポイント概要

- **ユーザー管理**: ユーザー検索、Google OAuth データ、購読情報
- **チャンネル管理**: チャンネル情報と一括操作
- **動画管理**: ライブ配信、配信予定、動画詳細

## ファイル構成

- `openapi.yaml` - 完全な OpenAPI 3.0 仕様書
- `examples/` - リクエスト/レスポンス例
- `docs/` - 生成されたドキュメント
- `.github/workflows/` - CI/CD パイプライン

## ドキュメント

### 🌐 オンラインドキュメント

**[📖 API ドキュメントを見る](https://hikuohiku.github.io/livetable-api-spec/)**

GitHub Pages で自動生成・更新されるドキュメントサイトです。

### 📋 利用方法

#### フロントエンド開発者向け

この仕様書を参照して API クライアントサービスを実装してください。

#### バックエンド開発者向け

この仕様書に従って API サーバーを実装し、フロントエンドとの互換性を確保してください。

## 開発

### 前提条件

- Node.js (latest)
- pnpm

### セットアップ

```bash
# リポジトリをクローン
git clone https://github.com/hikuohiku/livetable-api-spec.git
cd livetable-api-spec
```

### 利用可能なコマンド

```bash
# OpenAPI 仕様書の検証
pnpm validate

# ドキュメントの生成
pnpm build

# ローカルでドキュメントをプレビュー
pnpm serve
```

### ローカル開発

```bash
# 仕様書の検証
pnpm validate

# ドキュメントをローカルでプレビュー（ホットリロード対応）
pnpm serve
```

## CI/CD

### 自動化された処理

- **CI**: プルリクエスト・プッシュ時に仕様書の検証
- **CD**: `main` ブランチの `openapi.yaml` 変更時に GitHub Pages へ自動デプロイ

### ローカルテスト

```bash
# GitHub Actions をローカルで実行（要 act）
act --container-architecture linux/amd64 -W .github/workflows/ci.yml
```

## 開発ワークフロー

1. **仕様変更**: `openapi.yaml` を最初に更新
2. **レビュー**: フロントエンド・バックエンド両チームによるレビュー
3. **実装**: 更新された仕様書に基づいて実装
4. **テスト**: 実装が仕様書と一致することを確認

## バージョニング

このプロジェクトはセマンティックバージョニングに従います：

- **Major**: 既存エンドポイントへの破壊的変更
- **Minor**: 新エンドポイントまたは後方互換性のある変更
- **Patch**: ドキュメント修正、説明の改善

## 統合

### フロントエンド（Next.js）との統合

この仕様書から TypeScript 型定義と API クライアントを自動生成できます。

### バックエンドとの統合

この仕様書を使用してバックエンドの検証とルート生成が可能です。

## コントリビュート

1. フィーチャーブランチを作成
2. OpenAPI 仕様書を更新
3. 新しいエンドポイントを追加する場合は例も追加
4. 必要に応じて README を更新
5. 両チームによるレビューを受けてプルリクエストを作成

## ライセンス

MIT License