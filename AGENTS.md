# 技術部落格

## 專案簡介

Hexo + NexT 主題的技術部落格，使用 GitHub Pages 部署。內容涵蓋前端與後端開發。

## 資料夾結構

```
/
├── _config.yml          # Hexo 主設定（站名、網址、主題）
├── _config.next.yml     # NexT 主題設定覆蓋
├── .env.example         # 環境變數範本
├── .github/workflows/   # GitHub Actions CI/CD
│   └── deploy.yml       # 自動建置+部署到 GitHub Pages
├── scaffolds/           # 文章樣板
│   ├── post.md
│   ├── page.md
│   └── draft.md
├── source/
│   ├── _posts/          # 部落格文章 (Markdown)
│   └── (其他頁面)
├── themes/              # 主題目錄
├── package.json
└── AGENTS.md
```

## 常用指令

| 指令 | 說明 |
|------|------|
| `npm run server` | 啟動本地開發伺服器 (http://localhost:4000) |
| `npm run build` | 產生靜態檔案 (public/) |
| `npm run clean` | 清除快取與 public/ |
| `npm run deploy` | 手動部署 (若有設定 deploy) |

## 建立新文章

```bash
npx hexo new "文章標題"
npx hexo new draft "草稿標題"     # 建立草稿
npx hexo publish "草稿標題"       # 發布草稿
```

## 環境變數

敏感資訊（API Key、第三方服務 token）請使用環境變數管理：

1. 複製 `.env.example` 為 `.env`
2. 填入實際值（`.env` 已列入 `.gitignore`，不會上傳）
3. CI/CD 流程中可在 GitHub Repo Settings > Secrets and variables 設定

## 部署流程

- 推送 `main` 分支 → GitHub Actions 自動執行 `npm run build` → 上傳 `public/` 至 GitHub Pages
- 需在 GitHub Repo Settings > Pages 中設定 Source 為 **GitHub Actions**

## 同步對照表

| 本地路徑 | Obsidian 筆記 | 說明 |
|----------|---------------|------|
| `source/_posts/` | `技術部落格/文章/` | 部落格文章 |
| `source/_drafts/` | `技術部落格/草稿/` | 草稿 |
