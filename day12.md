## Day 12 : 申請網域名稱

### 申請固定 IP

申請網域前需要做好一些前置動作，

包括一開始申請 `固定IP` 以及後續的 `網域憑證` 都是重要的一環，

以 HINET 為例可以直接到網頁申請 `固定IP` ：

> [http://service.hinet.net/2004/adslstaticip.php](http://service.hinet.net/2004/adslstaticip.php)

向 HINET 申請後會根據不同網速方案有不同數量的 IP 配發如圖所示：

![](https://i.imgur.com/2rjhenW.jpg)

接著只要 `PPPoE` 登入的帳號名稱增加一個 `ip` 改成

> 8(7)xxxxxxx@`ip.`hinet.net

如此連線後 IP 就會變成固定的了，

如果想要一開機就自動連線，

要記得設定一下伺服器啟動後進行 PPPoE 自動連線，

這部分可以參考一下網路上眾多的文章。

### 網域名稱的重要性

取得固定 IP 之後就可以開始來申請網域了，

這部分我的方案是直接購買喜歡的網域，

可至 GoDaddy 、 Google Domain 等平台付費申請來用，

有些便宜的網域一年也僅需要 10 美元，

GoDaddy:

> [https://www.godaddy.com/](https://www.godaddy.com/)

Google Domain:

> [https://domains.google/](https://domains.google/)

一方面經營自己的網域也是一種提升自我能見度的方法，

當然如果妳是免費仔的話也是可以自行找尋免費網域。

### 申請憑證

如果覺得申請免費憑證很麻煩，

同樣可以至 `Comodo` 等平台購入付費的憑證來使用，

便宜的 SSL 憑證一年也僅需 6 美元，

> [https://comodosslstore.com/](https://comodosslstore.com/)

或是使用 `Let's Encrypt` 的免費憑證，

搭配 `Certbot` 自動在到期前自動續約，

> [https://certbot.eff.org/](https://certbot.eff.org/)

這部分在網路上同樣有許多相關的教學資源，

鐵人賽也有不少網友分享更詳細的內容，

本系列僅提供關鍵字給大家參考。