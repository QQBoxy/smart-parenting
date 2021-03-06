## Day 24 : Home Assistant

### 開源智慧家庭平台

透過 `Line Bot` 的物聯網裝置可以獨立運作，

但是我們也會希望可以透過智慧家庭平台來控制這些家電，

那麼有什麼好方法可以簡單又彈性呢?

答案應該就是開源的智慧家庭平台 `HA (Home Assistant)` 了。

使用的這套開源平台的人非常多，

感謝社群的力量使它的平台架設也相當容易，

有 `樹莓派` 、 `Docker` 等快速且方便的安裝方式，

伺服器架設在家中當然也有許多好處囉。

例如需要熱水瓶來泡奶時外部網路又剛好出現異常，

這時智慧裝置還是能透過區網來繼續正常運作，

它也具備能根據自己想要而修改的開源精神，

可以跨平台的整合多種品牌智慧裝置，

不會撰寫程式的人也能透過 `UI` 介面來設定與操作。

### HA平台架構

![](https://i.imgur.com/LbBMYFO.png)

`HA` 與其它智慧家庭平台架構相當，

它主要是以 `Web APP` 的方式來進行各種操作，

當然也可以安裝官方的 `APP` 但底層應該還是 `Web APP` ，

`HA` 也如同其他平台一樣可以連接各種智慧裝置。

不過不同的是當對方平台沒有提供一般連接方式的時候，

就必須要 `破解` 才能使用，沒錯妳沒看錯，

這就是為何 `HA` 還沒有辦法讓一般大眾簡單入門的原因。

畢竟 `HA` 就是一個免費開源的系統，

各家付費智慧家庭裝置都希望妳在它們官方平台來使用，

藉此它才能拿到妳的個人使用資料來做各種分析，

如果妳改用 `HA` 來作為智慧裝置平台的話，

那麼廠商就拿不到相關可分析的資料了唷。

由於 `HA` 也具備相當多的家庭自動化控制功能，

先前提到過的控制智慧裝置來輔助育兒也都可以在 `HA` 來設定使用，

相信對育兒會有更多好處與幫助的。