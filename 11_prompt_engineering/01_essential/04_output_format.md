# 出力形式の指定方法（Output Format Specification）

## 概要

出力形式の指定は、AIの回答を特定のフォーマットで出力させる手法です。Markdown、JSON、XML、YAML、表形式、コードブロックなど、用途に応じた構造化された出力を得ることで、回答の可読性、再利用性、後処理のしやすさが大幅に向上します。

特にMarkdown形式のコードブロック（```）を使った出力指定は、コードやデータを明確に区別でき、コピー&ペーストでそのまま使用できるため、実務で最も重要な手法の一つです。

## 重要度

**⭐ 必須** - 実務でAIを活用する際、ほぼすべてのケースで使用する基本手法

## 使用場面

- コードを生成してもらう時（プログラミング）
- データをJSON/YAML/CSVなどで受け取りたい時
- ドキュメントやレポートを作成する時
- 構造化されたリストや表を作成する時
- 複数の回答を比較可能な形式で受け取りたい時
- APIレスポンスやデータベーススキーマを設計する時
- そのままコピー&ペーストで使いたい時

## 基本パターン

### パターン1: Markdownコードブロック

```
以下の形式で出力してください：

```言語名
[コード内容]
\```
```

### パターン2: 構造化Markdown

```
以下の形式で出力してください：

## セクション1
[内容]

## セクション2
[内容]

### サブセクション
- 項目1
- 項目2
```

### パターン3: JSON形式

```
以下のJSON形式で出力してください：

```json
{
  "key1": "value1",
  "key2": "value2"
}
\```
```

### パターン4: 表形式

```
以下の表形式で出力してください：

| 列1 | 列2 | 列3 |
|-----|-----|-----|
| データ1 | データ2 | データ3 |
```

## 実務例

### 例1: Pythonコードの生成

**プロンプト:**
```
Pythonで、CSVファイルを読み込んで特定の列の平均値を計算する関数を作成してください。

以下の形式で出力してください：

```python
# ファイル名: calculate_average.py
# コードをここに記述
\```

使用例も別のコードブロックで示してください。
```

**期待される出力:**
````
```python
# ファイル名: calculate_average.py
import csv
from typing import List

def calculate_column_average(csv_file: str, column_name: str) -> float:
    """
    CSVファイルから特定の列の平均値を計算する

    Args:
        csv_file: CSVファイルのパス
        column_name: 平均を計算する列名

    Returns:
        列の平均値

    Raises:
        FileNotFoundError: ファイルが見つからない場合
        KeyError: 指定された列が存在しない場合
        ValueError: 数値に変換できない値がある場合
    """
    values: List[float] = []

    with open(csv_file, 'r', encoding='utf-8') as f:
        reader = csv.DictReader(f)

        for row in reader:
            if column_name not in row:
                raise KeyError(f"列 '{column_name}' が見つかりません")

            try:
                values.append(float(row[column_name]))
            except ValueError:
                raise ValueError(f"数値に変換できない値: {row[column_name]}")

    if not values:
        raise ValueError("データが空です")

    return sum(values) / len(values)
```

**使用例:**

```python
# example.py
from calculate_average import calculate_column_average

try:
    # sales.csvの'amount'列の平均を計算
    avg = calculate_column_average('sales.csv', 'amount')
    print(f"平均値: {avg:.2f}")

except FileNotFoundError:
    print("ファイルが見つかりません")
except KeyError as e:
    print(f"エラー: {e}")
except ValueError as e:
    print(f"値のエラー: {e}")
```
````

### 例2: JSON APIレスポンス設計

**プロンプト:**
```
ユーザー情報を取得するREST APIのレスポンス形式を設計してください。
以下の情報を含めてください：
- ユーザーID
- 名前
- メールアドレス
- 登録日
- プロフィール情報（任意）
- アドレス情報（複数可）

以下のJSON形式で出力してください：

```json
{
  // レスポンス構造をここに記述
}
\```

成功時とエラー時の両方のパターンを示してください。
```

**期待される出力:**
````
**成功時のレスポンス:**

