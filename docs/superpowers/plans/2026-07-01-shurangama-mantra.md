# 楞嚴咒梵文記憶訓練頁面 — 實作計畫

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 從 `memory-plan.html` 複製骨架，建立楞嚴咒 21 天記憶訓練頁面 `lengyanzhou.html`

**Architecture:** 自包含單頁 HTML。複製現有頁面的完整 `<style>` 和 `<script>`，僅替換 `<body>` 內的 HTML 內容。CSS tokens、class 命名、主題切換、scroll reveal 全部復用，零改動。

**Tech Stack:** HTML5 + CSS3 (Custom Properties) + Vanilla JS (Intersection Observer) — 與現有頁面完全相同

## Global Constraints

- 純靜態單檔，零框架，零建置步驟
- 複製 `memory-plan.html` 的全部 `<style>` 和 `<script>`，不做任何修改
- 僅替換 `<body>` 內 HTML 內容
- 字型載入：Cormorant Garamond (400/400i/600) + Inter (400/500/600)，與現有頁面相同
- 保留 `<html lang="zh-Hant">`、`<meta charset="UTF-8">`、viewport meta
- 保留 theme toggle button 及其 script
- 保留 scroll reveal 的 Intersection Observer
- 所有梵文文本取自 `lengyanzhou/lengyanzhou-fanwen.md`
- 訓練計畫：21 天四階段，與設計規格一致

---

### Task 1: 建立新檔案並替換 Hero 區塊

**Files:**
- Create: `lengyanzhou.html`（從 `memory-plan.html` 複製）

- [ ] **Step 1: 複製 memory-plan.html 為 lengyanzhou.html**

```bash
cp memory-plan.html lengyanzhou.html
```

- [ ] **Step 2: 更新 `<title>`**

將：
```html
<title>大悲咒 · 7日記憶訓練計畫</title>
```
替換為：
```html
<title>楞嚴咒 · 21日記憶訓練計畫</title>
```

- [ ] **Step 3: 替換 Hero 區塊**

找到 `<header class="hero">` 整區塊（從 `<header class="hero">` 到 `</header>`），替換為：

```html
<header class="hero">
  <p class="mantra-display" aria-label="楞嚴咒梵音開篇">
    Namaḥ sarva buddha bodhi-satve-bhyaḥ<br>
    Namaḥ saptānāṃ samyak-saṃbuddha koṭīnāṃ<br>
    sa-śrāvaka saṃghānāṃ · Namo loke arhattāṃ
  </p>
  <h1>楞嚴咒 · 記憶訓練計畫</h1>
  <p class="subtitle">廿一日四階 · 梵音護體 · 從零開始</p>

  <div class="timeline-mini" aria-label="四階段時間線">
    <div class="timeline-dot t1"><span>第一階段 1–5日</span></div>
    <div class="timeline-dash" aria-hidden="true"></div>
    <div class="timeline-dot t2"><span>第二階段 6–10日</span></div>
    <div class="timeline-dash" aria-hidden="true"></div>
    <div class="timeline-dot t3"><span>第三階段 11–15日</span></div>
    <div class="timeline-dash" aria-hidden="true"></div>
    <div class="timeline-dot t4"><span>第四階段 16–21日</span></div>
  </div>
</header>
```

- [ ] **Step 4: 在瀏覽器中打開確認 Hero 區塊顯示正確**

```bash
open lengyanzhou.html
```

- [ ] **Step 5: Commit**

```bash
git add lengyanzhou.html
git commit -m "feat: add Shurangama mantra page with hero section"
```

---

### Task 2: 替換文本結構分析區塊（表格 + 模式亮點卡）

**Files:**
- Modify: `lengyanzhou.html`

- [ ] **Step 1: 替換 section label/title/sub**

找到第一個 `<section>` 中的 `<p class="section-label">`、`<h2 class="section-title">`、`<p class="section-sub">`，替換為：

```html
<p class="section-label">第一步 · 認識文本</p>
<h2 class="section-title">文本結構分析</h2>
<p class="section-sub">在開始背誦之前，先理解這篇文章的骨架。<br>楞嚴咒全文共 193 行，依自然段落可分為五大段。</p>
```

- [ ] **Step 2: 替換結構總覽表 `<tbody>`**

找到 `<table class="structure-table">` 中的 `<tbody>`，替換為：

