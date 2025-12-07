# 1on1 Agent

A 1on1 support agent powered by Claude Code. Proposes discussion topics based on past session history and continuously improves 1on1 quality.

---

## ⚠️ Important: Handling Personal Information

**The information handled by this tool includes personal and confidential member data.**

### Precautions

1. **Local Execution Recommended**
   - Claude Code runs locally, but input information is sent to Anthropic's servers via API
   - Please verify compliance with your company policies and privacy regulations before use

2. **Repository Visibility Settings**
   - If forking this repository, **always operate as a private repository**
   - `users/` and `manager-profile.md` are excluded via `.gitignore`, but be careful not to commit them accidentally

3. **Handling Information from 1on1s**
   - Content discussed in 1on1s is confidential information based on trust between manager and member
   - Do not share with third parties without consent

---

## Design Philosophy

### Multi-Agent Review from Multiple Perspectives

Rather than relying on a single AI, multiple specialized agents review from different perspectives.

```
Manager Agent → EM Best Practice → Tech Specialist Agent
(Initial Draft)   (General Perspective)  (Specialized Perspective)
                                              ↓
                                      Career Agent
                                      (Conditional Activation)
```

| Agent | Role |
|-------|------|
| Manager Agent | Topic proposals reflecting the EM's personality and values |
| EM Best Practice | Alignment with general 1on1 best practices |
| Tech Specialist Agent | Technical perspective specific to member's role |
| Career Agent | Turnover risk and career growth perspective (conditional) |

### Articulating EM's Personality and Style

By defining the EM's values and style in `manager-profile.md`, the AI functions as a **tool that extends the EM's own thinking** rather than a generic assistant.

---

## Setup

### Prerequisites

