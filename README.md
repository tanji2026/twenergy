# 碳吉 TanJi：淨零群募平台 🌿

## 1. 專案介紹

### 1.1 系統目的簡介

本系統旨在打造全台首創透明、低門檻的轉型金融（Transition Finance）群募媒合平台。

透過「多元淨零專案切換」、「微型投資效益即時試算」、「銀行信託撥款進度牆」與「個人永續履歷（碳吉寶寶）」等模組，結合現代化數位支付展示與去中心化防偽憑證（SHA256 加密展示），將艱澀氣候資金缺口與轉型金融，轉化為一般大眾百元即可參與的普惠金融行動，杜絕企業「漂綠（Greenwashing）」風險，實踐公正轉型與氣候正義。

---

## 2. 系統架構與範圍

### 2.1 系統架構圖

本系統採用 **Serverless 無伺服器架構** 設計，前端採 Vanilla JS 搭配 Tailwind CSS 進行響應式交互渲染，後端完全整合 Firebase 雲端生態系進行即時數據同步與去中心化驗證。

```mermaid
graph TD
    classDef client fill:#f0f9fa,stroke:#007d8a,stroke-width:2px,color:#071528
    classDef auth fill:#e0f2fe,stroke:#0284c7,stroke-width:2px,color:#071528
    classDef logic fill:#fef3c7,stroke:#d97706,stroke-width:2px,color:#071528
    classDef data fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px,color:#071528

    subgraph Client_Zone [用戶端環境 - 前端展示與交互層]
        Browser[("使用者瀏覽器<br>HTML5 / Tailwind CSS / ES6 Module")]:::client
    end

    subgraph Cloud_Service [Firebase Cloud Serverless 環境]
        subgraph Auth_Layer [身分授權層]
            FirebaseAuth["Firebase Authentication<br>(Email-密碼 / 匿名訪客)"]:::auth
        end

        subgraph Data_Layer [分散式即時數據層]
            Firestore[("Cloud Firestore<br>公共配置 / Feeds 動態 / 用戶 Profile")]:::data
        end
    end

    Browser -- "1. 帳戶登入/註冊/匿名認證" --> FirebaseAuth
    FirebaseAuth -- "2. 回傳 Token 與 UID 安全上下文" --> Browser
    Browser -- "3. 即時訂閱與雙向寫入數據 (Snapshot)" --> Firestore
    Firestore -- "4. WebSocket 即時推播更新" --> Browser

```

### 2.2 系統範圍

* **前端展示層（Tailwind CSS / HTML5 / Canvas）**：
* 全站架構採用單頁式響應式設計（RWD），導入主次分明的高層級視覺架構（Visual Hierarchy）。
* **碳吉寶寶培育艙**：利用放射狀漸層（Radial Gradient）與 CSS 動態浮動（Float Animation）技術模擬智慧溫室光影深度，避免大面積模糊濾鏡，大幅優化行動端滾動流暢度。
* **動態特效模組**：內建 HTML5 Canvas 高效能五彩紙屑（Confetti）粒子物理碰撞系統，於完成專案投資時即時渲染慶祝動畫；每日打卡導入貝茲曲線浮動上升葉片特效（Floating Leaf Animation）。


* **業務邏輯層（ES6 JavaScript）**：
* 負責即時計算專案募資進度百分比、處理打卡防重複限制、計算碳吉寶寶 **5 大階段等級進化算法**、以及依據不同專案方法學換算減碳效益當量與經驗值（EXP）。


* **數據同步與安全層（Firebase Web SDK v10.11.0）**：
* 串聯安全授權層，若雲端資料庫連線因故受阻，系統將自動降級（Graceful Degradation）啟動**本地快取沙盒備援（LocalStorage / In-memory storage）**，確保用戶體驗不中斷。



### 2.3 交付項目

1. **網頁應用程式**：單頁式高整合原始碼檔案 `index.html`（內含完整模組化 JS 與各視窗 Modal 元件）。
2. **多媒體與圖資資產（Assets Package）**：
* `assets/tanjibaby/`：包含碳吉寶寶各型態靜態圖像（`tanjibaby.png`、`tanjibaby9.png`、`tanjibaby_ceo.png`、`tanjibaby_tech.png`）及打卡動態交互影片（`tanjibaby_hi.mp4`）。
* `assets/projects/`：淨零專案與成功案例縮圖資產（如 `project_solar.png`、`success_hualien.png` 等）。


3. **合規合約文件檔（Docs Mimic）**：包含平台隱私條款、計算方法學說明書、信託契約範本、銀行撥款申請書等四大 PDF 靜態下載路徑。
4. **系統規格說明書**：本 `README.md` 開發者規格文件。

---

## 3. 業務功能需求