```html
<tbody>
  <tr>
    <td class="sec-num">第一段</td>
    <td class="sec-name">歸敬諸尊 · Namaḥ 段</td>
    <td class="sec-lines">第 1–57 行</td>
    <td class="sec-desc">以 Namaḥ / Namo 反覆向三世諸佛、菩薩、護法神致敬，是全咒最長的歸敬段落。Namo bhagavate… 句型重複 6 次形成穩定禮敬節奏</td>
  </tr>
  <tr>
    <td class="sec-num">第二段</td>
    <td class="sec-name">核心咒鬘 · Hūṃ Trūṃ 段</td>
    <td class="sec-lines">第 60–77 行</td>
    <td class="sec-desc">以 Oṃ 啟動，每句 hūṃ trūṃ 收尾。四大行動（震撼/僵止/迷惑/粉碎）構成咒語的力量核心引擎</td>
  </tr>
  <tr>
    <td class="sec-num">第三段</td>
    <td class="sec-name">破除障難 · Cchinda 段</td>
    <td class="sec-lines">第 80–114 行</td>
    <td class="sec-desc">列出各類恐懼（bhaya）與惱害眾生（graha），以 cchinda-yāmi kīla-yāmi（我斬斷、我釘住）為重複破除口號，共出現 19 次</td>
  </tr>
  <tr>
    <td class="sec-num">第四段</td>
    <td class="sec-name">降伏諸魔 · Phaṭ 段</td>
    <td class="sec-lines">第 117–151 行</td>
    <td class="sec-desc">全咒最具爆發力的段落。phaṭ! 如雷擊般連續出現 30+ 次，逐一破除天龍八部、疾病、鬼神等各類障礙</td>
  </tr>
  <tr>
    <td class="sec-num">第五段</td>
    <td class="sec-name">結界護身 · Bandha 段</td>
    <td class="sec-lines">第 154–193 行</td>
    <td class="sec-desc">從疾病、疼痛到各類惱害的全面防護。七重 bandhaṃ karomi（我作結界）層層守護，最後以根本咒 Oṃ anale anale… 收攝全文</td>
  </tr>
</tbody>
```

- [ ] **Step 3: 替換四大模式亮點卡**

找到 `<div class="pattern-grid reveal">` 整區塊，替換為：

```html
<div class="pattern-grid reveal">
  <div class="pattern-card">
    <span class="pattern-icon" aria-hidden="true">📿</span>
    <div>
      <h4>Namaḥ 歸敬鏈</h4>
      <p>第一段中「Namo bhagavate… tathāgatāya arhate samyak-saṃbuddhāya」重複 6 次，形成穩定的禮敬節奏，如念珠般一氣呵成。</p>
    </div>
  </div>
  <div class="pattern-card">
    <span class="pattern-icon" aria-hidden="true">⚡</span>
    <div>
      <h4>Hūṃ Trūṃ 行動引擎</h4>
      <p>第二段每句以 hūṃ trūṃ 結尾，四種行動（震撼→僵止→迷惑→粉碎）層層推進，構成咒語的力量核心。</p>
    </div>
  </div>
  <div class="pattern-card">
    <span class="pattern-icon" aria-hidden="true">🔪</span>
    <div>
      <h4>Cchinda-Kīla 破除雙刃</h4>
      <p>第三段 cchinda-yāmi kīla-yāmi 出現 19 次——「我斬斷」如刀砍、「我釘住」如釘定，是全文最強的重複記憶鉤。</p>
    </div>
  </div>
  <div class="pattern-card">
    <span class="pattern-icon" aria-hidden="true">⛈️</span>
    <div>
      <h4>Phaṭ 雷音陣</h4>
      <p>第四段 phaṭ 連續轟擊 30+ 次，每句一個目標（天龍八部→疾病→鬼神），如雷音陣般清晰可數、勢不可擋。</p>
    </div>
  </div>
</div>
```

- [ ] **Step 4: Commit**

```bash
git add lengyanzhou.html
git commit -m "feat: add structure analysis section for Shurangama mantra"
```

---

### Task 3: 替換五段全文拆解（寫經卡片）

**Files:**
- Modify: `lengyanzhou.html`

- [ ] **Step 1: 替換 section label/title/sub**

找到第二個 `<section>`（全文拆解區塊）的 label/title/sub，替換為：

```html
<p class="section-label">第二步 · 通讀全文</p>
<h2 class="section-title">五段全文拆解</h2>
<p class="section-sub">以下是完整的楞嚴咒梵音文本，按五段結構排列。<br>篇幅較長，不用一次讀完——先感受各段的韻律特徵，讓聲音在腦中留下印記。</p>
```

- [ ] **Step 2: 替換五張 manuscript 卡片**

找到 `<div class="manuscript-grid">` 整區塊，替換為五張卡片。梵文文本直接取自 `lengyanzhou/lengyanzhou-fanwen.md` 原始換行：

**卡片 1 — 歸敬諸尊 · Namaḥ 段（第 1–57 行）：**