- [Claude Code](https://claude.ai/code) installed

### Steps

1. **Fork the repository** (as a private repository)

2. **Initial setup**
   ```
   /init
   ```
   Creates your own profile through interactive dialogue.

3. **Register team members**
   ```
   /create-user
   ```

---

## Usage

### Before Session

```
/create-session {user_name}
```

- Loads profile and past sessions
- Runs multi-agent review
- Proposes 3-5 focused topics

### After Session

```
/complete-session {user_name}
```

- Paste the transcript
- Calculates member assessment scores (Turnover Risk / Burnout Risk / Motivation)
- Conducts manager review
- Updates profile and session files

---

## Directory Structure

```
1on1-agent/
├── .claude/
│   └── commands/           # Slash command definitions
│       ├── init.md
│       ├── create-user.md
│       ├── create-session.md
│       └── complete-session.md
│
├── agents/                 # Agent profiles
│   ├── em-best-practice.md
│   ├── career-agent.md
│   ├── member-assessment.md
│   ├── manager-review.md
│   └── tech-specialist-*.md
│
├── templates/              # Template files
│   ├── manager-profile.md
│   ├── user-profile.md
│   └── session.md
│
├── samples/                # Sample files (for reference)
│   ├── en/                 # English samples
│   └── ja/                 # Japanese samples
│
├── users/                  # User data (.gitignore target)
│   └── {user_name}/
│       ├── profile.md
│       └── sessions/
│           └── YYYY-MM-DD.md
│
├── manager-profile.md      # Manager profile (.gitignore target)
├── CLAUDE.md
└── README.md
```

---

## Customization

### Adding Tech Specialist Agents

You can add new tech specialist agents to the `agents/` directory:

```
agents/tech-specialist-mobile.md
agents/tech-specialist-data.md
```

After adding, update the tech agent selection table in `create-session.md`.

### Editing Manager Profile

The `manager-profile.md` created by `/init` can be manually edited anytime. Refer to samples in `samples/en/manager-profile.md` or `samples/ja/manager-profile.md`.

### Language Settings

The system supports multilingual output:
- Configure your preferred language in `manager-profile.md` during `/init`
- Each team member can have a different 1on1 language in their profile
- Session files and feedback will be generated in the configured language

---

## Notes

- Score evaluations are reference values; final judgment should be made by the manager
- This tool supports 1on1 "preparation" and "reflection" but does not replace the 1on1 itself
- **Use raw transcripts, not summaries**
  - Fillers like "um", "well" and hedging expressions ("not super... but") contain important nuances
  - Summaries strip these out, reducing scoring accuracy for turnover risk etc.
  - We recommend pasting raw data from Google Meet transcription or similar tools

---

## License

MIT

---

---

# 1on1 Agent（日本語版）

Claude Codeを活用した1on1サポートエージェント。過去のセッション情報をもとに話すべき話題を提案し、1on1の品質を継続的に改善します。

---

## ⚠️ 重要：個人情報の取り扱いについて

**このツールで扱う情報には、メンバーの個人情報や機密性の高い内容が含まれます。**

### 注意事項

1. **ローカル実行を推奨**
   - Claude Codeはローカル環境で動作しますが、入力した情報はAPIを通じてAnthropicのサーバーに送信されます
   - 社内規定やプライバシーポリシーを確認の上、ご利用ください

2. **リポジトリの公開設定に注意**
   - このリポジトリをフォークして使用する場合、**必ずプライベートリポジトリ**として運用してください
   - `users/` と `manager-profile.md` は `.gitignore` で除外されていますが、誤ってコミットしないよう注意してください

3. **1on1で得た情報の取り扱い**
   - 1on1で話した内容は、マネージャーとメンバー間の信頼関係に基づく機密情報です
   - 本人の同意なく第三者に共有しないでください

---

## 設計思想

### マルチエージェントによる多角的レビュー

単一のAIに頼るのではなく、複数の専門エージェントが異なる視点からレビューを行います。

```
マネージャーエージェント → EMベストプラクティス → 技術エージェント
（初稿作成）              （一般的観点）          （専門的観点）
                                                      ↓
                                              キャリアエージェント
                                              （条件付き発動）
```

| エージェント | 役割 |
|-------------|------|
| マネージャーエージェント | EM本人の人格・価値観を反映した話題提案 |
| EMベストプラクティス | 一般的な1on1のベストプラクティスとの整合性 |
| 技術エージェント | メンバーの職種に特化した技術的観点 |
| キャリアエージェント | 転職リスクやキャリア成長の観点（条件付き） |

### EMの人格・スタイルの言語化

`manager-profile.md` にEM本人の価値観・スタイルを定義することで、AIが単なる汎用アシスタントではなく、**EM本人の思考を拡張するツール**として機能します。

---

## セットアップ

### 前提条件

- [Claude Code](https://claude.ai/code) がインストールされていること

### 手順

1. **リポジトリをフォーク**（プライベートリポジトリとして）

2. **初期設定**
   ```
   /init
   ```
   対話形式であなた自身のプロファイルを作成します。

3. **メンバーを登録**
   ```
   /create-user
   ```

---

## 使い方

### セッション前

```
/create-session {user_name}
```

- プロファイルと過去セッションを読み込み
- マルチエージェントレビューを実行
- 話題を3〜5個に絞り込んで提案

### セッション後

```
/complete-session {user_name}
```

- 文字起こしを貼り付け
- メンバー評価スコアを算出（退職リスク/休職リスク/モチベーション）
- マネージャーレビューを実施
- プロファイルとセッションファイルを更新

---

## ディレクトリ構造

```
1on1-agent/
├── .claude/
│   └── commands/           # スラッシュコマンド定義
│       ├── init.md
│       ├── create-user.md
│       ├── create-session.md
│       └── complete-session.md
│
├── agents/                 # エージェントプロファイル
│   ├── em-best-practice.md
│   ├── career-agent.md
│   ├── member-assessment.md
│   ├── manager-review.md
│   └── tech-specialist-*.md
│
├── templates/              # テンプレートファイル
│   ├── manager-profile.md
│   ├── user-profile.md
│   └── session.md
│
├── samples/                # サンプルファイル（参考用）
│   ├── en/                 # 英語版サンプル
│   └── ja/                 # 日本語版サンプル
│
├── users/                  # ユーザーデータ（.gitignore対象）
│   └── {user_name}/
│       ├── profile.md
│       └── sessions/
│           └── YYYY-MM-DD.md
│
├── manager-profile.md      # マネージャープロファイル（.gitignore対象）
├── CLAUDE.md
└── README.md
```

---

## カスタマイズ

### 技術エージェントの追加

`agents/` ディレクトリに新しい技術エージェントを追加できます：

```
agents/tech-specialist-mobile.md
agents/tech-specialist-data.md
```

追加後、`create-session.md` の技術エージェント選択テーブルに追記してください。

### マネージャープロファイルの編集

`/init` で作成した `manager-profile.md` はいつでも手動で編集できます。サンプルは `samples/ja/manager-profile.md` または `samples/en/manager-profile.md` を参照してください。

### 言語設定

システムは多言語出力に対応しています：
- `/init` 実行時に `manager-profile.md` で希望の言語を設定
- 各メンバーのプロファイルで個別に1on1の言語を設定可能
- セッションファイルやフィードバックは設定した言語で生成されます

---

## 注意事項

- スコア評価は参考値であり、最終判断はマネージャーが行ってください
- このツールは1on1の「準備」と「振り返り」を支援するものであり、1on1そのものを代替するものではありません
- **文字起こしは要約ではなく生データを使用してください**
  - 「えーと」「まあ」などのフィラーや、打ち消し表現（「別にめっちゃ〜じゃないけど」など）には重要なニュアンスが含まれます
  - 要約を通すとこれらが省略され、退職リスク等のスコアリング精度が低下することが確認されています
  - Google Meetの文字起こし機能などの生データをそのまま貼り付けることを推奨します

---

## License

MIT