| 需求編號 | 功能名稱 | 參與者 | 功能描述 | 業務邏輯與計量備註 |
| --- | --- | --- | --- | --- |
| **FR-01** | 多重永續帳戶授權 | 投資人 | 提供 Email 與密碼註冊、登入功能，亦支援訪客匿名登入，免註冊即刻建立臨時 UID 展開體驗。 | 優先串聯 Firebase Auth 雲端驗證。若遇斷線或特定管理員帳號 admin@tanji.com 則切換至本地 LocalStorage 快取備援機制。 |
| **FR-02** | 淨零專案調度與試算 | 投資人 | 支援切換 5 大淨零計畫。拖拉滑桿或手動輸入金額，系統即時連動試算該專案對應減碳量與 EXP，並實時放大與加深寶寶培養艙光影。 | 減碳效益當量公式：個人減碳效益(kg CO2e) = (個人參與金額 / 專案目標總額) × 首年預估總減量當量。EXP 公式：每投入 10 元可轉換為 1 EXP。 |
| **FR-03** | 信託金流交付模擬 | 投資人 | 點擊參與跳出信託確認視窗，提供信用卡繳款、行動支付轉帳、銀行虛擬帳號三大代收代付保管管道。 | 模擬完成後，金額累計至個人與專案總額，異步完成雲端同步，並觸發全螢幕 Canvas Confetti 五彩紙屑煙火動畫。 |
| **FR-04** | 日常永續打卡任務 | 投資人 | 點擊日常打卡按鈕進行每日任務。完成時培育艙顯示打卡成功視覺特效，並與碳吉寶寶進行即時動態文字反饋互動。 | 每日限制單次點擊。打卡成功可直接獲得 5 EXP，隨後按鈕切換為灰色鎖定狀態，當日限制重複觸發。 |
| **FR-05** | 五階段寶寶等級進化 | 系統 | 依據累積總經驗值(EXP)，動態定義用戶等級與碳吉寶寶成長型態、生態背景描述與養成文字狀態，建構可視化綠色身分。 | 等級劃分：Lv.1種子期(0+ EXP)、Lv.2幼苗期(200+ EXP)、Lv.3灌木期(500+ EXP)、Lv.4大樹期(1000+ EXP)、Lv.5守護神(2000+ EXP)。 |
| **FR-06** | 個人永續履歷與賦能獎勵 | 系統 | 累積里程碑與回饋專區隨經驗值進度，自動解除灰階濾鏡並點亮解鎖對應虛實整合綠色獎勵卡片。 | 門檻機制：100 EXP 解鎖綠色身分徽章、300 EXP 解鎖低碳實體賦能兌換、800 EXP 解鎖金融利率優惠。未達標點擊觸發阻擋警告提示。 |
| **FR-07** | 管理員信託公告主控台 | 管理員 | 具備手動變更審核狀態與佐證文件上傳模擬介面以解鎖前台三階段撥款進度牆，並可插播緊急公告推送到動態牆。 | 後台按鈕嚴格與官方管理員帳號 admin@tanji.com 鎖定。三階段驗證包含：結構安全檢測、設備進場簽收、併網完工營運。送出時具備檔案檢驗防呆邏輯。 |
| **FR-08** | 碳吉寶寶 AI 智能助手 | 投資人 | 右下角常駐客服對話模組。使用者可輸入氣候金融相關痛點，助手支援多輪對話，內建關鍵字匹配模擬回覆。 | 觸發信託安全、服務費比例、當量計算公式、憑證下載等關鍵字時，助手輸出符合淨零法規解答。 |
| **FR-09** | 永續身分憑證下載 | 投資人 | 進入帳戶模態框可切換至憑證檢視區。卡片動態渲染個人 Email、專屬認證編號、當前等級與模擬 Voucher 條碼。 | 點擊下載時，系統透過 HTML5 Canvas 於背景繪製高解析度憑證圖資，自動附加模擬 SHA256 去中心化安全防偽金鑰明碼並存為 PNG。 |

---

## 4. 非業務功能需求與學理合規

### 4.1 科學化減碳量化機制

本平台溫室氣體減量效益數據均具備嚴謹學理基礎，拒絕綠色虛報：

1. **電力減量雙軌制**：電力減量係數嚴格依據經濟部能源署最新劃分標準實施。
* **產業營業用電專案**（如：屋頂太陽能、智慧養殖）：適用產業電力排碳係數（$0.466\text{ kg CO}_2\text{e/度}$）。
* **民生公共用電專案**（如：偏鄉節能照明）：適用民生住宅電力排碳係數（$0.471\text{ kg CO}_2\text{e/度}$）。


