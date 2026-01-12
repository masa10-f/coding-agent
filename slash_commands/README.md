# Claude Code カスタム Slash Commands ガイド

このディレクトリには Claude Code で使用するカスタム slash command のテンプレートが含まれています。

## 配置場所

Claude Code はカスタム slash command を以下の場所から読み込みます：

| 場所 | スコープ | パス |
|------|----------|------|
| プロジェクト単位 | 特定のリポジトリ内でのみ有効 | `.claude/commands/` |
| ユーザー単位 | 全プロジェクトで有効 | `~/.claude/commands/` |

### 使用方法

1. **プロジェクト単位で使う場合**
   ```bash
   mkdir -p .claude/commands
   cp slash_commands/codex-review.md .claude/commands/codex-review.md
   ```

2. **ユーザー単位で使う場合**
   ```bash
   mkdir -p ~/.claude/commands
   cp slash_commands/codex-review.md ~/.claude/commands/codex-review.md
   ```

配置後、Claude Code 内で `/codex-review` として呼び出せます。

## Slash Command のファイル形式

### 基本構造

```markdown
---
description: コマンドの説明（必須）
argument-hint: 引数のヒント（オプション）
allowed-tools: 許可するツール（オプション）
---

# コマンド本体

ここに Claude への指示を記述
```

### Frontmatter フィールド

| フィールド | 説明 |
|------------|------|
| `description` | コマンドの短い説明。`/help` で表示される |
| `argument-hint` | 引数のフォーマットヒント |
| `allowed-tools` | 自動許可するツール（カンマ区切り） |

### `!` プレフィックスによる事前コマンド実行

`!` を付けた bash コマンドは **slash command 実行前に実行され、その出力がコンテキストに含まれます**。

```markdown
- Current branch: !`git branch --show-current`
- Changed files: !`git diff --name-status`
```

#### ログを抑える（コンテキスト節約）

出力が長いコマンド（例: `codex review`）は、そのままだと実行ログまで含まれてコンテキストを消費します。  
以下のように **標準出力/標準エラーをファイルへ退避**し、必要な最終結果だけを `cat` で注入してください。

```markdown
!`codex exec -o /tmp/codex-review.last.md review $ARGUMENTS -c hide_agent_reasoning=true >/tmp/codex-review.run.log 2>&1`
!`cat /tmp/codex-review.last.md`
```

失敗時は `/tmp/codex-review.run.log` を参照します（普段はコンテキストに入れない）。

### `$ARGUMENTS` 変数

ユーザーが `/command arg1 arg2` と入力した場合、`$ARGUMENTS` には `arg1 arg2` が入ります。

```markdown
!`codex review $ARGUMENTS`
```

### `allowed-tools` の書式

ツールの許可パターンを指定：

```yaml
allowed-tools: >
  Bash(git status:*),
  Bash(npm:*),
  Bash(pytest:*)
```

`Bash(command:*)` は「`command` で始まるコマンド」を許可します。

## codex-review コマンドについて

### 前提条件

Codex CLI がインストールされていること：

```bash
npm i -g @openai/codex
```

初回実行時に認証が必要です（ChatGPT アカウントまたは API key）。

### 使用例

```bash
# 未コミット差分をレビューして修正
/codex-review --uncommitted

# main ブランチとの差分をレビューして修正
/codex-review --base main

# 特定コミットをレビューして修正
/codex-review --commit abc1234
```

### 注意点

1. **ネットワーク接続が必要**
   Codex CLI は OpenAI API に接続するため、sandbox モードでネットワークが遮断されていると動作しません。

2. **出力が長い場合**
   `-c hide_agent_reasoning=true` オプションで Codex の思考過程を省略できます（デフォルトで設定済み）。

3. **プロジェクト固有のカスタマイズ**
   `allowed-tools` をプロジェクトに合わせて調整してください。Python プロジェクトなら `uv`, `pytest`, `ruff` など、Node.js なら `npm`, `jest` などを許可します。

## 参考リンク

- [Claude Code Slash Commands ドキュメント](https://docs.anthropic.com/en/docs/claude-code/slash-commands)
- [Codex CLI](https://platform.openai.com/docs/codex-cli)
