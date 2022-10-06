# [day27] Graph Databases
## Native Graph Databases
與一般開發者常用關聯式資料差別為，在一般使用sql時，以main key(主鍵)來當作資料的唯一識別，再與其他表關聯時會使用join來將兩個表做介接，但Graph Databases在建立表與表關西時，已經將錶的相對關西以指針儲存在欄位，因此在查表使用上效能會比關聯式資料快速。

graph db有分為三大類
* Property Graphs: Neo4j 就是這一類，藉由許多的 nodes、relations、properties 所組合而成
* Hypergraphs: 和前者的差別在於，一個 relation 可以連接多個 nodes，很適合用於資料彼此有大量的「多對多」關係的情境
* Triple Stores: 使用 W3C 的 RDF（資源描述框架）

### neo4j
大數據時代來臨，當數據量龐大且數據關係複雜時，若使用傳統的 SQL 資料庫儲存需要大量的表格，花費大量的時間寫程式描述數據間的關係。
因此若遇到複雜關聯、龐大的資料，可以使用 Neo4j 開源的圖形數據庫 ( Graph DB ) 不但可以靈活存取也可以達到快速查詢的功能，使用上主要以`Node-節點`與`Relation-關係`與周圍建立關係。

![](https://i.imgur.com/Slz6D2h.png)


## 參考
* https://www.webcomm.com.tw/blog/neo4j/