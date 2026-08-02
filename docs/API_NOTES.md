# API技術ノート (API_NOTES.md)

## 1. 使用モデルおよびエンドポイント
- **モデル名**: `gemini-3.5-flash-lite`
- **選定理由**: 高速な応答性能を持ち、音声データの解析、文字起こし、および要約生成を効率的に実行できるため採用した。また、現在利用可能なGemini APIのモデルの中で軽量かつ応答速度に優れている。
- **エンドポイント**:
  `POST https://generativelanguage.googleapis.com/v1/models/gemini-3.5-flash-lite:generateContent?key=YOUR_API_KEY`

音声ファイルはブラウザの `FileReader` を利用して Base64 形式へ変換し、`inlineData` として Gemini API に送信する。

```json
{
  "contents": [
    {
      "parts": [
        {
          "inlineData": {
            "mimeType": "audio/mp3",
            "data": "<BASE64_ENCODED_AUDIO>"
          }
        },
        {
          "text": "以下の音声を聞き、文字起こし・要約・主要ポイントを出力してください。"
        }
      ]
    }
  ]
}
```

---

## 3. プロンプト設計

Geminiには以下の指示を与えている。

- 音声内容を全文文字起こしする。
- 内容を3行で要約する。
- 重要なポイントを3〜5個抽出する。
- 指定した区切り文字（`---3行要約---`、`---主要ポイント---`、`---全文文字起こし---`）を付けて出力する。

これにより、JavaScript側では区切り文字を利用して要約・主要ポイント・全文を分割し、それぞれ画面へ表示している。

---

## 4. APIレスポンス処理

Gemini APIから返されたレスポンスは

```javascript
data.candidates[0].content.parts[0].text
```

から取得する。

取得した文字列を区切り文字で分割し、

- 3行要約
- 主要ポイント
- 全文文字起こし

の3つに分類して画面へ表示する。

---

## 5. APIキー管理

APIキーはソースコードへ直接記述せず、ブラウザの `localStorage` に保存して管理する。

```javascript
localStorage.setItem("gemini_api_key", apiKey);
```

実行時には

```javascript
const apiKey = localStorage.getItem("gemini_api_key");
```

で取得し、APIリクエストに利用する。

この方式により、GitHubなどの公開リポジトリへAPIキーが含まれないようにしている。
