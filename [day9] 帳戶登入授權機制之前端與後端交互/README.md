# [day9] 帳戶登入授權機制之前端與後端交互
### cookie authorization
在運用cookie情況下，使用者在登入伺服器後，伺服器會在後端生成一串unique的token，並且回傳給使用者，使用者在每次發送request給後端時cookie都會帶token一起發送到後端，後端會根據token返回權限，以下將介紹user登入後端運用cookie生成token的過程為何。
![](https://i.imgur.com/AMNaMHP.png)

1. 使用者發出request給後端要求註冊帳號
2. 後端將密碼透過hash加密，並且儲存於database
3. 使用者在發出登入request給後端要求登入
4. 後端會在透過hash加密使用者密碼後比對database裡帳戶資訊，如果相同則升成一串token儲存於database並且返回cookie給前端，此token會帶有效時限
5. 此後前端發出每個request都會帶著cookie資訊給後端，如果token過期，比對token失敗後則會拒絕訪問

### JWT(JSON Web Token)介紹
為restapi的其中一種架構機制，在使用者透過JWT對後端請求資源，後端會驗證此JWT的資訊是否有效返回對應內容給前端。
JWT由三個部分所組成Header、Payload、Signature所組成
* Header: 通常由演算法加密，Token類型所組成的JSON，之後會在經由Base64 URL編碼
* Payload: 放置要傳給後端的資料
* Signature: Header(base64後)、Payload(base64後)、secret

### OAuth2.0
OAuth2.0為使用第三方授權登入應用程式，此時應用程式從第三方業者取得基本用戶資料，使用者就不需要使用帳密登入伺服器，假設今天進入hackmd透過google帳號登入，詳細流程後面會介紹，這裡先介紹OAuth2.0常見名詞
* Resource Owner: 這裡指使用者，指擁有決定給予權限與否的使用者
* Resource Server: 這裡擁有帳戶資訊的伺服器端，如上述google
* Client: 指第三方應用程式如上述hackmd
* Authorization Server: 驗證Resource Owner身分，同意後會發放token給第三方伺服器，並同意使用者的登入

![](https://i.imgur.com/UDT8OHd.png)

1. 首先點擊Client登入會導到Authorization Server，使用者可以選擇要授權給Client的資訊，常見如: Client Id、Redirect URI、Response Type、Scope
2. Authorization Server進行身分驗證後，會根據剛剛設定的scope，確認是否同意授權，會明確標示要授權的資訊，如:名稱、email等等
3. 同意授權後會導向Redirect URI，並且將token以及相關資訊透過前面設定的Response Type回覆Authorization grant給使用者
4. Client端獲得Authorization grant後，會拿著他再向Authorization Server要求token，Authorization Server會在此驗證資訊以及Client身分後核發token
5. 最終使用者帶著此token向Client發送request，此時Client也只會取得使用者授權的資訊

### OpenID
上面提到的OAuth2.0只有提供登入授權，OIDC(OpenID Connection)目的是認證（Authentication），OAuth2.0目的則是授權（Authorization），並擴充了在OAuth2.0不足的機制
* ID Token：認證所需的用戶資訊，這是 OIDC 最重要的擴充。不要和 OAuth 2.0 的 Access Token 攪混了，Access Token 是用於授權，不帶有用戶資訊來做認證。
* UserInfo Endpoint：除了上面 ID Token 提供基本用戶資訊，OIDC 還規定認證提供者應提供一個 API 界面，讓 Client 能取的更完整的用戶資訊。
* Standard Set of Scopes：OAuth 2.0 沒有定義 scope（忘記這是什麼了嗎？先回去看一下前一篇文章吧！），造成 Facebook 可能有 Facebook 的 scope，Google 有 Google 的 scope，實做的時候必須參閱各家的手冊客製化。OIDC 規範了共通的 scope 讓大家有規可循。詳細規範可以參考文件。

![](https://i.imgur.com/hbUO4KJ.png)
流程圖將 OIDC 變動的部份醒目標示。第一個變化是第 2 步在要求 Authorization Code 的時候，scope 新增了 openid 值。

第二個不一樣的地方，是第 8 步在換 Access Token 的時候，除了取得 Access Token，還取得了 ID Token。這是因為前面的scope 有指定 openid ，讓 Client 有取得 ID Token 的權限。

最後的差異是第 10 步。先前 OAuth 2.0 的流程在取得授權後是去存取用戶持有的資源（用戶的照片、文件等等），但 OIDC 的目的是認證。這邊是從 OIDC UserInfo Endpoint 取得認證所需的用戶資訊，來完成註冊的流程。

### SALM
SALM透過http傳送經由base64編碼過後的xml文件，其中會包含使用者的認證(Authentication)與授權(Authorization)相關的資訊，其好處為保密性更高，其概念如同上述儲存在cookie authorization機制，因此詳細內如探討實作。

![](https://i.imgur.com/m5ow0a6.png)

* https://medium.com/%E9%BA%A5%E5%85%8B%E7%9A%84%E5%8D%8A%E8%B7%AF%E5%87%BA%E5%AE%B6%E7%AD%86%E8%A8%98/%E7%AD%86%E8%A8%98-%E8%AA%8D%E8%AD%98-oauth-2-0-%E4%B8%80%E6%AC%A1%E4%BA%86%E8%A7%A3%E5%90%84%E8%A7%92%E8%89%B2-%E5%90%84%E9%A1%9E%E5%9E%8B%E6%B5%81%E7%A8%8B%E7%9A%84%E5%B7%AE%E7%95%B0-c42da83a6015
* https://mgleon08.github.io/blog/2018/07/16/jwt/
* https://ithelp.ithome.com.tw/articles/10264580
* https://medium.com/%E4%BC%81%E9%B5%9D%E4%B9%9F%E6%87%82%E7%A8%8B%E5%BC%8F%E8%A8%AD%E8%A8%88/jwt-json-web-token-%E5%8E%9F%E7%90%86%E4%BB%8B%E7%B4%B9-74abfafad7ba
* https://5xruby.tw/posts/what-is-jwt
* https://medium.com/@henry-chou/%E8%88%87%E4%BC%81%E6%A5%AD%E6%95%B4%E5%90%88%E9%A9%97%E8%AD%89%E7%B3%BB%E7%B5%B1-saml-%E9%A9%97%E8%AD%89-1c5dc32a17cd
