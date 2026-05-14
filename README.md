# EduEventSystem

活動報到管理系統，用於活動現場報到、報到紀錄查詢、面試叫號與即時狀態總覽。系統前端以 HTML、CSS、JavaScript 建置，並透過 Google Apps Script API 存取後端資料。

## 專案功能

- 登入與角色權限管理
- 系統總覽儀表板
- 活動管理與報到開關
- 現場報到名單查詢與報到操作
- 依活動地點、報到狀態、面試狀態、報到時間區間進行篩選
- 報到紀錄查詢與統計
- 面試叫號、取消叫號、完成面試
- 批次叫號與批次完成面試
- 遲到報到提示與單獨叫號限制
- 當日各活動場地叫號與報到進度總覽
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

## Git 使用方式

第一次推送分支：

```bash
git add .
git commit -m "Update project documentation"
git push -u origin 20260514-3
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
- 場地篩選選項會依實際名單資料產生，不使用固定試場名稱。
- 若 Apps Script 權限或部署網址變更，需同步更新前端 API 設定。

