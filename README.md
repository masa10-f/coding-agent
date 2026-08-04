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
| [unit-test-review](./skills/unit-test-review/) | unit test の品質レビューで壊れやすい・価値の低いテストを検出する skill |
| [writing-structure-review](./skills/writing-structure-review/) | 英語文書の全体構成を見出しレベルで評価し、章の移動・統合・削除案または「変更不要」の根拠を出す skill (phase 1) |
| [writing-flow-review](./skills/writing-flow-review/) | 節内の段落のつながり、主張の位置、接続語の妥当性をレビューする skill (phase 2) |
| [writing-evidence-review](./skills/writing-evidence-review/) | 主張と根拠の対応、過剰一般化、用語・数値・図表・引用の整合を検証する skill (phase 3) |
| [writing-concision-review](./skills/writing-concision-review/) | まわりくどい英文から前置き・言い換え・空虚な抽象語・過剰なヘッジを削る skill (phase 4) |
| [writing-revision-review](./skills/writing-revision-review/) | 指摘対応後の再点検。防御的加筆、局所修正の波及、継ぎ足しによる解決を検出する skill (phase 5) |

`writing-*` skill は英語の論文・技術文書を対象とします。phase 1 から 4 を順に実行し、指摘に対応させたあと phase 5 を実行する構成です。各 phase は見る範囲を意図的に制限しており、まとめて実行すると効果が落ちます。

phase 4 (concision) は phase 3 (evidence) の後に置いています。どのヘッジが根拠上必要か、どの抽象語に置き換えるべき具体値が存在するかは evidence phase の出力で決まるため、順序を入れ替えると CO-003 と CO-004 が判断不能になります。

対象範囲は構成・論理・根拠・冗長性です。**文法・冠詞・時制・句読点・綴りといった mechanics は対象外**なので、その層は別途 grammar checker を使ってください。日本語文書は対象外です。

### Claude Code Slash Commands

`slash_commands/` は Claude Code 専用です。Codex の skill 管理ディレクトリにはコピーしません。

| Command | Description |
| --- | --- |
| [codex-review](./slash_commands/codex-review.md) | Claude Code から Codex CLI review を実行し、指摘修正と検証を行う |
| [plan-review](./slash_commands/plan-review.md) | Claude Code の plan file を Codex CLI でレビューし、フィードバックを反映する |
| [writing-review](./slash_commands/writing-review.md) | `writing-*` skill を phase 順に駆動し、deferral と語数を集約する |

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

詳細な追加手順とレビュー観点は [docs/adding-skills.md](./docs/adding-skills.md) を参照してください。

## Prerequisites

`codex-consult` と Claude Code 用 slash commands を使う場合は、Codex CLI のインストールと認証が必要です。

```bash
npm install -g @openai/codex
codex login
```

## License

MIT
