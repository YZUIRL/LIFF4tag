# LIFF4tag 專案架構文件

## 系統概述
這是一個建置於 GitHub Pages 上的 LINE LIFF (LINE Front-end Framework) 單頁應用程式。主要功能為讀取網址中帶有的參數，並透過 WebSocket (Socket.IO) 向後端的 Python 伺服器發送對應的事件與訊息，達到快速為使用者貼上標籤或觸發流程的目的。

## 核心技術與依賴
*   **HTML/CSS/JavaScript**: 原生前端語言與簡單的響應式版面設計。
*   **LIFF SDK (`https://static.line-scdn.net/liff/edge/2/sdk.js`)**: 處理 LINE 登入授權並獲取使用者的 User ID。
*   **Socket.IO Client (`https://cdn.socket.io/4.7.2/socket.io.min.js`)**: 處理與 Python 後端伺服器 (使用 `python-socketio`) 的即時雙向連線。

## 參數與連線機制

網頁透過 URL Query Parameters (`?key=value`) 接收動態變數：
1.  **`bot`**: 代表目標伺服器的 App Name 或機器人識別名稱。
    *   **Heroku 環境**: 當僅傳入字串（如 `yzulabuse`）時，系統會自動組合出 `https://yzulabuse.herokuapp.com`。
    *   **備註**: 不論 `bot` 參數為何，為了配合後端設定，Socket.IO 的 Namespace 固定為 `/websoc`，發送事件名稱固定為 `websoc_message`。
2.  **`tag`**: 代表欲幫使用者新增的標籤名稱。將與系統指令組合為 `set_tag|標籤名稱` 後送出。
3.  **`port` (選用)**: 用於本地端測試環境。當有提供此參數時（如 `?port=5016`），連線目標將會轉向本地伺服器 `https://irl-svr.ee.yzu.edu.tw:5016`。
4.  **`redirect` (選用)**: 用於發送事件後的畫面跳轉。若有提供此參數（如 `?redirect=https://google.com`），網頁將在 2 秒後跳轉至該網址，而非直接關閉視窗。

## 觸發流程
1.  使用者點擊夾帶 `bot` 與 `tag` 參數的 LIFF 網址。
2.  LIFF SDK 啟動，進行登入驗證取得 User ID。
3.  前端程式解析網址參數，建構對應的伺服器連線網址與 Namespace。
4.  建立 Socket.IO 連線並在連線成功 (`connect`) 觸發時，發送 JSON 格式的 Sensor Payload。
5.  收到成功發送後，等待 300 毫秒。若有設定 `redirect` 參數，則跳轉至指定網頁；否則呼叫 `liff.closeWindow()` 關閉網頁。
6.  **例外處理與超時保護**：若發生 `connect_error` 或是連線卡住超過 5 秒，系統將視為超時並強制作為中繼站將使用者跳轉至 `redirect` 目標（如果有的話），以避免畫面永久卡死。
