# [day15] web資安問題
### HTTPS (Hyper Text Transfer Protocol Secure)
最初http協議被設計來進行web與server之間進行通進，但http在現今的網路上運行並不安全，容易被第三方竊取資料或是安插廣告等等，
其明顯缺點為在http協議裡，所有的資料都是經由明文的方式去做傳輸，因為http本身不具備加密的功能，就算今天自己寫加密方法，仍有機會被破解，再加上沒有使用SSL/TLS進行加密，不會驗證web與server雙方的身分，只要收到request都會回復出去

### Open Web Application Security Project(OWASP)
開放網路軟體安全計畫，OWASP是一個非營利性組織，主要協助解決網路軟體安全之標準，以下列出10個網站安全風險
1. Broken Access Control (權限控制失效): 帳號管理權限未設定為預期權限，如果沒有預設帳號訪問權限，會導致駭客可以透過漏洞進入企業系統查看、修改、洩露、刪除其他帳號和管理員的數據。
2. Cryptographic Failures (加密機制失效): 手動加密方式很容易被破解，因此選用SSL/TLS等等受信任的方式進行加密
3. Injection (注入式攻擊): injection 包括SQL injection、跨站點腳本 (XSS)、模板注入、XPath injection、電子郵件標頭注入、shell injection等等。
解決方案: 盡量不要採用密碼登入，通過行動 OTP、生物識別身份驗證、下拉式選項和使用第三方支付平台來取代，或是使用 Web 應用程式防火牆 (WAF)、或是第三方產品來解決。
4. Insecure Design (不安全設計): 例如前100位登入網站給予商品免費服務，可能被駭客切換ip方式給拿走。
5. Security Misconfiguration (安全設定缺陷): 安全設定缺陷最常見原因是系統管理員沒有更改預設配置，或者他們在打開系統進行測試後忘記重新關閉系統。因此企業需應禁用所有預設的不必要功能、特權和權限斗等
6. Vulnerable and Outdated Components (危險或過舊的元件): 使用危險或過舊的元件是指網路中的元件包含了未修補已知漏洞的情況。
7. Identification and Authentication Failures (認證及驗證機制失效): 採用行動 OTP 和生物識別等高級身份驗證技術，這些技術都有助防禦社交攻擊。
8. Software and Data Integrity Failures (軟體及資料完整性失效): 軟體及資料完整性失效是由於缺乏資料完整性驗證過程而使用篡改或損壞的資料做出某些決定的狀況。例如，駭客使用惡意軟體去破壞軟體更新文件，而應用程式會自動安裝更新，而無需驗證文件是否為原始文件。這是影響全球數萬組織SolarWinds供應鏈攻擊事件的主要原因。
9. Security Logging and Monitoring Failures (資安記錄及監控失效): 資安記錄及監控失效描述了入侵監控和report系統未能捕獲和寫入駭客入侵的跡象。
10. Server-Side Request Forgery (伺服端請求偽造): 當網頁應用程式正在取得遠端資源，卻未驗證由使用者提供的網址，此時就會發生偽造伺服端請求。

參考以下網址
[https://owasp.org/www-project-top-ten/](https://owasp.org/www-project-top-ten/)

### Content Security Policy(CSP)
CSP提供網站進行白名單設置，網站會告知伺服器那些ip位址可以連線，那些需要block掉，現在大部分瀏覽器都有支援CSP，因此在使用上CSP用來避免資安問題可參考[https://devco.re/blog/2014/04/08/security-issues-of-http-headers-2-content-security-policy/](https://devco.re/blog/2014/04/08/security-issues-of-http-headers-2-content-security-policy/)

CSP header設置有兩種方式:
1. HTTP Header 加入 Content-Security-Policy: {Policy}
當有不符合安全政策的情況，瀏覽器就會提報錯誤， 並終止該行為執行。
2. HTTP Header 加入 Content-Security-Policy-Report-Only: {Policy}
當有不符合安全政策的情況，瀏覽器就會提報錯誤， 但會繼續執行 。


## 參考
* https://docfunc.com/posts/48/%E5%B9%AB%E7%B6%B2%E7%AB%99%E6%8E%9B%E4%B8%8A-https%E4%BD%BF%E7%94%A8-certbot-%E5%90%91-lets-encrypt-%E7%94%B3%E8%AB%8B%E6%86%91%E8%AD%89-post
* https://www.heminfosec.com/eDM/2021-10-OWASPtop10-2021-WAPPLES-OSCAN.html
* https://owasp.org/www-project-top-ten
* https://ithelp.ithome.com.tw/articles/10196896
* https://devco.re/blog/2014/04/08/security-issues-of-http-headers-2-content-security-policy/