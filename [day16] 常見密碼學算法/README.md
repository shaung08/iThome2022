# [day16] 常見密碼學算法
以下列出密碼學中常見的算法
## 雜湊演算法 (Hashing)
雜湊演算法是不可逆的，數據再經過雜湊演算法過程中會遺失資訊，用於驗證資料的正確性。

## 現今已被破解的密碼演算法
### md5 (message-digest algorithm 5)
md5使用雜湊演算法，可以將字串、檔案、壓縮包轉成一串128bit。
特性:
* 在進行演算法過程中是單向的，意即被加密後無法被還原
* 相同的輸入必定得到相同的輸出
* 輸入內容即使相似，輸出也會差異非常大

用途: 常被用來當作檔案的校驗碼或是不需要被還原的資料，針對相同帳密輸入，會去比對經由md5算法出來後的結果，相同字串則讓使用者登入，但因為輸出輸入輸出固定，因此利用比對生成輸出結果(2^69)是可以被暴力破解的。

### SHA-1 (Secure Hash Algorithm 1)
由上面md5長度增加到160bit，長度越長越不容易被破解，但SHA-1與md5現今在使用上都已經都不安全。

## 尚安全的密碼演算法
### SHA-2
SHA-1算法加強版，為了解決SHA-1算法被破解而產生，SHA-2有可以生成兩種形式，SHA-256與SHA-512分別可以產生256bit與512bit，為現今被大量使用的算法
### SHA-3
為了預防SHA-2被破解，因此SHA-3用了與上述兩種不同的全新的算法去做加密
### scrypt
scrypt是一種密碼衍生演算法，使用scrypt演算法來衍生key，其過程中需要使用到大量的記憶體，scrypt演算法主要為預防暴力破解攻擊

### bcrypt
bcrypt使用雜湊演算法，其生成的出來的結果都不一樣，就算相同輸入，輸出的結果都會不一樣，因此如果要使用密碼比對，生成出來的hash值要再經由bcrypt算法提供函數去比對。

## 參考
* https://blog.m157q.tw/posts/2017/12/25/differences-between-encryption-and-hashing/
* https://www.796t.com/content/1547468467.html
* https://www.gushiciku.cn/pl/pcHM/zh-tw
* https://ithelp.ithome.com.tw/articles/10293822?sc=rss.qu
* https://ithelp.ithome.com.tw/articles/10294539?sc=iThelpR
* https://iter01.com/631161.html
* https://ithelp.ithome.com.tw/articles/10196477