```html
<div class="manuscript-grid">

  <div class="ms-card s1 reveal">
    <div class="ms-header">
      <span class="ms-num">第一段</span>
      <span class="ms-title">歸敬諸尊 · Namaḥ 段</span>
      <span class="ms-tag">第 1–57 行</span>
    </div>
    <p class="ms-text">
      Namaḥ sarva buddha bodhi-satve-bhyaḥ.
      Namaḥ saptānāṃ samyak-saṃbuddha koṭīnāṃ
      sa-śrāvaka saṃghānāṃ. Namo loke arhattāṃ.
      Namaḥ srotāpannānāṃ. Namaḥ sakṛdāgāmināṃ.
      Namaḥ anāgāmināṃ. Namo loke
      samyag-gatānāṃ samyak-prati-pannānāṃ. Namo
      devarṣiṇāṃ. Namaḥ siddha-vidyā-dhāra-rṣiṇāṃ,
      śāpānugraha-samarthānāṃ. Namo brahmaṇe.
      Nama indrāya. Namo bhagavate rudrāya
      umāpati-sahīyāya. Namo bhagavate nārāyaṇāya,
      lakṣmi paṃca-mahā-mudrā namas-kṛtāya.
      Namo bhagavate mahā-kālāya,
      tripura-nagara-vidrāpaṇa-karāya, adhi-muktaka
      śmaśāna-vāsine, mātṛ-gaṇa namas-kṛtāya.
      Namo bhagavate tathāgata kulāya. Namo
      bhagavate padma kulāya. Namo bhagavate vajra
      kulāya. Namo bhagavate maṇi kulāya. Namo
      bhagavate gaja-kulāya. Namo bhagavate
      dṛḍha-śūra-sena-pra-haraṇa-rājāya, tathāgatāya
      arhate samyak-saṃbuddhāya. Namo bhagavate
      Amitābhāya, tathāgatāya arhate
      samyak-saṃbuddhāya. Namo bhagavate
      akṣobhyāya, tathāgatāya arhate
      samyak-saṃbuddhāya. Namo bhagavate
      bhaiṣajya-guru-vaiḍūrya-prabha-rājāya,
      tathāgatāya arhate samyak-saṃbuddhāya.
      Namo bhagavate saṃpuṣpita-sālendra-rājāya,
      tathāgatāya arhate samyak-saṃbuddhāya.
      Namo bhagavate Śākyamunaye, tathāgatāya
      arhate samyak-saṃbuddhāya. Namo bhagavate
      ratna-kusuma-ketu-rājāya, tathāgatāya arhate
      samyak-saṃbuddhāya. Teṣāṃ namas-kṛtva imāṃ
      bhagavata stathāgatoṣṇīṣaṃ, sitātapatraṃ
      namāparājitaṃ pratyaṅgirāṃ. Sarva bhūta-graha
      nigraha-karaṇīṃ. Para vidyā cchedanīṃ.
      Akālaṃ-mṛtyu pari-trāṇa-karīṃ. Sarva bandhana
      mokṣaṇīṃ. Sarva duṣṭa duḥ-svapna nivāraṇīṃ.
      Caturaśītīnāṃ graha sahasrāṇāṃ
      vi-dhvaṃsana-karīṃ. Aṣṭā-viṃśatināṃ
      nakṣatrāṇāṃ pra-sādana-karīṃ. Aṣṭānāṃ
      mahā-grahāṇāṃ vi-dhvaṃsana-karīṃ. Sarva śatrū
      nivāraṇīṃ. Ghoraṃ duḥ-svapnānāṃ ca nāśanīṃ.
      Viṣa śastra agni uttaraṇīṃ. Aparājitaṃ
      mahā-ghorāṃ, mahā-balāṃ mahā-caṇḍāṃ
      mahā-dīptaṃ mahā-tejaṃ, mahā-śvetāṃ
      mahā-jvalaṃ mahā-balā pāṇḍara-vāsinī, ārya-tārā
      bhṛkuṭīṃ ceva vijaya vajra-maleti vi-śrutāṃ,
      padmaṃkaṃ vajra-jihva ca mālā-cevāparājita,
      vajrā daṇḍīṃ viśālā ca śanta vaideva-pūjitāṃ,
      saumya-rūpaṃ mahā-śvetā, ārya-tārā mahā-bala
      aparā vajra śaṅkalā ceva, vajra kaumāri
      kulan-dharī, vajra hastā ca mahā-vidyā kāṃcana
      mālikā, kusuṃbhā ratna ceva vairocanā
      kulāthadāṃ uṣṇīṣa, vi-jṛmbha-māṇā ca savajra
      kanaka prabha locana, vajrā tuṇḍī ca śvetā ca
      kamalākṣī śaśī-prabha, ityete mudrā gaṇā,
      sarve rakṣaṃ kurvantu mama sarva satvānāṃ ca.
    </p>
  </div>
```

**卡片 2 — 核心咒鬘 · Hūṃ Trūṃ 段（第 60–77 行）：**

```html
  <div class="ms-card s2 reveal">
    <div class="ms-header">
      <span class="ms-num">第二段</span>
      <span class="ms-title">核心咒鬘 · Hūṃ Trūṃ 段</span>
      <span class="ms-tag">第 60–77 行</span>
    </div>
    <p class="ms-text compact">
      Oṃ ṛṣi-gaṇa praśastāya sarva tathāgatoṣṇīṣāya
      hūṃ trūṃ. Jambhana-kara hūṃ trūṃ.
      Stambhana-kara hūṃ trūṃ.
      Mohana-kara hūṃ trūṃ. Mathana-kara hūṃ trūṃ.
      Para-vidyā saṃ-bhakṣaṇa-kara hūṃ trūṃ.
      Sarva duṣṭānāṃ stambhana-kara hūṃ trūṃ.
      Sarva yakṣa rākṣasa grahāṇāṃ,
      vi-dhvaṃ sana-kara hūṃ trūṃ. Caturaśītīnāṃ
      graha sahasrāṇāṃ, vi-dhvaṃsana-kara hūṃ trūṃ.
      Aṣṭā-viṃśatīnāṃ nakṣatrānāṃ
      pra-sādana-kara hūṃ trūṃ. Aṣṭānāṃ
      mahā-grahāṇāṃ utsādana-kara hūṃ trūṃ.
      Rakṣa rakṣa māṃ. Bhagavan stathāgatoṣṇīṣa
      sitātapatra mahā vajroṣṇīṣa, mahā pratyaṅgire
      mahā sahasra-bhuje sahasra-śīrṣe, koṭī-śata
      sahasra-netre, abhedya jvalitā-taṭaka,
      mahā-vajrodāra tri-bhuvana maṇḍala.
      Oṃ svastir bhavatu māṃ mama
    </p>
  </div>
```

