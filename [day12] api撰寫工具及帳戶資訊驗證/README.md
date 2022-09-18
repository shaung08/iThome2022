# [day12] api撰寫工具及帳戶資訊驗證機制
### Open api
open api為定義在restful api文件端口撰寫的格式，現在最多人使用的為swagger工具，其使用方法為撰寫yaml file去生成前端的api request，在撰寫完成後，swagger也提供直接在網頁去測試。

### Authorization
前端與後端常見的帳戶驗證機制
#### SSO (Single Sign On)
SSO最常見的例子就是google帳戶，用戶登入google帳戶後，在各個google服務間都可以通用同一個帳戶而不需重複建立帳號，在相同網域下通常可以使用cookie去使用同一個token登入，但是當服務在不同網域時，可以使用proxy代理來將相同token代入將不同網域，不過當服務多時就必須使用相對應不同的策略去實現多網域登入，例如使用:OpenID Connect, Facebook Connect, SAML, Microsoft Account等等

下圖流程為多網域之間共享token方法。
![](https://i.imgur.com/ZHj8xoD.png)

接下來藉由流程圖可以了解大致上帳戶驗證的運作原理，大部分都在在前面介紹過，詳細可以看[day 9]介紹
#### OAuth
![](https://i.imgur.com/oB9Zvjc.jpg)

#### JWT
![](https://i.imgur.com/p7249kK.jpg)

#### Token Based Authentication
![](https://i.imgur.com/gbjW20W.jpg)

#### Session Based Authentication
![](https://i.imgur.com/svFLJtN.jpg)

#### Based Authentication
![](https://i.imgur.com/AMCUpsy.png)


## 參考
* https://roadmap.sh/guides/sso.png
* https://roadmap.sh/guides/oauth.png
* https://roadmap.sh/guides/jwt-authentication
* https://roadmap.sh/guides/token-authentication
* https://roadmap.sh/guides/session-authentication
* https://roadmap.sh/guides/basic-authentication