# 變更日誌 (Changelog)

所有關於本專案的顯著變更都將記錄於此檔案中。

## [Unreleased] - 2026-04-27
### 新增 (Added)
- 整合 `Socket.IO` 客戶端程式庫，實作透過 WebSocket 與後端伺服器通訊的功能。
- 新增解析 URL Query Parameters 中 `tag` 變數的邏輯，以決定要給予使用者的標籤。
- 新增解析 URL Query Parameters 中 `port` 變數的邏輯，用以支援本地端伺服器測試 (`irl-svr.ee.yzu.edu.tw:port`)。
- 在 `bot` 參數的處理上增加彈性，可自動辨識組合為 Heroku 網域。
- 新增 `redirect` 參數支援，允許在上完標籤後跳轉至指定的目標網頁。

### 變更 (Changed)
- 調整 `index.html` 畫面，新增顯示「欲設定標籤」資訊。
- 連線成功送出事件後，預設延遲兩秒關閉視窗，若有提供 `redirect` 參數則改為執行網頁跳轉。
- 改善 `connect_error` 事件處理，增加 `transports` 設定以強化連線穩定性，並在畫面上顯示更詳細的錯誤原因。
