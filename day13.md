## Day 13 : 首先把鍋燒熱

### DNS 設定

有了 `IP` 、 `網域` 、 `憑證` 這些材料之後，

還需要把菜切一切，把肉給醃一醃，

以 Google Domain 為例需要先將 Domain 綁定到 IP 上，

先到 Google Domain 網站上新增一筆 A 紀錄，

設定如下圖範例所示：

![](https://i.imgur.com/ojtdhSb.png)

每次的變更設定可能會根據不同國家地區，

稍微等待過一定時間後才會生效。

### Proxy Server

接下來就要來把這三者炒在一起變成一鍋好菜，

在這之前需要了解一下 Proxy 是什麼，

一般大眾聽到要掛 Proxy 來當跳板通常是指 `正向代理` ，

就是有好多的使用者都連到 Proxy 伺服器，

然後因為這台伺服器可能位在不同國家，

所以經由這台 Proxy 送出的請求就會是使用該國家的 IP，

![](https://i.imgur.com/ihxemoR.jpg)

而我們今天要使用的是 `反向代理` ，

恰好是反過來由伺服器根據請求分配給好多的伺服器，

可以根據不同的需求對應到適合的應用，

![](https://i.imgur.com/pRLM1BH.jpg)

### 使用 NginX 做代理吧

以 NginX 為例可下載已封裝好的 `Zip` 安裝包，

> [http://nginx.org/](http://nginx.org/)

安裝流程請參考網路上相關教學，

因 `express-generator` 預設產生的伺服器框架採用了 `Port 3000` ，

對外則需使用 `SSL` 連線並使用 `Port 443` 來做 `https` 的連線，

並且需要加入 `certificate` 設定 `bundle` 的憑證 與 `私鑰`，

所以 `NginX` 的 `nginx.conf` 可以設定如下，

```conf
server {
        listen       443 ssl;
        server_name  qqboxy.com;

        ssl_certificate      C:/nginx/certs/qqboxy_com.bundle.crt;
        ssl_certificate_key  C:/nginx/certs/qqboxy_com.key;

        ssl_session_cache    shared:SSL:1m;
        ssl_session_timeout  5m;

        ssl_ciphers  HIGH:!aNULL:!MD5;
        ssl_prefer_server_ciphers  on;

        location / {
            proxy_pass http://localhost:3000;
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection 'upgrade';
            proxy_set_header Host $host;
            proxy_cache_bypass $http_upgrade;
        }
    }
```

完成後外部的請求都會從 `Port 443` 反向代理至 `Local` 端的 `Port 3000` ，

然後啟動 Node.js Server 後就可以在網域上看到自己的網站囉。