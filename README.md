# AI-Perxona-website-prototype

LiamZ 的作品集網站 — 單一 HTML 檔，無建置步驟。

## 檔案

- `index.html` — 整個網站。CSS 與 JS 全部 inline，直接用瀏覽器打開就能看。
- `.claude/skills/web-quick-builder/` — 產生這個網站的 Claude Skill。之後要改版時它會自動載入同一套約束（視覺系統、無障礙、SEO、文案規則）。

## 上線順序（不能顛倒）

Perxona 的 embed code 要**先有網址才拿得到** —— 後台 STEP 3 會要你填上線網域，API Key 綁死在那個網域上。所以：

1. repo 轉 public，並改名為 `zolic0112.github.io`
2. Settings → Pages → Source 選 `Deploy from a branch`，分支選 `main`、資料夾 `/ (root)`
3. 等一分鐘，確認 `https://zolic0112.github.io/` 打得開
4. Perxona 後台：發布 → Web Embed Code → 網域填 `zolic0112.github.io` → Create
5. 複製 embed code，貼進 `index.html`（見下一節），再 push 一次

**網域一定要跟實際網址完全一致**，差一個字元 avatar 就載不出來。改名成 `zolic0112.github.io` 就是為了讓網址剛好等於後台要的格式，不會有專案頁路徑的問題。

## 活動當天：接上 Perxona avatar

`index.html` 裡搜尋 `PERXONA MOUNT POINT`，把 `<p class="avatar-pending">` 那行換成 Perxona 的嵌入碼。

- 嵌入碼如果是 `<script>` 而且要指定容器，容器 id 是 `perxona-mount`
- 如果是 `<iframe>`，直接貼進去就好，CSS 已經會把 iframe 撐滿整張卡

保留外層 `.c-avatar` 卡片與 `id="avatar"`，版面和導覽列連結才不會跑掉。

角色的人格設定在 `persona/`，那是給 Perxona 後台用的，跟這裡的嵌入無關。

## 還要填的佔位內容

`index.html` 中所有 `[方括號]` 都是待填欄位：三個作品的年份／角色／標題／說明、目前在做什麼、關於段落、所在城市。圖片是 CSS 幾何佔位，換成真圖時記得加 `loading="lazy"` 與 `width`／`height`。
