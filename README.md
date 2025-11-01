# 手把手教你：如何在本地運行你的 Google AI Studio App

## 本指南將一步步帶你完成如何在本地端啟動你的 AI Studio App。

### 前置條件 (Prerequisites)

在我們開始之前，請確保你的電腦已經具備以下工具：

1.  **Node.js：** 你的 AI Studio app 是一個基於 Node.js 的應用程式，因此你需要安裝 Node.js 和其套件管理器 `npm`。
    *   你可以從 [Node.js 官方網站](https://nodejs.org/en/download/) 下載並安裝適合你作業系統的版本。

2.  **你的 AI Studio App 程式碼：** 確保你已經將你的 AI Studio app 的程式碼下載到你的電腦上。這通常是一個資料夾，裡面包含了 `package.json`、`README.md` 等文件。

---

### 第一步：準備你的開發環境

#### 1.1 開啟終端機並導航到專案目錄

這是最關鍵的第一步，也是許多人初次嘗試時容易出錯的地方。你需要讓你的終端機 (Terminal 或 Command Prompt) 進入到你的 AI Studio App 程式碼所在的資料夾。

*   **如何操作：**
    1.  開啟你的終端機應用程式。
    2.  使用 `cd` (change directory) 命令，後面跟著你專案資料夾的完整路徑。

    **範例：**
    如果你的專案資料夾位於 `C:\Users\YourName\Documents\my-ai-studio-app`，你應該輸入：
    ```bash
    cd C:\Users\YourName\Documents\my-ai-studio-app
    ```
    （請將 `C:\Users\YourName\Documents\my-ai-studio-app` 替換成你實際的專案路徑）

*   **如何確認：**
    *   切換目錄後，可以執行 `dir` (Windows) 或 `ls` (macOS/Linux) 命令，你應該會看到列表中包含 `package.json` 這個檔案。

#### 1.2 安裝專案依賴

你的 app 依賴於許多第三方套件才能正常運行。`npm` 會讀取 `package.json` 文件，並下載所有必要的套件。

*   **在終端機中，執行以下命令：**
    ```bash
    npm install
    ```
*   **預期輸出：**
    你會看到 npm 下載並安裝套件的過程。成功完成後，會顯示類似 `up to date, audited XXX packages in Xs` 和 `found 0 vulnerabilities` 的訊息。
    ```
    up to date, audited 181 packages in 1s

    28 packages are looking for funding
      run `npm fund` for details

    found 0 vulnerabilities
    ```

---

### 第二步：設定 Gemini API 金鑰

你的 AI Studio App 需要一個 Gemini API 金鑰來與 Google 的 AI 模型進行互動。這個金鑰應該被安全地儲存在環境變數中。

*   **操作步驟：**
    1.  在你的專案根目錄下，找到並打開名為 `.env.local` 的文件。
    2.  在這個文件中，添加或修改以下這行，將 `你的_實際_Gemini_API_金鑰` 替換成你自己的 Gemini API 金鑰：
        ```
        GEMINI_API_KEY=你的_實際_Gemini_API_金鑰
        ```
    *   **哪裡取得金鑰？** 你可以在 Google AI Studio 的介面中找到並建立你的 API 金鑰。
    *   **安全提示：** `.env.local` 檔案通常會被 Git 忽略 (即不會上傳到公共版本庫)，這是為了保護你的金鑰不被公開。請務必妥善保管你的金鑰！

---

### 第三步：運行你的 AI Studio App

現在，萬事俱備，只欠東風！

*   **在終端機中，執行以下命令來啟動應用程式：**
    ```bash
    npm run dev
    ```
*   **預期輸出：**
    成功啟動後，你通常會看到應用程式正在監聽某個埠號的訊息，例如：
    ```
    ready - started server on 0.0.0.0:3000, url: http://localhost:3000
    ```
*   **查看 App：**
    打開你的網頁瀏覽器，並輸入終端機中顯示的網址 (通常是 `http://localhost:3000`)。恭喜你！你的 AI Studio App 應該已經在本地端運行起來了！

---

### 常見問題與疑難排解 (Troubleshooting)

#### 問題一：`npm ERR! enoent Could not read package.json`

*   **錯誤訊息：**
    ```
    npm ERR! enoent Could not read package.json: Error: ENOENT: no such file or directory, open 'C:\Users\YourName\package.json'
    ```
*   **原因：**
    你沒有在專案的根目錄下執行 `npm install` 命令。`npm` 試圖在你當前的終端機路徑 (`C:\Users\YourName\`) 尋找 `package.json` 但找不到。
*   **解決方法：**
    請回到「第一步：準備你的開發環境」中的「開啟終端機並導航到專案目錄」，確保你已經使用 `cd` 命令切換到包含了 `package.json` 的專案資料夾。

#### 問題二：App 沒有回應或顯示 API 錯誤

*   **原因：**
    `GEMINI_API_KEY` 設定不正確、金鑰過期或無效。
*   **解決方法：**
    1.  仔細檢查 `.env.local` 文件中的 `GEMINI_API_KEY` 是否與你在 AI Studio 中獲取的金鑰完全一致，沒有多餘的空格或其他字符。
    2.  確認你的 Gemini API 金鑰仍然有效且沒有達到使用限制。

---

### 專業提示：清理與重新安裝 (Re-installing)

有時候，為了確保一個全新的環境，或者當你遇到一些難以解決的套件問題時，你可能需要「清理」現有的安裝並重新來過。

1.  **進入專案根目錄：**
    ```bash
    cd C:\Users\YourName\Documents\my-ai-studio-app
    ```
2.  **清理舊的套件和鎖定文件：**
    這會刪除所有已安裝的 Node.js 套件 (`node_modules` 資料夾) 和 `package-lock.json` 文件 (它鎖定了所有套件的版本)。
    *   **Windows:**
        ```bash
        rd /s /q node_modules
        del package-lock.json
        ```
    *   **macOS / Linux:**
        ```bash
        rm -rf node_modules package-lock.json
        ```
3.  **重新安裝依賴套件：**
    ```bash
    npm install
    ```
    這將重新根據 `package.json` 安裝所有所需的套件。

4.  **確保 `GEMINI_API_KEY` 已設定** (同第二步)。
5.  **重新運行 App：**
    ```bash
    npm run dev
    ```
