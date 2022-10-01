# [day 23] 搜索引擎工具
### Elasticsearch 
Elasticsearch 是一個分散式的搜索引擎，假設今天要搜索有關 dogs的貼文，一般使用關鍵是自料搜索會像`select * from posts WHERE content LIKE %dog%;`，但如果是使用dog關鍵次則無法被上述查詢找到，因此就出現了Elasticsearch的關鍵字搜索引擎，
Elasticsearch使用invert index用來儲存文字到文件映射關係，其資料結構類似map，例如:
1. this is a dog.
2. this is a cay.

invert index其資料結構如下:
|key|value|
|---|---|
|this|1, 2|
|is|1, 2|
|a|1, 2|
|dog|1|
|cat|2|

因此今天如果要建立搜索引擎可以使用此Elasticsearch去建置，但其需要花時間去建置其搜索引擎

### Solr 
Solr是基於Lucene的流行、高效能的開源企業級搜尋平臺，其也是用來建置搜索平台工具

Solr與Elasticsearch簡易比較
* Elasticsearch: 
1. 分散式系統，某些節點出現故障時會自動分配其他節點代替其進行工作
2. 由於其易用性而在較新的開發人員中更受歡迎
3. 用來處理分析查詢以及搜索文本是更好的選擇
* solr: 
1. 有一個更大、更成熟的使用者、開發和貢獻者社群，相較穩定。

## 參考 
* https://iter01.com/503555.html
* https://www.cnblogs.com/gezifeiyang/p/10999238.html
* https://www.twblogs.net/a/5da94108bd9eee310d9fc356
* https://medium.com/happy-friday/elasticsearch-%E5%85%A8%E6%96%87%E5%AD%97%E6%90%9C%E5%B0%8B%E5%BC%95%E6%93%8E-%E5%9F%BA%E6%9C%AC%E6%A6%82%E5%BF%B5%E4%BB%8B%E7%B4%B9-f38a0cab9717
* https://www.51cto.com/article/701897.html