**卡片 3 — 破除障難 · Cchinda 段（第 80–114 行）：**

```html
  <div class="ms-card s3 reveal">
    <div class="ms-header">
      <span class="ms-num">第三段</span>
      <span class="ms-title">破除障難 · Cchinda 段</span>
      <span class="ms-tag">第 80–114 行</span>
    </div>
    <p class="ms-text compact">
      Rāja-bhayā cora-bhayā udaka-bhayā agni-bhayā,
      viṣa-bhayā śastra-bhayā para-cakra-bhayā
      dur-bhikṣa-bhayā, aśani-bhayā akāla-mṛtyu-bhayā
      dharaṇī-bhūmi-kampā-bhayā ulkā-pāta-bhayā,
      rāja-daṇḍa-bhayā suparṇi-bhayā nāga-bhayā
      vidyu-bhayā. Deva-grahā nāga-grahā yakṣa-grahā
      rākṣasa-grahā preta-grahā, piśāca-grahā
      bhūta-grahā kumbhaṇḍa-grahā pūtana-grahā,
      kaṭa-pūtana-grahā skanda-grahā apasmāra-grahā
      utmāda-grahā, cchāya-grahā revati-grahā
      jamika-grahā kaṇṭha-kamini-grahā. Ojāhāriṇyā
      garbhāhāriṇyā jātāhāriṇyā jīvitāhāriṇyā,
      rudhirāhāriṇyā vasāhāriṇyā māṃsāhāriṇyā
      medāhāriṇyā, majjāhāriṇyā vāntāhāriṇyā
      aśucyāhāriṇyā ciccāhāriṇyā, teṣāṃ sarveṣāṃ.
      Sarva grahāṇāṃ vidyāṃ cchinda-yāmi kīla-yāmi.
      Pari-brajāka kṛtāṃ vidyāṃ cchinda-yāmi kīla-yāmi.
      Ḍāka-ḍākinī kṛtāṃ vidyāṃ cchinda-yāmi kīla-yāmi.
      Mahā-paśupati rudra kṛtāṃ vidyāṃ cchinda-yāmi
      kīla-yāmi. Nārāyaṇā paṃca mahā mudrā kṛtāṃ
      vidyāṃ cchinda-yāmi kīla-yāmi. Tatva garuḍa
      sahīyāya kṛtāṃ vidyāṃ cchinda-yāmi kīla-yāmi.
      Mahā-kāla mātṛgaṇa sahīyāya kṛtāṃ vidyāṃ
      cchinda-yāmi kīla-yāmi. Kāpālika kṛtāṃ vidyāṃ
      cchinda-yāmi kīla-yāmi. Jayakarā madhukara
      sarvārtha-sādhaka kṛtāṃ, vidyāṃ cchinda-yāmi
      kīla-yāmi. Catur-bhaginī bhratṛ-paṃcama sahīyāya
      kṛtāṃ, vidyāṃ cchinda-yāmi kīla-yāmi.
      Bhṛṅgi-riṭika nandi-keśvara gaṇapati sahīya kṛtāṃ,
      vidyāṃ cchinda-yāmi kīla-yāmi. Nagna-śramaṇa
      kṛtāṃ vidyāṃ cchinda-yāmi kīla-yāmi. Arhanta
      kṛtāṃ vidyāṃ cchinda-yāmi kīla-yāmi. Vīta-rāga
      kṛtāṃ vidyāṃ cchinda-yāmi kīla-yāmi. Vajra-pāṇi
      guhyakādhipati kṛtāṃ vidyāṃ cchinda-yāmi
      kīla-yāmi. Rakṣa rakṣa māṃ.
    </p>
  </div>
```

**卡片 4 — 降伏諸魔 · Phaṭ 段（第 117–151 行）：**

