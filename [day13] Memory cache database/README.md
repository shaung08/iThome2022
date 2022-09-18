# [day13] Memory cache database

### Redis
Redis為nosql，其資料讀寫在Ram Memory上實行，因此執行速度比一般資料庫快許多，是Key-Value類型資料庫，其提供非常多種類型格式(string, hash, list, set)，通常與關聯式資料庫搭配，再某些情況下當系統大量的使用者湧入，可以將使用者多次query的資料儲存在Redis上，利用其特性使用ram快速讀取，可以大幅加快使用者使用體驗，並且避免系統多次查找disk，導致系統效能緩慢導致當機

### Memcached
Memcached也是使用將資料儲存在ram memory上的技術以達成系統快速查找的功能，是key-Value類型資料庫，其使用情形同Redis，都是通過ram memory快速查找來提升使用者體驗，與Redis詳細比較如下

### 比較Memcached和Redis
#### Memcached優點:
* 在multi thread上執行更有效率
* 提供使用者簡易資料(圖片、音檔)的快速讀寫

#### Redis優點:
* 在系統掛掉時數據可以修復
* 在ram memory不夠時，會通過演算法將資料移動至disk上永久保存，因此可以儲存大於ram memory大小數據
* 可儲存較複雜的資料結構

### CDN (Content delivery network)
CDN服務用途為在使用者與origin server中間間接一個緩存伺服器，優點為在使用者request資料時，透過緩存伺服器可以快速響應使用者資料(如果緩存有使用者需要的資料)，並且可以隱藏實際origin server的ip位址，並且中間層去過濾並阻擋駭客入侵威脅

![](https://i.imgur.com/K9O4abV.png)
圖片來源來自[https://www.apeiro8.com/what-is-cdn/](https://www.apeiro8.com/what-is-cdn/)

## 參考
* https://blog.techbridge.cc/2016/06/18/redis-introduction/
* https://tw.alphacamp.co/blog/memcached-memory-cache-optimize-performance
* https://blog.csdn.net/shmnh/article/details/53409783
* https://www.apeiro8.com/what-is-cdn/
