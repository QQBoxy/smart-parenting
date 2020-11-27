## Day 25 : 架設 HA 伺服器

### 架設方法

談到要架設 HA 可能又有人要打退堂鼓了，

但其實官方都已經包好很簡單的安裝方法，

所以快回來坐好安裝屬於妳的 HA 伺服器吧，

官方推薦的安裝方法主要有兩種：

1. 使用 Raspberry Pi 4 Model B

2. 使用 Docker 容器

這兩種推薦的安裝方式也都很容易，

不過第一種方法必須要先購入一塊樹莓派，

通常包含電源與透明殼等弄到好大概需要台幣 2000 元左右，

但我們系列已經請大家建立自己的伺服器了，

自然也就考慮使用第二個方法 Docker 來安裝即可，

就不用額外再花一筆小錢來購置硬體了。

### 安裝 Docker

首先要安裝 `Docker` 前必須先打開虛擬化功能，

這部分請搭配不同主機板的說明書來找到選項，

通常是到 `BIOS` 找到 `Virtualization` 選項將它 `Enable`，

啟用後就可以回到 `Windows` 設定來啟用 `Hyper-V` ，

> 應用程式與功能 > 程式和功能 > 開啟或關閉 `Windows` 功能 > `Hyper-V`

![](https://i.imgur.com/eX7JoUT.png)

如果妳是家用版的使用者可能無法啟用 `Hyper-V` 功能，

妳也可以參考 Docker 官方網站的做法：

[https://docs.docker.com/docker-for-windows/install-windows-home/](https://docs.docker.com/docker-for-windows/install-windows-home/)

或是使用參考筆者部落格紀錄的方法：

[https://blog.qqboxy.com/2020/09/windows-10-hyper-v.html](https://blog.qqboxy.com/2020/09/windows-10-hyper-v.html)

歷經了這麼辛苦的過程後，

終於可以來安裝我們的 `Docker` 了，

這部分安裝就非常的簡單一直下一步就可以了：

[https://www.docker.com/](https://www.docker.com/)

### 安裝 Home Assistant

如果妳看得懂英文也可以參考官方網站的安裝手冊，

[https://www.home-assistant.io/docs/installation/docker/](https://www.home-assistant.io/docs/installation/docker/)

其實安裝 `HA` 只要一行指令而已，

但要記得先稍微修改一下指令內容以符合自己的需求：

```shell=
docker run --init -d --name="home-assistant" -e "TZ=Asia/Taipei" -v /c/config:/config -p 8123:8123 homeassistant/home-assistant:stable
```

稍微說明一下 -v 這個語法是指路徑對應的意思，

這個語法由冒號分為前後兩段的部分，

前半段 `/c/config` 是指要存放設定檔的路徑，

對應原本的 `Windows` 路徑就是 `C:\config` ，

這個目錄是妳可以自訂自行創建喜歡的名稱，

後半段是 `Docker` 內的設定檔路徑就是 `/config` ，

這個 `config` 目錄的路徑通常是不會變動的，

它是用來存放 `HA` 的設定檔，

設定好後它就會將 `Docker` 內的設定映射到 `Windows` 目錄內，

執行完指令後就可以正常啟動 `Docker` 版本的 `HA` ，

最後打開瀏覽器輸入網址就可以看到 `HA` 的介面了：

> http://localhost:8123