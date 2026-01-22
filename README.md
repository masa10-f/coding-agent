# Coding Agent

Claude Code用のスキルとコマンドのコレクション。

## 概要

このリポジトリは、Claude Codeで使用するためのカスタムスキルとスラッシュコマンドを管理しています。ユーザーは必要なものを自分の`.claude`ディレクトリにコピーして使用します。

## コンテンツ

### Skills

| スキル | 説明 |
|--------|------|
| [codex-consult](./skills/codex-consult/) | OpenAI Codex CLIを使用した実装相談スキル。より深い推論モデルによるアーキテクチャ設計や実装方針の相談が可能 |

### Slash Commands

| コマンド | 説明 |
|----------|------|
| [codex-review](./slash_commands/codex-review.md) | Codex CLIでコードレビューを実行し、修正を適用 |
| [plan-review](./slash_commands/plan-review.md) | Codex CLIで実装プランをレビューし、フィードバックに基づいて更新 |

## インストール方法

### Skills のインストール

スキルを使用するには、`skills/`ディレクトリの内容を`.claude/skills/`にコピーします：

```bash
# 特定のスキルをコピー
cp -r skills/codex-consult ~/.claude/skills/

# または、プロジェクト固有の.claudeにコピー
cp -r skills/codex-consult /path/to/your/project/.claude/skills/
```

### Slash Commands のインストール

スラッシュコマンドを使用するには、`slash_commands/`ディレクトリの内容を`.claude/commands/`にコピーします：

```bash
# 特定のコマンドをコピー
cp slash_commands/codex-review.md ~/.claude/commands/

# または、プロジェクト固有の.claudeにコピー
cp slash_commands/codex-review.md /path/to/your/project/.claude/commands/
```

### 一括インストール

すべてのスキルとコマンドを一括でインストール：

```bash
# ユーザーレベルにインストール
mkdir -p ~/.claude/skills ~/.claude/commands
cp -r skills/* ~/.claude/skills/
cp slash_commands/*.md ~/.claude/commands/

# プロジェクトレベルにインストール
PROJECT_DIR=/path/to/your/project
mkdir -p $PROJECT_DIR/.claude/skills $PROJECT_DIR/.claude/commands
cp -r skills/* $PROJECT_DIR/.claude/skills/
cp slash_commands/*.md $PROJECT_DIR/.claude/commands/
```

## 前提条件

### Codex CLI

codex-consult スキルと codex-review/plan-review コマンドを使用するには、Codex CLIのインストールと認証が必要です：

```bash
# インストール
npm install -g @openai/codex

# 認証
codex login
```

## スキル詳細

### codex-consult

OpenAI Codex CLIを使用して、より深い推論モデル（gpt-5.2-codex）に実装の相談ができるスキルです。

**特徴:**
- **Plan Mode**: 実装方針と戦略を提案（デフォルト）
- **Patch Mode**: unified diff形式の具体的なコード変更を提案
- **Web Search**: デフォルトで有効、最新情報を参照可能
- **Read-only**: 安全なサンドボックスで実行

**使用例:**
- 「Codexに相談して」
- 「実装方針をcodexに聞きたい」
- 「アーキテクチャの設計をcodexにレビューしてもらって」

**ディレクトリ構成:**
```
skills/codex-consult/
├── SKILL.md           # スキル定義
├── scripts/
│   └── codex-exec.sh  # Codex CLI実行ラッパー
├── references/
│   ├── codex-cli-reference.md  # CLI リファレンス
│   └── output-format.md        # 出力フォーマット仕様
└── examples/
    └── sample-consultation.md  # サンプル出力
```

## ライセンス

MIT
