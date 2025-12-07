# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

1on1管理システム - EMとしてメンバーと1on1を行う際に、過去のセッション情報をもとに話すべき話題を提案するシステム。

## Commands

### `/init`
マネージャー（自分自身）のプロファイルを作成する。対話形式で情報を収集し、`./manager-profile.md` を生成。

### `/create-user`
新しいメンバーのプロファイルを作成する。対話形式で基本情報を収集し、`./users/{user_name}/` 配下にプロファイルを生成。

### `/create-session {user_name}`
指定したメンバーの次回1on1セッション用ファイルを作成。マルチエージェントレビューを経て話題を3〜5個提案。

### `/complete-session {user_name}`
1on1セッション終了後の処理。文字起こしをもとにメンバー評価・マネージャーレビューを実施。

## Directory Structure

```
1on1-agent/
├── .claude/commands/     # スラッシュコマンド定義
├── agents/               # エージェントプロファイル
├── templates/            # テンプレートファイル
├── samples/              # サンプルファイル（参考用）
├── users/                # ユーザーデータ（.gitignore対象）
└── manager-profile.md    # マネージャープロファイル（.gitignore対象）
```

## Notes

- セッション履歴は直近最大10件を読み込む
- `users/` ディレクトリと `manager-profile.md` は個人情報を含むため `.gitignore` で除外済み
