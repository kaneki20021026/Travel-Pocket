# Cheap.com 樣式規範與視覺驗收（2026-11-20）

## 共用規範
以首頁液態玻璃為基準。index.html 的 --cheap-* 變數是共用外觀來源。
- 主色 --cheap-ink: #173e62；主要按鈕白字、深藍背景。
- 次要文字 --cheap-muted: #526e86；日期 --cheap-date-color: #6385a4。
- 日期 metadata: 12px / 500；頁面標題 20px / 800；區塊標題 --cheap-text-heading: 15px；內容 --cheap-text-body: 14px；輔助文字 --cheap-text-small: 12px。
- 玻璃表面、邊框、陰影用 --cheap-glass、--cheap-inner、--cheap-edge、--cheap-shadow、--cheap-inner-shadow。
- 一般表單欄位高 44px；文字 14px。日期外框 44px，內部原生日期欄 42px。保留原生日期選擇器及兩欄等寬排列。
- Disclosure 使用 icon('chevron')，20px、stroke 1.8、深藍；向下代表收合，向上代表展開。
- 刪除操作用 --cheap-danger；不可套成主要操作藍。
- 導航、時間數字、日期選擇 chips、緊湊工具按鈕保留各自語意尺寸。

## 維護要求
新增頁面優先重用 .glass、.btn / .btn.primary、表單及現有圖示。
不要另寫相近色碼或再追加一套頁面主題。先修改既有規則；只為佈局或明確狀態增加局部樣式。
避免在 :is() 中混入額外 ID 的 :has() 分支，令整組規則無意提升 specificity。
本次移除 412 項被相同 selector 後續宣告覆蓋的頂層屬性；媒體查詢、業務邏輯、儲存資料及日期自動對齊邏輯未改動。
本次並非把所有歷史 CSS 全部重寫；往後仍須按元件維護及驗收。

## 已實際檢查
在本機隔離來源、預設示範資料，以瀏覽器操作及截圖檢查：
- 390px：其他頁、航班設定展開、收據、每日行程、附近頁、設定收合。
- 320px：行程管理、地點新增表單、旅行清單展開、四個分類可見、連結管理、酒店表單、導航偏好、匯率計算機展開。
- 768px：首頁置中及主要卡片。
- 首頁今日行程與航班日期 computed style 均為 12px / 500 / rgb(99,133,164)。
- 航班編號欄 44px；日期框內欄 42px；航班設定及備份主要按鈕背景 rgb(23,62,98)。
- 匯率箭嘴 computed stroke 1.8px，顏色 rgb(23,62,98)；320px 收據頁 document scrollWidth 與視窗同為 320px。
- 兩個 inline scripts 通過語法解析，CSS 大括號配對，無 token 自我循環；最後一次載入未捕獲 console error。

## 尚未驗證
實體 iPhone Safari / 加入主畫面安全區、鍵盤彈出及原生日期選擇器；定位後地圖、天氣與航班 API；相機及照片上傳、備份匯入匯出；多於六日的日期自動捲動與長按排序。這些不列作本次通過項目。
