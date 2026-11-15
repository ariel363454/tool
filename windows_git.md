# Windows Git 常用指令與操作指南

在 Windows 上使用 Git，建議下載官方安裝包後，使用內建的 **Git Bash**（指令與 Mac/Linux 相同，最推薦）或 **PowerShell / CMD（命令提示字元）**。

---

## 一、 終端機基礎路徑指令（確認自己在哪裡）

在執行任何 Git 指令前，請先確認終端機目前位於正確的專案資料夾內：

* **查看目前所在完整路徑：**
  * Git Bash / PowerShell：`pwd`
  * CMD（命令提示字元）：`cd`
* **列出資料夾內所有檔案（包含隱藏的 `.git` 資料夾）：**
  * Git Bash：`ls -la`
  * PowerShell：`ls -Force`
  * CMD：`dir /a`
* **切換進入專案資料夾：**
  ```bash
  cd 資料夾名稱
  ```
* **跨磁碟機切換（例如從 C 槽切到 D 槽）：**
  * Git Bash：`cd /d/你的資料夾路徑`
  * CMD / PowerShell：先輸入 `D:` 按 Enter，再輸入 `cd 你的資料夾路徑`
* **返回上一層資料夾：**
  ```bash
  cd ..
  ```
* **快速技巧：** 在檔案總管打開專案資料夾，在空白處按右鍵選擇 **「Open Git Bash here」**（或在網址列直接輸入 `cmd` 按 Enter），就能直接開啟並定位到該資料夾。

---

## 二、 首次安裝與全域設定（新電腦只需做一次）

1. **安裝 Git：** 前往 [git-scm.com](https://git-scm.com/) 下載並安裝 Git for Windows（安裝過程保持預設選項即可，會內建 Git Credential Manager 方便登入 GitHub）。
2. **設定你的 Git 顯示名稱與 Email（Commit 紀錄會顯示這個資訊）：**
   ```bash
   git config --global user.name "你的名字"
   git config --global user.email "你的GitHub註冊信箱@example.com"
   ```
3. **解決中文檔名顯示亂碼（顯示為數字編碼）的問題：**
   ```bash
   git config --global core.quotepath false
   ```
4. **自動處理 Windows 與 Mac/Linux 換行符號（CRLF/LF）差異：**
   ```bash
   git config --global core.autocrlf true
   ```

---

## 三、 新專案綁定 GitHub（每個專案只需做一次）

### 情境 A：本機已經寫好檔案，要上傳到 GitHub 空的 Repo
1. 進入專案資料夾後，初始化 Git：
   ```bash
   git init
   ```
2. 綁定遠端 GitHub Repo 網址：
   ```bash
   git remote add origin https://github.com/你的帳號/你的Repo名稱.git
   ```
3. 加入檔案、建立版本並首次推送：
   ```bash
   git add .
   git commit -m "first commit"
   git branch -M main
   git push -u origin main
   ```

### 情境 B：直接把 GitHub 上的專案下載到本機（自動完成初始化與綁定）
```bash
git clone https://github.com/你的帳號/你的Repo名稱.git
```

---

## 四、 日常開發常用指令（每天重複使用）

* **查看目前檔案修改狀態（最常用，隨時確認）：**
  ```bash
  git status
  ```
* **將所有修改過的檔案加入暫存區：**
  ```bash
  git add .
  ```
* **提交一個新版本並寫上說明：**
  ```bash
  git commit -m "這裡寫這次修改了什麼內容"
  ```
* **推送到 GitHub（設定過 `-u` 後，以後只需打 `git push`）：**
  ```bash
  git push
  ```
* **從 GitHub 拉取最新進度（在別台電腦改過，或團隊協作時使用）：**
  ```bash
  git pull
  ```

---

## 五、 檢查與切換遠端 Repo / 帳號憑證

* **查看目前資料夾連到哪個 GitHub Repo：**
  ```bash
  git remote -v
  ```
* **修改目前資料夾連接的遠端 Repo 網址：**
  ```bash
  git remote set-url origin https://github.com/新帳號/新Repo名稱.git
  ```
* **清除 Windows 記住的舊 GitHub 帳號密碼（切換不同 User 帳號時使用）：**
  1. 按下 `Win 鍵`，搜尋並開啟 **「認證管理員」（Credential Manager）**。
  2. 點選右側的 **「Windows 認證」（Windows Credentials）**。
  3. 在「一般認證」清單中找到 `git:https://github.com`，展開後點擊 **「移除」**。
  4. 回到終端機重新執行 `git push`，系統便會彈出視窗讓你登入新的 GitHub 帳號。