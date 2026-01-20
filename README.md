# Pomodoro App

AWS Amplify Gen2 + Next.js 14 で構築する Pomodoro タイマーアプリ

## 機能概要

- Google アカウントでのユーザー認証
- Pomodoro タイマー（25分作業 + 休憩）
- 完了した Pomodoro の集計・履歴表示
- タイマー設定のカスタマイズ
- Google Calendar 連携

## 技術スタック

| カテゴリ | 技術 |
|----------|------|
| フロントエンド | Next.js 14 (App Router), TypeScript, Tailwind CSS |
| バックエンド | AWS Amplify Gen2 (AppSync, DynamoDB, Cognito) |
| 認証 | Amazon Cognito + Google OAuth |
| UI | Amplify UI React |

## 必要な環境

- Node.js 24.x (LTS)
- npm 10.x
- AWS CLI
- mise（Node.js バージョン管理）

## セットアップ手順

### 1. 事前準備

#### AWS CLI の設定確認

```bash
aws sts get-caller-identity
```

未設定の場合は以下を実行：

```bash
aws configure
```

#### Google Cloud Console の設定

1. [Google Cloud Console](https://console.cloud.google.com/) でプロジェクト作成
2. OAuth 同意画面を設定
3. OAuth クライアント ID を作成（ウェブアプリケーション）
4. 以下の情報を控えておく：
    - クライアント ID
    - クライアントシークレット

### 2. プロジェクトのクローン

```bash
git clone https://github.com/k-taiga/amplify-pomodoro-app
```

### 3. Node.js バージョン設定

```bash
# mise で Node.js をインストール & 有効化
mise use node@24

# バージョン確認
node -v  # v24.x.x
```

### 4. 依存パッケージのインストール

```bash
npm install
```

### 5. 環境変数の設定

```bash
cp .env.example .env
```

#### .env

```env
GOOGLE_CLIENT_ID=your-google-client-id
GOOGLE_CLIENT_SECRET=your-google-client-secret
```
## 6. Next.js プロジェクト作成

```bash
npx create-next-app@latest . --typescript --tailwind --eslint --app --src-dir --import-alias "@/*"
```

## 7. Amplify パッケージ追加
```bash
npm install aws-amplify @aws-amplify/ui-react
npm install -D @aws-amplify/backend @aws-amplify/backend-cli
```

### 8. Amplify Sandbox の起動

```bash
npx ampx sandbox
```

初回起動時は AWS リソースの作成に数分かかります。

### 9. 開発サーバーの起動

別ターミナルで実行：

```bash
npm run dev
```

http://localhost:3000 にアクセス

## ディレクトリ構成

```
amplify-pomodoro-app/
├── amplify/                 # Amplify Gen2 バックエンド
│   ├── auth/
│   │   └── resource.ts     # 認証設定
│   ├── data/
│   │   └── resource.ts     # データスキーマ
│   └── backend.ts
├── src/
│   ├── app/                # Next.js App Router
│   ├── components/         # React コンポーネント
│   ├── hooks/              # カスタムフック
│   └── lib/                # ユーティリティ
├── .mise.toml              # Node.js バージョン管理
└── README.md
```

## 開発コマンド

| コマンド | 説明 |
|----------|------|
| `npm run dev` | 開発サーバー起動 |
| `npm run build` | ビルド |
| `npm run lint` | Lint 実行 |
| `npx ampx sandbox` | Amplify Sandbox 起動 |
| `npx ampx generate graphql-client-code` | GraphQL 型生成 |