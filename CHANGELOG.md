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
- 修正 Socket.IO 的 `Namespace` 與事件名稱 (`eventName`) 為固定的 `websoc` 與 `websoc_message`。
- 連線成功送出事件後，預設會給予 300 毫秒的微小緩衝再執行網頁跳轉或關閉，以確保 WebSocket 封包能確實送出，避免因瞬間換頁導致傳輸被瀏覽器強制中斷。
- 改善 `connect_error` 事件處理：除了顯示詳細錯誤訊息外，若上標籤失敗也會在 3 秒後將使用者跳轉至目標網頁，避免卡在中繼站。
- 增加 Socket 連線超時（Timeout）機制，當連線卡住無回應時，確保 5 秒後自動執行重新導向，提升中繼跳轉的穩定性。