```json
{
  "status": "success",
  "data": {
    "user_id": "usr_1234567890",
    "name": {
      "first_name": "太郎",
      "last_name": "山田",
      "display_name": "山田太郎"
    },
    "email": "taro.yamada@example.com",
    "registered_at": "2024-01-15T10:30:00Z",
    "profile": {
      "bio": "ソフトウェアエンジニア",
      "avatar_url": "https://example.com/avatars/usr_1234567890.jpg",
      "website": "https://taro-yamada.com"
    },
    "addresses": [
      {
        "type": "home",
        "postal_code": "100-0001",
        "prefecture": "東京都",
        "city": "千代田区",
        "street": "千代田1-1-1",
        "building": "サンプルビル101",
        "is_default": true
      },
      {
        "type": "work",
        "postal_code": "150-0001",
        "prefecture": "東京都",
        "city": "渋谷区",
        "street": "渋谷2-2-2",
        "building": "オフィスタワー5F",
        "is_default": false
      }
    ],
    "metadata": {
      "last_login": "2024-03-20T15:45:00Z",
      "login_count": 127,
      "email_verified": true
    }
  }
}
```

**エラー時のレスポンス:**

```json
{
  "status": "error",
  "error": {
    "code": "USER_NOT_FOUND",
    "message": "指定されたユーザーが見つかりません",
    "details": {
      "user_id": "usr_9999999999"
    },
    "timestamp": "2024-03-20T16:00:00Z"
  }
}
```

**エラーコード一覧:**

```json
{
  "error_codes": {
    "USER_NOT_FOUND": "ユーザーが存在しない",
    "UNAUTHORIZED": "認証が必要",
    "FORBIDDEN": "アクセス権限がない",
    "INVALID_USER_ID": "ユーザーIDの形式が不正",
    "INTERNAL_SERVER_ERROR": "サーバー内部エラー"
  }
}
```
````

### 例3: Markdown形式のドキュメント

**プロンプト:**
```
新しいWebアプリケーションのREADME.mdを作成してください。
プロジェクト名: TaskMaster
技術スタック: React, TypeScript, Node.js, PostgreSQL

以下の構成で出力してください：

# プロジェクト名
[概要]

## Features
[主な機能]

## Tech Stack
[技術スタック]

## Getting Started
[セットアップ手順]

## Usage
[使い方]

## Contributing
[貢献方法]

## License
[ライセンス]
```

**期待される出力:**
````markdown
# TaskMaster

タスク管理を効率化する、モダンでシンプルなWebアプリケーション。個人からチームまで、あらゆる規模のプロジェクト管理に対応します。

## Features

- ✅ **直感的なタスク管理** - ドラッグ&ドロップで簡単にタスクを整理
- 👥 **リアルタイムコラボレーション** - チームメンバーと即座に同期
- 📊 **進捗の可視化** - ガントチャートとカンバンビューで進捗を一目で把握
- 🔔 **スマート通知** - 重要なタスクと期限をお知らせ
- 🎨 **カスタマイズ可能** - プロジェクトに合わせたワークフローを構築
- 🔒 **セキュア** - エンタープライズグレードのセキュリティ

## Tech Stack

### Frontend
- **React 18** - UIライブラリ
- **TypeScript** - 型安全な開発
- **Tailwind CSS** - ユーティリティファーストCSS
- **React Query** - データフェッチングとキャッシング
- **Zustand** - 状態管理

### Backend
- **Node.js** - ランタイム
- **Express** - Webフレームワーク
- **TypeScript** - 型安全なバックエンド
- **PostgreSQL** - リレーショナルデータベース
- **Prisma** - ORMとデータベースツール

### DevOps
- **Docker** - コンテナ化
- **GitHub Actions** - CI/CD
- **Vercel** - フロントエンドホスティング
- **Railway** - バックエンドホスティング

## Getting Started

### Prerequisites

- Node.js 18.x以上
- PostgreSQL 14.x以上
- npm または yarn

### Installation

1. リポジトリをクローン

```bash
git clone https://github.com/yourusername/taskmaster.git
cd taskmaster
```

2. 依存関係をインストール

```bash
# フロントエンドとバックエンドの両方
npm install
```

3. 環境変数を設定

```bash
cp .env.example .env
# .envファイルを編集してデータベース接続情報などを設定
```

4. データベースをセットアップ

```bash
npm run db:migrate
npm run db:seed
```

5. 開発サーバーを起動

```bash
npm run dev
```

アプリケーションは http://localhost:3000 で起動します。

## Usage

### タスクの作成

```typescript
// 新しいタスクを作成
const task = await createTask({
  title: "新機能の実装",
  description: "ユーザープロフィール編集機能",
  priority: "high",
  dueDate: "2024-04-01",
  assignee: "user_123"
});
```

