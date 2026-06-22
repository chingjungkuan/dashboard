# Lucy's Dashboard — 開發規範

## 專案概述
個人 Dashboard PWA，vanilla HTML/CSS/JS，無框架依賴。
資料同步：JSONBin.io + localStorage。

---

## Design System

參考基準：**Tailwind CSS token 命名規範 + shadcn/ui 語意色彩命名**

所有 token 定義在 `css/style.css` 的 `:root` 區塊。

### Color Tokens

| Token | 值 | 用途 |
|---|---|---|
| `--color-bg` | `#070709` | 頁面背景 |
| `--color-surface` | `rgba(20,20,25,0.4)` | 卡片、面板背景 |
| `--color-surface-hover` | `rgba(30,30,40,0.6)` | 卡片 hover 狀態 |
| `--color-overlay` | `rgba(18,18,24,0.98)` | Modal、Drawer 背景 |
| `--color-input` | `rgba(255,255,255,0.04)` | 輸入框背景 |
| `--color-primary` | `#00F0FF` | 主要操作色（青色） |
| `--color-secondary` | `#7000FF` | 次要操作色（紫色） |
| `--color-destructive` | `#FF0055` | 危險操作（刪除、警示） |
| `--color-active` | `#063F64` | 日曆打卡填色 |
| `--color-success` | `#34d399` | 成功狀態 |
| `--color-warning` | `#fbbf24` | 警告狀態 |
| `--color-foreground` | `#FFFFFF` | 主要文字 |
| `--color-muted-foreground` | `#8A8A93` | 輔助文字、label |
| `--color-border` | `rgba(255,255,255,0.08)` | 邊框 |
| `--color-border-hover` | `rgba(255,255,255,0.15)` | 邊框 hover |

### Spacing Scale（Tailwind 4px base）

| Token | 值 | 常見用途 |
|---|---|---|
| `--spacing-1` | `4px` | icon gap、細小間距 |
| `--spacing-2` | `8px` | chip padding、小間距 |
| `--spacing-3` | `12px` | badge padding |
| `--spacing-4` | `16px` | 基礎間距 |
| `--spacing-5` | `20px` | section gap |
| `--spacing-6` | `24px` | modal padding |
| `--spacing-8` | `32px` | card padding |
| `--spacing-12` | `48px` | page margin |
| `--spacing-16` | `64px` | 大區塊間距 |

### Typography Scale

| Token | 值 | 用途 |
|---|---|---|
| `--font-size-xs` | `0.75rem / 12px` | badge、caption |
| `--font-size-sm` | `0.8125rem / 13px` | label、link、meta |
| `--font-size-base` | `1rem / 16px` | body、input |
| `--font-size-lg` | `1.125rem / 18px` | modal title |
| `--font-size-xl` | `1.25rem / 20px` | section heading |
| `--font-size-2xl` | `1.75rem / 28px` | page title |
| `--font-size-3xl` | `2rem / 32px` | category title |

Font family：`Inter`（body）、`Outfit`（heading/card title）、`Poppins`（dashboard title）

### Border Radius

| Token | 值 | 用途 |
|---|---|---|
| `--radius-sm` | `8px` | button、badge、toggle |
| `--radius-md` | `10px` | input、small card |
| `--radius-lg` | `16px` | avatar |
| `--radius-xl` | `20px` | card、modal（預設） |
| `--radius-full` | `9999px` | chip、switch |

---

## 開發規範

### 顏色使用
- **新增或修改樣式時，一律使用 `--color-*` token**，不要直接寫色碼
- 舊的 `--text-muted`、`--accent-cyan` 等為 legacy alias，仍可用但不要再新增
- 漸層直接用 `--gradient-brand`（青→紫）或 `--gradient-progress`

### Spacing 使用
- 優先使用 `--spacing-*` token
- 允許使用 `rem` 直接對應（例如 `1.5rem` = `--spacing-6`）
- 避免使用奇數 px 值（7px、11px 等）

### 新增元件規則
1. 顏色用 token
2. 圓角優先用 `--radius-*`
3. 間距參考 spacing scale
4. 互動 hover/active 狀態要定義

### 資料儲存
- 所有狀態存於 `appData` 物件
- 儲存：`saveState()` → JSONBin + localStorage 雙備份
- 讀取：session 啟動時從 JSONBin 拉取，fallback localStorage

### 模組架構
- 靜態模組：`gym`（健身房）
- 動態模組：`appData.customModules[]`（type: `gym` | `rental`）
- 口袋名單：`appData.pocketList[]`（type: `food` | `sight`）

---

## 檔案結構
```
/
├── index.html        # 主檔案（所有 HTML + JS）
├── css/
│   └── style.css     # 所有樣式（含 DS tokens）
├── js/
│   └── lucide.min.js # Icon library
└── CLAUDE.md         # 本文件
```

---

*最後更新：2026-06-22*