```html
  <div class="ms-card s4 reveal">
    <div class="ms-header">
      <span class="ms-num">第四段</span>
      <span class="ms-title">降伏諸魔 · Phaṭ 段</span>
      <span class="ms-tag">第 117–151 行</span>
    </div>
    <p class="ms-text compact">
      Bhagavata stathāgatoṣṇīṣaṃ sitātapatraṃ
      namo-stute. Asitānalārka prabha-sphuṭa
      vikasitātapatre. Jvala jvala dhaka-dhaka
      vidhaka-vidhaka dara dara vidara vidara, cchinda
      cchinda bhinda bhinda, hūṃ hūṃ phaṭ! phaṭ!
      svāhā. Hehe phaṭ. Amogha phaṭ. Apratihata phaṭ.
      Vara-prada phaṭ. Asura vidrāpaka phaṭ.
      Sarva deve-bhyaḥ phaṭ. Sarva nāge-bhyaḥ phaṭ.
      Sarva yakṣe-bhyaḥ phaṭ. Sarva rākṣase-bhyaḥ
      phaṭ. Sarva garuḍe-bhyaḥ phaṭ. Sarva
      gāndharve-bhyaḥ phaṭ. Sarva asure-bhyaḥ phaṭ.
      Sarva kindare-bhyaḥ phaṭ. Sarva mahorage-bhyaḥ
      phaṭ. Sarva manuṣe-bhyaḥ phaṭ.
      Sarva amanuṣe-bhyaḥ phaṭ. Sarva bhūte-bhyaḥ
      phaṭ. Sarva piśāce-bhyaḥ phaṭ. Sarva
      kumbhaṇḍe-bhyaḥ phaṭ. Sarva pūtane-bhyaḥ
      phaṭ. Sarva kaṭa-pūtane-bhyaḥ phaṭ.
      Sarva dur-laṅghite-bhyaḥ phaṭ. Sarva
      duṣ-prekṣite-bhyaḥ phaṭ. Sarva jvare-bhyaḥ phaṭ.
      Sarva apasmāre-bhyaḥ phaṭ. Sarva
      śramaṇe-bhyaḥ phaṭ. Sarva tirthike-bhyaḥ phaṭ.
      Sarva utmāde-bhyaḥ phaṭ. Sarva
      vidyā-rājācārye-bhyaḥ phaṭ. Jayakarā madhukara
      sarvārtha-sādhake-bhyaḥ phaṭ. Sarva
      vidyācārye-bhyaḥ phaṭ. Catur bhaginī-bhyaḥ phaṭ.
      Vajra kaumāri kulan-dharī mahā-vidyā-rājebhyaḥ
      phaṭ. Mahā-pratyaṅgire-bhyaḥ phaṭ. Vajra
      śaṅkalāya phaṭ. Mahā-pratyaṅgira-rājāya phaṭ.
      Mahā-kālāya mahā-mātṛ-gaṇa namas-kṛtāya phaṭ.
      Vaiṣṇuvīye phaṭ. Brahmaṇīye phaṭ. Agnīye phaṭ.
      Mahā-kālīye phaṭ. Kāla-daṇḍīye phaṭ.
      Indrīye phaṭ. Raudrīye phaṭ. Cāmuṇḍīye phaṭ.
      Kāla-rātrīye phaṭ. Kāpālīye phaṭ.
      Adhi-muktaka śmaśāna vāsinīye phaṭ.
      Yeke-citta satva mama.
    </p>
  </div>
```

**卡片 5 — 結界護身 · Bandha 段（第 154–193 行）：**

```html
  <div class="ms-card s5 reveal">
    <div class="ms-header">
      <span class="ms-num">第五段</span>
      <span class="ms-title">結界護身 · Bandha 段</span>
      <span class="ms-tag">第 154–193 行</span>
    </div>
    <p class="ms-text compact">
      Duṣṭa-cittā pāpa-cittā raudra-cittā vi-dveṣa
      amaitra-cittā. Utpāda-yanti kīla-yanti mantra-yanti
      japanti juhvanti. Ojāhārā garbhāhārā rudhirāhārā
      vasāhārā, majjāhārā jātāhārā jīvitāhārā malyāhārā,
      gandhāhārā puṣpāhārā phalāhārā sasyāhārā.
      Pāpa-cittā duṣṭa-cittā raudra-cittā. Yakṣa-graha
      rākṣasa-graha preta-graha piśāca-graha,
      bhūta-graha kumbhaṇḍa-graha
      skanda-graha utmāda-graha, cchāya-graha
      apasmāra-graha ḍāka-ḍākinī-graha, revati-graha
      jamika-graha śakuni-graha mantra-nandika-graha,
      lamvika-graha hanu kaṇṭha-pāṇi-graha. Jvara
      ekāhikā dvaitīyakā straitīyakā catur-thakā.
      Nitya-jvarā viṣama-jvarā vātikā paittikā,
      śleṣmikā san-nipatikā sarva-jvarā.
      Śirortti ardhavabhedaka arocaka, akṣi-rogaṃ
      nasa-rogaṃ mukha-rogaṃ hṛd-rogaṃ
      gala-grahaṃ, karṇa-śūlaṃ danta-śūlaṃ
      hṛdaya-śūlaṃ marma-śūlaṃ, pārśva-śūlaṃ
      pṛṣṭha-śūlaṃ udara-śūlaṃ kaṇṭī-śūlaṃ,
      vasti-śūlaṃ ūru-śūlaṃ jāṅgha-śūlaṃ hasta-śūlaṃ,
      pāda-śūlaṃ sarvāṅga-pratyaṅga-śūlaṃ.
      Bhūta vetāḍa ḍāka-ḍākinī jvara. Dadru kāṇḍu
      kiṭibhalota vaisarpa-lohāliṅga, śūṣa trasa gara
      viṣa-yoga, agni udaka mara vaira kāntāra
      akālaṃ-mṛtyu. Traibuka trai-laṭaka vṛścika sarpa
      nakula, siṃgha vyāghra ṛkṣa tarakṣa mṛga,
      sva-para jīva teṣāṃ sarveṣāṃ. Sitātapatraṃ
      mahā-vajroṣṇīṣaṃ mahā-pratyaṅgiraṃ.
      Yāvadvā-daśa yojanābhyantareṇa,
      sīmā-bandhaṃ karomi, diśā-bandhaṃ karomi,
      pāra-vidyā-bandhaṃ karomi, tejo-bandhaṃ
      karomi, hasta-bandhaṃ karomi, pāda-bandhaṃ
      karomi, sarvāṅga-pratyaṅga-bandhaṃ karomi.
      Tadyathā: Oṃ anale anale viśade viśade
      vīra vajra-dhare, bandha bandhani,
      vajra-pāṇi phaṭ! hūṃ trūṃ phaṭ! svāhā.
      Namaḥ stathāgatāya sugatāya arhate
      samyak-saṃ buddhāya,
      siddhyantu mantra-pada svāhā.
    </p>
  </div>

</div>
```

