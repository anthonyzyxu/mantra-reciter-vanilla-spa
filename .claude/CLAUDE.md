# mantra-reciter-vanilla-spa

> 多咒語背誦訓練平台 — 從大悲咒開始
>
> 命名規範：`[專案]-[應用]-[技術棧]-[類型]`

---

## 1. 專案概覽

### 1.1 一句話描述

幫助使用者高效背誦佛教梵音咒語的單頁網頁應用。以記憶教練的角色，將長篇咒語拆解為結構化段落，配合七日四階段訓練計畫、多感官記憶技巧，讓初學者從零開始逐步掌握全文背誦。

### 1.2 為什麼做這個

背誦長篇梵音咒語（如大悲咒）對初學者門檻極高：
- 文本為梵文音譯，缺乏語義線索輔助記憶
- 市面上沒有專門針對「咒語背誦」設計的系統化訓練工具
- 傳統方法依賴反覆跟讀，效率低、容易放棄

這個專案將認知科學中的記憶技巧（韻律錨定、空間分段、睡眠固化、多感官輸入等）轉化為可執行的七日訓練計畫，用網頁形式交付，零門檻開啟。

### 1.3 當前狀態（2026-06）

| 項目 | 狀態 |
|------|------|
| 大悲咒訓練頁 | ✅ 已完成 |
| 多咒語首頁 | 🔜 規劃中 |
| 心經訓練頁 | 🔜 規劃中 |
| 楞嚴咒訓練頁 | 🔜 規劃中 |

**當前唯一的頁面**：`memory-plan.html` — 大悲咒（Great Compassion Mantra / 大悲心陀羅尼）七日記憶訓練計畫。

---

## 2. 專案結構

```
project_dabeizhou/
├── .claude/
│   ├── CLAUDE.md              ← 本文件（專案交接文檔）
│   └── settings.local.json    ← Claude Code 本地設定
├── dabeizhou.md               ← 大悲咒梵音全文（14 行）
└── memory-plan.html           ← 大悲咒訓練頁面（當前唯一產品頁）
```

### 2.1 檔案說明

| 檔案 | 角色 | 備註 |
|------|------|------|
| `dabeizhou.md` | 原始文本 | 大悲咒梵文音譯全文，背誦的目標材料 |
| `memory-plan.html` | 產品頁面 | 自包含的單頁 HTML（CSS + JS 內嵌），無建置步驟 |
| `CLAUDE.md` | 交接文檔 | 專案知識總匯，人與 AI 皆可閱讀 |

---

## 3. 技術架構

### 3.1 技術棧

```
純靜態頁面，零依賴，零建置步驟
HTML5 + CSS3（Custom Properties）+ Vanilla JS（Intersection Observer）
```

- **無框架**：不依賴 React/Vue/Svelte 等任何前端框架
- **無建置工具**：無 webpack/vite，直接打開 HTML 即可運行
- **無後端**：純靜態頁面，可部署到任何靜態主機（GitHub Pages / Vercel / Netlify）
- **外部依賴**：僅 Google Fonts（Cormorant Garamond + Inter），透過 `<link>` 載入

### 3.2 設計哲學

每個頁面都是一個**自包含的 `.html` 檔案**。CSS 和 JS 全部內嵌在 `<style>` 和 `<script>` 標籤中，目的：
- 零環境依賴，新人 clone 後雙擊即可打開
- 無 CSS/JS 打包、無快取失效問題
- 每個咒語訓練頁獨立存在，互不耦合

### 3.3 未來多頁面架構（規劃）

當咒語數量增加時，提取共用設計系統：

```
mantra-reciter-vanilla-spa/
├── index.html                 ← 咒語選擇首頁
├── shared/
│   └── design-tokens.css      ← 共用 CSS tokens（從現有頁面提取）
├── pages/
│   ├── dabeizhou.html         ← 大悲咒（從 memory-plan.html 重命名）
│   ├── heart-sutra.html       ← 心經（新建）
│   └── shurangama.html        ← 楞嚴咒（新建）
├── CLAUDE.md
└── README.md
```

