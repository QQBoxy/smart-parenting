## Day 22 : 第一支物聯網程式

### 育兒工具大集合

這一集先回頭來談談二十幾天來學到的技能，

一路到現在我們已經學習了很多育兒方法，

包含使用現成的 `智慧家庭裝置` ，

架設自己的伺服器來建立專屬 `網路育兒工具` ，

也學會使用 `Line Bot` 來建立育兒工具，

以及建立自己的 `嵌入式育兒裝置` 來協助育兒，

那麼後半段就要來建立自己的 `物聯網` 育兒程式了。

### 物聯網程式

其實 `Arduino` 除了可以經由燒錄後獨立運作以外，

也可以透過 `USB` 傳輸線以 `Serial Port` 的方式來連線控制，

此範例我們使用 `Node SerialPort` 來達到在 `Node.js` 發送訊號的目的：

[https://serialport.io/](https://serialport.io/)

首先在 `Node.js Server` 安裝好 `Node SerialPort` 套件：

```conf
npm install serialport
```

然後新建一個 `Router` 用來撰寫物聯網應用程式，

設定好 `COM Port` 來建立一個連線範例如下：

```javascript=
var express = require('express');
var router = express.Router();
var SerialPort = require("serialport");
var serial = new SerialPort("COM5", { baudRate: 115200 });

router.get('/', function (req, res) {
    serial.write('1');
    res.send('OK');
});

module.exports = router;
```

關於使用的 `COM Port` 可以從裝置管理員查詢到，

![](https://i.imgur.com/zXybSSW.png)

然後建立一個 `Arduino` 接收範例程式如下：

```cpp=
void setup()
{
    pinMode(LED_BUILTIN, OUTPUT);
    Serial.begin(115200);
}

void loop()
{
    int cmd;
    if ((cmd = Serial.read()) != -1)
    {
        digitalWrite(LED_BUILTIN, HIGH);
        delay(1000);
    }
    digitalWrite(LED_BUILTIN, LOW);
}
```

當接收到訊息後就讓板子上的 `LED` 燈亮一秒：

![](https://i.imgur.com/TSp4upI.gif)

這樣就是一個基礎的物聯網應用程式了，

趕快來動動腦建立各種育兒的有趣點子吧！