- [ ] **Step 3: Commit**

```bash
git add lengyanzhou.html
git commit -m "feat: add full text breakdown cards for Shurangama mantra"
```

---

### Task 4: 替換四階段訓練計畫（Phase Cards）

**Files:**
- Modify: `lengyanzhou.html`

- [ ] **Step 1: 替換 section label/title/sub**

找到第三個 `<section>`（訓練計畫區塊）的 label/title/sub，替換為：

```html
<p class="section-label">第三步 · 開始訓練</p>
<h2 class="section-title">四階段訓練計畫</h2>
<p class="section-sub">廿一天分散練習，每天不超過一小時。分散勝於集中，睡眠是記憶的盟友。</p>
```

- [ ] **Step 2: 替換四張 phase card 內容**

找到 `<div class="cards-grid">` 整區塊（從 `<div class="cards-grid">` 到對應的 `</div>`），替換為以下四張卡片。每張保留原有 class（`card p1`、`card p2` 等）：

**Phase 1 — 建立聽覺記憶（Day 1–5）：**

```html
<div class="cards-grid">

  <article class="card p1 reveal">
    <div class="card-header">
      <p class="card-phase-label">第一階段</p>
      <span class="day-badge">Day 1–5</span>
    </div>
    <h2>建立聽覺記憶</h2>
    <ul>
      <li>Day 1–2：跟讀<strong>歸敬段</strong>（第 1–57 行），感受 Namaḥ 禮敬節奏，跟讀 5 遍</li>
      <li>Day 3：攻克<strong>核心咒鬘 + 破除段</strong>（第 60–114 行），抓住 hūṃ trūṃ 和 cchinda-kīla 的韻律</li>
      <li>Day 4：攻克<strong>降伏段 + 結界段</strong>（第 117–193 行），感受 phaṭ 雷音陣和 bandha 結界</li>
      <li>Day 5：<strong>全文串聽</strong>，不看文本完整跟讀 2 遍，感受整體流動</li>
      <li>每天睡前播放當天區段錄音 15 分鐘，利用睡眠記憶鞏固機制</li>
    </ul>
    <div class="daily-schedule">
      <p class="daily-schedule-title">每日時間分配</p>
      <div class="daily-slots">
        <span class="time-slot">Day 1–2 歸敬段跟讀+指讀 約40min</span>
        <span class="time-slot">Day 3 核心+破除段 約35min</span>
        <span class="time-slot">Day 4 降伏+結界段 約35min</span>
        <span class="time-slot">Day 5 全文串聽+睡前音頻 約45min</span>
      </div>
    </div>
    <p class="card-note">像學一首史詩般去感受它的韻律，不急於理解，讓聲音先在腦中留下印記</p>
  </article>
```

**Phase 2 — 結構化拆解（Day 6–10）：**

```html
  <article class="card p2 reveal">
    <div class="card-header">
      <p class="card-phase-label">第二階段</p>
      <span class="day-badge">Day 6–10</span>
    </div>
    <h2>結構化拆解</h2>
    <ul>
      <li><strong>Day 6 — 歸敬段：</strong>利用 6 次「Namo bhagavate…」重複句型分組，每組 4–5 行逐組擊破</li>
      <li><strong>Day 7 — 核心咒鬘段：</strong>四種行動（震撼→僵止→迷惑→粉碎）配四種手勢，用身體動作輔助記憶</li>
      <li><strong>Day 8 — 破除段：</strong>19 次 cchinda-yāmi kīla-yāmi 如念珠計數，邊撥念珠邊背誦，建立觸覺記憶</li>
      <li><strong>Day 9 — 降伏段：</strong>30+ phaṭ 按目標分類（天龍八部→疾病→鬼神→咒師），分組逐類背誦</li>
      <li><strong>Day 10 — 結界段：</strong>七重 bandha 結界配七個身體部位觸碰（頭→肩→胸→腹→腿→腳→全身），建立空間記憶</li>
    </ul>
    <div class="daily-schedule">
      <p class="daily-schedule-title">每日時間分配</p>
      <div class="daily-slots">
        <span class="time-slot">每天攻克一段 約40–50min</span>
        <span class="time-slot">早晚各一次串聯複習 約15min</span>
      </div>
    </div>
    <p class="card-note">每段攻克後立即串聯前面已學段落，避免學一段忘一段</p>
  </article>
```

