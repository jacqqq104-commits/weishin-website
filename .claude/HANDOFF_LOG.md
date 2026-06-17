# Weishin Website Handoff Log

這份文件記錄 Codex 接手後的操作紀錄，讓之後 Claude Code 或其他 AI Agent 進入 `/Users/user/AI/weishin` 時能快速理解目前狀態。

## 專案目前狀態

- 本機路徑：`/Users/user/AI/weishin`
- 主要檔案：`index.html`
- 線上網站：`https://weishin-website.netlify.app`
- GitHub remote：`git@github-jacqqq104:jacqqq104-commits/weishin-website.git`
- Branch：`main`
- Netlify 已連 GitHub，自動部署。
- 最新已推送 commit：`b0d0b68 歷史照片改為黑白濾鏡`

## Codex 已完成事項

### 1. 讀取工作區與專案狀態

- 讀取 `/Users/user/AI` 主要資料結構。
- 讀取 AI Agent 核心文件：
  - `/Users/user/AI/AI_Agent/README.md`
  - `/Users/user/AI/AI_Agent/CLAUDE.md`
  - `/Users/user/AI/AI_Agent/AGENTS.md`
  - `/Users/user/AI/AI_Agent/000_Agent/Core/CORE_RULES.md`
  - `/Users/user/AI/AI_Agent/000_Agent/Memory/References/PROFILE.md`
  - `/Users/user/AI/AI_Agent/000_Agent/Memory/Feedback/STYLE_PREFERENCES.md`
- 讀取網站部署文件：`.claude/DEPLOY.md`
- 確認專案實際資料夾名稱是 `weishin`，不是 `weshin`。

### 2. 專案健康檢查

- 確認 `index.html` 是單頁靜態網站，包含：
  - Hero
  - 關於維新
  - 維新歷史
  - 為何選擇維新
  - 五大部門
  - 產品應用
  - 認證
  - 聯絡資訊、Google Map、詢價表單
  - 中英切換
- 確認線上網站回應正常：`HTTP 200`
- 確認本機 `index.html` 與線上 Netlify HTML 曾經 hash 一致。
- 圖片引用檢查結果：
  - 主要頁面圖片都存在。
  - `images/favicon.ico` 被 HTML 引用但檔案不存在，線上會 404。
- 表單狀態：
  - 目前 `<form>` action 是 `contact_form_handler.asp`。
  - 因為 Netlify 是靜態部署，這個表單大概率不能實際收信，後續應改成 Netlify Forms、Formspree、mailto 或其他後端。
- 其他素材狀態：
  - `images/h-01bg.jpg` 副檔名是 jpg，但檔案內容實際是 HTML，且目前未被 `index.html` 引用。

### 3. 第一次 HTML 修改：移除歷史區塊寬版照片

使用者指出歷史區塊 2019/2020 下方的寬版鋁材照片不要使用，只保留上方三張照片。

修改內容：

- 檔案：`index.html`
- 位置：第四章「全程數位化生產 2008–今」的圖片列
- 移除這行：

```html
<img src="images/hero-history.jpg" alt="現代設備" loading="lazy">
```

保留：

```html
<img src="images/frame02.jpg" alt="數位化生產設備" loading="lazy">
<img src="images/frame03.jpg" alt="擠型生產線" loading="lazy">
<img src="images/frame04.jpg" alt="現代廠房" loading="lazy">
```

Commit：

```text
4132d3e 移除歷史區塊寬版照片
```

部署驗證：

- 已 push 到 GitHub。
- Netlify 已更新。
- 線上 HTML 已確認不再引用 `images/hero-history.jpg`。

### 4. 第二次 HTML 修改：右下角照片加黑白濾鏡

使用者指出 1991 區塊右下角彩色設備照看起來不一致，希望改成黑白濾鏡。

修改內容：

- 檔案：`index.html`
- 新增 CSS：

```css
.tl-img-row img.img-bw { filter: grayscale(100%); }
```

- 將 `images/frame0021.jpg` 加上 class：

```html
<img src="images/frame0021.jpg" alt="早期設備" loading="lazy" class="img-bw">
```

注意：

- 沒有修改原始圖片檔。
- 只透過 HTML/CSS 套黑白濾鏡，方便未來恢復。

Commit：

```text
b0d0b68 歷史照片改為黑白濾鏡
```

部署驗證：

- 已 push 到 GitHub。
- Netlify 已更新。
- 線上 HTML 已確認包含 `class="img-bw"`。

## 目前未提交變更

截至 Codex 紀錄時，工作樹仍有兩個先前存在、非本次任務造成的未提交變更：

```text
M .DS_Store
M images/about-p1.jpg
```

注意：

- Codex 沒有 stage 或 push 這兩個檔案。
- `images/about-p1.jpg` 本機版本大小約 55KB，線上版本約 306KB。
- 目前 `images/about-p1.jpg` 沒有被 `index.html` 引用，因此暫時不影響線上畫面。

## 建議下一步

1. 處理 favicon：
   - 新增 `images/favicon.ico`，或移除/改寫 HTML 裡的 favicon 引用。
2. 決定詢價表單要怎麼收：
   - Netlify Forms
   - Formspree
   - Google Form
   - mailto
   - 自建後端
3. 清理或確認未提交變更：
   - `.DS_Store` 建議不要提交，之後可加 `.gitignore`。
   - `images/about-p1.jpg` 需確認是否要保留新版本、恢復舊版、或移除未使用素材。
