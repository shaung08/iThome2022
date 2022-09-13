# [day6] Git version control
## Gitlab 架設
使用gitlab去做版本控制，以下介紹如何架設gitlab
### 使用 docker compose 架設 gitlab
環境須先下載好 docker 和 docker-compse componenet
### 先 pull gitlab docker image
```
$ docker pull gitlab/gitlab-ce:latest
```
使用 docker-compose 的方式去執行 container 啟動 gitlab，Web protocol 為 http://10.101.6.80:80
#### docker-compose.yml
```
version: "3.3"
services:
  gitlab:
    image: gitlab/gitlab-ce:latest
    shm_size: '8gb'
    restart: always
    hostname: 'gitlab.example.com'
    environment:
      GITLAB_OMNIBUS_CONFIG: |
        external_url 'http://10.101.6.80'
    ports:
      - '80:80'
      - '443:443'
      - '24:22'
    volumes:
      - '~/gitlab01/data:/var/opt/gitlab'
      - '~/gitlab01/logs:/var/log/gitlab'
      - '~/gitlab01/config:/etc/gitlab'

```


```
$ docker-compose up -d
```

等到 container 狀態為 healthy 即可以登入 gitlab
![](https://i.imgur.com/FNtDOaG.png)

## gitlabe 備份設定
### gitlab 內部定期備份設定

修改 backup_path 至想要儲存的位置，並重新 reconfigure 設定
```
$ nano /etc/gitlab/gitlab.rb
$ gitlab-ctl reconfigure
```

![](https://i.imgur.com/7d1V0fN.png)

### 使用 rclone 將 onedrive service 與本地端綁定

#### install rclone
```
$ curl https://rclone.org/install.sh | sudo bash install.sh  #rclone on Linux/macOS/BSD systems
```

#### config rclone
配置 rclone 並依序執行 process，如果沒有 GUI 可以先在 windows 端下載 rclone，並且follow [generate onedrive access key](#生成-onedrive-access-key)，如果 server 有 GUI 可以直接跳至 [config rclone](#config-rclone)

##### generate onedrive access key
windows端先下載rclone並且解壓縮，在 cmd 進入 rclone 目錄執行以下 command，執行完畢後會跳出 mocrosoft 登入視窗，登入完畢後 cmd 會生成 onedrive access key
```
$ rclone authorize "onedrive"
```

#### config rclone
執行以下 command 開始 config 設定
```
$ rclone config
```

```
n) New remote
s) Set configuration password
q) Quit config
n/s/q> n
name> onedrive
Type of storage to configure.
Enter a string value. Press Enter for the default ("").
Choose a number from below, or type in your own value
 1 / 1Fichier
   \ "fichier"
 2 / Alias for an existing remote
   \ "alias"
 3 / Amazon Drive
   \ "amazon cloud drive"
 4 / Amazon S3 Compliant Storage Provider (AWS, Alibaba, Ceph, Digital Ocean, Dreamhost, IBM COS, Minio, etc)
   \ "s3"
 5 / Backblaze B2
   \ "b2"
 6 / Box
   \ "box"
 7 / Cache a remote
   \ "cache"
 8 / Dropbox
   \ "dropbox"
 9 / Encrypt/Decrypt a remote
   \ "crypt"
10 / FPT Connection
   \ "fpt"
11 / Google Cloud Storage (this is not Google Drive)
   \ "google cloud storage"
12 / Google Drive
   \ "drive"
13 / Google Photos
   \ "google photos"
14 / Hubic
   \ "hubic"
15 / JottaCloud
   \ "jottacloud"
16 / Koofr
   \ "koofr"
17 / Local Disk
   \ "local"
18 / Mega
   \ "mega"
19 / Microsoft Azure Blob Storage
   \ "azureblob"
20 / Microsoft OneDrive
   \ "onedrive"
21 / OpenDrive
   \ "opendrive"
22 / Openstack Swift (Rackspace Cloud Files, Memset Memstore, OVH)
   \ "swift"
23 / Pcloud
   \ "pcloud"
24 / Put.io
   \ "putio"
25 / QingCloud Object Storage
   \ "qingstor"
26 / SSH/SFTP Connection
   \ "sftp"
27 / Union merges the contents of several remotes
   \ "union"
28 / Webdav
   \ "webdav"
29 / Yandex Disk
   \ "yandex"
30 / http Connection
   \ "http"
31 / premiumize.me
   \ "premiumizeme"
Storage> 20
** See help for onedrive backend at: https://rclone.org/onedrive/ **

Microsoft App Client Id
Leave blank normally.
Enter a string value. Press Enter for the default ("").
client_id>      #press enter
Microsoft App Client Secret
Leave blank normally.
Enter a string value. Press Enter for the default ("").
client_secret>      #press enter
Edit advanced config? (y/n)
y) Yes
n) No
y/n> n
Remote config
Use auto config?
 * Say Y if not sure
 * Say N if you are working on a remote or headless machine
y) Yes
n) No
y/n> n
For this to work, you will need rclone available on a machine that has a web browser available.
Execute the following on your machine (same rclone version recommended):
	rclone authorize "onedrive"
Then paste the result below:
result>      # 將生成的 onedrive access key 貼在這
Choose a number from below, or type in an existing value
 1 / OneDrive Personal or Business
   \ "onedrive"
 2 / Root Sharepoint site
   \ "sharepoint"
 3 / Type in driveID
   \ "driveid"
 4 / Type in SiteID
   \ "siteid"
 5 / Search a Sharepoint site
   \ "search"
Your choice> 1
Found 1 drives, please select the one you want to use:
0: OneDrive (business) id=
Chose drive to use:> 0  #choose your onedrive path
Found drive 'root' of type 'business', URL:
Is that okay?
y) Yes
n) No
y/n> y
--------------------
[rc]
type = onedrive
token = {"access_token":"auth","expiry":"2022-07-22T16:33:33.456212+08:00"}
drive_id =
drive_type = business
--------------------
y) Yes this is OK
e) Edit this remote
d) Delete this remote
y/e/d> y
Current remotes:

Name                 Type
====                 ====
onedrive             onedrive

e) Edit existing remote
n) New remote
d) Delete remote
r) Rename remote
c) Copy remote
s) Set configuration password
q) Quit config
e/n/d/r/c/s/q> q     # q退出，配置完成
```


### 使用 crontab 定時備份

修改 crontab 定期排成
```
$ crontab -e
```
![](https://i.imgur.com/eAbcySm.png)

**`baskup.sh`**
![](https://i.imgur.com/OsbyKN5.png)

#### restart crontab
```
$ /etc/init.d/cron reload
$ service cron restart
```
最後完成每日 gitlab 定期備份並且將 backup 檔案備份到 Microsoft onedrive storage 上
## Git Commnad

### 上傳到 master
```
$ git init
$ git add <filename>
$ git commit -m <description>
$ git push -u origin
```
### 上傳到 branch
```
$ git init
$ git add <filename>
$ git commit -m <description>
$ git checkout -b <branch>
$ git push -u origin <branch>
```

### 查看目前分支

```
$ git status
```

### 建立一個新的分支

```
$ git checkout -b <branch>
```

### 查看所有分支

```
$ git branch --all
```

### 查看遠端分支

```
$ git branch -r
```

### 從本地推上遠端分支 (遠端沒有分支情況下)

remote add 綁上遠端分支 5g-use-case 組織底下 ai_platform fold
```
$ cd <folder>
$ git init
$ git add .
$ git commit -m <description>
$ git remote add origin http://10.101.6.80/5g-use-case/ai_platform.git
$ git push -u origin master
```

![](https://i.imgur.com/GODUJkh.png)

## gitlab備份還原

### 備份 gitlab 
```
$ /usr/bin/gitlab-rake gitlab:backup:create
```
備份資料會儲存於 `/var/opt/gitlab/backups/<backup_time>_gitlab_backup.tar`
![](https://i.imgur.com/36iyBSs.png)

### 還原 gitlab 

先停止會用到 shema 資料庫的servive，之後將備份資料用於 rollback ，之後再啟動先前停止的  service
```
$ gitlab-ctl stop unicorn
$ gitlab-ctl stop sidekiq
$ cd /var/opt/gitlab/backups
$ gitlab-rake gitlab:backup:restore BACKUP=<backup_time>
$ gitlab-ctl start unicorn
$ gitlab-ctl start sidekiq
```


## 參考
* https://www.gushiciku.cn/pl/gOey/zh-tw
* https://blog.csdn.net/rdp1305442102/article/details/105768441
* https://cloud.tencent.com/developer/article/1936298
* https://blog.gtwang.org/linux/linux-crontab-cron-job-tutorial-and-examples/
* https://ithelp.ithome.com.tw/articles/10280309
* https://www.twblogs.net/a/5c820077bd9eee35cd6984cb
* https://www.gushiciku.cn/pl/pGvF/zh-tw
* https://ithelp.ithome.com.tw/articles/10211148
* https://www.796t.com/article.php?id=68796
