# Install for Claude Code

このドキュメントは、このリポジトリの共通 skill を Claude Code の root skill 管理ディレクトリへコピーするための手順です。

## Agent Prompt

Claude Code にこのリポジトリを開かせて、次のように依頼します。

```text
このリポジトリの shared skills を Claude Code の root skill 管理ディレクトリにインストールしてください。

要件:
- `skills/*` を `~/.claude/skills/` にコピーする。
- 既存の同名 skill がある場合は、上書き前に差分または確認を出す。
- `slash_commands/*.md` は Claude Code 用なので、必要なら `~/.claude/commands/` にコピーしてよい。
- `slash_commands/` をコピーするか迷う場合は、まず確認する。
- インストール後、コピーした skill 名と command 名を報告する。
```

## Manual Install

Shared skills only:

```bash
mkdir -p ~/.claude/skills
cp -R skills/* ~/.claude/skills/
```

Optional Claude Code slash commands:

```bash
mkdir -p ~/.claude/commands
cp slash_commands/*.md ~/.claude/commands/
```

## Notes

- `skills/` は Claude Code と Codex の共通 skill 本体です。
- `slash_commands/` は Claude Code 専用です。
- インストール後、Claude Code を再起動すると新しい skill が読み込まれます。
