<div align="center">

<a href="https://blog.dei3c.com" target="_blank" rel="noopener noreferrer">
  <img src="https://github.com/user-attachments/assets/2830eb70-512c-4ddb-87ec-5213a6e465b1" alt="得翼科技 | 印表機耗材追蹤器" height="70" />
</a>

<br /><br />

**繁體中文** · [English](docs/readme/README_en.md) · [简体中文](docs/readme/README_zh-CN.md)

# 印表機耗材追蹤器 (Printer Supply Tracker)

### 專為企業辦公室、總務採購與電腦資訊網管打造的印表機耗材自動監控與 Google 試算表同步工具
告別手動巡檢與逐台抄表！透過 SNMP 自動輪詢碳粉剩餘量與列印計數，智慧排程背景上傳，開機自動補查補登。

[![Platform](https://img.shields.io/badge/Platform-Windows%207%20%7C%208%20%7C%2010%20%7C%2011%20%7C%20WinPE-blue?style=flat-square&logo=windows)](https://github.com/robert820/printer-supply-tracker)
[![License](https://img.shields.io/badge/License-Freeware-informational?style=flat-square)](LICENSE)
[![Type](https://img.shields.io/badge/Type-Freeware%20%7C%20Portable-success?style=flat-square)](#-下載與使用說明)
[![Download](https://img.shields.io/badge/Download-GitHub%20Releases-blue?style=flat-square&logo=github)](https://github.com/robert820/printer-supply-tracker/releases)

**徹底擺脫 Windows 工作排程器失靈窘境，以輕量常駐系統列實現 100% 無人值守自動化管理！**

[軟體簡介](#-軟體簡介) · [核心功能](#-核心功能) · [軟體操作畫面](#-軟體操作畫面) · [下載與使用說明](#-下載與使用說明) · [系統需求](#-系統相容性與需求) · [常見問題](#-常見問題-faq) · [問題反饋](#-問題反饋與支援)

</div>

---

## 📖 軟體簡介

在企業、學校、辦公室或租賃事務機管理中，總務與 IT 人員每逢月底或固定週期，往往面臨繁重的手動作業：
1. **逐台抄表耗時費力**：必須親自走到每台印表機/影印機前調出計數器選單，記錄黑白與彩色列印張數。
2. **耗材庫存措手不及**：無法即時掌握黑色、青色、洋紅、黃色（CMYK）碳粉消耗速率，常等到印表機亮紅燈才緊急叫貨。
3. **傳統工作排程器容易開天窗**：使用 Windows 工作排程器執行指令碼時，常因電腦休眠、密碼過期、權限不符或國定假日放假而錯過排程，造成整期統計數據缺漏。

**「印表機耗材追蹤器 (Printer Supply Tracker)」** 是一款專為 Windows 環境打造的原生免安裝綠色常駐工具。本工具透過標準 SNMP 網路協定定期自動輪詢所有印表機狀態，精確獲取列印總張數與各色碳粉百分比，並經由 Web API 自動同步寫入至指定的 **Google 試算表**。

內建獨立的**智慧排程與補登引擎**，能自動避開週末與台灣國定假日，若開機時發現錯過指定排程時間，將立即主動執行「開機補查」，確保報表永遠準時完整！

---

## ✨ 核心功能

### 1. ⚡ 自動掃描多廠牌印表機狀態 (SNMP 協定)
- 透過網路以 SNMP 協定自動查詢所有列印設備。
- 完整讀取：設備型號、序號、放置位置、黑白列印總張數、彩色列印總張數、CMYK 各色碳粉剩餘趴數。
- **具體支援品牌與型號適配清單**：
  - **Ricoh (理光)**：
    - 彩色機種：全系列商用彩色事務機（支援黑白/彩色獨立計數與 CMYK 4 色碳粉水位）
    - 黑白機種：MP 3554、MP 3555、IM 3500、MP 6054、MP 6055、MP 6502、MP 6503、MP 7502、MP 7503
  - **Fuji Xerox / FUJIFILM (富士全錄 / 富士軟片)**：
    - 彩色機種：ApeosPort 系列、DocuCentre 系列彩色事務機
    - 黑白機種：ApeosPort 3060、ApeosPort 3560、DocuCentre 3060
  - **SHARP (夏普)**：
    - 彩色機種：MX 彩色系列、BP 彩色系列複合機
    - 黑白機種：MX-M 系列（包含 MX-M365N）、BP-M 系列
- 防呆與離線防卡死：若設備離線或無回應，自動標示「連線失敗」並繼續輪詢下一台，查詢流程絕不卡住中斷。

### 2. 📊 自動同步至 Google 試算表 (雲端自動彙整)
- 查詢完畢後自動將所有設備的計數、碳粉與時間戳記格式化上傳至 Google 試算表。
- 支援 Google Apps Script Web App 整合，無須在本機安裝龐大的 Python 或 Node.js 執行環境。
- 具備上傳防呆驗證，若網址錯誤或試算表分頁權限異常，主動提示精確錯誤資訊方便排查。

### 3. ⏰ 智慧排程與自動補登防漏機制 (告別工作排程器)
- **內建計時排程引擎**：放棄易受系統環境干擾的 Windows Task Scheduler，改由程式內部常駐計時，精準觸發。
- **支援每月多日排程**：可自由勾選每月固定多天自動執行（如每月 1 號、15 號、25 號）。
- **週末自動提前／順延**：遇週六、週日自動改於鄰近工作日執行。
- **國定假日自動辨識**：自動比對台灣政府行政機關辦公日曆，遇連假順延至工作日。
- **開機自動補查（補登機制）**：若排程時間電腦未開機，只要重新開機進入系統，程式自動偵測並補做錯過的排程，報表絕不漏登。

### 4. 🛡️ 系統匣 (System Tray) 常駐與三色狀態指示燈
- 縮小至工作列右下角系統匣，不佔用任何桌面空間。
- 即時狀態 LED 指示燈：
  - 🔵 **藍燈**：正在執行 SNMP 輪詢或上傳中
  - 🟢 **綠燈**：所有設備連線正常且排程待命
  - 🔴 **紅燈**：有設備連線異常或尚未設定 IP
- 雙擊系統列圖示可隨時喚醒設定介面；滑鼠右鍵選單支援「立即執行」與「安全退出」。

### 5. 🧪 手動測試與立即執行
- 提供 **「測試 SNMP 連線」** 按鈕：即時測試各 IP 是否能正常通訊，不會寫入雲端試算表。
- 提供 **「立即執行與上傳」** 按鈕：隨時手動完整走一次掃描與上傳流程，不用苦等排程。

### 6. 📝 完整本機稽核日誌 (Log)
每一次輪詢結果、上傳歷程、錯誤代碼皆完整記錄於本機日誌檔（`PST_Unattended.log`），便於 IT 人員事後追蹤與稽核。

---

## 📸 軟體操作畫面

<div align="center">
  <img src="images/應用程式執行畫面.png" alt="印表機耗材追蹤器操作介面" width="720" />
  <p>▲ 印表機耗材追蹤器主介面：即時設備狀態清單、CMYK 碳粉水位進度條與排程參數配置</p>
</div>

---

## 📦 下載與使用說明

### 📥 下載方式
1. 前往本專案的 [Releases 頁面](https://github.com/robert820/printer-supply-tracker/releases) 下載最新版執行檔。
2. 本程式為**單一免安裝綠色二進位執行檔**，無須安裝額外相依庫或 Runtime，下載即可隨身攜帶。

### 🚀 快速上手五步驟

#### 第一步：設定目標印表機清單
開啟主畫面進入「目標設備與 SNMP」分頁，輸入欲監控的印表機 IP 位址（一行一個），並填寫 SNMP Community 字串（多數預設為 `public`）。

#### 第二步：配置 Google 試算表整合
進入「一般設定」分頁，貼上您的 Google Apps Script Web App 部署網址（以 `https://.../exec` 結尾）並指定寫入的工作表分頁名稱。

#### 第三步：連線測試確認
點擊「測試 SNMP 連線」按鈕確認每台事務機能正常回應。若有顯示連線失敗，請檢查該設備電源或防火牆設定。

#### 第四步：設定執行時間參數
進入「執行時間參數」分頁：
1. 勾選每月預計執行的日期與時間。
2. 建議保持勾選 **「週末提前執行」**、**「國定假日提前執行」** 與 **「啟用開機補查機制」**。
3. 點擊儲存，排程器即進入全自動倒數監控狀態。

#### 第五步：啟用開機自動啟動
在「系統設定」分頁中開啟「開機自動啟動」，日後電腦開機即可自動常駐於系統列無人值守運作。

---

## 🖥️ 系統相容性與需求

- **作業系統**：Windows 11 / 10 / 8.1 / 8 / 7 (SP1) 及 Windows Server 2012 以上版本
- **硬體架構**：64 位元 (x64) 與 32 位元 (x86) 通用相容
- **網路環境**：本機需與印表機處於同一區域網路 (LAN) 或具備路由通訊能力，並具備對外網際網路連線以同步 Google 試算表
- **相依套件**：原生 Rust 編譯，**純淨綠色單檔**，無須額外安裝 .NET Framework、VC++ 執行庫或 Python

---

## ❓ 常見問題 (FAQ)

<details>
<summary><b>Q1: 這款軟體完全免費嗎？中小企業或工作室可以使用嗎？</b></summary>
A: 是的！本軟體採用專有免費軟體授權（Freeware），免費提供個人、機關行號、中小企業內部使用，亦可由電腦維修與辦公事務機租賃商作為維護工具使用。惟嚴禁單獨販售、出租或重新捆綁商業收費軟體營利。
</details>

<details>
<summary><b>Q2: 目前具體支援哪些印表機與影印機機型？</b></summary>
A: 本工具核心已針對辦公事務機三大主力品牌建立專屬 OID 解析規則，具體支援機型涵蓋：
- **Ricoh (理光)**：
  - 彩色機種：全系列商用彩色多功能事務機（黑白與彩色列印張數、CMYK 四色碳粉剩餘量）
  - 黑白機種：MP 3554、MP 3555、IM 3500、MP 6054、MP 6055、MP 6502、MP 6503、MP 7502、MP 7503
- **Fuji Xerox / FUJIFILM (富士全錄 / 富士軟片)**：
  - 彩色機種：ApeosPort 系列、DocuCentre 系列彩色複合機
  - 黑白機種：ApeosPort 3060、ApeosPort 3560、DocuCentre 3060
- **SHARP (夏普)**：
  - 彩色機種：MX 彩色系列、BP 彩色系列複合機
  - 黑白機種：MX-M 系列（含 MX-M365N）、BP-M 系列
只要設備開啟標準 SNMP 服務，程式即會自動識別機型並提取正確欄位數據。
</details>

<details>
<summary><b>Q3: 為什麼要自己做排程常駐，而不是用 Windows 工作排程器？</b></summary>
A: Windows 工作排程器在個人電腦進入睡眠 (Sleep) 時常無法如期喚醒，遇密碼過期容易靜默中斷，且缺乏友善的「休眠/關機後重開自動補跑」防漏機制。本工具自建常駐排程與開機補查引擎，徹底杜絕數據漏失風險。
</details>

<details>
<summary><b>Q4: 關閉視窗後程式會停止運作嗎？</b></summary>
A: 不會。點擊右上角關閉視窗只會將畫面縮小至系統匣繼續在背景待命。若要徹底關閉程式，請在右下角系統匣圖示點擊滑鼠右鍵並選擇「結束程式」。
</details>

---

## 💬 問題反饋與支援

- 🐛 **錯誤回報與功能建議**：歡迎至本專案的 [Issues 頁面](https://github.com/robert820/printer-supply-tracker/issues) 提出。
- 🌐 **得翼科技官方網站**：[https://blog.dei3c.com](https://blog.dei3c.com)

---

## 📄 授權條款 (License)

本軟體採用專有免費軟體授權（Proprietary Freeware），完整授權條款、散布限制與免責聲明請參閱 [LICENSE](LICENSE) 檔案。
