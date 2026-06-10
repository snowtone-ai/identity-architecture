# Identity Architecture Research OS v1.0

単独研究者が Claude App（Pro）と Claude Code のみで
「Identity Architecture」理論を長期的に構築・検証するための研究オペレーティングシステム。

## 設計思想（30秒で理解する）

本リポジトリの中核は **主張台帳（Claim Ledger）** である。

- 理論は「文書」ではなく「検証可能な主張（Claim）の集合」として管理する
- すべての主張は、概念（Concept）と証拠（Evidence）に明示的にリンクされる
- 主張は反証探索を経なければ「支持」ステータスに昇格できない
- 確証バイアス対策は意志ではなく **構造** で実装する

## ディレクトリ構成

```
identity-architecture/
├── CLAUDE.md              ← Claude Code が常時読み込む運用規則（軽量・500トークン以下）
├── governance/            ← 研究憲章・品質基準・意思決定記録
├── theory/
│   ├── concepts/          ← 概念台帳（1概念=1ファイル）
│   ├── claims/            ← 主張台帳（本OSの中核。1主張=1ファイル）
│   └── models/            ← 複数の主張を統合したモデル（後期段階）
├── evidence/
│   ├── items/             ← 証拠台帳（1証拠=1ファイル、等級E1〜E5）
│   └── refutations/       ← 反証・反例記録（削除禁止）
├── literature/            ← 文献ノート・調査キュー・Zotero/OpenAlex連携
├── workflows/             ← W01〜W06 の標準研究手順
├── publication/           ← 論文化パイプラインと草稿
├── state/                 ← 研究状態・課題・教訓（セッション間の記憶）
└── .claude/               ← Claude Code のエージェント定義・スラッシュコマンド
```

## 命名規則（重要）

- **ディレクトリ名・ファイル名は ASCII**（git / grep / クロスプラットフォーム / Claude Code ツールの安定性のため）
- **ファイルの中身はすべて日本語**（理論構築は日本語で行う）
- ID 規則：
  - 概念: `C-001_<slug>.md`
  - 主張: `CL-001_<slug>.md`
  - 証拠: `E-001_<slug>.md`
  - 反証: `R-001_<slug>.md`
  - 文献: `L-001_<著者年>.md`
  - 意思決定: `DR-0001_<slug>.md`

## 最初にやること（セットアップ手順）

1. このリポジトリを git 初期化する（`git init && git add -A && git commit -m "OS v1.0"`）
2. `~/.claude/CLAUDE.md` を同梱の `グローバルCLAUDE.md` で置き換える
3. Zotero をインストールし、`literature/README.md` に従って MCP を接続する（任意・推奨）
4. `state/research-state.md` を開き、現在地を記入する
5. `workflows/W02_concept-refinement.md` から開始する（最初の仕事は概念の操作化）

## 日常の運用サイクル

| 頻度 | 作業 | 入口 |
|---|---|---|
| 毎セッション | 状態読込→1タスク→状態更新 | CLAUDE.md が自動制御 |
| 随時 | 文献調査 | `/lit` コマンド |
| 主張作成時 | 定式化→反証探索→批判 | `/claim` → `/critique` |
| 週1回 | 週次レビュー | `/weekly` |
| 月1回 | 整合性監査 | auditor エージェント |
