# Dashboard 字體探索 — 下一步任務

> 給 AI 的工作交接文件。直接接著做，不需要問太多。

---

## 專案位置

- 本機路徑：`~/Documents/dashboard/`
- GitHub：https://github.com/chingjungkuan/dashboard
- 主要檔案：`index.html`、`css/style.css`

---

## 目前完成的狀態

字體探索頁面（`#view-fonts`）已實作：

- **FONT_DB**：77 款中文/日文字型，每筆有 `zhName, enName, maker, license, type, desc, gFont`
- **type 欄位目前的值**：`gothic | mincho | round | handwrite | brush | kai | display`
- **篩選列**：類型篩選（黑體/明體/圓體…）+ 授權篩選（免費/Mac/Adobe/付費）
- **Google Fonts 即時預覽**：有 `gFont` 的字型自動載入並預覽
- **收藏功能**：儲存到 JSONBin 雲端（`appData.fontCollection`）
- **AI 搜尋**：輸入字體名稱 → Claude Haiku 推薦相似字體（需 API Key）

---

## 下一步要做的事

### 任務：加入英文字型 + 改為風格導向篩選

來源：PDF《FONTS-COLLECTION》by designnotdeep，共約 160 款免費英文字型。

---

### Step 1：擴充 FONT_DB 資料結構

在每筆 FONT_DB 加入 `lang` 欄位區分中英文：

```js
// 現有中文字型加上 lang: 'zh'
{ zhName:'思源黑體', enName:'Noto Sans TC', lang:'zh', type:'gothic', ... }

// 新增英文字型用 lang: 'en'，type 改用英文風格名稱
{ zhName:'Inter', enName:'Inter', lang:'en', type:'humanist', maker:'Google', license:'free',
  desc:'排版師公認最清晰的人文無襯線體，UI 設計首選', gFont:'Inter:wght@400;700' }
```

---

### Step 2：英文字型的 `type` 風格分類

用以下 style key（對應 PDF 章節）：

| style key | 中文說明 | PDF 分類 |
|-----------|---------|---------|
| `grotesk` | 怪誕 | Grotesk |
| `humanist` | 人文 | Humanist |
| `neo-grotesque` | 新怪誕 | Neo-Grotesque |
| `geometric` | 幾何 | Geometric |
| `old-style` | 舊體 | Old Style Serif |
| `transitional` | 過渡 | Transitional Serif |
| `modern-serif` | 現代襯線 | Modern Serif |
| `slab` | 平板襯線 | Slab Serif |
| `script` | 書寫體 | Scripts & Calligraphic |
| `handwritten` | 手寫 | Handwritten |
| `brush` | 筆刷 | Brush |
| `blackletter` | 黑體字 | Blackletter |
| `elegant` | 質感 | Elegant Display |
| `poster` | 海報 | Poster & Art Deco |
| `display-en` | 標題特色 | Display / Others |

---

### Step 3：要加入的英文字型清單

以下是從 PDF 整理的字型，標示哪些在 Google Fonts（可直接用 gFont）：

#### Grotesk（怪誕無襯線）
```
Questrial         → Google Fonts ✓
HK Grotesk        → 非 Google，gFont: null
Clash Display     → 非 Google，gFont: null
Cabinet Grotesk   → 非 Google，gFont: null
Sporting Grotesque → 非 Google，gFont: null
Syne              → Google Fonts ✓ (Syne:wght@400;700)
```

#### Humanist（人文無襯線）
```
Lato              → Google Fonts ✓
Inter             → Google Fonts ✓
Golos UI          → Google Fonts ✓
Aileron           → 非 Google，gFont: null
Roboto            → Google Fonts ✓
Cabin             → Google Fonts ✓
Open Sans         → Google Fonts ✓
```

#### Neo-Grotesque（新怪誕）
```
Raleway           → Google Fonts ✓
```

#### Geometric（幾何無襯線）
```
Montserrat        → Google Fonts ✓  ← 已在收藏中，勿重複
Poppins           → Google Fonts ✓
Jost              → Google Fonts ✓
Josefin Sans      → Google Fonts ✓
DM Sans           → Google Fonts ✓  ← 已在收藏中，勿重複
Manrope           → Google Fonts ✓
Lexend            → Google Fonts ✓
Poiret One        → Google Fonts ✓
```

#### Old Style Serif（舊體襯線）
```
EB Garamond       → Google Fonts ✓
Cormorant         → Google Fonts ✓ (Cormorant:wght@400;700)
Cardo             → Google Fonts ✓
Quattrocento      → Google Fonts ✓
```

