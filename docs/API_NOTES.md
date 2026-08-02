# API技術ノート (API_NOTES.md)

## 1. 公式ドキュメント・URL
- **公式ドキュメント**: [Google AI Studio / Gemini API Docs](https://ai.google.dev/docs)
- **エンドポイント**:
  `POST https://generativelanguage.googleapis.com/v1/models/gemini-3.5-flash-lite:generateContent?key={API_KEY}`

## 2. 使用モデルおよび選定理由
- **モデル名**: `gemini-3.5-flash-lite`
- **選定理由**: 音声マルチモーダルデータの直接読み込みに対応しており、高速かつ軽量で、講義音声の文字起こしおよび要約タスクに優れているため。

## 3. 送信データ構造 (JSON)
`FileReader` 経由で音声ファイルを Base64 形式にエンコードし（先頭の Data URL プレフィックス `data:audio/...;base64,` は除去）、`inlineData` オブジェクトとしてプロンプトテキストと共に送信します。

```json
{
  "contents": [
    {
      "parts": [
        {
          "inlineData": {
            "mimeType": "audio/mp3",
            "data": "<BASE64_ENCODED_STRING>"
          }
        },
        {
          "text": "<プロンプトテキスト>"
        }
      ]
    }
  ]
}
