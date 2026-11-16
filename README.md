# 👾 生活管理（公版）安裝說明

這個資料夾就是整個 app。放上網站後，任何人打開網址、輸入名字、用自己的 Google 帳號登入，就會：

- 在**他自己的** Google 雲端硬碟建立一份「👾 名字 的生活管理」試算表（資料都存在這裡）
- 在**他自己的** Google 日曆建立一個「👾生活」日曆
- 每個人的資料完全分開，你看不到朋友的，朋友也看不到你的
- 不需要 Claude

只要做一次，大約 20–30 分鐘。

---

## 步驟一：申請 Google 登入用的「用戶端 ID」

1. 打開 https://console.cloud.google.com/ ，用你的 Gmail 登入。
2. 左上角「選取專案」→「新增專案」，名稱填「生活管理」→ 建立。
3. 左邊選單「API 和服務」→「程式庫」，搜尋並分別按「啟用」：
   - Google Sheets API
   - Google Drive API
   - Google Calendar API
4. 左邊選單「Google Auth Platform」（或「OAuth 同意畫面」）→「開始」：
   - 應用程式名稱：生活管理
   - 使用者支援電子郵件：你的 Gmail
   - 目標對象：**外部**
   - 聯絡資訊：你的 Gmail → 完成
5. 「目標對象」→「測試使用者」→「新增使用者」，把**你自己和每位朋友的 Gmail** 加進去（最多 100 人）。
   沒加進去的人會無法登入。
6. 「用戶端」→「建立用戶端」：
   - 應用程式類型：**網頁應用程式**
   - 已授權的 JavaScript 來源：先填 `https://你的GitHub帳號.github.io`（步驟二會知道帳號名稱）
   - 建立後會出現一串「用戶端 ID」，像 `123456-abc.apps.googleusercontent.com`，先複製起來。

## 步驟二：把 app 放上網站（GitHub Pages，免費）

1. 到 https://github.com/ 註冊帳號（帳號名稱就是你網址的一部分）。
2. 右上角「＋」→「New repository」，名稱填 `lifeapp`，選 **Public** → Create repository。
3. 按「uploading an existing file」，把這個資料夾裡的檔案全部拖進去：
   `index.html`、`manifest.json`、`sw.js`、`icon-192.png`、`icon-512.png` → Commit changes。
4. 在 repository 裡點 `index.html` → 右上角鉛筆圖示編輯 → 搜尋 `%%CLIENT_ID%%`（只有一個），
   換成步驟一複製的用戶端 ID → Commit changes。
5. 「Settings」→ 左邊「Pages」→ Branch 選 `main`、資料夾選 `/ (root)` → Save。
6. 等 1–2 分鐘，網址會是：`https://你的GitHub帳號.github.io/lifeapp/`
7. 回到 Google Cloud 的「用戶端」，確認「已授權的 JavaScript 來源」是 `https://你的GitHub帳號.github.io`（不要加 /lifeapp）。

## 步驟三：分享給朋友

把網址傳給朋友就好。朋友第一次使用：

1. 打開網址，輸入名字（月薪可以先不填）。
2. 按「用 Google 帳號開始」，選自己的 Gmail。
3. 會看到「Google 尚未驗證這個應用程式」→ 按「繼續」（因為 app 還在測試模式，這是正常的）。
4. 勾選允許存取試算表和日曆 → 完成，app 會自動建好他自己的試算表和日曆。

**放到手機桌面**：iPhone 用 Safari 打開 → 分享 →「加入主畫面」；Android 用 Chrome →「安裝應用程式」。
從桌面打開時不會有網址列，就像一般 app。

---

## 常見問題

- **為什麼有時候上方會出現「重新連線」？**
  Google 的登入每次有效約 1 小時。過期後資料會先存在手機或電腦裡，按「重新連線」就會同步回 Google 試算表。
- **換手機或電腦怎麼辦？**
  在新裝置打開網址、用同一個 Gmail 登入，app 會找到原本的試算表，選「確定」繼續使用。
- **可以重新開始嗎？**
  Settings → Account →「建立新的試算表」，會開一份全新的空白版本，舊的試算表還留在雲端硬碟。
- **試算表裡有什麼？**
  - 「收支表」：每個月的實領薪資、年終、儲蓄，改了會自動同步到 app。
  - 「支出紀錄」：所有記過的帳，方便自己看或匯出。
  - 隱藏的「_app」分頁：app 的資料，請不要修改。
- **app 能看到我其他的檔案或行程嗎？**
  不能。它只拿得到自己建立的那份試算表和「👾生活」日曆。
- **超過 100 位朋友要用？**
  需要在 Google Cloud 把 app「發布正式版」並送 Google 審核，到時候再處理即可。
