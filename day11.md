## Day 11 : 為孩子架站吧

### 架設一個 Node.js 網站

自製 IoT 工具其實並不難，

第一步就是需要架設一個自己的伺服器，

那麼該如何架設一個網站呢?

筆者選擇在 `Windows` 系統環境下架設 `Node.js` ，

因為 `Javascript` 程式語言的學習門檻較低，

而 `Windows` 也是大家較為熟悉的作業系統，

首先到官方網站 ( [https://nodejs.org/](https://nodejs.org/) ) 下載安裝包，

安裝後可以在 `Command Line` 測試看看有沒有安裝成功，

```
node -v
```

由於 `Node.js` 現在已內建了 `npm` 套件管理工具，

所以先開好一個資料夾來做為開發目錄，

然後在目錄下執行命令：

```
npm init
```

按照步驟說明逐一輸入內容，

就會自動幫妳建好一個安裝管理設定檔 `package.json` 。

### 使用 Express 框架

我們在 `Web` 應用的部份採用 `Express` 框架來撰寫程式，

[https://expressjs.com/zh-tw/](https://expressjs.com/zh-tw/)

因為有了 `npm` 套件管理工具，

只要執行安裝命令就可以自動裝好套件，

```
npm install express --save
```

記得參數加上 `--save` 才會把安裝設定寫入 `package.json` 設定檔，

執行完畢後會多出一個 `node_modules` 目錄存放著套件，

從沒寫過 `Node.js` 的話程式碼該怎麼辦呢?

其實 `Express` 有出了一個應用程式產生器，

同樣的執行指令就可以裝好 `express-generator` ，

```
npm install express-generator -g
```

安裝好後可以使用 `-h` 來查看指令選項，

```
express -h
```

然後到專案目錄下執行自動產生指令，

```
express --view=ejs
```

產生檔案後的資料結構如圖所示：

![](https://i.imgur.com/CEkqInn.png)

啟動伺服器前先執行指令來安裝 `express-generator` 所需的相依套件，

```
npm install
```

安裝後就可以下命令啟動我們的伺服器，

```
npm start
```

最後打開網頁看看有沒有成功

> http://localhost:3000/

應該會看到這樣的結果：

![](https://i.imgur.com/yxY3xdm.png)

這樣就完成架設 Local 端的網頁伺服器了，

來給自己一個掌聲吧。