4. 檢查未引用素材：
   - `images/h-01bg.jpg` 內容異常，建議確認是否可刪除或修正。
5. 若後續 Claude 接手修改，請先執行：

```bash
cd /Users/user/AI/weishin
git status --short --branch
git log --oneline --decorate -5
```

避免把既有未提交檔案誤包進下一次 commit。

## 後續 Codex 修改紀錄

### 5. 重建新版部門介紹區塊

使用者指出原始網站 `http://www.weishin.com/eng/index.html` 有完整部門介紹，新版雖有簡短部門卡片，但不夠完整；要求依照新網頁風格重新建構，不要自行亂做。

參考來源：

- 英文原站：
  - `http://www.weishin.com/eng/rawmaterialmanagement.html`
  - `http://www.weishin.com/eng/dieshop.html`
  - `http://www.weishin.com/eng/extrusion.html`
  - `http://www.weishin.com/eng/highalloyextrusion.html`
  - `http://www.weishin.com/eng/qualitycontrol.html`
- 中文原站：
  - `http://www.weishin.com/rawmaterialmanagement.html`
  - `http://www.weishin.com/dieshop.html`
  - `http://www.weishin.com/extrusion.html`
  - `http://www.weishin.com/highalloyextrusion.html`
  - `http://www.weishin.com/qualitycontrol.html`

注意：

- 原站 `HEAD` request 會回 404，但 `GET` 可取得實際 HTML，因此內容抽取以 `GET` 結果為準。
- 原站曾出現錯誤連結 `qualityxontrol.html`，正確頁面是 `qualitycontrol.html`。

修改內容：

- 檔案：`index.html`
- 將原本簡短的 5 張部門摘要卡重建為完整的新版部門區塊。
- 保留新版設計語言：深藍 / 金色、`sec-label`、`sec-title`、8px 卡片、Bootstrap Icons、雙語切換。
- 新增五個子區塊 anchor：
  - `#dept-raw`
  - `#dept-die`
  - `#dept-extrusion`
  - `#dept-alloy`
  - `#dept-quality`
- 導覽列 Department 改為下拉選單，可跳到各部門子區。
- 新增實際使用的部門圖片：
  - `images/raw-01.jpg`
  - `images/raw-02.jpg`
  - `images/raw-03.jpg`
  - `images/hero-depart-1.jpg`
  - `images/die-05.jpg`
  - `images/hero-depart-2.jpg`
  - `images/main.jpg`
  - `images/ex-04.jpg`
  - `images/ex-05.jpg`
  - `images/hero-depart-4.jpg`
  - `images/q001.jpg`
  - `images/p5-1.jpg`
  - `images/p502.jpg`
  - `images/p5-3.jpg`
  - `images/p5-4.jpg`
  - `images/p5-5.jpg`

驗證：

- 本機檢查所有新增部門圖片皆可載入。
- `#departments` 下共有 5 個 `.dept-section`。
- 品保區共有 5 個 `.quality-item`。
- 目前尚未 commit / push。

### 6. 首頁 Hero 桌機與手機版版面平衡

使用者提供截圖指出首頁 hero 文字太靠左，要求同時考慮電腦版與手機版。

修改內容：

- 檔案：`index.html`
- 調整 `.hero-content`：
  - 桌機：限制最大寬度並加上 responsive 左側位移，讓文字群不要貼左。
  - 手機：在 `max-width: 768px` 斷點取消額外位移，維持正常 12px 內距。
- 增加 `body { overflow-x: hidden; }`。
- 手機斷點加入 `.row { --bs-gutter-x: 0; }`，避免 Bootstrap row 負 gutter 造成手機橫向溢出。

驗證：

- 2048px 桌機模擬：hero 文字區從約 23% viewport 位置開始，比原截圖更平衡。
- 390px 手機模擬：
  - hero 文字 x=12px。
  - `scrollWidth` 等於 viewport width。
  - 無橫向 overflow。
- 目前尚未 commit / push。

### 7. 語言切換移到導覽列外層

使用者提供手機選單截圖，指出英文版 `ENG` 按鈕藏在展開選單底部太不明顯，應放在更明顯的外層。

修改內容：

- 檔案：`index.html`
- 將原本放在 `#navMenu` collapse 內的語言切換按鈕移到 navbar 外層。
- 新位置：品牌 logo 右側空間自動推到最右，固定顯示在漢堡選單左邊。
- 按鈕改為金色樣式，加入 `bi-globe2` 圖示，提高可見性。
- 更新 `toggleLang()`：
  - 改成只更新按鈕內的 `<span>` 文字，避免切換後圖示消失。
  - 同步更新 `aria-label`。

驗證：

- 1280px 桌機量測：
  - `ENG` 按鈕在漢堡左側。
  - 與漢堡間距約 9px。
- 390px 手機量測：
  - `ENG` 按鈕固定顯示在外層，不需展開選單即可看到。
  - 與漢堡間距約 9px。
  - `scrollWidth` 等於 viewport width，無橫向 overflow。
- 點擊語言按鈕後：
  - `html.lang` 會切成 `en`。
  - `body` class 會切成 `lang-en`。
  - 按鈕文字會從 `ENG` 變成 `中文`。
- 目前尚未 commit / push。
