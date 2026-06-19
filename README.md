# AI Dock

AI Dock は、本文入力・下書き保存・コピー・各AIサービス起動を 1 つの画面から扱う Windows 向けデスクトップアプリです。

## 必要環境

- Windows 10 / 11
- `AI Dock Setup 0.3.0.exe`

## インストール方法

1. `dist\AI Dock Setup 0.3.0.exe` を実行します。
2. 画面の案内に従ってインストールします。
3. インストール後に AI Dock を起動します。

## 基本機能

- 本文入力
- 下書き保存
- コピー
- ChatGPT / Claude / Gemini / カスタムAI起動
- 設定保存

## Ollama が不要な機能

以下の機能は Ollama なしで使えます。

- アプリ起動
- 本文入力
- 下書き保存
- コピー
- ChatGPT / Claude / Gemini / カスタムAI起動
- 設定保存

## Ollama が必要な機能

以下の機能を使う場合のみ Ollama が必要です。

- AI整形
- AI整形用プロンプト生成
- 引継ぎ文生成

## Ollama の導入

### 1. Ollama 本体をインストールする

まず Ollama 本体をインストールしてください。

### 2. 初期モデル `gpt-oss:20b` を使う

AI Dock の初期設定モデルは `gpt-oss:20b` です。PowerShell またはコマンドプロンプトで次を実行してください。

```powershell
ollama run gpt-oss:20b
```

このコマンドで、モデルが未取得ならダウンロードされ、その後モデルが起動します。モデルのダウンロードには時間がかかる場合があります。

### 3. 別のモデルを使う

別の Ollama モデルを使う場合は、先に Ollama 側でモデルを取得してから、AI Dock の設定画面でモデル名を変更してください。

例:

```powershell
ollama run llama3.1
```

AI Dock 側のモデル名:

```text
llama3.1
```

## Ollama 設定

設定画面から次の項目を変更できます。

- `Ollama URL`
- `Ollama モデル名`

初期値:

- `Ollama URL`: `http://127.0.0.1:11434/api/generate`
- `Ollama モデル名`: `gpt-oss:20b`

## AIサービス起動について

- ChatGPT は既定で [https://chatgpt.com](https://chatgpt.com) を開きます
- Claude は既定で [https://claude.ai](https://claude.ai) を開きます
- Gemini は既定で [https://gemini.google.com](https://gemini.google.com) を開きます
- カスタムAIは設定画面から名前・URL・起動コマンド・アイコンを設定できます

AI 起動時の優先順位:

1. ユーザーが設定したカスタム起動コマンド
2. 既定 URL
3. 本文をクリップボードへコピーして案内表示

## APIキーについて

AI Dock は OpenAI APIキー、Claude APIキー、Gemini APIキーを必要としません。各AIサービスを利用するには、それぞれのサービスのアカウントが必要です。

## Node.js / npm について

配布版を利用するだけなら、Node.js / npm / Electron 開発環境は不要です。

## 保存先

配布版では、設定や下書きは Electron の `userData` 配下に保存されます。

例:

`C:\Users\<ユーザー名>\AppData\Roaming\AI Dock`

主な保存対象:

- 設定
- 下書き
- セッション関連データ

アンインストール後も `userData` 配下のデータは残る場合があります。

## トラブルシューティング

### AIサービスが起動しない場合

- まず既定ブラウザで URL が開けるか確認してください
- カスタムAIの起動コマンドを使っている場合は、コマンドを PowerShell で直接実行して動作確認してください
- 起動に失敗した場合でも、本文はクリップボードにコピーされます

### Ollamaに接続できない場合

表示例:

```text
Ollamaに接続できませんでした。

AI整形・引継ぎ文生成を使うには、Ollamaのインストールと起動が必要です。

本文入力、下書き保存、コピー、AI起動はこのまま利用できます。
```

確認ポイント:

- Ollama がインストール済みか
- Ollama が起動中か
- 設定画面の `Ollama URL` が正しいか

### 指定モデルが見つからない場合

表示例:

```text
Ollamaには接続できましたが、指定モデルが見つかりません。

現在のモデル: gpt-oss:20b

以下を実行してモデルを準備してください。
ollama run gpt-oss:20b
```

別のモデルを使う場合は、先に `ollama run <モデル名>` で取得してから、AI Dock の設定画面でモデル名を変更してください。

### AI整形が使えない場合

- Ollama が起動しているか確認してください
- 設定画面の `Ollama モデル名` が、実際に入っているモデル名と一致しているか確認してください
- 必要に応じて次を実行してください

```powershell
ollama run gpt-oss:20b
```

### カスタムAIの起動コマンドが動かない場合

- コマンドを PowerShell や `Win + R` で直接実行して確認してください
- コマンドが失敗する場合は URL 起動へフォールバックします

### カスタムAIアイコンが表示されない場合

- ローカル画像ファイルが移動・削除されていないか確認してください
- `png` `jpg` `jpeg` `gif` `webp` `svg` `ico` を使用できます
- 別のPCへ配布する場合、元のPCの画像パスはそのままでは使えません

### アンインストール後も設定が残る場合

- `userData` 配下の保存フォルダを手動削除してください
- 例: `C:\Users\<ユーザー名>\AppData\Roaming\AI Dock`

### 修正が反映されない場合

- 古い AI Dock が起動していないか確認してください
- インストール済みの AI Dock を完全に終了してから、再インストール後に起動してください
- 設定画面下部のバージョン表示が想定のものか確認してください

## 配布前確認手順

1. `npm run build` を実行する
2. `dist\AI Dock Setup 0.3.0.exe` が生成されることを確認する
3. 別 Windows ユーザー、または別 PC でインストールする
4. 初回起動できることを確認する
5. Ollama 未導入状態で起動できることを確認する
6. 本文入力・下書き保存・コピーが使えることを確認する
7. ChatGPT / Claude / Gemini がブラウザで開くことを確認する
8. AI整形を実行し、Ollama 未接続時に分かりやすい案内が出ることを確認する
9. 指定モデル未導入時に `ollama run <モデル名>` の案内が出ることを確認する
10. 設定を変更して再起動後も保持されることを確認する
11. アンインストール後の `userData` の扱いを確認する

## ビルド

```powershell
npm run build
```

生成物:

- `dist\AI Dock Setup 0.3.0.exe`
- `dist\win-unpacked\AI Dock.exe`
