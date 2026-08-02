# 講義ノートAI (Gemini API連携)

講義や自習の録音音声（MP3, M4A, WAV等）から「全文文字起こし」「3行要約」「主要ポイント（3〜5個）」を自動生成するスマホ対応Webアプリです。

## ✨ 特徴
- **フロントエンド完結（サーバーレス）**: HTML/CSS/JS のみで動作し、GitHub Pages で簡単にホスティング可能。
- **安全なAPIキー管理**: Gemini APIキーはユーザーのブラウザ（`localStorage`）にのみ保存され、リポジトリや外部サーバーへ送信・公開されることはありません。
- **スマホ最適化（レスポンシブ UI）**: Tailwind CSS を活用し、スマートフォン（iOS/Android）から快適に操作可能。

## 🚀 使い方
1. **APIキーの設定**:
   - 右上の「APIキー未設定」ボタンをタップ。
   - [Google AI Studio](https://aistudio.google.com/) で取得した API キーを入力して「保存する」をタップ。
2. **講義名の入力（任意）**:
   - 講義名や回数を入力（例: 経済学入門 第5回）。
3. **音声ファイルの選択**:
   - 「音声ファイルを選択」から、録音した講義音声（数分程度の短尺推奨）を選択。
4. **実行**:
   - 「✨ 文字起こし＆要約を実行」ボタンをタップ。
5. **結果の確認・コピー**:
   - 「📊 要約 & 要点」タブと「📝 全文文字起こし」タブを切り替えて結果を確認。
   - コピーボタンでクリップボードに取得可能。

## 🛠️ 技術スタック
- **Frontend**: HTML5, Vanilla JavaScript, Tailwind CSS (CDN)
- **AI Model**: Google Gemini API (`gemini-2.5-flash`)
- **Hosting**: GitHub Pages

## 📂 ドキュメント
詳しい仕様やテスト結果については `/docs` フォルダーを参照してください。
- [仕様書 (SPEC.md)](./docs/SPEC.md)
- [APIノート (API_NOTES.md)](./docs/API_NOTES.md)
- [テストケース (TESTCASES.md)](./docs/TESTCASES.md)
- [ステータス・ログ (STATUS.md)](./docs/STATUS.md)
- [使用プロンプト (PROMPTS.md)](./docs/PROMPTS.md)