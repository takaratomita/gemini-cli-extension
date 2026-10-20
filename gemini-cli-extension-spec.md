# gemini-cli-extension 仕様書・実装計画書・進捗台帳

作成：2026-10-08 / ステータス：計画中
関連調査：`secondry-brain/1_Projects/集客ハック/research/2026-10-08-t12-loopholes.md`・`t13-implementation-ranking.md`

## 0. この資料の読み方

- 仕様・実装計画・TODOを1ファイルで持つ
- 数値の一次ソースは Vault の research/ 側。本ファイルは実装判断の正
- 完了したTODOは `[x]` に変え、進捗台帳に1行追記する

## 1. 概要と受け入れ条件

### 目的

Gemini CLI拡張を作り、**ギャラリーへの自動掲載で先行者利益を取る**。審査・申請・費用が一切なく、公開GitHubリポジトリに `gemini-cli-extension` トピック＋`gemini-extension.json` を置くだけで日次クロールで掲載される（公式確認済み）。

### 受け入れ条件（Go判定）

| 条件 | 判定方法 |
|---|---|
| ギャラリーに掲載される | geminicli.com の拡張一覧で検索して表示される |
| 掲載後30日でインストールが発生 | GitHubのclone/traffic統計・star数 |

### 収益の位置づけ

掲載は露出面であり収益源ではない。インストール→関連ツール（mcp-tools等）への導線を作るのが目的。

## 2. 市場の裏付け（調査済み・再検証済み）

- Gemini CLI拡張ギャラリー：GitHub topic＋`gemini-extension.json`で自動インデックス（日次・バリデーション通過のみ）。審査・費用ゼロを公式確認
- Gemini CLIユーザー100万+（ローンチ3ヶ月時点・Google公称）
- GitHub star順表示のため、新規でもニッチ名で上位に入りやすい構造
- 「日本語/日本サービス系ツール接続」は未開拓の余地が大きい（t12調査）

## 3. スコープ

### やること（v1）

- `gemini-extension.json`（マニフェスト）をルートに置く
- 拡張内容：日本向けツール群への接続（MCPサーバー参照 or カスタムコマンド or GEMINI.mdコンテキスト）
- GitHubリポジトリをpublicにし、`gemini-cli-extension`トピックを付ける

### やらないこと（v1）

- 独自のMCPサーバー実装（mcp-tools側と共通利用は検討）
- 有料機能・APIキー必須の機能

## 4. 設計

### 4-1. gemini-extension.json の構成（公式仕様準拠）

```json
{
  "name": "gemini-cli-extension",
  "version": "0.1.0",
  "description": "Japanese public data from Gemini CLI: ...",
  "mcpServers": {},
  "contextFileName": "GEMINI.md",
  "excludeTools": []
}
```

- `mcpServers`：mcp-tools側のリモートMCPを参照すれば共通基盤を使い回せる（要デプロイ後）
- `GEMINI.md`：拡張のコンテキスト・使い方を記述
- カスタムコマンド（`commands/`配下のtoml）も追加可能

### 4-2. 掲載の仕組み（確認済み）

1. 公開GitHubリポジトリに `gemini-cli-extension` トピックを付ける
2. ルートに `gemini-extension.json` を置く
3. 日次クローラーが自動収集（バリデーション通過が条件）
4. ギャラリーに掲載される

## 5. 実装計画（フェーズ）

- [x] P0：リポジトリ初期設定（README・LICENSE・.gitignore）
- [x] P1：`gemini-extension.json` 最小構成（名前・バージョンのみで動く）
- [x] P2：`GEMINI.md` にコンテキスト記述（日本語ツール接続の説明）
- [x] P3：トピック `gemini-cli-extension` をリポジトリに設定
- [ ] P4：ギャラリー掲載を確認（翌日以降・日次クロール）
- [x] P5：（任意）`commands/` にカスタムコマンド追加
- [ ] P6：掲載後30日の流入実測→継続/停止判定

## 6. コスト・収支

- コスト：完全0円（GitHub公開リポジトリのみ）
- 収益：直接課金なし。露出面として機能

## 7. 検討した選択肢と却下理由

| 選択肢 | 却下理由 |
|---|---|
| 最初からMCPサーバー内蔵 | mcp-tools側の実装が先。まず最小構成で掲載を取る |
| 多言語対応 | 日本語ニッチが狙い目。英語併記はdescription程度で |

## 8. リスク・注意点

- 自動掲載でもバリデーションに落ちると載らない（`gemini-extension.json`のスキーマ遵守が必須）
- topic方式なので競合増加とともに埋もれる。先行者利益は時間で薄れる
- ギャラリー掲載≠流入の保証なし

## 9. 未検証事項

- ギャラリーの現在の掲載総数（UNVERIFIED）
- 掲載後の個別流入・インストール数の実測値
- `mcpServers`で外部リモートMCPを参照する場合の挙動（mcp-toolsデプロイ後に検証）

## 10. 進捗台帳

| 日付 | 内容 |
|---|---|
| 2026-10-08 | リポジトリ作成・Orca連携・本ファイル作成 |
| 2026-10-08 | P0〜P3・P5 実装（gemini-extension.json・GEMINI.md・commands/japan-data/{support-org,houjin}.toml・README・LICENSE・.gitignore）。トピック設定・public確認済み。P4（掲載確認）は翌日以降 |
| 2026-10-14 | 6日経ってもギャラリー未掲載。マニフェストに `description` を追加した（表示に使う項目のため。未掲載の原因かは未確認） |
