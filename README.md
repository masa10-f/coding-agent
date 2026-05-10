# Coding Agent Skills

Claude Code と Codex の両方で使うことを想定した agent skill リポジトリです。

## Overview

このリポジトリでは、複数の coding agent から読める共通 skill 本体を `skills/` に置きます。各 CLI 固有の配置方法や任意機能はドキュメントで分け、skill 本体はできるだけ共通形式に保ちます。

## Contents

### Shared Skills

| Skill | Description |
| --- | --- |
| [antipatterns](./skills/antipatterns/) | 実装・レビュー時に避けるべきアンチパターン集 |
| [codex-consult](./skills/codex-consult/) | Codex CLI を別プロセスで実行し、実装方針やレビュー観点を相談する skill |

### Claude Code Slash Commands

`slash_commands/` は Claude Code 専用です。Codex の skill 管理ディレクトリにはコピーしません。

| Command | Description |
| --- | --- |
| [codex-review](./slash_commands/codex-review.md) | Claude Code から Codex CLI review を実行し、指摘修正と検証を行う |
| [plan-review](./slash_commands/plan-review.md) | Claude Code の plan file を Codex CLI でレビューし、フィードバックを反映する |

## Install

このリポジトリは copy 方式でインストールします。symlink 前提にはしません。

- Claude Code: [docs/install-claude.md](./docs/install-claude.md)
- Codex: [docs/install-codex.md](./docs/install-codex.md)

各ドキュメントには、対象 CLI にこのリポジトリを読ませて root skill 管理ディレクトリへコピーさせるためのプロンプトと、手動 copy コマンドの両方を記載しています。

## Shared Skill Rules

共通 skill を追加・更新するときは、以下を守ります。

- skill は `skills/<skill-name>/SKILL.md` を必須にする。
- `SKILL.md` の frontmatter は `name` と `description` を必須にし、必要なら `version` だけを追加する。
- Claude Code 専用の `allowed-tools` や `${CLAUDE_PLUGIN_ROOT}` を `skills/` 配下に入れない。
- 付属ファイルは `scripts/`, `references/`, `examples/` など、`SKILL.md` からの相対パスで案内する。
- CLI 固有の install 手順は `docs/` に置く。

## Prerequisites

`codex-consult` と Claude Code 用 slash commands を使う場合は、Codex CLI のインストールと認証が必要です。

```bash
npm install -g @openai/codex
codex login
```

## License

MIT
