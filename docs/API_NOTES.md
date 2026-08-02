# API技術ノート (API_NOTES.md)

## 1. 使用モデルおよびエンドポイント
- **モデル名**: `gemini-2.5-flash`
- **選定理由**: 音声マルチモーダル対応、高速レスポンス、トークン効率に優れ、講義などの長尺音声処理に適しているため。
- **エンドポイント**:
  `POST https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash:generateContent?key=YOUR_API_KEY`

## 2. 送信データ構造 (JSON)
`FileReader` 経由で音声ファイルを Base64 形式にエンコードし、`inlineData` オブジェクトとして送信。

```json
{
  "contents": [{
    "parts": [
      {
        "inlineData": {
          "mimeType": "audio/mp3",
          "data": "<BASE64_ENCODED_AUDIO>"
        }
      },
      {
        "text": "プロンプト指示文章..."
      }
    ]
  }]
}