當前階段 **不要過早提取共用層**。讓每個頁面先獨立演化，等第二個咒語頁面完成後再回頭重構——那時才能看清哪些是真正的共用模式，哪些只是巧合相似。

---

## 4. 設計系統

### 4.1 色彩

設計取材自佛教寫經的物質文化——紺紙（深藍染紙）+ 泥金書法 + 朱砂印記。

#### 基礎色

| Token | 色值 | 用途 |
|-------|------|------|
| `--ink` | `#16161f` | 頁面底色（深紺紙色） |
| `--ink-light` | `#1f1f2b` | 深色卡片底色（略淺於底色） |
| `--ink-card` | `#1c1c28` | 寫經文本卡片底色 |
| `--gold` | `#c4a35a` | 主強調色（標題、連結、邊框） |
| `--gold-dim` | `#8a7340` | 次級金色（section label、次要文字） |
| `--gold-pale` | `#e8d5a3` | 淺金色（梵文文本展示色） |
| `--parchment` | `#f7f3eb` | 暖羊皮色（主要卡片底色） |
| `--parchment-dim` | `#e8e1d5` | 卡片內分隔區底色 |
| `--vermillion` | `#c2453a` | 紅色強調（極少使用，僅 Phase 4 等關鍵處） |

#### 階段色（記憶輔助）

四階段使用漸進色編碼，色彩本身作為記憶線索：

| Token | 色值 | 階段 |
|-------|------|------|
| `--phase-1` | `#5a8a7a` | 第一階段：青綠 — 平靜、接收 |
| `--phase-2` | `#c4973a` | 第二階段：琥珀 — 組織、分析 |
| `--phase-3` | `#d4783c` | 第三階段：暖橙 — 行動、強化 |
| `--phase-4` | `#c2453a` | 第四階段：朱紅 — 完成、驗收 |

每個 phase color 配套兩個透明背景變體：
- `--phase-N-bg`: 8% 透明度（badge 底色）
- `--phase-N-bg-strong`: 14% 透明度（time-slot 底色）

### 4.2 字型

| 角色 | 字型棧 | 用途 |
|------|--------|------|
| 梵文咒語 | `'Cormorant Garamond', 'Noto Serif', 'Times New Roman', serif` | Hero 咒語展示、寫經文本卡片 |
| 中文標題 | `'Cormorant Garamond', 'Songti SC', 'Noto Serif SC', serif` | h1、卡片標題、section 標題 |
| 內文 | `'Inter', 'PingFang SC', 'Noto Sans SC', system-ui, sans-serif` | 所有說明文字、清單 |

載入方式：Google Fonts `<link>`，僅載入 `Cormorant Garamond`（400/400i/600）和 `Inter`（400/500/600）。中文字型依賴系統內建。

### 4.3 佈局

- **最大內容寬度**：`1100px`，水平置中
- **卡片圓角**：`12px`（主卡片）、`6px`（小卡片/技術卡）
- **響應式斷點**：`740px` — 2 欄 → 1 欄
- **間距系統**：使用 `gap` + `padding`，無統一的 spacing scale（當前規模不需要）

### 4.4 設計原則

1. **一個簽名元素**：Hero 區的金色梵音文字帶呼吸光暈動畫，是整頁唯一的大動畫。其他所有動畫（hover lift、scroll reveal）保持克制。
2. **顏色來自內容**：每個設計選擇（紺紙金泥、念珠連接線、硃砂點綴）都可以追溯到佛教物質文化，不做無來源的裝飾。
3. **卡片是主角**：核心內容用 `parchment` 卡片承載，與深色背景形成對比，幫助閱讀和記憶。
4. **色彩輔助記憶**：四階段漸進色不只用於裝飾，本身即為記憶線索。

---

## 5. 頁面結構說明（memory-plan.html）

頁面按「從認識到執行」的邏輯排列，共五大區塊：

