# [day26] Websocket
### Websocket
websocket的優短為在一段連線建立後，這段連線會持續存在直到主動將通道關閉，在通道存在期間client和server可以持續互相傳輸data。

![](https://i.imgur.com/xFLLqJj.png)
websocket的一些狀態簡介
* url: `ws://`未經過加密，`wss://`為經過加密
* readyState: 
    * 0: 表示連線尚未建立
    * 1: 連線已建立，可以開始進行通訊
    * 2: 連線正在關閉
    * 3: 連線已經關閉或連結異常不能開啟
* bufferedAmount: client端要給server訊息會被丟入send序列中，即為message在序列中尚未發出
* onopen: 通道建立成功後會觸發
* onerror: 通訊發生錯誤時會觸發
* onclose: 通道關閉時會觸發
* onmessage: 收到server message時觸發
* binaryType: 支援string、blob、array buffer



## 參考
* https://www.letswrite.tw/websocket/
