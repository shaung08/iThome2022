# day3 DNS介紹
### DNS簡介
DNS可以將網域轉換為ip位址，例如將`www.example.com`轉為10.85.85.10，DNS Server大致分為四個部分

* DNS resolver: DNS後端查找第一站，作後DNS後端中間人，用來查找DNS所在ip
* Root nameserver: 查找儲存根網域(`.com`, `.net`)的table，告訴DNS resolver要再去哪個server進一步查找
* TLD nameserver: 假設到達儲存網域(`.com`)ip table的server，會以疊代方式開始查詢example.com table，返回Authoritative nameserver位址
* Authoritative nameserver: 最後一站，經過網域查找返回ip位址

![](https://i.imgur.com/0wfS3MZ.png)

#### DNS record
在Authoritativer裡，DNS紀錄四種訊息，如下列所述:
* A record: 裡面存放ip4的位址
* CNAME record: 將網域mapping到另一個網域，例如`www.example01.com`指向`www.google.com`，這樣在更改`www.google.com`網域的ip時，`www.example01.com`也會自動更新成最新的ip，像是c++裡的指標概念
* AAAA record: 裡面存放ipv6的位址
* MX record: 記錄自己server的ip位址，讓其他的server可以來查找資料

## 參考
* https://www.cloudflare.com/en-gb/learning/dns/what-is-dns/
* https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_domain_name
* https://www.cloudflare.com/en-gb/learning/dns/glossary/what-is-a-domain-name/
* https://www.pcnet.idv.tw/pcnet/network/network_ip_dns.htm