### 5.1 Hero（英雄區）
- 金色梵音咒語開篇（帶呼吸光暈動畫）
- 主標題 + 副標題
- 四階段迷你時間線

### 5.2 文本結構分析
- 五段結構總覽表（HTML table）
- 四個韻律模式亮點卡片（Svaha 節奏、疊詞對稱、Om 啟動、頭尾呼應）

### 5.3 五段全文拆解
- 五張深色「寫經」風格卡片（`.ms-card`）
- 每張卡片展示對應段落的完整梵文文本
- 金色文字（`--gold-pale`）在深色背景上模擬寫經效果
- 左側彩色邊條標記段落歸屬

### 5.4 四階段訓練計畫
- 2×2 網格佈局（桌面端），中央垂直金線 + 念珠點裝飾
- 每張卡片包含：階段標籤、標題、日期 badge、活動清單、每日時間分配、底部提示
- Phase 1 卡片內嵌 YouTube 播放連結（紅色播放鈕圖標）

### 5.5 核心記憶技巧
- 七張小型技巧卡，flex wrap 自動排列
- 每張：emoji 圖標 + 技巧名 + 一句說明

### 5.6 注意事項
- 四張編號筆記卡（01–04）
- 內容：不要死記硬背 / 每天不超過 1 小時 / 卡住不求全 / 保持恭敬心

### 5.7 Footer
- 總結句 + 咒語結尾梵音

---

## 6. CSS 架構

### 6.1 組織方式

```
TOKENS (Custom Properties)
RESET & BASE (box-sizing, body, focus-visible)
HERO (mantra display, title, timeline)
SECTIONS (shared section styles)
STRUCTURE TABLE (analysis table)
PATTERN HIGHLIGHTS (4 pattern cards)
MANUSCRIPT CARDS (5 text section cards)
PHASE CARDS (2x2 grid, card base, lists, daily schedule)
TECHNIQUES (7 small cards)
NOTES (4 numbered cards)
FOOTER
SCROLL REVEAL
REDUCED MOTION
```

### 6.2 關鍵 CSS 模式

**卡片頂部色條**：用 `::before` 偽元素實現，避免額外 DOM：
```css
.card::before {
  content: '';
  position: absolute; top: 0; left: 0; right: 0; height: 4px;
  border-radius: var(--radius) var(--radius) 0 0;
}
.card.p1::before { background: var(--phase-1); }
```

**階段色變體**：卡片內的互動元素（badge、list bullet、daily time-slot）透過 `.card.pN <child>` 選擇器繼承階段色，避免在每個子元素上重複綁定顏色類。

**中央念珠連接線**：僅桌面端顯示（`@media (max-width:740px)` 隱藏），使用多層 `radial-gradient` 模擬念珠位置。

**捲動揭示**：Intersection Observer + `.reveal` 類，threshold 0.12，rootMargin `-36px`。

### 6.3 新增頁面時的 CSS 策略

1. 複製現有頁面的 `:root` tokens 區段
2. 替換內容區塊的 HTML，保留 Hero 和 Footer 結構骨架
3. 階段色可根據新咒語的訓練階段數調整（不限於四個）
4. 保持 CSS 扁平結構——選擇器嵌套不超過 3 層

---

## 7. 內容版權與來源

### 7.1 咒語文本

`dabeizhou.md` 中的大悲咒梵文音譯文本，源自漢傳佛教《千手千眼觀世音菩薩廣大圓滿無礙大悲心陀羅尼經》的梵音還原。文本本身屬於宗教經典，無版權限制。

### 7.2 音頻參考

YouTube 標準唱誦錄音：
- 連結：<https://youtu.be/QH7J26UhT9c>
- 用途：Phase 1 聽覺記憶階段的跟讀參考

### 7.3 記憶訓練方法論