**Phase 3 — 鞏固與內化（Day 11–15）：**

```html
  <article class="card p3 reveal">
    <div class="card-header">
      <p class="card-phase-label">第三階段</p>
      <span class="day-badge">Day 11–15</span>
    </div>
    <h2>鞏固與內化</h2>
    <ul>
      <li><strong>Day 11–12 — 費曼輸出法：</strong>假裝你要教別人楞嚴咒，大聲說出每段的功能、記憶技巧和關鍵梵文詞</li>
      <li><strong>Day 13 — 手寫抄寫：</strong>分兩天各抄約 97 行，手寫激活運動記憶腦區，與聽覺記憶形成雙通道</li>
      <li><strong>Day 14 — 干擾抗練：</strong>邊走路邊背誦，測試身體分心時記憶是否穩固；請人隨機說關鍵詞（如 phaṭ / cchinda / bandha），從該處往後接</li>
      <li><strong>Day 15 — 加速挑戰：</strong>以 1.2 倍速連貫背誦全文，標記所有卡頓處，只練那些弱點段落各 10 遍</li>
      <li>排隊、等車、洗澡……抓住所有碎片時間各背一次</li>
    </ul>
    <div class="daily-schedule">
      <p class="daily-schedule-title">每日時間分配</p>
      <div class="daily-slots">
        <span class="time-slot">Day 11–12 費曼輸出+碎片背誦 約30min</span>
        <span class="time-slot">Day 13 手寫抄寫 約50min</span>
        <span class="time-slot">Day 14 干擾抗練+隨機接龍 約30min</span>
        <span class="time-slot">Day 15 加速挑戰+弱點修復 約30min</span>
      </div>
    </div>
    <p class="card-note">卡住處不要從頭來，只練那一小段 10 遍，精準打擊弱點</p>
  </article>
```

**Phase 4 — 終極驗收（Day 16–21）：**

```html
  <article class="card p4 reveal">
    <div class="card-header">
      <p class="card-phase-label">第四階段</p>
      <span class="day-badge">Day 16–21</span>
    </div>
    <h2>終極驗收</h2>
    <ul>
      <li><strong>Day 16–17：</strong>分段錄音對照文本，逐段檢查準確度，標記所有錯誤處</li>
      <li><strong>Day 18：</strong>首次全文完整背誦錄音，對照文本逐字檢查</li>
      <li><strong>Day 19：</strong>集中修復薄弱段落，針對錯誤處重複練習至無誤</li>
      <li><strong>Day 20：</strong>第二次全文錄音，目標：✅ 15 分鐘內完成 ✅ 錯誤不超過 3 處</li>
      <li><strong>Day 21：</strong>24 小時冷卻後最終檢驗，無新增錯誤即為過關</li>
      <li>✅ 驗收完成後保持每週溫習 1–2 次，間隔遞增（3天→7天→14天→30天）</li>
    </ul>
    <div class="daily-schedule">
      <p class="daily-schedule-title">驗收方式</p>
      <div class="daily-slots">
        <span class="time-slot">分段錄音對照</span>
        <span class="time-slot">全文錄音逐字檢查</span>
        <span class="time-slot">24h 冷卻最終檢驗</span>
      </div>
    </div>
    <p class="card-note">驗收不是終點，是長期記憶的起點。每週溫習，讓楞嚴梵音永不褪色</p>
  </article>

</div>
```

- [ ] **Step 2: Commit**

```bash
git add lengyanzhou.html
git commit -m "feat: add 21-day four-phase training plan for Shurangama mantra"
```

---

### Task 5: 替換技巧卡、注意事項、Footer

**Files:**
- Modify: `lengyanzhou.html`

- [ ] **Step 1: 替換核心記憶技巧區塊**

找到 `<section class="techniques">` 中的 label/title/sub 和 `<div class="tech-grid">`，替換為：

```html
<section class="techniques">
  <p class="section-label">工具箱</p>
  <h2 class="section-title">核心記憶技巧</h2>
  <p class="section-sub">七種方法，多重感官，讓楞嚴梵音自然銘刻</p>
  <div class="tech-grid">
    <div class="tech-card reveal">
      <span class="tech-icon" aria-hidden="true">📿</span>
      <h3>Namaḥ 禮敬鏈</h3>
      <p>6 次重複的禮敬句型形成穩定節奏，如念珠般一氣呵成</p>
    </div>
    <div class="tech-card reveal">
      <span class="tech-icon" aria-hidden="true">🗂️</span>
      <h3>五段空間分段</h3>
      <p>將 193 行拆成五個有意義的功能段落，化整為零</p>
    </div>
    <div class="tech-card reveal">
      <span class="tech-icon" aria-hidden="true">🔢</span>
      <h3>Cchinda-Kīla 念珠法</h3>
      <p>19 次破除雙刃如念珠撥動，配合實體念珠建立觸覺記憶</p>
    </div>
    <div class="tech-card reveal">
      <span class="tech-icon" aria-hidden="true">⛈️</span>
      <h3>Phaṭ 雷音分類</h3>
      <p>30+ phaṭ 按天龍八部、疾病、鬼神分組，化混亂為有序</p>
    </div>
    <div class="tech-card reveal">
      <span class="tech-icon" aria-hidden="true">✋</span>
      <h3>Hūṃ Trūṃ 四行動手勢</h3>
      <p>震撼→僵止→迷惑→粉碎，四種手勢將梵音寫入身體記憶</p>
    </div>
    <div class="tech-card reveal">
      <span class="tech-icon" aria-hidden="true">📍</span>
      <h3>七重結界身體錨</h3>
      <p>七個 bandha 對應七個身體部位，用空間位置輔助回憶</p>
    </div>
    <div class="tech-card reveal">
      <span class="tech-icon" aria-hidden="true">🌙</span>
      <h3>睡眠固化</h3>
      <p>睡前聽、醒後背，21 天充分利用睡眠記憶鞏固機制</p>
    </div>
  </div>
</section>
```

