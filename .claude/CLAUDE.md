# mantra-reciter-vanilla-spa

> 多咒語背誦訓練平台 — 大悲咒 · 楞嚴咒
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

### 1.3 當前狀態（2026-07）

| 項目 | 狀態 |
|------|------|
| 入口首頁 | ✅ 已完成 |
| 大悲咒訓練頁 | ✅ 已完成 |
| 楞嚴咒訓練頁 | ✅ 已完成 |
| 心經訓練頁 | 🔜 規劃中 |

**三個頁面**：
- `index.html` — 微軟磁貼風格入口首頁，提供咒語選擇
- `memory-plan.html` — 大悲咒（Great Compassion Mantra）七日記憶訓練
- `lengyanzhou.html` — 楞嚴咒（Śūraṅgama Mantra / Sitātapatra）廿一日記憶訓練

---

## 2. 專案結構

```
mantra-reciter-vanilla-spa/
├── .claude/
│   ├── CLAUDE.md              ← 本文件（專案交接文檔）
│   └── settings.local.json    ← Claude Code 本地設定
├── index.html                 ← 入口首頁（磁貼風格咒語選擇）
├── memory-plan.html           ← 大悲咒訓練頁面（7 日四階段）
├── lengyanzhou.html           ← 楞嚴咒訓練頁面（21 日四階段）
├── dabeizhou.md               ← 大悲咒梵音全文（14 行）
├── lengyanzhou/
│   ├── lengyanzhou-fanwen.md  ← 楞嚴咒梵音全文（193 行）
│   └── lengyanzhou-fanwen.pdf ← 楞嚴咒梵文 PDF
├── docs/superpowers/
│   ├── specs/                 ← 設計規格文件
│   └── plans/                 ← 實作計畫文件
└── README.md
```

### 2.1 檔案說明

| 檔案 | 角色 | 備註 |
|------|------|------|
| `index.html` | 入口首頁 | 微軟磁貼（Metro）風格，兩塊咒語選擇磚 |
| `memory-plan.html` | 大悲咒訓練頁 | 自包含單頁 HTML，7 日四階段、14 行 |
| `lengyanzhou.html` | 楞嚴咒訓練頁 | 自包含單頁 HTML，21 日四階段、193 行 |
| `dabeizhou.md` | 原始文本 | 大悲咒梵文音譯全文，背誦目標材料 |
| `lengyanzhou/lengyanzhou-fanwen.md` | 原始文本 | 楞嚴咒梵文音譯全文 |
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

### 3.3 頁面架構（當前實際）

當前三個頁面各自獨立，共用相同的設計 tokens 和 CSS 模式，但尚未提取共用層。每個頁面都是自包含的 `.html` 檔案。

```
mantra-reciter-vanilla-spa/
├── index.html                 ← 入口首頁（咒語選擇）
├── memory-plan.html           ← 大悲咒訓練頁
├── lengyanzhou.html           ← 楞嚴咒訓練頁
├── dabeizhou.md               ← 大悲咒原始文本
└── lengyanzhou/
    └── lengyanzhou-fanwen.md  ← 楞嚴咒原始文本
```

每個訓練頁面左上角有「← 首頁」按鈕可返回入口頁。入口頁使用微軟磁貼（Metro）風格，兩塊大色塊卡片分別連結到對應訓練頁。

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

## 5. 頁面結構說明

### 5.0 入口首頁（index.html）

微軟磁貼（Metro）風格，單頁居中佈局：
- 標題區：平台名稱 + 副標
- 兩塊大色塊磁貼（hover 縮放動畫）：
  - 大悲咒磁貼（青綠色）：中文名 + 梵文提示 + 行數與訓練週期
  - 楞嚴咒磁貼（深藍色）：中文名 + 梵文提示 + 行數與訓練週期
- 點擊磁貼進入對應訓練頁
- 支援 light/dark 主題切換

### 5.1 訓練頁共用結構

每個訓練頁面按「從認識到執行」的邏輯排列，共五大區塊（大悲咒與楞嚴咒結構相同，內容不同）：

#### Hero（英雄區）
- 金色梵音咒語開篇（帶呼吸光暈動畫）
- 主標題 + 副標題
- 四階段迷你時間線（天數依咒語長度調整）

#### 文本結構分析
- 五段結構總覽表（HTML table）
- 四個韻律模式亮點卡片（咒語特定的記憶錨點）

#### 五段全文拆解
- 五張深色「寫經」風格卡片（`.ms-card`）
- 每張卡片展示對應段落的完整梵文文本
- 金色文字（`--gold-pale`）在深色背景上模擬寫經效果
- 左側彩色邊條標記段落歸屬
- 楞嚴咒每句以 `<br>` 斷行，提升可讀性

#### 四階段訓練計畫
- 2×2 網格佈局（桌面端），中央垂直金線 + 念珠點裝飾
- 每張卡片：階段標籤、標題、日期 badge、活動清單、每日時間分配、底部提示
- Phase 1 卡片內嵌 YouTube 音頻參考連結

#### 核心記憶技巧
- 七張小型技巧卡，flex wrap 自動排列，咒語特定的記憶方法

#### 注意事項
- 四張編號筆記卡（01–04）

#### Footer
- 總結句 + 咒語結尾梵音

### 5.2 兩頁差異對照

