## Day 16 : 第一支機器人

### SDK 串接

很高興各位堅持到現在繼續建立自己的育兒小幫手，

接下來我們要使用到的是 `LINE Messaging API SDK for nodejs` ，

> [https://github.com/line/line-bot-sdk-nodejs](https://github.com/line/line-bot-sdk-nodejs)

回到我們建立的 `Express` 伺服器應用程式，

先將 SDK 安裝一下，

```
npm install @line/bot-sdk --save
```

新增一個 `config.json` 的 `JSON` 檔案，

填入先前申請的 `Channel access token` 、 `Channel secret` 資訊，

```javascript=
{
  "channelAccessToken": "YOUR_CHANNEL_ACCESS_TOKEN",
  "channelSecret": "YOUR_CHANNEL_SECRET"
}
```

在 `app.js` 中引用 `Line SDK` 及 `config.json` ，

```javascript=
var middleware = require('@line/bot-sdk').middleware;
var config = require('./config.json');
```

並且加入中間件指向至 `/webhook` 用來與 `Line` 連線，

```javascript=
app.use('/webhook', middleware(config));
```

改寫 `routes\index.js` 建立一個應聲蟲範例如下：

```javascript=
const express = require('express');
const router = express.Router();
const line = require('@line/bot-sdk');
const config = require('../config.json');
const client = new line.Client(config);

/* GET home page. */
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
    return client.replyMessage(event.replyToken, {
        type: 'text', text: event.message.text // 應聲蟲範例
    }).catch((err) => {
        if (err) {
            console.error(err);
        }
    });
};

module.exports = router;
```

範例是引用 `Line SDK` 並建立 `Client` 物件來回應一個相同的訊息，

完整語法說明請參考 `Line` 官方的 `SDK` 手冊，

> [https://line.github.io/line-bot-sdk-nodejs/#getting-started](https://line.github.io/line-bot-sdk-nodejs/#getting-started)

完成應聲蟲範例後效果如圖所示：

![](https://i.imgur.com/3iny8tl.png)

這就是一個簡單的 `Line Bot` 了，

利用 `Line` 可以串接到伺服器做到許多的事情，

這時候的妳一定也有許多創意，趕緊試試看吧。