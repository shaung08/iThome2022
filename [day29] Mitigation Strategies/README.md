# [day29] Mitigation Strategies
### uwsgi
python套件中用來管理後端service的套件，在django中直接使用runserver的話預設會使用wsgi tool去開啟後端service。
uwsgi其支援graceful reload的功能，為開發者在修改代碼後重啟uwsgi service，不會中斷後端正在運行中的管道，等到後端管道全部執行完畢後，才會重啟服務。

#### 使用方式
先下載uwsgi tool
```
$ pip3 install uwsgi
```
在django的project下新增`uwsgi.ini`檔案，裡面寫入
```
# deploy it on HTTP port 10010
[uwsgi]
http = :10010　 #serve protocol
module = visual_inference_sdk_backend.wsgi:application  #the front is django folder name
master = True
processes = 1
threads = 1
vacuum = True
pidfile = /tmp/dj3-master.pid
master-fifo = /tmp/uwsgi_api.fifo
lazy-apps = true  #graceful restart lazy-apps mode
```
使用下列commamd去執行django service服務
```
$ uwsgi --ini uwsgi.ini
```

用下列command去重啟django
```
$ echo c > /tmp/uwsgi_api.fifo
```

### Throttle 
情境為在前端中當使用者連續觸發同個function，會導致後端服務重複接收資訊，因此在前端function的內容中加入計時器功能，紀錄最後一次執行此function的時間，下一次執行時就去相減避免在一定時間內重複執行數次function，例如: leetcode的run test以及submit都有此機制


## 參考
* https://blog.wu-boy.com/2020/02/what-is-graceful-shutdown-in-golang/
* https://medium.com/@alexian853/debounce-throttle-%E9%82%A3%E4%BA%9B%E5%89%8D%E7%AB%AF%E9%96%8B%E7%99%BC%E6%87%89%E8%A9%B2%E8%A6%81%E7%9F%A5%E9%81%93%E7%9A%84%E5%B0%8F%E4%BA%8B-%E4%B8%80-76a73a8cbc39
* https://www.cnblogs.com/AcAc-t/p/uWSGI_graceful_reload.html
* https://uwsgi-docs-zh.readthedocs.io/zh_CN/latest/articles/TheArtOfGracefulReloading.html