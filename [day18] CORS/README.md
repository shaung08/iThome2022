# [day18] CORS
### Cross-Origin Resource Sharing (CORS)
跨域資源共享( CORS ) 是一種基於HTTP標頭的機制，它允許服務器指示除其自身之外的任何來源（域、方案或端口），瀏覽器應允許從中加載資源，因為安全機制瀏覽器只被允許從同一來源request的到後端資料，如需加載不同來源的後端需使用cors去跨域請求。

假設假設web(https://foo.example)希望調用後端(https://bar.other)，今天前端發送get請求到後端，其實際發送內容如下，origin表示請求來源。
```
GET /resources/public-data/ HTTP/1.1
Host: bar.other
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.14; rv:71.0) Gecko/20100101 Firefox/71.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-us,en;q=0.5
Accept-Encoding: gzip,deflate
Connection: keep-alive
Origin: https://foo.example
```

後端接到請求返回response回去內容如下，其中`Access-Control-Allow-Origin: *`表示允許前端來自任何來源，也可以設定`Access-Control-Allow-Origin: https://foo.example`來指定前端網域
```
HTTP/1.1 200 OK
Date: Mon, 01 Dec 2008 00:23:53 GMT
Server: Apache/2
Access-Control-Allow-Origin: *
Keep-Alive: timeout=2, max=100
Connection: Keep-Alive
Transfer-Encoding: chunked
Content-Type: application/xml
```


## 參考
* https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS