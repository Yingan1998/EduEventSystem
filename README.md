# EduEventSystem

活動報到管理系統，用於活動現場報到、報到紀錄查詢、面試叫號與即時狀態總覽。系統前端以 HTML、CSS、JavaScript 建置，並透過 Google Apps Script API 存取後端資料。

## 專案功能

- 登入與角色權限管理
- 系統總覽儀表板
- 活動管理與報到開關
- 現場報到名單查詢與報到操作
- 現場報到支援活動地點、報到狀態、面試狀態、報到時間區間等多條件篩選
- 現場報到支援清除篩選與長名單固定表頭
- 手機、平板、電腦可使用相機掃描身分證條碼輔助報到
- 掃描報到會先顯示姓名、身分證字號、活動編號與試場供人工確認
- 報到紀錄查詢、篩選與即時統計
- 面試叫號、取消叫號、完成面試與自動完成逾時面試
- 批次叫號、批次取消叫號與批次完成面試
- 批次叫號前顯示確認名單
- 面試叫號依場地分組，並顯示下一位建議叫號人員
- 已叫號未完成者置頂，已完成面試者隱藏
- 遲到報到提示、可叫號時段設定與單獨叫號限制
- 遲到報到者獨立區塊顯示
- 當日各活動場地叫號與報到進度總覽
- 各場地狀態標籤：正常、報到中、等待叫號、進度落後
- 訪客模式即時查看總覽資訊

## 使用角色

| 角色 | 可使用功能 |
| --- | --- |
| 管理者 | 系統總覽、活動管理、現場報到、報到紀錄、面試叫號、系統設定 |
| 報到人員 | 系統總覽、現場報到、報到紀錄 |
| 面試人員 | 系統總覽、面試叫號 |
| 訪客 | 系統總覽查詢 |

## 技術架構

- 前端：HTML、CSS、JavaScript
- UI：Bootstrap 5
- 條碼掃描：BarcodeDetector API，並使用 ZXing Browser 作為 fallback
- 後端資料介接：Google Apps Script Web App
- 資料來源：Google 試算表或 Apps Script 對應資料服務

## 檔案結構

```text
EduEventSystem/
├── index.html              # 系統主頁面與前端邏輯
├── style.css               # 系統樣式
├── cte-logo-HFD82aLI.png   # 系統相關圖片資源
└── README.md               # 專案說明文件
```

## 本機執行

此專案為靜態前端頁面，可直接使用瀏覽器開啟：

```text
index.html
```

若使用 XAMPP，可將專案放在：

```text
C:\xampp\htdocs\EduEventSystem
```

再透過瀏覽器開啟：

```text
http://localhost/EduEventSystem/
```

## API 設定

前端 API 位於 `index.html`：

```javascript
const API_URL = "Google Apps Script Web App URL";
```

若更換 Google Apps Script Web App，請更新此常數。

## Google Apps Script Actions

前端目前會呼叫下列主要 actions：

```text
login
getActivities
createActivity
updateActivity
toggleCheckin
getCheckinMembers
checkinMember
cancelCheckin
writeCheckinLog
getCheckinLogs
batchSetCurrentCalling
batchUpdateInterviewStatus
cancelCurrentCalling
recordVisitor
visitorHeartbeat
getVisitorStats
markAbsent
setLateCallAvailableTime
```

後端需支援 `markAbsent` 與 `setLateCallAvailableTime`，才能完整保存自動缺考與遲到報到可叫號時段。

`活動人員資料` 建議包含 `可叫號時段` 欄位，用於保存遲到報到者可被單獨叫號的時間。

## 上版備註

### 20260516-2

- 現場報到管理隱藏「目前叫號」欄位，表格欄位與載入狀態同步調整。
- 現場報到管理搜尋支援姓名、身分證字號與活動編號查詢。
- 現場報到管理時間篩選改為依活動報到時段篩選。
- 現場報到管理將「操作」欄移至第一欄，方便現場快速報到或取消報到。
- 面試叫號預設每頁 5 筆，並可彈性切換為每頁 10 筆或 20 筆。
- 面試叫號全選與批次叫號/完成/取消叫號改為只處理目前頁面已勾選人員，降低跨頁誤操作風險。

## Git 使用方式

目前主要開發分支：

```bash
20260516-2
```

第一次推送分支可使用：

```bash
git add .
git commit -m "Release 20260516-2"
git push -u origin 20260516-2
```

之後更新：

```bash
git add .
git commit -m "Describe your changes"
git push
```

## 注意事項

- 面試叫號頁僅顯示已報到、遲到報到，以及仍在報到截止時間內的人員。
- 遲到報到者不會進入批次叫號，需於面試叫號階段單獨叫號。
- 遲到報到者可設定彈性可叫號時段；時段未到時會阻擋叫號。
- 面試叫號、取消叫號、面試完成與自動完成面試都會寫入報到紀錄。
- 設定遲到可叫號時段不會寫入報到時間，避免被統計成重複報到。
- 面試完成者會鎖定，不可取消報到或回退叫號。
- 場地篩選選項會依實際名單資料產生，不使用固定試場名稱。
- 相機掃描需瀏覽器允許 camera permission；正式環境建議使用 HTTPS。
- ZXing fallback 透過 CDN 載入，現場環境需可連外網；若需離線使用，建議改成本機檔案。
- 若 Apps Script 權限或部署網址變更，需同步更新前端 API 設定。
