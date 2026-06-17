# 維新網站部署完整資料

## 線上網址
**https://weishin-website.netlify.app**

## 本機網站資料
- 網站路徑：`/Users/user/AI/weishin/`
- 主要檔案：`index.html`

## GitHub
- 帳號：`jacqqq104-commits`（注意：`jacwu28` 是另一個不同帳號，不要搞混）
- Repo：https://github.com/jacqqq104-commits/weishin-website
- Branch：`main`

## SSH 設定（已設定好，不需重做）
- Key 路徑：`~/.ssh/id_ed25519_jacqqq104`
- SSH Config Host：`github-jacqqq104`
- Git remote：`git@github-jacqqq104:jacqqq104-commits/weishin-website.git`

## Netlify
- 網址：https://app.netlify.com
- 帳號：`jacqqq104-commits`（Jacqueline Wu）
- 專案：`weishin-website`，連結 GitHub repo，自動部署

---

## 更新並部署（每次改網頁後執行這個）

```bash
cd /Users/user/AI/weishin
git add .
git commit -m "更新網頁"
git push
```

Push 後 Netlify 自動部署，約 30 秒生效。不需要輸入密碼。
