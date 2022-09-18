# [day10] 常見傳輸協定
### json api
http在資料傳送上最常使用為rest api格式為使用json formjat來跟後端交互

### SOAP（Simple Object Access Protoco）
簡單物件訪問協議，是基於XML的協議，其包含四個部分

envelop: 定義訊息內容，傳送端以及目的地
encoding rules: 定義傳送資料type
RPC representation: 定義遠端屋較以及應答協定
binding: 定義底層協定(TCP/UDP/HTTP)

##### soap基本訊息格式
```
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
soap:encodingStyle="http://www.w3.org/2003/05/soap-encoding">
<soap:Header>
<!-- 訊息頭，可選 -->
</soap:Header>
<soap:Body>
<!-- 訊息內容，必需 -->
<soap:Fault>
<!-- 錯誤資訊，可選 -->
</soap:Fault>
</soap:Body>
</soap:Envelope>
```

### gRPC
gRPC底層是由http/2.0所組成，其在傳輸過程中會透過protobuf編碼，傳輸的資料量小於restful api，因此當後端有大量服務需要交換資料時，使用gRPC可以有效解決速度慢的問題，實際使用時，gRPC會如同在call function，然後return值回來，因此設計上也比restful api簡單許多，但須注意其仍是經由網路溝通傳輸資料。

gRPC有三種模式
* 單向傳輸: 只發送一次訊息即關閉通道
* 單向串流: client發出一個request後，server可以發出多個response直到另外把通道關閉
* 雙向串流: client可以不同發出多個request後，server也可以發出多個response直到另外把通道關閉

## 參考
* https://ithelp.ithome.com.tw/articles/10242947
* https://pjchender.dev/golang/grpc-getting-started/
* https://www.w3schools.com/xml/xml_soap.asp