- [ ] **Step 2: 替換注意事項區塊 label/title/sub**

```html
<p class="section-label">心法</p>
<h2 class="section-title">注意事項</h2>
<p class="section-sub">技巧是工具，心態是地基。楞嚴咒篇幅長，這四條原則決定你能走多遠。</p>
```

- [ ] **Step 3: 替換注意事項卡片內容**

保留 `.notes-grid` 結構，替換四張 note-card 內容：

```html
<div class="notes-grid reveal">
  <div class="note-card">
    <span class="note-num" aria-hidden="true">01</span>
    <div>
      <h4>不要死記硬背</h4>
      <p>這是有韻律的護身咒語，不是考試條文。感受每一段的功能和力量——歸敬的莊嚴、phaṭ 的爆發、bandha 的守護——讓旋律帶著文字自然流淌。</p>
    </div>
  </div>
  <div class="note-card">
    <span class="note-num" aria-hidden="true">02</span>
    <div>
      <h4>每天不超過 1 小時</h4>
      <p>193 行的篇幅容易讓人想「惡補」，但過量練習導致邊際效益遞減。分散到每天 30–50 分鐘，21 天的累積效果遠勝短時間衝刺。</p>
    </div>
  </div>
  <div class="note-card">
    <span class="note-num" aria-hidden="true">03</span>
    <div>
      <h4>卡住不求全</h4>
      <p>某處反覆卡住時，不要每次都從頭開始。只練那一小段 10 遍，精準打擊弱點，直到它和上下文自然銜接。楞嚴咒的 cchinda-kīla 和 phaṭ 是天然的記憶救生索。</p>
    </div>
  </div>
  <div class="note-card">
    <span class="note-num" aria-hidden="true">04</span>
    <div>
      <h4>保持恭敬心</h4>
      <p>心態放鬆但莊重。緊張和焦慮是記憶的最大敵人。楞嚴咒本身就是護身咒——以被守護的安心感去背誦，而非被篇幅壓垮的恐懼。</p>
    </div>
  </div>
</div>
```

- [ ] **Step 4: 替換 Footer**

```html
<footer>
  <p>每日不超過 1 小時 · 保持恭敬放鬆之心 · 分散勝於集中 · 廿一日自然成誦</p>
  <p class="closing-mantra">Oṃ anale anale viśade viśade vīra vajra-dhare bandha bandhani vajra-pāṇi phaṭ hūṃ trūṃ phaṭ svāhā</p>
</footer>
```

- [ ] **Step 5: Commit**

```bash
git add lengyanzhou.html
git commit -m "feat: add techniques, notes, and footer for Shurangama mantra page"
```

---

### Task 6: 最終檢查與驗證

**Files:**
- Verify: `lengyanzhou.html`

- [ ] **Step 1: 確認 HTML 結構完整性**

檢查以下元素都存在且正確嵌套：
- `<html lang="zh-Hant">` + `<head>` 內所有 meta、title、字型 link
- `<style>` 標籤完整無修改（與 `memory-plan.html` 一致）
- `<button class="theme-toggle">` 存在
- 五大 `<section>` 都存在且內容完整
- `</main>` 和 `<footer>` 正確關閉
- `<script>` 標籤完整無修改（Intersection Observer + theme toggle）

- [ ] **Step 2: 在瀏覽器中打開驗證**

```bash
open lengyanzhou.html
```

檢查項目：
- [ ] 頁面載入無 JavaScript 錯誤（打開 DevTools Console）
- [ ] Hero 梵文文字有呼吸光暈動畫
- [ ] 結構總覽表正常顯示（5 列）
- [ ] 4 張 pattern 卡排列正常
- [ ] 5 張 manuscript 寫經卡顯示完整梵文，左側色條正確
- [ ] 4 張 phase 卡在桌面端呈 2×2 網格，中央念珠線可見
- [ ] 7 張技巧卡 flex wrap 排列
- [ ] 4 張筆記卡正常顯示
- [ ] Footer 顯示正確結尾梵音
- [ ] 主題切換按鈕可正常切換 light/dark
- [ ] 捲動時卡片有 reveal 動畫

- [ ] **Step 3: 縮小視窗至 740px 以下，確認響應式**

- [ ] phase 卡變為單欄
- [ ] 中央念珠線消失
- [ ] 表格可水平捲動

- [ ] **Step 4: 最終 commit**

```bash
git add lengyanzhou.html
git commit -m "feat: complete Shurangama mantra 21-day training page"
```
