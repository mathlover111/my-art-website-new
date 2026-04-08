# my-art-website-new
這是我目前開發的最終版本，也是我投入最多心思進行邏輯優化與功能整合的作品。本版本成功解決了前幾個版本的技術痛點，並實作了完整的內容管理系統 (CMS)。

最終版核心功能 (v4.0)

1.雲端新增/刪除畫作：實現了「免動程式碼」即可更新作品集的功能。管理員可直接透過控制台輸入圖片連結，系統會即時渲染至前台。

2.資源上限控制 (Resource Throttling)：加入邏輯判斷，限制作品上限為 10 張。這展現了我對資料庫負載與網頁效能的考量。

3.改用 .on("value") 監聽模式，解決了刪除圖片後畫面無法即時同步的 Bug，提升了使用者體驗的流暢度。

4.在介面上隱藏控制台，更在 addImage() 函式中加入 currentUser === adminID 的邏輯檢查，確保系統安全性。

📈 開發演進歷程
為了磨練技術，我將開發過程分為四個階段，每一階段都克服了不同的技術門檻：
【第一版至第三版：失敗與嘗試的養分】
[點此查看v1.0 ~ v2.0](https://github.com/mathlover111/my-art-website)

v1.0 (Local Storage)：解決資料重整後流失的問題。
v2.0 (Firebase 串接)：突破本地儲存限制，實現雲端資料同步。
v3.0 (身份驗證版)：導入 Google OAuth 與管理員權限邏輯。

前端：HTML5, CSS3 (Transition, Flexbox), JavaScript (Vanilla ES6)
後端服務：Firebase Realtime Database, Firebase Authentication
部署：GitHub Pages

針對使用者實測回饋，我進行了兩大關鍵的技術調整： 

1. 圖片縮放 
問題描述：原先圖片固定寬度，導致在手機端瀏覽時，圖片會超出螢幕範圍。

解決方案：導入 CSS Media Queries 與 Viewport Units (vw)。

2. 異步監聽優化：解決刪除後登入失效問題
問題描述：舊版本在刪除留言後會執行 location.reload()，強制重新整理導致使用者的 Google 登入狀態暫時遺失。

解決方案：

捨棄重整網頁，改用 Firebase 的 .on("child_removed") 監聽器。

透過 JavaScript DOM 操作 (element.remove()) 直接從前端移除該則留言節點。

成果：在刪除內容的同時，使用者能維持穩定的登入狀態，大幅提升操作流暢度。
