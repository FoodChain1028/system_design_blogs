# Web protocol

1. 瀏覽器發送一個 HTTP 請求到伺服器
2. 伺服器收到請求，生成一個 HTML Document
3. 伺服器將 HTML Document 作為 HTTP 的 payload 回傳給伺服器
4. 瀏覽器收到 HTTP 回應，從 HTTP 的 Body 中解析出 HTML Document 並顯示在瀏覽器上

HTTP Protocol 包含了什麼？

1. Start Line (POST / HTTP/1.1)
2. Header: 其中包含 `status code`、`content type`、`content length` 等等
3. Blank Line
4. Body

面試的時候：

1. 做需求的探索（Requirement）
    - functional requirement: 用戶可以...
    - non-functional requirement: 系統需要...
2. 做一個 high-level 的架構設計
3. 接下來再做深入設計 (deep dive)

## Functional Requirement

例如在開發一個 Twitter 時，用戶應該要可以：

1. 發送推文
2. 看到推文

這邊可以分類成兩類：

- Data Flow in: 其實就是 writing into database
- Data Flow out: 其實就是 reading from database

Data Flow in:

1. Upload a video/image
2. Post a post/article

Data Flow out:

1. Watch the video
2. Read the post/article

## Non-Functional Requirement

這個部分比較在乎系統的負載、性能、可擴充、可靠性還有安全性等等。

1. Scalability: 系統需要可以擴充，例如 Database
2. Latency: 使用者可以忍受的延遲時間
3. Availability: 可用性，例如在網頁商品展示時，不能讓圖片沒辦法跑出，使用者就會看不到商品。
4. Consistency: 一致性，例如在下訂單時，因為需要避免重複下單則需要有一致性
5. Reliability: 系統需要有高的可靠性，不能說用到一半突然伺服器掛掉完全無法使用
6. Fault Tolerance: 系統需要有高的容錯性，不能說用到一半突然伺服器掛掉完全無法使用

通常這個時候會問一些經典的問題：

1. 這個系統的 DAU (Daily Active User) 有多少？
2. 這個系統用戶可以容忍延遲性會是多少？
3. 這個系統對於寫入的 QPS (Queries Per Second) 有多少？
4. 這個系統對於讀取的 QPS (Queries Per Second) 有多少？
5. 這個系統的可用性或一致性哪個比較重要？

---

## Scaling

在 System Design 中可以在乎的擴充性：

1. Data partitioning/sharding: 將資料庫分成多個小資料庫，例如可以用 `user_id` 去 mod N 來決定放在哪一個 data shard
2. Function partitioning: 將不同的功能放在不同的 Service 上。例如將 post 和 read 分開成兩個 service
3. Replications: 將資料庫複製多份，例如可以做成 master-slave 架構。由一個 master 負責全部的寫入，其他的 slave 會負責複製 master 的資料供讀取。
