# gemini-cli-extension

日本の公開データ・日本向けツールを Gemini CLI から使うための拡張です。
A Gemini CLI extension for using Japanese public data and Japan-focused tools.

## インストール / Install

```bash
gemini extensions install https://github.com/takaratomita/gemini-cli-extension
```

## 内容 / Contents

| ファイル | 役割 |
|---|---|
| `gemini-extension.json` | 拡張のマニフェスト |
| `GEMINI.md` | 拡張が読み込むコンテキスト |
| `commands/japan-data/support-org.toml` | `/japan-data:support-org` 登録支援機関の検索方法を案内 |
| `commands/japan-data/houjin.toml` | `/japan-data:houjin` 法人番号・法人情報の調べ方を案内 |

## 使い方 / Usage

```
/japan-data:support-org 東京都 ベトナム語対応
/japan-data:houjin 株式会社〇〇
```

## ライセンス / License

MIT