| 項目 | 大悲咒 | 楞嚴咒 |
|------|--------|--------|
| 行數 | 14 行 | 193 行 |
| 訓練週期 | 7 天（每階段 1–2 天） | 21 天（每階段約 5 天） |
| 段落長度 | 1–8 行/段 | 18–57 行/段 |
| 記憶錨點 | Svaha 節奏、疊詞對稱、Om 啟動、頭尾呼應 | Namaḥ 歸敬鏈、Hūṃ Trūṃ 行動引擎、Cchinda-Kīla 破除雙刃、Phaṭ 雷音陣 |
| YouTube 音頻 | 大悲咒梵音標準唱誦 | 楞嚴咒梵音標準唱誦 |

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

1. 複製現有訓練頁面作為模板
2. 保留 `:root` tokens、主題切換、scroll reveal、back-home 等共用 CSS
3. 替換內容區塊的 HTML
4. 階段色沿用四個（不限於四階段），訓練天數在 HTML 內容中調整
5. 保持 CSS 扁平結構——選擇器嵌套不超過 3 層

### 6.4 入口首頁 CSS（index.html）

入口首頁有獨立的 CSS 設計：
- **磁貼樣式**：兩塊大正方形色塊（`--tile-size: clamp(160px, 40vw, 260px)`），flex 居中排列
- **色彩**：大悲咒青綠（`--tile-dabeizhou`）、楞嚴咒深藍（`--tile-lengyan`），各有 hover 變體
- **互動**：hover 時上浮 + 縮放（`translateY(-4px) scale(1.03)`），點擊時微縮（`scale(0.97)`）
- **圖標**：大號 emoji 作背景浮水印（opacity 0.18）
- **頂部色條**：用 `::before` 偽元素，金色（大悲咒）和朱紅（楞嚴咒）

---

## 7. 內容版權與來源

### 7.1 咒語文本

- **大悲咒**：`dabeizhou.md`，源自漢傳佛教《千手千眼觀世音菩薩廣大圓滿無礙大悲心陀羅尼經》的梵音還原
- **楞嚴咒**：`lengyanzhou/lengyanzhou-fanwen.md`，源自漢傳佛教《大佛頂如來密因修證了義諸菩薩萬行首楞嚴經》的梵音還原

文本本身屬於宗教經典，無版權限制。

### 7.2 音頻參考

YouTube 標準唱誦錄音：
- 大悲咒：<https://youtu.be/QH7J26UhT9c>
- 楞嚴咒：<https://youtu.be/Sdy02LeEENo>
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
# 入口首頁
open index.html

# 或啟動本地伺服器（推薦，確保頁面間導航正常）
python3 -m http.server 8080
# 打開 http://localhost:8080
```

### 8.2 編輯流程

1. 直接編輯目標 `.html` 檔案
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
| 純 HTML 單檔，不引入框架 | 零環境依賴，新人 clone 即開 | 2026-06 |
| 深色背景 + 淺色卡片 | 取材自紺紙寫經的真實物質文化 | 2026-06 |
| Cormorant Garamond 做梵文展示字 | 良好的拉丁變音符支援，有「經文」氣質 | 2026-06 |
| YouTube 使用連結而非 iframe 嵌入 | iframe 在 file:// 協議下頻繁報錯 | 2026-06 |
| 階段色使用青綠→琥珀→橙→紅漸進 | 色彩心理學輔助記憶線索 | 2026-06 |
| 暫不提取共用 CSS tokens | 只有一個頁面時無法區分「共用」和「巧合」 | 2026-06 |
| CLAUDE.md 同時服務人和 AI | 結構化 Markdown，人與 AI 皆可讀 | 2026-06 |
| 楞嚴咒訓練週期設為 21 天 | 全文 193 行（大悲咒 14 倍），7 天不足以消化 | 2026-07 |
| 入口首頁使用微軟磁貼風格 | 兩塊大色塊簡潔直觀，符合「選擇起點」的心智模型 | 2026-07 |
| 訓練頁面左上角放「← 首頁」連結 | 固定定位、低視覺干擾，隨時可返回入口 | 2026-07 |

---

## 10. 常見問題

**Q: 為什麼不直接用 React/Vue？**
A: 三個頁面仍屬小型規模。引入框架會增加建置步驟和依賴管理成本。等到頁面數量 ≥ 5 且出現共用元件需求時再評估。

**Q: 配色為什麼這麼深？**
A: 紺紙（深藍染紙）金泥是真實的佛教寫經傳統。這不是「暗色模式」，而是從主題本身的物質文化中長出來的選擇。

**Q: 如果 YouTube 影片被下架怎麼辦？**
A: Phase 1 卡片中的連結需要更新。可以換成其他梵音唱誦錄音，或改用自行託管的音頻檔案。

**Q: 訓練計畫有科學依據嗎？**
A: 計畫設計參考了間隔重複、睡眠記憶鞏固、多感官學習等已被認知科學驗證的原理。但它不是臨床試驗產物，是實用導向的記憶教練工具。

**Q: 楞嚴咒為什麼是 21 天而不是 7 天？**
A: 楞嚴咒 193 行，是大悲咒的 14 倍。訓練週期按文本長度等比調整，每個階段約 5 天，確保有充足的消化和鞏固時間。
