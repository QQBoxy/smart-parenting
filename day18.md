## Day 18 : 寶寶影像監控

### 寶寶的安全

父母都很在乎寶寶的安全，

有些意外往往就發生在一個沒注意，

我就曾經夢到寶寶發生意外而嚇醒，

還好這一切只是在夢境中，

若是真的發生了到時要後悔都來不及，

為了避免這類憾事與意外的發生，

有些人就購買寶寶智慧監視產品來隨時注意寶寶的狀況，

但也有人想省點錢所以像筆者一樣自己來搭建囉。

### 遠端影像監控

前面有教大家使用 `NginX` 建立反向代理，

也知道一個 `Proxy` 背後可以代理多個伺服器，

那麼今天就來增加一個影像監控伺服器吧，

首先筆者使用的是這一套非商用免費的 `IP Camera Adapter` ：

[https://ip-webcam.appspot.com/](https://ip-webcam.appspot.com/)

這套工具採用的是 `MJPG` 影像，

介面上看起來也相當陽春，

但僅僅是為了監控來說已經綽綽有餘，

首先到 `Play商店` 將 `APP` 安裝起來，

[https://play.google.com/store/apps/details?id=com.pas.webcam](https://play.google.com/store/apps/details?id=com.pas.webcam)

然後連上中華電信的 `Wifi` 使其與 `Proxy` 伺服器處於同一個內部網路，

打開 `IP Webcam` 滑到最下方執行 `Start Server` ，

妳也可以先設定帳號密碼來避免有心人士看到，

![](https://i.imgur.com/5nPwSou.jpg)

然後就會看到伺服器啟動了，

![](https://i.imgur.com/9HcPf1k.jpg)

目前連線路徑為 `https://192.168.1.107:8080` 每個人可能都不同，

這個 `虛擬IP` 其實還是有機會變動的，

如果要確保不會變動的話，

麻煩自行查詢並設定妳的無線 `AP` ，

由於 `NginX Server` 已經可以透過 `固定IP` 對接到外部網路，

為了要讓 `IP Camera` 可以順利在外部網路運作，

需要在 `Proxy Server` 內做一些設定，

```conf
# IP Camera SSL 設定
server {
    listen       443 ssl;
    server_name  webcam.qqboxy.com;

    location / {
        proxy_pass http://192.168.1.107:8080;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

如此一來就可以將 `IP Camera` 交給 `Proxy` 代理，

最後再到 `DNS` 代管加上 `CNAME` 紀錄，

![](https://i.imgur.com/rt5zMxf.png)

就可以透過指定的子網域進行遠端監控了，

這套工具只要打開瀏覽器就可以運作囉！

![](https://i.imgur.com/q8tzV1C.png)

筆者每次將孩子哄睡後都會架好遠端監控，

再到遠得要命的廚房開始洗奶瓶跟食器，

或是到更遙遠的後陽台洗衣服晾衣服，

有了遠端監控真的可以非常放心的處理各種事務，

再也不用擔心沒有聽到孩子醒來在心疼的哭哭了。