## Day 28 : 無線智慧裝置

### Wifi 開發板

現成的智慧裝置搭配 `HA` 來控制讓育兒變得更簡單，

生活品質的提升也讓妳的人生更加的精彩，

那麼是否也可以自己來動手做無線裝置呢?

其實只要透過具備 `Wifi` 能力的開發版，

就可以自製符合自己期望的智慧裝置囉！

本集文章我給大家分享一塊便宜的開發板 `ESP8266開發板` 。

![](https://i.imgur.com/poxaydI.jpg)

### ESP8266

為什麼市面上有這麼多 `Wifi` 開發板卻偏偏使用它呢？

一個簡單的原因就是它的價格 `超便宜` ！

自製的無線裝置通常僅是為了遠端控制而已，

邏輯運算大多也都寫在智慧平台來完成處理才送出訊號，

因此板子上的功能不多所以記憶體佔用不高，

小巧的 `ESP8266` 就足夠應付這樣的需求，

事不宜遲先來建立基本的編譯環境吧。

### Arduino IDE

`ESP8266` 可以使用 `Arduino` 新增套件來燒錄，

使用以下的套件就可以在 `Arduino IDE` 增加 `ESP8266` 這塊開發板：

[https://github.com/esp8266/Arduino](https://github.com/esp8266/Arduino)

打開 Arduino IDE 在 `偏好設定` 內的 `額外的開發板管理員網址` 新增：

```
https://arduino.esp8266.com/stable/package_esp8266com_index.json
```

![](https://i.imgur.com/yiBWQaq.png)

然後在 `工具` > `開發板` > `開發板管理員` 搜尋 `ESP8266` 並安裝：

![](https://i.imgur.com/BeG3qLk.png)

然後就可以選擇 `ESP8266` 的開發板了：

![](https://i.imgur.com/4LXauz6.png)

其中筆者使用的是 `NodeMCU ESP-12E` 的板子，

如果妳用的是不同的版本記得要選對，

那麼下一次我們將介紹如何使用 `ESP8266` 撰寫韌體，

期待您繼續努力完成。