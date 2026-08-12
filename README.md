# AI-Perxona-website-prototype

LiamZ 的作品集網站 — 單一 HTML 檔，無建置步驟。

## 檔案

- `index.html` — 整個網站。CSS 與 JS 全部 inline，直接用瀏覽器打開就能看。
- `.claude/skills/web-quick-builder/` — 產生這個網站的 Claude Skill。之後要改版時它會自動載入同一套約束（視覺系統、無障礙、SEO、文案規則）。

## 部署（GitHub Pages）

Settings → Pages → Source 選 `Deploy from a branch`，分支選這個 branch、資料夾選 `/ (root)`，存檔後約一分鐘就會有網址。

上線後記得把 `index.html` 裡兩處 `https://example.com/` 換成真實網址（`<link rel="canonical">` 與 `og:url`），JSON-LD 裡的 `url` 也一起換。

## 活動當天：接上 Perxona avatar

`index.html` 裡搜尋 `PERXONA MOUNT POINT`，把 `<p class="avatar-pending">` 那行換成 Perxona 的嵌入碼。

- 嵌入碼如果是 `<script>` 而且要指定容器，容器 id 是 `perxona-mount`
- 如果是 `<iframe>`，直接貼進去就好，CSS 已經會把 iframe 撐滿整張卡

保留外層 `.c-avatar` 卡片與 `id="avatar"`，版面和導覽列連結才不會跑掉。

角色的人格設定在 `persona/`，那是給 Perxona 後台用的，跟這裡的嵌入無關。

## 還要填的佔位內容

`index.html` 中所有 `[方括號]` 都是待填欄位：三個作品的年份／角色／標題／說明、目前在做什麼、關於段落、所在城市。圖片是 CSS 幾何佔位，換成真圖時記得加 `loading="lazy"` 與 `width`／`height`。
