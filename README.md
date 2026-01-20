# Pomodoro App

AWS Amplify Gen2 + Vite + React で構築する Pomodoro タイマーアプリ

<img width="3786" height="2300" alt="CleanShot 2026-01-20 at 14 39 48@2x" src="https://github.com/user-attachments/assets/deb8c48b-6d84-4d79-81c5-bed5c03e4860" />


## 機能概要

- Google アカウントでのユーザー認証
- Pomodoro タイマー（25分作業 + 休憩）
- 完了した Pomodoro の集計・履歴表示
- タイマー設定のカスタマイズ
- Google Calendar 連携

## 技術スタック

| カテゴリ | 技術 |
|----------|------|
| フロントエンド | Vite, React 19, TypeScript, Tailwind CSS |
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

### 4. 依存関係のインストール

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

### 6. Amplify バックエンドの初期化

```bash
npm create amplify@latest
```

### 7. Amplify Sandbox の起動

```bash
npx ampx sandbox
```

初回起動時は AWS リソースの作成に数分かかります。

### 8. 開発サーバーの起動

別ターミナルで実行：

```bash
npm run dev
```

http://localhost:5173 にアクセス

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
│   ├── components/         # React コンポーネント
│   ├── hooks/              # カスタムフック
│   ├── lib/                # ユーティリティ
│   ├── App.tsx             # メインコンポーネント
│   └── main.tsx            # エントリーポイント
├── .mise.toml              # Node.js バージョン管理
└── README.md
```

## 開発コマンド

| コマンド | 説明 |
|----------|------|
| `npm run dev` | 開発サーバー起動（localhost:5173） |
| `npm run build` | ビルド |
| `npm run lint` | Lint 実行 |
| `npm run preview` | ビルド結果のプレビュー |
| `npx ampx sandbox` | Amplify Sandbox 起動 |
| `npx ampx generate graphql-client-code` | GraphQL 型生成 |
