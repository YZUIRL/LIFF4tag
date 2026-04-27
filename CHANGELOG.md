# 變更日誌 (Changelog)

所有關於本專案的顯著變更都將記錄於此檔案中。

## [Unreleased] - 2026-04-27
### 新增 (Added)
- 整合 `Socket.IO` 客戶端程式庫，實作透過 WebSocket 與後端伺服器通訊的功能。
- 新增解析 URL Query Parameters 中 `tag` 變數的邏輯，以決定要給予使用者的標籤。
- 新增解析 URL Query Parameters 中 `port` 變數的邏輯，用以支援本地端伺服器測試 (`irl-svr.ee.yzu.edu.tw:port`)。
- 在 `bot` 參數的處理上增加彈性，可自動辨識組合為 Heroku 網域。

### 變更 (Changed)
- 調整 `index.html` 畫面，新增顯示「欲設定標籤」資訊。
- 連線成功送出事件後，新增自動延遲兩秒關閉 LIFF 視窗的流程。
