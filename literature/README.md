# literature/ — 文献管理の運用ルール

## ツール構成（2026-06時点・すべて無料）

| 役割 | ツール | 接続方法 |
|---|---|---|
| 書誌・PDF管理 | Zotero 7（無料） | デスクトップアプリ + ブラウザコネクタ |
| Zotero連携 | Zotero MCP（ローカル動作・無料） | Claude Code / Claude Desktop に MCP 登録 |
| 学術検索 | OpenAlex（2.5億件超・APIキー不要・無料） | OpenAlex MCP または Claude の Web 検索 |
| 補助検索 | Semantic Scholar / Crossref / arXiv | 同上（無料API） |

セットアップ例は `.mcp.json`（リポジトリ直下）を参照。MCP はローカルで動くため
API課金は発生しない（Claude Pro の範囲内で運用可能）。

## 運用フロー（W01 文献調査ワークフローと対応）

1. 探索: OpenAlex MCP / Web検索で候補を発見（librarian エージェントに委譲推奨）
2. 取込: Zotero に書誌+PDFを保存（一次保管庫は Zotero。リポジトリにPDFを置かない）
3. ノート: 重要文献のみ `notes/L-XXX_<著者年>.md` を作成
4. 抽出: 主張に関係する知見を `evidence/items/` に原子化して登録
5. 照合: AI要約は必ず原典と照合してから台帳へ（引用ハルシネーション対策）

## 重要原則
- **全文献にノートを書かない。** ノートは「概念・主張に接続される文献」のみ（推定: 読んだ文献の2〜3割）
- 書誌の真実は Zotero、知見の真実は evidence/、の二層構造を崩さない
