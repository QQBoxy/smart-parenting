## Day 14 : 網路育兒工具

### 網路應用程式

網路應用 WebApp 在網路生活中隨處可見，

例如日前因為疫情關係而產生了許多口罩購買問題，

民間自主開發了許多口罩地圖這類的應用，

透過網路就可以省去許多排隊等候的時間，

因此隨地可以使用的網路應用將帶來許多方便。

架站的好處之一就是可以將應用放上網，

前面已經有介紹過簡單的撰寫應用程式，

現在就來試試看將不同的應用放上網路吧。

### 將應用上網

孩子出生後，

父母除了會想知道孩子幾個月了，

也會好奇孩子長得多高? 體重多少?

有沒有符合一般新生兒的成長趨勢，

不過沒有符合也不要擔心，只是一個參考，

有疑問可向醫生詢問是否有需要注意的地方即可，

如果寶寶活力正常也健健康康是不用太擔心的，

那麼就來做一個簡單的成長趨勢查詢工具吧！

首先建立一個平均身高體重資料 `grow.json` ，

```javascript=
{
    "boy": [
        { "month": 0, "height": { "min": 46.3, "max": 53.4 }, "weight": { "min": 2.5, "max": 4.3 }},
        { "month": 1, "height": { "min": 51.1, "max": 58.4 }, "weight": { "min": 3.4, "max": 5.7 }},
        { "month": 2, "height": { "min": 54.7, "max": 62.2 }, "weight": { "min": 4.4, "max": 7.0 }},
        { "month": 3, "height": { "min": 57.6, "max": 65.3 }, "weight": { "min": 5.1, "max": 7.9 }},
        { "month": 4, "height": { "min": 60.0, "max": 67.8 }, "weight": { "min": 5.6, "max": 8.6 }},
        { "month": 5, "height": { "min": 61.9, "max": 69.9 }, "weight": { "min": 6.1, "max": 9.2 }},
        { "month": 6, "height": { "min": 63.6, "max": 71.6 }, "weight": { "min": 6.4, "max": 9.7 }},
        { "month": 7, "height": { "min": 65.1, "max": 73.2 }, "weight": { "min": 6.7, "max": 10.2 }},
        { "month": 8, "height": { "min": 66.5, "max": 74.7 }, "weight": { "min": 7.0, "max": 10.5 }},
        { "month": 9, "height": { "min": 67.7, "max": 76.2 }, "weight": { "min": 7.2, "max": 10.9 }},
        { "month": 10, "height": { "min": 69.0, "max": 77.6 }, "weight": { "min": 7.5, "max": 11.2 }},
        { "month": 11, "height": { "min": 70.2, "max": 78.9 }, "weight": { "min": 7.7, "max": 11.5 }},
        { "month": 12, "height": { "min": 71.3, "max": 80.2 }, "weight": { "min": 7.8, "max": 11.8 }},
        { "month": 13, "height": { "min": 72.4, "max": 81.5 }, "weight": { "min": 8.0, "max": 12.1 }},
        { "month": 14, "height": { "min": 73.4, "max": 82.7 }, "weight": { "min": 8.2, "max": 12.4 }},
        { "month": 15, "height": { "min": 74.4, "max": 83.9 }, "weight": { "min": 8.4, "max": 12.7 }},
        { "month": 16, "height": { "min": 75.4, "max": 85.1 }, "weight": { "min": 8.5, "max": 12.9 }},
        { "month": 17, "height": { "min": 76.3, "max": 86.2 }, "weight": { "min": 8.7, "max": 13.2 }},
        { "month": 18, "height": { "min": 77.2, "max": 89.5 }, "weight": { "min": 8.9, "max": 13.5 }},
        { "month": 19, "height": { "min": 78.1, "max": 90.5 }, "weight": { "min": 9.0, "max": 13.7 }},
        { "month": 20, "height": { "min": 78.9, "max": 91.6 }, "weight": { "min": 9.2, "max": 14.0 }},
        { "month": 21, "height": { "min": 79.7, "max": 92.6 }, "weight": { "min": 9.3, "max": 14.3 }},
        { "month": 22, "height": { "min": 80.5, "max": 91.6 }, "weight": { "min": 9.5, "max": 14.5 }},
        { "month": 23, "height": { "min": 81.3, "max": 92.6 }, "weight": { "min": 9.7, "max": 14.8 }},
        { "month": 24, "height": { "min": 82.1, "max": 93.6 }, "weight": { "min": 9.8, "max": 15.1 }}
    ],
    "girl": [
        { "month": 0, "height": { "min": 45.6, "max": 52.7 }, "weight": { "min": 2.4, "max": 4.2 }},
        { "month": 1, "height": { "min": 50.0, "max": 57.4 }, "weight": { "min": 3.2, "max": 5.4 }},
        { "month": 2, "height": { "min": 53.2, "max": 60.9 }, "weight": { "min": 4.0, "max": 6.5 }},
        { "month": 3, "height": { "min": 55.8, "max": 63.8 }, "weight": { "min": 4.6, "max": 7.4 }},
        { "month": 4, "height": { "min": 58.0, "max": 66.2 }, "weight": { "min": 5.1, "max": 8.1 }},
        { "month": 5, "height": { "min": 59.9, "max": 68.2 }, "weight": { "min": 5.5, "max": 8.7 }},
        { "month": 6, "height": { "min": 61.5, "max": 70.0 }, "weight": { "min": 5.8, "max": 9.2 }},
        { "month": 7, "height": { "min": 62.9, "max": 71.6 }, "weight": { "min": 6.1, "max": 9.6 }},
        { "month": 8, "height": { "min": 64.3, "max": 73.2 }, "weight": { "min": 6.3, "max": 10.0 }},
        { "month": 9, "height": { "min": 65.6, "max": 74.7 }, "weight": { "min": 6.6, "max": 10.4 }},
        { "month": 10, "height": { "min": 66.8, "max": 76.1 }, "weight": { "min": 6.8, "max": 10.7 }},
        { "month": 11, "height": { "min": 68.0, "max": 77.5 }, "weight": { "min": 7.0, "max": 11.0 }},
        { "month": 12, "height": { "min": 69.2, "max": 78.9 }, "weight": { "min": 7.1, "max": 11.3 }},
        { "month": 13, "height": { "min": 70.3, "max": 80.2 }, "weight": { "min": 7.3, "max": 11.6 }},
        { "month": 14, "height": { "min": 71.3, "max": 81.4 }, "weight": { "min": 7.5, "max": 11.9 }},
        { "month": 15, "height": { "min": 72.4, "max": 82.7 }, "weight": { "min": 7.7, "max": 12.2 }},
        { "month": 16, "height": { "min": 73.3, "max": 83.9 }, "weight": { "min": 7.8, "max": 12.5 }},
        { "month": 17, "height": { "min": 74.3, "max": 85.0 }, "weight": { "min": 8.0, "max": 12.7 }},
        { "month": 18, "height": { "min": 75.2, "max": 86.2 }, "weight": { "min": 8.2, "max": 13.0 }},
        { "month": 19, "height": { "min": 76.2, "max": 87.3 }, "weight": { "min": 8.3, "max": 13.3 }},
        { "month": 20, "height": { "min": 77.0, "max": 88.4 }, "weight": { "min": 8.5, "max": 13.5 }},
        { "month": 21, "height": { "min": 77.9, "max": 89.4 }, "weight": { "min": 8.7, "max": 13.8 }},
        { "month": 22, "height": { "min": 78.7, "max": 90.5 }, "weight": { "min": 8.8, "max": 14.1 }},
        { "month": 23, "height": { "min": 79.6, "max": 91.5 }, "weight": { "min": 9.0, "max": 14.3 }},
        { "month": 24, "height": { "min": 80.3, "max": 92.5 }, "weight": { "min": 9.2, "max": 14.6 }}
    ]
}
```