訓練計畫的原創設計結合了以下認知科學原理：
- 間隔重複（Spaced Repetition）
- 睡眠記憶鞏固（Sleep-dependent Memory Consolidation）
- 費曼學習法（Feynman Technique）
- 雙重編碼理論（Dual Coding Theory）
- 多感官學習（Multi-sensory Learning）
- 干擾效應訓練（Contextual Interference）

---

## 8. 開發指南

### 8.1 本地開發

```bash
# 唯一需要的指令：用瀏覽器打開
open memory-plan.html

# 或者啟動一個簡單的本地伺服器（如果你需要測試 YouTube 嵌入等跨域功能）
python3 -m http.server 8080
# 然後打開 http://localhost:8080/memory-plan.html
```

### 8.2 編輯流程

1. 直接編輯 `memory-plan.html`
2. 儲存後刷新瀏覽器
3. 不需要任何 watch/build/lint 指令

### 8.3 新增咒語訓練頁

1. 複製 `memory-plan.html` → `new-mantra.html`
2. 準備咒語原始文本（`.md` 檔案）
3. 分析文本結構（分段、韻律模式、記憶關鍵點）
4. 設計階段訓練計畫（階段數可不同於 4）
5. 更新頁面內容（Hero 咒語文本、分析表格、全文卡片、訓練階段、技巧清單、注意事項）
6. 如需調整色彩，修改 `:root` tokens

### 8.4 重構為多頁面（將來）

觸發條件：**第二個咒語頁面完成後**。

步驟：
1. 提取共用 tokens → `shared/design-tokens.css`
2. 提取共用元件樣式（card、section、footer） → `shared/base.css`
3. 各頁面改為 `<link>` 引入共用樣式，頁面特有樣式留在 `<style>` 中
4. 建立 `index.html` 咒語選擇首頁
5. 重命名 `memory-plan.html` → `pages/dabeizhou.html`

---

## 9. 設計決策記錄

| 決策 | 理由 | 日期 |
|------|------|------|
| 純 HTML 單檔，不引入框架 | 零環境依賴，新人 clone 即開。規模（單頁）不需要 React/Vue 的複雜度 | 2026-06 |
| 深色背景 + 淺色卡片 | 取材自紺紙寫經的真實物質文化，不是追隨暗色模式潮流 | 2026-06 |
| Cormorant Garamond 做梵文展示字 | 義大利體襯線 + 良好的拉丁變音符支援，比系統 Times 更有「經文」氣質 | 2026-06 |
| YouTube 使用連結而非 iframe 嵌入 | iframe 在 file:// 協議下頻繁報錯，連結卡片更可靠且設計更可控 | 2026-06 |
| 階段色使用青綠→琥珀→橙→紅漸進 | 色彩心理學：從冷靜接收到熱烈完成，本身構成記憶輔助線索 | 2026-06 |
| 暫不提取共用 CSS tokens | 只有一個頁面時無法區分「共用」和「巧合」，第二個頁面完成後再重構 | 2026-06 |
| CLAUDE.md 同時服務人和 AI | 結構化 Markdown，對人類可讀、對 AI 可解析、對新人可入門 | 2026-06 |

---

## 10. 常見問題

**Q: 為什麼不直接用 React/Vue？**
A: 當前只有一個頁面。引入框架會增加建置步驟、依賴管理和新人學習成本，而收益為零。等到頁面數量 ≥ 3 且出現共用元件需求時，再評估。

**Q: 配色為什麼這麼深？**
A: 紺紙（深藍染紙）金泥是真實的佛教寫經傳統。這不是「暗色模式」，而是從主題本身的物質文化中長出來的選擇。

**Q: 如果 YouTube 影片被下架怎麼辦？**
A: Phase 1 卡片中的連結需要更新。可以換成其他梵音唱誦錄音，或改用自行託管的音頻檔案（屆時需調整播放器設計）。

**Q: 訓練計畫有科學依據嗎？**
A: 計畫設計參考了間隔重複、睡眠記憶鞏固、多感官學習等已被認知科學驗證的原理。但它不是臨床試驗產物，是實用導向的記憶教練工具。
