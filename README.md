# AI Dock

AI Dock は、Windows 上で使うサイドドック型の Electron アプリです。本文入力、AI 整形、下書き保存、引継ぎ文生成、外部 AI サービス起動を 1 つの画面にまとめています。

## 現在の実装で確認できる主な機能

- 本文入力
- Ollama を使った AI 整形
- 下書き保存、一覧表示、削除
- 複数 URL からの引継ぎ文生成
- ChatGPT / Claude / Gemini / Custom AI の起動
- AI ごとの URL、コマンド、アイコン設定
- ホットゾーン表示、表示位置、ショートカットなどの設定
- テーマプリセットと配色調整
- ChatGPT Export を Obsidian 向け Markdown に変換する取り込み機能

## 動作環境

- Windows 10 / 11
- Node.js / npm
- ローカル実行時: Electron 31
- AI 整形と引継ぎ文生成を使う場合は Ollama

## 開発コマンド

```powershell
npm start
```

```powershell
npm run build
```

ビルド成果物は `dist/` に出力されます。

## Ollama について

AI 整形と引継ぎ文生成は Ollama を使います。既定値は次のとおりです。

- URL: `http://127.0.0.1:11434/api/generate`
- モデル: `gpt-oss:20b`

初期モデルを使う場合の例:

```powershell
ollama run gpt-oss:20b
```

別のモデルを使う場合は、アプリの設定画面でモデル名を変更できます。

## ChatGPT Export の Obsidian 取り込み

`scripts/chatgpt_export_to_obsidian.py` を同梱しており、設定画面から次を指定して実行できます。

- ChatGPT Export の入力元
- Obsidian 出力先フォルダ
- Vault ルート
- Python 実行ファイル
- `flat` / `dry-run` / 日付フィルタ

パス例は、実際の個人環境ではなく次のようなプレースホルダーで考えてください。

```text
<ChatGPT Export Folder or Zip>
<Obsidian Vault Root>
<Obsidian Vault Root>\ChatGPT Import
<Obsidian Vault Root>\chatgpt-assets
```

Vault ルートを指定した場合、添付画像や PDF などのアセットは Vault 直下の `chatgpt-assets/` に保存されます。Vault ルート未指定時は Markdown 出力先直下の `chatgpt-assets/` を使います。

同名の Markdown が出力先に既に存在する場合は、上書きや別名保存を行わず、その会話の取り込みをスキップします。

取り込み実行時はアプリ内ログに進捗が表示されます。README や公開資料では、実在するローカルパスではなく上記のようなプレースホルダーを使ってください。

## 保存先

開発時:

- `./.runtime-data/settings.json`
- `./.runtime-data/drafts.json`
- `./.runtime-data/debug.log`

パッケージ版:

- Electron の `userData` 配下

`.runtime-data/` や `debug.log` にはローカル実行時の設定やログが保存されるため、公開用のコミットや配布物には含めない想定です。

## プロジェクト構成

```text
AI Dock/
├─ assets/
├─ docs/
├─ scripts/
├─ index.html
├─ styles.css
├─ renderer.js
├─ preload.js
├─ main.js
└─ package.json
```

## 補足

- 現在のアプリバージョンは `0.4.0` です。
- 詳細な方針や履歴は `docs/` を参照してください。
- Obsidian取り込みまわりで `main.js` / `preload.js` / `renderer.js` を修正した場合は、確認前に AID を完全終了して再起動してください。