建好基本的資料清單後，

再來建立基本的 `Express` 查詢應用範例 `tools.js` ：

```javascript=
var express = require('express');
var router = express.Router();
var moment = require('moment');
var grow = require('./grow.json');

router.get('/', function (req, res, next) {
    var birthday = moment("2020-09-28"); // 寶寶生日
    var sex = "girl"; // 寶寶性別
    var diffTime = moment().diff(birthday);
    var duration = moment.duration(diffTime);
    var month = duration.months();
    var day = duration.days();
    var info = grow[sex].find(item => item.month === month);
    res.send(`小寶貝已經出生 ${month} 個月又 ${day} 天，平均身高 ${info.height.min} ~ ${info.height.max} ，平均體重 ${info.weight.min} ~ ${info.weight.max}`);
});

module.exports = router;
```

別忘了引用剛剛寫好的 `tools.js` 模組至 `app.js` 主函數中，

```javascript=
var toolsRouter = require('./routes/tools');
```

然後在 `Express` 中加入 `Router` 模組，

```javascript=
app.use('/tools', toolsRouter);
```

重新啟動伺服器後就可以看到範例輸出：

```
小寶貝已經出生 0 個月又 7 天，平均身高 45.6 ~ 52.7 ，平均體重 2.4 ~ 4.2
```

現在建立好簡單的網路應用程式了，

但看起來還很陽春不是很方便使用，

不要著急繼續一步步的學習吧。