#### Transitional Serif（過渡襯線）
```
Libre Caslon Text → Google Fonts ✓
Libre Baskerville → Google Fonts ✓
```

#### Modern Serif（現代/新古典襯線）
```
Libre Bodoni      → Google Fonts ✓ (Libre+Bodoni:wght@400;700)
GFS Didot         → Google Fonts ✓
Bodoni Moda       → Google Fonts ✓
Vidaloka          → Google Fonts ✓
Old Standard TT   → Google Fonts ✓
```

#### Slab Serif（平板襯線）
```
Aleo              → Google Fonts ✓
Roboto Slab       → Google Fonts ✓
Arvo              → Google Fonts ✓
Bevan             → Google Fonts ✓
Alfa Slab One     → Google Fonts ✓
Hepta Slab        → Google Fonts ✓
```

#### Script & Calligraphic（書寫/書法）
```
Pacifico          → Google Fonts ✓
Sacramento        → Google Fonts ✓
Lobster           → Google Fonts ✓
Oleo Script       → Google Fonts ✓
Yellow Tail       → Google Fonts ✓ (Yellowtail)
Dancing Script    → Google Fonts ✓
```

#### Handwritten（手寫）
```
Caveat            → Google Fonts ✓
Gochi Hand        → Google Fonts ✓
Gloria Hallelujah → Google Fonts ✓
Itim              → Google Fonts ✓
Patrick Hand      → Google Fonts ✓
```

#### Brush（筆刷）
```
Caveat Brush      → 非 Google，gFont: null
```

#### Blackletter（哥特字）
```
UnifrakturMaguntia → Google Fonts ✓
```

#### Elegant Display（質感標題）
```
Cinzel            → Google Fonts ✓
Italiana          → Google Fonts ✓
Philosopher       → Google Fonts ✓
Bona Nova         → Google Fonts ✓
Cormorant Garamond → Google Fonts ✓
```

#### Poster & Art Deco（海報/裝飾）
```
Poiret One        → Google Fonts ✓  ← 已在 Geometric，可雙重標記或擇一
Abril Fatface     → Google Fonts ✓
```

---

### Step 4：篩選 UI 改為語言導向

在 `index.html` 的 `#view-fonts` 篩選列，改成：

```
[語言切換] 中文  英文

選「中文」時顯示：全部 | 黑體 | 明體 | 圓體 | 手寫 | 毛筆 | 楷體 | 特色
選「英文」時顯示：全部 | Grotesk | Humanist | Geometric | Serif | Slab | Script | Brush | Display
```

JS 邏輯：`_dbLangFilter` 新變數，`renderFontDB()` 根據 lang filter 決定顯示哪些字型和哪些 type 按鈕。

---

### Step 5：Lazy Load（效能優化）

目前 `_loadGFont()` 是渲染時直接插入 `<link>`，font 增加後會一次發大量請求。

改用 `IntersectionObserver` 讓卡片進入視窗才載入：

```js
const _fontObserver = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      const gParam = entry.target.dataset.gfont;
      if (gParam) _loadGFont(gParam);
      _fontObserver.unobserve(entry.target);
    }
  });
}, { rootMargin: '200px' });
```

每張卡片的預覽 div 加上 `data-gfont="${font.gFont}"` 並 observe，而不是在 render 時直接 `_loadGFont()`。

---

### Step 6（選做）：改 AI 搜尋為「風格描述 → 推薦字體」

目前搜尋 prompt 是「找與 X 字體相似的字體」。

可以改成支援兩種輸入：
- 輸入字體名稱 → 找相似（現有行為）
- 輸入風格描述（如「復古海報感」「乾淨現代」）→ 推薦 DB 內的字型

修改 `searchSimilarFonts()` 的 prompt，讓 Claude 判斷輸入是字體名還是風格描述，並在後者情況下優先推薦 FONT_DB 內有的字型名稱。

---

## 注意事項

- DB 卡片目前**沒有加入收藏按鈕**（已故意移除），只有 AI 搜尋結果才有書籤按鈕
- 收藏的字型會出現在右欄最上方（青色邊框），篩選條件同時作用
- `appData.fontCollection` 存在 JSONBin，key: `$2a$10$TxsupRh7kHjCZb3VceR.xehsu2Ff0jG3.nz.c5mi4F67I9Z5qacmy`，bin: `69eedda0856a68218977c12e`
- 密碼保護用 SHA-256 hash，不要動到

---

## 建議執行順序

1. Step 5（Lazy Load）— 先做，避免加字型後變慢
2. Step 1 + 2（擴充資料結構）
3. Step 3（加英文字型，可分批）
4. Step 4（改篩選 UI）
5. Step 6（選做，AI 風格搜尋）