### プロジェクトの管理

```typescript
// プロジェクトを作成
const project = await createProject({
  name: "Q2 Product Launch",
  team: ["user_123", "user_456"],
  startDate: "2024-04-01",
  endDate: "2024-06-30"
});
```

詳細な使用方法は [Documentation](https://docs.taskmaster.com) を参照してください。

## Contributing

貢献を歓迎します！以下の手順でプルリクエストを送ってください：

1. このリポジトリをフォーク
2. 機能ブランチを作成 (`git checkout -b feature/amazing-feature`)
3. 変更をコミット (`git commit -m 'Add amazing feature'`)
4. ブランチにプッシュ (`git push origin feature/amazing-feature`)
5. プルリクエストを作成

### Code Style

- ESLintとPrettierの設定に従ってください
- コミットメッセージは [Conventional Commits](https://www.conventionalcommits.org/) に準拠
- テストを追加してください（カバレッジ80%以上）

## License

このプロジェクトは MIT License の下でライセンスされています。詳細は [LICENSE](LICENSE) ファイルを参照してください。

---

Made with ❤️ by the TaskMaster Team
````

### 例4: 比較表の作成

**プロンプト:**
```
React、Vue、Angularの3つのフレームワークを比較してください。
以下の観点で表形式にまとめてください：

| フレームワーク | 学習曲線 | パフォーマンス | エコシステム | 企業サポート | ユースケース |
|--------------|---------|-------------|-----------|------------|------------|
| [各項目を埋める] |
```

**期待される出力:**

| フレームワーク | 学習曲線 | パフォーマンス | エコシステム | 企業サポート | ユースケース |
|--------------|---------|-------------|-----------|------------|------------|
| **React** | 中程度<br>JSXとHooksの理解が必要 | 高速<br>Virtual DOM、React 18のConcurrent機能 | 非常に豊富<br>Next.js、Redux、React Query等 | Meta（Facebook） | SPA、SSR、モバイル（React Native）、大規模アプリ |
| **Vue** | 易しい<br>HTMLベース、段階的導入可能 | 高速<br>最適化されたReactivity System | 豊富<br>Nuxt.js、Vuex、Pinia等 | コミュニティ主導 | SPA、プログレッシブWebアプリ、小〜中規模アプリ |
| **Angular** | 難しい<br>TypeScript、RxJS、DI等の概念 | 高速<br>Ahead-of-Time コンパイル | 統合的<br>公式で多くの機能を提供 | Google | エンタープライズアプリ、大規模SPA、TypeScript重視 |

**詳細比較:**

### 学習曲線
- **React**: JSXの記法とHooksの概念を理解する必要があるが、基本は比較的シンプル
- **Vue**: HTMLテンプレートベースで直感的。初心者に最も優しい
- **Angular**: 習得すべき概念が多く、学習曲線は急だが、マスターすれば強力

### パフォーマンス
- すべて本番環境で高速。差は主に最適化の方法と開発者の実装による

### エコシステム
- **React**: 最大のエコシステム。選択肢が多いが、決定疲れも
- **Vue**: バランスの取れたエコシステム。公式ツールも充実
- **Angular**: 統合的アプローチ。必要な機能はほぼ公式で提供

### 例5: YAML設定ファイル

**プロンプト:**
```
Docker Composeの設定ファイルを作成してください。
以下のサービスを含めてください：
- Webアプリケーション（Node.js）
- データベース（PostgreSQL）
- Redis
- Nginx（リバースプロキシ）

```yaml
# docker-compose.yml形式で出力
\```
```

**期待される出力:**
````yaml
```yaml
version: '3.8'

services:
  # Webアプリケーション（Node.js）
  app:
    build:
      context: .
      dockerfile: Dockerfile
    container_name: web_app
    restart: unless-stopped
    environment:
      - NODE_ENV=production
      - DATABASE_URL=postgresql://postgres:password@db:5432/myapp
      - REDIS_URL=redis://redis:6379
      - PORT=3000
    ports:
      - "3000:3000"
    depends_on:
      - db
      - redis
    volumes:
      - ./src:/app/src
      - /app/node_modules
    networks:
      - app-network

  # PostgreSQLデータベース
  db:
    image: postgres:15-alpine
    container_name: postgres_db
    restart: unless-stopped
    environment:
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=password
      - POSTGRES_DB=myapp
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data
      - ./init.sql:/docker-entrypoint-initdb.d/init.sql
    networks:
      - app-network

  # Redis
  redis:
    image: redis:7-alpine
    container_name: redis_cache
    restart: unless-stopped
    command: redis-server --appendonly yes
    ports:
      - "6379:6379"
    volumes:
      - redis_data:/data
    networks:
      - app-network

  # Nginx（リバースプロキシ）
  nginx:
    image: nginx:alpine
    container_name: nginx_proxy
    restart: unless-stopped
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx/nginx.conf:/etc/nginx/nginx.conf
      - ./nginx/ssl:/etc/nginx/ssl
    depends_on:
      - app
    networks:
      - app-network

volumes:
  postgres_data:
    driver: local
  redis_data:
    driver: local

networks:
  app-network:
    driver: bridge
```
````

## 組み合わせ

### Role-playing + 出力形式指定
```
あなたはシニアソフトウェアアーキテクトです。
マイクロサービスアーキテクチャの設計書を作成してください。

以下のMarkdown形式で出力してください：

# アーキテクチャ設計書

## 概要
[システム概要]

## サービス構成
[各マイクロサービスの説明]

## データフロー
```mermaid
[Mermaid記法でフロー図]
\```

## API仕様
[APIエンドポイント]
```

### CoT + 出力形式指定
```
以下の問題を解決してください。

問題: [複雑な問題]

以下の形式で、思考プロセスを示しながら回答してください：

## 問題分析
[段階的な分析]

## 解決策
```python
[Pythonコード]
\```

## 説明
[コードの説明]
```

## 注意点

### ✅ 効果的な使い方

1. **明示的なフォーマット指定**
   - テンプレートやサンプルを示す
   - コードブロックの言語を指定（```python、```json等）

2. **構造の明確化**
   - セクション、見出しレベルを明示
   - 箇条書き、番号付きリストの使い分け

3. **実例の提示**
   - 期待する出力の例を示すと精度が上がる

### ⚠️ 避けるべきこと

1. **曖昧な指示**
   - ❌ 「わかりやすく出力してください」
   - ✅ 「Markdown形式で、コードは```pythonブロックで出力してください」

2. **複雑すぎるフォーマット**
   - シンプルで再現可能な構造を指定
   - 過度に複雑なフォーマットは避ける

3. **フォーマットの不統一**
   - 同じプロンプト内で矛盾するフォーマット指示を避ける

## ベストプラクティス

### よく使用される出力形式テンプレート

**1. コード出力テンプレート:**
````
以下の形式で出力してください：

```言語名
[コード]
\```

**説明:**
[コードの解説]

**使用例:**
```言語名
[使用例のコード]
\```
````

**2. JSON出力テンプレート:**
```
以下のJSON形式で出力してください：

```json
{
  "key": "value"
}
\```
```

**3. 表形式テンプレート:**
```
以下の表形式で出力してください：

| 項目 | 内容 | 備考 |
|------|------|------|
| [データ] | [データ] | [データ] |
```

**4. 構造化ドキュメントテンプレート:**
```
以下の構成で出力してください：

# タイトル

## セクション1
[内容]

### サブセクション
- 項目1
- 項目2

## セクション2
[内容]

```code
[コード例]
\```
```

### プログラミング言語別の指定

**Python:**
```
以下のPythonコードで出力してください。
- 型ヒントを使用
- Docstringを含める
- PEP 8に準拠

```python
[コード]
\```
```

**JavaScript/TypeScript:**
```
以下のTypeScriptコードで出力してください。
- 厳密な型定義
- JSDocコメント
- ESLint準拠

```typescript
[コード]
\```
```

**SQL:**
```
以下のSQL文で出力してください。
- フォーマット済み
- コメント付き

```sql
[SQL文]
\```
```

## まとめ

出力形式の指定は、AIの回答を実務で即座に活用可能にする重要な手法です。

**主な利点:**
- コピー&ペーストでそのまま使える
- 可読性が大幅に向上
- 後処理や統合が容易
- チーム内での共有がしやすい
- バージョン管理に適した形式

**推奨される使用法:**
1. 常に具体的なフォーマットを指定する
2. Markdownコードブロック（```）を積極的に活用
3. 構造化された形式（JSON、YAML、表など）を使用
4. 実例やテンプレートを示す

この手法は、特にコード生成、データ処理、ドキュメント作成において必須です。
