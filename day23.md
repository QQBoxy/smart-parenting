## Day 23 : Line Bot 物聯網

### Line Bot 物聯網

看到這裡已經開始有網友想放棄了嗎?

趕緊來整合正流行的 Line Bot 吧，

很簡單就可以串接起來跟隔壁妹子炫耀一下，

也許妹子也覺得育兒好簡單然後就在一起了呢(啾咪

由於我們已經建立過應聲蟲這樣的簡單應用，

只要再加上訊息文字的過濾就可以區分各種應用，

例如可以規定 `開燈` 、 `關燈` 等關鍵字會啟動物聯網程式，

那麼就趕緊來試試看吧！

### 建立命令程式

直接修改先前的應聲蟲範例，

把 `IoT` 的程式搬過來並加上 `關鍵字` 判斷如下範例

```javascript=
/*jshint node: true, esversion: 9 */
const express = require('express');
const router = express.Router();
const line = require('@line/bot-sdk');
const SerialPort = require("serialport");
const serial = new SerialPort("COM4", { baudRate: 115200 });
const config = require('../config.json');
const client = new line.Client(config);

router.get('/', function (req, res, next) {
    res.render('index', { title: 'Express' });
});

router.post('/webhook', (req, res) => {
    Promise
        .all(req.body.events.map(handleEvent))
        .then((result) => res.json(result))
        .catch((err) => {
            res.status(500).end();
        });
});

const handleEvent = (event) => {
    if (event.type !== 'message' || event.message.type !== 'text') {
        return Promise.resolve(null);
    }
    if (event.message.text === "開燈") {
        serial.write('1');
        return client.replyMessage(event.replyToken, {
            type: 'text', text: "開燈了"
        }).catch((err) => {
            if (err) {
                console.error(err);
            }
        });
    } else {
        return Promise.resolve(null);
    }
};

module.exports = router;

```

注意需要先將上次的 `IoT` 範例關掉避免 `COM Port` 被占用，

以及 `COM Port` 有可能因為換孔位變動記得要修改一下，

改完後直接連結上回的 `Arduino` 程式來試試看：

![](https://i.imgur.com/s9fo55I.gif)

燈號看起來也正常的亮起來了呢！

使用 `Line Bot` 來建立物聯網的應用就是這麼容易。

### 土炮紅外線冷氣控制

筆者前陣子還土炮了紅外線控制冷氣：

![](https://i.imgur.com/KMXKARe.jpg)

![](https://i.imgur.com/LjB20IT.gif)

有興趣的可以看看 `Arduino-IRremote` 固定碼編解碼函數：

[https://github.com/z3t0/Arduino-IRremote](https://github.com/z3t0/Arduino-IRremote)

就能自製家庭用紅外線控制器囉。

題外話，最近中秋節家裡很熱鬧，

小孩不曉得是不是被哪個親戚傳染而感冒了，

邊顧小孩還要寫鐵人賽真是人生最大的挑戰...