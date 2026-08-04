# Adding Shared Skills

このドキュメントは、このリポジトリに Claude Code と Codex の両方で読める skill を追加・更新するためのガイドラインです。

## Basic Policy

- `skills/` 配下は agent 共通の skill 本体だけを置く。
- Claude Code 固有、Codex 固有、インストール固有の説明は `docs/` または `slash_commands/` に分ける。
- skill は agent のコンテキストを消費するため、本文は短くし、詳細は必要時に読む `references/` へ分離する。
- 既存 skill の構成・文体・命名に合わせる。

## Required Structure

最小構成:

```text
skills/<skill-name>/
└── SKILL.md
```

必要に応じて追加する構成:

```text
skills/<skill-name>/
├── SKILL.md
├── checks/
├── scripts/
├── references/
├── examples/
└── assets/
```

- `checks/`: review 系 skill の個別チェック項目を 1 ファイル 1 項目で入れる。
- `scripts/`: 繰り返し実行する処理、壊れやすい手順、長いコードを入れる。
- `references/`: 詳細仕様、API メモ、長い例、ドメイン知識を入れる。
- `examples/`: 入出力例や sample artifact を入れる。
- `assets/`: 出力に使うテンプレートや画像など、agent が読むより利用するファイルを入れる。

`checks/` を使う場合は以下に従う。

- ファイル名は `<PREFIX>-<連番>-<kebab-case-name>.md` にする (例: `UT-001-specific-test-names.md`)。
- 各ファイルの見出しは `## Category`, `## Description`, `## Why It Matters`, `## Correct Approach`, `## Examples`, `## Review Guidance` に揃える。
- `SKILL.md` に ID・名称・カテゴリの一覧表と、check ファイルパスの一覧を書く。
- `SKILL.md` の本文で「全部読ませず、関連する check だけ選ばせる」ことを明示する。必ず適用させたい check がある場合はそれを名指しする。

skill ディレクトリ直下に `README.md`, `INSTALL.md`, `CHANGELOG.md` などの補助文書は作らない。必要な説明は `SKILL.md` か `references/` に入れる。

## SKILL.md Requirements

`SKILL.md` は YAML frontmatter と Markdown 本文で構成する。

```markdown
---
name: example-skill
description: Use this skill when the user asks for ...
version: 1.0.0
---

# Example Skill

## Overview

...
```

- `name` は必須。ディレクトリ名と同じ lowercase kebab-case にする。
- `description` は必須。いつ発火すべきかを具体的に書く。
- `version` は任意。追加する場合は semantic version 形式にする。
- frontmatter に `allowed-tools` など Claude Code 専用項目を入れない。
- `${CLAUDE_PLUGIN_ROOT}` や `${CODEX_HOME}` など CLI 固有の環境変数に依存しない。
- 付属ファイルは `scripts/foo.sh`, `references/bar.md` のように skill 内の相対パスで参照する。

## Writing Guidelines

- 本文は agent が実行時に必要な手順に絞る。
- 一般的なプログラミング説明や背景知識を長く書かない。
- 手順が壊れやすい場合は文章で説明しすぎず、`scripts/` に寄せる。
- 詳細資料が複数ある場合は、`SKILL.md` に「いつどの reference を読むか」を明記する。
- 複数の CLI で挙動が違う場合は、共通動作を本文に書き、CLI 固有の install や操作は `docs/` へ逃がす。
- Codex から Codex CLI を呼ぶなど自己参照になり得る skill は、使用条件を明確に制限する。

## Adding a Skill

1. `skills/<skill-name>/SKILL.md` を作る。
2. `name` と `description` を具体的に書く。
3. 本文に最小限の workflow、入力、出力、失敗時の扱いを書く。
4. 長い仕様や例がある場合は `references/` または `examples/` に分ける。
5. 実行可能な定型処理がある場合は `scripts/` に置き、`bash -n` などで検証する。
6. `README.md` の Shared Skills 一覧に追加する。
7. Claude Code と Codex の install docs に変更が必要か確認する。

## Review Checklist

追加・更新時は以下を確認する。

- `skills/<skill-name>/SKILL.md` が存在する。
- `name` がディレクトリ名と一致している。
- `description` だけで発火条件が分かる。
- `SKILL.md` が長すぎず、詳細が `references/` に分離されている。
- `skills/` 配下に Claude Code 専用記述や Codex 専用 install 手順が混ざっていない。
- すべての参照パスが skill ディレクトリ内の相対パスになっている。
- script がある場合、syntax check または軽い dry-run を通している。
- README の skill 一覧が更新されている。

## Suggested Validation

```bash
find skills -maxdepth 2 -name SKILL.md | sort
rg -n "CLAUDE_PLUGIN_ROOT|allowed-tools|\\.claude" skills
rg -n "CODEX_HOME|~/.codex/skills" skills
bash -n skills/<skill-name>/scripts/*.sh
```

`rg` は一致しないことを期待する。CLI の設定ファイルなどを reference として説明する必要がある場合は例外としてよいが、install 先や agent 固有の実行環境に依存する手順は `docs/` に置く。
