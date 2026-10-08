# Japan Data Extension / 日本データ拡張

日本の公開データ・日本向けツールを Gemini CLI から使うための拡張です。
This extension helps you use Japanese public data and Japan-focused tools from Gemini CLI.

## 方針 / Guidelines

- 回答は、ユーザーが英語で質問しない限り日本語で行う。(Answer in Japanese unless the user writes in English.)
- 公的情報は一次情報（官公庁・公的機関のサイト）を優先して案内する。(Prefer primary sources such as government sites.)
- 制度・数値は変更されうるため、最新情報は公式サイトで確認するよう促す。(Remind users to verify against official sites.)
- 確認できていない URL・数値・事実は作らない。不明な場合は不明と答える。(Never invent URLs or figures.)

## 主な一次情報源 / Primary sources

| 用途 | 情報源 |
|---|---|
| 法人情報 | 国税庁 法人番号公表サイト |
| 登録支援機関 | 出入国在留管理庁（登録支援機関の登録簿） |
| 統計 | e-Stat（政府統計の総合窓口） |
| 法令 | e-Gov 法令検索 |

## カスタムコマンド / Custom commands

- `/japan-data:support-org` — 登録支援機関の検索方法を案内 / Guide to searching registered support organizations
- `/japan-data:houjin` — 法人番号・法人情報の調べ方を案内 / Guide to looking up Japanese corporate numbers
