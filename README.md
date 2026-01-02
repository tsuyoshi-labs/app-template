# App Template

新しいアプリリポジトリを作成するためのテンプレートリポジトリです。タスク管理システムと統合されています。

## 使い方

### 1. このテンプレートから新しいリポジトリを作成

GitHub UI で "Use this template" をクリックして新しいリポジトリを作成します。

または、GitHub CLI を使用：

```bash
gh repo create tsuyoshi-labs/YOUR-NEW-REPO --template tsuyoshi-labs/app-template --private --clone
cd YOUR-NEW-REPO
```

### 2. 初期設定の自動化

Workspace リポジトリで Claude Code を起動し、`/setup-new-app` skill を実行してください。

```bash
cd ../Workspace
claude
> /setup-new-app
```

このコマンドは以下を自動的に実行します：

- `.claude/task-config.json` の自動生成（リポジトリ名を自動検出）
- GitHub Secrets の設定（`ADD_TO_PROJECT_PAT`）
- 設定の検証

### 3. 手動セットアップ（skill を使わない場合）

#### 3-1. 設定ファイルの更新

`.claude/task-config.json` を編集：

```json
{
  "repository": "tsuyoshi-labs/YOUR-NEW-REPO",
  "project_number": 4,
  "default_assignee": "tsuyoshi-labs"
}
```

#### 3-2. GitHub Secrets の設定

Personal Access Token (PAT) を設定します。

1. https://github.com/settings/tokens にアクセス
2. "Generate new token (classic)" をクリック
3. スコープで `project` と `repo` を選択
4. トークンを生成してコピー
5. リポジトリの Settings → Secrets and variables → Actions → New repository secret
6. Name: `ADD_TO_PROJECT_PAT`、Value: コピーしたトークン

### 4. 動作確認

Issue を作成してテスト：

```bash
gh issue create --title "テストIssue" --body "動作確認用" --label "task"
```

Issue が自動的に Project #4 に追加されることを確認してください。

## 含まれるもの

### ワークフロー

- **add-to-project.yml**: Issue を Project #4 に自動追加
- **ci.yml**: CI（テスト実行）
- **lint.yml**: リンター実行

### 設定ファイル

- **.claude/task-config.json**: タスク管理設定（要編集）
- **package.json**: Node.js プロジェクト設定

### テンプレート

Issue/PR テンプレートは `.github` リポジトリから自動的に利用可能です：

- Goal テンプレート（年次目標・長期的な方針）
- Epic テンプレート（複数タスクで構成される成果物）
- Task テンプレート（1日以内で完了する具体的なタスク）

## 開発開始

サンプルコードを置き換えて開発を開始してください：

```bash
npm install
npm start
```

## ドキュメント

- [Workspace リポジトリ](https://github.com/tsuyoshi-labs/Workspace) - タスク管理システムの本部
- [.github リポジトリ](https://github.com/tsuyoshi-labs/.github) - 共有テンプレートとワークフロー

## ライセンス

MIT
