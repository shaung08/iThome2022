# [day28] Web Server
web server存儲服務器軟件和網站組件文件（例如，HTML 文檔、圖像、CSS 樣式表和 JavaScript 文件）。Web 服務器連接到Internet並支持與連接到Web的其他設備進行物理數據交換。

### Nginx Server
nginx為常見的web server服務代理，其常見有兩種模式正向代理與反向代理。
* 正向代理: client端發request到proxy server，由proxy server向真正的伺服器要資料，此時伺服器並不知道client的真實位址，只會知道資料是由proxy server去訪問。
* 反向代理: client端發request到後端伺服器，此時後端會有load balancer去平衡server負載，此時前端不會知道後端真實伺服器位址為何。

### Apache server
apache service是常見Web server application，負責的工作是client和server之間的HTTP 通訊，但現今在使用上以nginx輕巧特色使用上為大宗。

### Caddy 
Caddy為新興的web server，其以go語言撰寫而成，其特色如下
* 支援自動從Let’s Encrypt取得與更新TLS 1.3加密憑證
* 以HTTPS作為預設的通訊協定
* 支援HTTP/3 (caddy v2)
* 支援IPv6
* 支援反向代理




## 參考
* https://medium.com/starbugs/web-server-nginx-1-cf5188459108
* https://mnya.tw/cc/word/1696.html
* https://editor.leonh.space/2022/caddy/