2. **生質沼氣專案**：導入環境部盤查指引方法學，將甲烷（$\text{CH}_4$）全球暖化潛勢值（GWP）折算為二氧化碳當量。
3. **循環經濟專案**：套用網購包裝生命週期評估（LCA）盤查數據，每單次循環使用減少 **$1.2\text{ kg CO}_2\text{e}$**。

### 4.2 嚴謹的金融信託合規架構

1. **專款專用保管**：本平台非金融特許機構，所有群募資金遵循法規全數匯入合作商業銀行信託部進行代收代付保管。
2. **工程進度查核牆**：建立透明進度查驗機制。提案廠商必須依工程進度，檢具第三方查證報告（技師簽證、材料核實清冊、台電併網公文與物聯網數據連動）送交銀行與平台核收，通過審查始得分批解鎖撥款，100% 杜絕資金挪用風險。
3. **平台媒合收費**：平台不向參與大眾收取額外手續費，僅在專案成功達標撥款時，向提案廠商收取 **3% 轉型媒合服務費**，用以支持物聯網監測串聯與信託審查成本。

### 4.3 介面效能優化

* **渲染流暢度優化**：主動捨棄耗能毛玻璃濾鏡（`backdrop-filter`）與全畫面模糊（`blur`），採純色背景（如 `bg-slate-50`）配合微透明邊框（`border-slate-200/60`）與原生放射狀漸層，使中低階行動裝置滑動幀率穩定維持 **60 FPS**。
* **多媒體延遲載入**：針對隱藏動態交互影片（`tanjibaby_hi.mp4`）設定 `preload="none"` 與 `muted playsinline` 屬性，防止網頁初次渲染時耗費頻寬載入未使用資源，優化首屏白畫面時間。
* **不破圖防護機制**：全面為 `<img>` 標籤配置 `onerror` 事件監聽器，當圖片因路徑或環境遺失時，自動注入內嵌 Base64 SVG 向量圖，確保 UI 視覺不破裂。

---

## 5. 數據庫架構與實時 API 規格

本系統主要依賴 Firebase Web SDK v10.11.0 進行分散式資料交互與實時異步訂閱（onSnapshot）。

### 5.1 Cloud Firestore 數據庫路徑與 JSON 結構

#### 1. 個人永續帳戶 Profile 節點

* **路徑**：`artifacts/{appId}/users/{uid}/profile/data`
* **結構範例**：

```json
{
  "email": "user@example.com",
  "invested": 3500,
  "co2": 42.1,
  "exp": 350,
  "level": 2,
  "role": "user"
}

```

#### 2. 公共專案資產與信託狀態配置節點

* **路徑**：`artifacts/{appId}/public/data/config/projects`
* **結構範例**：

```json
{
  "raisedAmounts": [3451000, 840000, 880000, 420000, 1250000],
  "stages": [
    {
      "s1": true,
      "s1_status": "approved",
      "s1_doc": "report_2026.pdf",
      "s2": false,
      "s2_status": "pending",
      "s2_doc": "",
      "s3": false,
      "s3_status": "pending",
      "s3_doc": ""
    }
  ]
}

```

#### 3. 即時參與動態牆流水號節點

* **路徑**：`artifacts/{appId}/public/data/feeds`
* **結構範例**：

```json
{
  "name": "台北林先生",
  "action": "參與 廠房屋頂太陽能建置專案 5,000 元",
  "exp": 500,
  "timestamp": 1780830000000,
  "timeStr": "剛剛"
}

```

---

## 6. 專案安裝與正式部署

### 6.1 前置環境需求

* 支援 ES6 模組標準（`<script type="module">`）主流現代瀏覽器（Chrome、Edge、Safari）。
* 已啟用 Firebase Web 專案環境（需開啟 Authentication 匿名/Email 服務與 Cloud Firestore 資料庫）。

### 6.2 部署與啟動步驟

1. **取得程式碼與資源配置**：
將 `index.html` 部署於 Web 伺服器根目錄，並依據結構建立 `assets/` 資料夾與相關 PDF 靜態文件。
2. **本地開發沙盒測試**：
現代瀏覽器針對 ES6 模組具備嚴格 CORS 安全限制，不可直接雙擊點開 `.html` 檔案。請使用本地 HTTP 伺服器容器開啟：
* *Node.js* 環境：`npx serve .` 或安裝 VS Code `Live Server` 擴充套件。
* *Python* 環境：`python -m http.server 8000`


3. **Firebase 金鑰配置**：
原始碼內建一組參賽專用測試金鑰。如需更換為生產資料庫，請直接修改 `<script type="module">` 內 `firebaseConfig` 配置物件。
4. **雲端靜態託管發布**：
本平台屬於純前端 Serverless 架構，可直接發布至 GitHub Pages、Vercel 或 Firebase Hosting 等 CDN 靜態託管服務完成全站正式上線。
