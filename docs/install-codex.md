# Install for Codex

このドキュメントは、このリポジトリの共通 skill を Codex の root skill 管理ディレクトリへコピーするための手順です。

## Agent Prompt

Codex にこのリポジトリを開かせて、次のように依頼します。

```text
このリポジトリの shared skills を Codex の root skill 管理ディレクトリにインストールしてください。

要件:
- `skills/*` を `${CODEX_HOME:-~/.codex}/skills/` にコピーする。
- 既存の同名 skill がある場合は、上書き前に差分または確認を出す。
- `slash_commands/` は Claude Code 専用なので Codex にはコピーしない。
- インストール後、コピーした skill 名を報告し、Codex の再起動が必要なことを伝える。
```

## Manual Install

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
cp -R skills/* "${CODEX_HOME:-$HOME/.codex}/skills/"
```

## Notes

- `skills/` は Claude Code と Codex の共通 skill 本体です。
- `slash_commands/` は Codex にはインストールしません。
- インストール後、Codex を再起動すると新しい skill が読み込まれます。
