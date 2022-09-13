# [day7] Database與backend結合以及常見問題解析
### ORM(Object-Relational Mapping)
ORM在網站開發結構中在設計用來幫助更容易去取得資料庫資料，其特性為用程式語言來取得sql資料

優點: 可以迅速開發、代碼轉移方便、防止Sql Injection攻擊
缺點: 比其直接使用sql語法效能較差

#### SQL Injection
假設要登入一個網站，再輸入帳密後後台直接使用sql語法的話會執行下列command查詢
`select * from members where account='$name' and password='$password'`
但如果此時駭客使用特殊字符帳號`or 1=1 /*`，這時sql語法會變成如下
`select * from members where account='' or 1=1 /*' and password=''`
因為`/*`在sql語法裡為註解意思，所以後面都不會被執行此時判斷式1=1會成立因此會導致網站可以登入

### ACID Compliance
資料庫在處理資料時，會需要遵從transaction，
例如:銀行金融系統，A要轉帳給B，假設今天A帳戶已經扣掉金額，但在B帳戶新增金額時處理錯誤，會導致金額消失，因此ACID主要在定義database中容易出現上述問題的情形

* Atomicity 原子性: 保持操作的完整性，要馬成功要馬都失敗
* Consistency 一致性: 像上述例子，會定義`1.交易金額不得小於0`、`2.雙方金額加總一樣`，在處理前處理後都必須遵守此規則為一致性
* Isolation 隔離性: 多個數據之間處理不會互相干擾，且不能修改到同一個值，假設A帳戶有300元，同時要轉給兩個人各100元，因此轉出後應該剩300元，但如果兩個thread同時讀值讀到原始值500元，轉出後金額會剩下400元有誤。
* Durability 持久性: Server關機、斷電，資料庫都要能保持完整

### transaction
transaction主要在保證資料庫在處理資料時不會發生上述ACID情況，數據庫在執行時包括以下幾種狀態
* Active states: 當資料庫讀寫被執行時會在此階段
* Partially committed: 一部分資料庫被commit但還沒完全變動完畢
* Committed: 所有資料都被更新完畢會進入此狀態
* Failed: 當資料庫更新或請求遭到終止會進入Failed狀態
* Terminated: 當所有狀態執行結束(包含Committed、Terminated)後會進入最終狀態Terminated
![](https://i.imgur.com/gnOxWQ3.png)

### N+1 problem 
當程序要查詢id=125的query時，在sql裡會逐行去查詢，因此假設query裡有N列，包括一開始打開table表，會執行N+1次，因此在使用table表時可以先將所有的database直接load進程式後再做處理，詳細使用需參考各個tool ORM的使用方式，sql語法主要使用到in語法，django可以使用以下工具檢測N+1 problem [nplusone](https://github.com/jmcarp/nplusone)


### 參考
* https://ithelp.ithome.com.tw/articles/10207752
* https://www.puritys.me/docs-blog/article-11-SQL-Injection-%E5%B8%B8%E8%A6%8B%E7%9A%84%E9%A7%AD%E5%AE%A2%E6%94%BB%E6%93%8A%E6%96%B9%E5%BC%8F.html
* https://lance.coderbridge.io/2021/04/24/short-what-is-acid/
* https://hung-x0x0.medium.com/orm-n-1-problem-c98e39b9c96
* https://medium.com/doctolib/understanding-and-fixing-n-1-query-30623109fe89
