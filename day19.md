## Day 19 : 嵌入式系統

### 開發板

大家具備了網路應用程式的能力之後，

也學會一些可以活用及實用的方法，

那麼接下來就要進入硬體的部分了，

其中最重要的莫過於 `嵌入式系統` 了，

早期這一塊技術其實是難以輕鬆入門的，

因為需要單晶片都是獨立的需要自行焊接，

還要具備一定的電子電路知識來串接電晶體做放大電路，

但是現代技術的進步讓我們不再需要花大量時間在開發，

坊間有了各式各樣的開發板供客官自行挑選，

其中筆者使用的是 `Arduino` 這塊開發板，

原因在於它行之有年擁有大量的技術資源，

對於新手來說容易在網路上查詢文獻得到問題的解決。

### Arduino

`Arduino` 是一個易於使用的軟硬體開發平台，

它可以透過 `感測器` 、 `按鈕` 等讀取與輸入訊號，

於是你可以撰寫程式來發送指令給微控制器，

系統就會輸出訊號來驅動 `燈號` 、 `伺服機` 等元件，

市面上也有各種模組化的元件讓你省去處理電路的時間，

而 Arduino 現在價格也是相對的便宜，

可以根據使用的需求購買不同的版本來使用，

官方也提供了一個簡單的 IDE 供撰寫與燒錄程式。

### 開發環境

筆者會在安裝後改用 VSCode 的擴充套件來開發，

因為相關的套件更多因此可以更方便撰寫程式，

所以首先到官方網站下載 IDE 來安裝：

[https://www.arduino.cc/en/Main/Software](https://www.arduino.cc/en/Main/Software)

接著在 VSCode 安裝擴充套件：

[https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino)

安裝後就可以在右下角設定燒錄器與開發板型號：

![](https://i.imgur.com/dLt257g.png)

建立好環境後是不是想趕緊買一塊 Arduino 來試試看了呢?

建議可以先買一片大概 200 元的副廠 Arduino Nano 來用，

再買一塊小片的麵包板就可以開始遊玩囉。

![](https://i.imgur.com/X7p99S5.jpg)