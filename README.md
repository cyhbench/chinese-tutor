# LinguaAI — AI 語言口語練習助手

> 純前端、免安裝，開啟即用的 AI 對話與發音評分工具。

## 功能特色

| 功能 | 說明 |
|------|------|
| 🗣️ AI 對話練習 | 與 GPT-4.1 AI 教師自然對話，即時糾正語法與用詞 |
| 🎙️ 語音辨識 | Azure Speech Services（優先）或 OpenAI Whisper |
| 📊 發音評分 | Azure 發音評分，顯示準確度 / 流暢度及逐字得分 |
| 🔊 語音朗讀 | Azure TTS → OpenAI TTS → Web Speech API 三層備援 |
| 📖 句子練習 | AI 隨機生成練習句，朗讀後立即顯示評分 |
| 📝 學習記錄 | 所有對話與評分儲存於瀏覽器 LocalStorage |

## 支援語言

- 🇹🇼 繁體中文 (zh-TW)
- 🇨🇳 簡體中文 (zh-CN)
- 🇺🇸 英語 (en-US)
- 🇹🇭 泰語 (th-TH)

## 快速開始

1. 直接用瀏覽器開啟 `hanyu_tutor.html`（或部署到任意靜態主機）
2. 輸入 **OpenAI API Key**（必填）
3. 選填 **Azure 語音 Key** — 啟用發音評分功能
4. 選擇想學習的語言，點擊「開始使用」

> 沒有 Azure Key 也能正常使用，語音辨識改由 OpenAI Whisper 提供，但不顯示發音評分。

## 取得 API Key

| 服務 | 申請連結 | 用途 |
|------|----------|------|
| OpenAI | [platform.openai.com](https://platform.openai.com/api-keys) | 對話、語音辨識、TTS（必填） |
| Azure Speech | [portal.azure.com](https://portal.azure.com) | 高品質 STT / TTS / 發音評分（選填） |

## 技術架構

```
hanyu_tutor.html          ← 單一 HTML 檔，無任何框架相依
├── CSS                   設計系統變數、RWD、深色主題
├── HTML                  設定頁、主介面、設定 Modal
└── JavaScript (vanilla)
    ├── 語言 / UI 設定    LANG / UI 物件
    ├── 音訊處理          MediaRecorder → WAV 轉換 → STT
    ├── Azure STT         含發音評分 (Pronunciation Assessment)
    ├── Whisper STT       備援語音辨識
    ├── GPT 對話          系統提示 + 14 訊息滾動視窗
    ├── TTS               Azure / OpenAI / Web Speech 三層
    └── 歷史記錄          LocalStorage，最多 500 筆
```

## 隱私說明

- API Key 僅儲存於**您的裝置**（瀏覽器 LocalStorage）
- 不經過任何中間伺服器，直接呼叫 OpenAI / Azure API
- 學習記錄僅存於本機，關閉瀏覽器資料後即消失

## 瀏覽器支援

需支援 `MediaRecorder API` 與 `Web Audio API`：

- Chrome / Edge 89+
- Safari 15.4+（iOS 需授權麥克風）
- Firefox 99+

## 檔案說明

| 檔案 | 說明 |
|------|------|
| `hanyu_tutor.html` | 主程式，完整應用程式 |
| `notebookLM_moon_中文.htm` | 中文學習參考資料（NotebookLM 匯出） |
