# 🧪 思思實驗室 - sissi Lab

思思實驗室為你挑選生活好物 🔬✨

## 📋 專案介紹

思思實驗室是一個基於 Hugo 的靜態網站，專門提供好物推薦內容。透過詳細的研究分析和誠實的評價，幫助讀者找到最適合的生活好品。

### 網站特色

- 🧪 **專業研究**：每個推薦都經過嚴謹的分析
- 💖 **誠實推薦**：不掩飾產品弱點，不推薦劣質產品
- 💬 **親切分享**：用溫柔的語氣分享研究成果
- 🌟 **SEO 優化**：針對搜尋引擎優化，增加曝光

## 🚀 快速開始

### 前置需求

- [Hugo](https://gohugo.io/) 0.120.4 或更新版本
- Git
- GitHub 帳號（如需部署到 GitHub Pages）

### 本地開發

1. **克隆專案**
   ```bash
   git clone https://github.com/your-username/sisi_lab.git
   cd sisi_lab
   ```

2. **安裝依賴**
   ```bash
   hugo mod tidy
   ```

3. **啟動本地開發伺服器**
   ```bash
   hugo server -D
   ```

4. **瀏覽器開啟**
   ```bash
   http://localhost:1313
   ```

## 📁 專案結構

```
sisi_lab/
├── archetypes/          # 內容模板
├── content/             # 主要內容
│   ├── 3c-reviews/      # 科技產品類別
│   ├── home-living/     # 家居生活類別
│   ├── beauty/          # 美妝保養類別
│   ├── food/            # 食品推薦類別
│   ├── pets/            # 寵物用品類別
│   ├── fitness/         # 運動戶外類別
│   ├── clothing/        # 服飾穿搭類別
│   ├── about.md         # 關於頁面
│   └── disclaimer.md    # 免責聲明
├── layouts/             # 模板檔案
│   ├── _default/        # 預設模板
│   ├── partials/        # 部分模板
│   └── pages/           # 頁面模板
├── static/              # 靜態資源
│   ├── css/             # 樣式表
│   ├── js/              # JavaScript
│   └── images/          # 圖片資源
├── staging/             # 暫存區（內容審核）
├── .github/             # GitHub Actions
├── config.toml          # Hugo 設定檔
└── README.md            # 專案說明
```

## 📝 內容創作

### 新增文章

在對應的類別目錄下建立新的 Markdown 檔案：

```markdown
---
title: "2026年最值得入手的空氣炸鍋推薦"
date: 2026-03-31
description: "2026年最值得投資的空氣炸鍋推薦，思思為你詳細分析..."
categories: ["3c-reviews"]
tags: ["2026推薦", "空氣炸鍋", "CP值", "選購指南"]
featuredImage: "/images/2026/03/air-fryer.jpg"
momoLink: "https://www.momo.com.tw/product/..."
---

# 2026年最值得入手的空氣炸鍋推薦

思思今天要跟大家分享的是...
```

### 暫存區機制

所有由 Agent 生成的內容都會先儲存在 `staging/` 目錄中，等待用戶審核通過後才會部署到正式網站。

詳細工作流程請參考 `staging/README.md`。

## 🎨 客製化主題

### 修改顏色

在 `static/css/custom.css` 中修改 CSS 變數：

```css
:root {
  --primary-color: #ff6b81;
  --secondary-color: #feca57;
  /* ... */
}
```

### 修改設定

編輯 `config.toml` 檔案：

```toml
[params]
  description = "你的網站描述"
  author = "作者名稱"
  brandTagline = "你的標語"
  # ... 其他設定
```

## 🌐 部署到 GitHub Pages

### 自動部署

1. **推送到 GitHub**
   ```bash
   git add .
   git commit -m "主要描述"
   git push
   ```

2. **啟用 GitHub Pages**
   - 前往 GitHub Repository 的 Settings
   - 選擇 Pages
   - Source 選擇 GitHub Actions

### GitHub Actions 工作流程

專案已配置 `.github/workflows/hugo.yml`，會在每次推送到 main 分支時自動部署。

## 📱 本地測試

### 預覽網站

```bash
hugo server -D
```

### 建立生產版本

```bash
hugo --minify
```

生成檔案會輸出到 `public/` 目錄。

## 🔧 Hugo 指令參考

| 指令 | 說明 |
|------|------|
| `hugo server -D` | 啟動開發伺服器（包含草稿） |
| `hugo server -D --buildDrafts` | 建立並包含草稿 |
| `hugo new content/about.md` | 建立新內容 |
| `hugo` | 建立生產版本 |
| `hugo --minify` | 建立並壓縮版本 |

## 🧪 思思的語氣風格

所有內容創作都應遵循思思的語氣風格：

- **溫柔親切**：使用「～」語尾，展現親切感
- **熱情活潑**：使用驚嘆號，展現分享熱情
- **專業可靠**：分析時嚴謹，結論有依據
- **誠摯真實**：不美化缺點，誠實告訴大家

詳細內容創作指南請參考 `AGENT_CONTENT_GUIDE.md`。

## 📞 聯絡方式

- Email: {{ .Site.Params.email }}
- Instagram: {{ .Site.Params.instagram }}
- Threads: {{ .Site.Params.threads }}

## 📄 授權

本專案採用 MIT 授權條款。

## 🙏 致謝

感謝所有貢獻者和使用者的支持！

---

*思思實驗室 - 用心研究，為你挑選最適合的好物 🧪✨*
