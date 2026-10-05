# 同學評分榜

和朋友一起為同學打分：**顏值、性格、社交、財富** 四個維度（1–10 分），即時排行榜。

## 用法

1. 開啟網站（GitHub Pages 連結或直接開 `index.html`）。
2. 右上角「新增同學」→ 上傳相片（可裁剪 / 旋轉 / 翻轉）→ 填名稱與標籤。
3. 點進同學詳情，用滑桿評分，儲存後即時上榜。
4. 第一次投票 / 新增 / 刪除前，需要輸入**房間金鑰**（見 Discord 訊息或專案內 `ROOM_KEY`）。

## 即時同步（雲端共用）

- 所有資料存放在 **Firebase Firestore**（專案 `class-rating-hk`），所有人打開同一個網址即見同一份資料。
- 新增、評分、刪除會**即時同步**：排行榜自動更新，唔使匯出 / 匯入。
- 離線時改動會暫存喺本機，重新上線自動補交；「資料」頁可以下載 JSON 做備份。
- 瀏覽器本地仍會快取一份（localStorage），亦可手動匯入 JSON 合併到雲端。
- 淘汰賽（`#/tour/male`、`#/tour/female`）亦已雲端即時同步：每場對決所有人見到同一份，投票合併（每人一票可改），滿 3 票自動晉級（多數者贏）或按「鎖定賽果」，完賽後顯示合併賽果表（collection `tournaments`）。

## 技術

- 純靜態單頁（HTML + CSS + JS），前端直連 Firebase Firestore（開放讀寫規則 + 客戶端房間金鑰把關）。
- Firebase 設定：`firebase.json`（規則）、`.firebaserc`（專案）、`firestore.rules`。
- 資料結構：collection `entries`，每份 doc 含 `id / name / photo / tags / desc / createdBy / createdAt / votes`，`votes` 以 `voter` 為鍵（map）。
- 相片上傳後經 Cropper.js 裁切並壓縮為 640px JPEG 存入資料，便於傳輸。
- `data.json` 為舊版共用種子檔，已不再自動讀取，僅作歷史參考。

## 備註

- 此站為朋友間的主觀娛樂評分。請尊重每一位同學：只上傳經當事人同意嘅相片，評分不代表事實，唔好用嚟欺凌、嘲笑或公開羞辱。
