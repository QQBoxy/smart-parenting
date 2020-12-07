## Day 29 : 第一個無線智慧裝置

### 網頁伺服器

學習了快一個月後總算可以來撰寫無線的智慧裝置，

相信利用這些技術肯定能提升妳的育兒體驗，

那麼就趕緊來撰寫智慧裝置的韌體程式，

首先試著在 `ESP8266` 建立一個獨立的網頁伺服器，

再利用它來做個簡單的範例吧。

### 撰寫程式

此範例目標是透過 `Wifi` 連線至網頁來控制點亮與關閉 `LED` ，

首先要加入基本的 `Wifi` 連線功能，

以及建立出一個獨立的伺服器服務，

需要引用兩個 `Library` ：

```cpp=
#include <ESP8266WiFi.h>
#include <ESP8266WebServer.h>
```

然後需要兩個變數來存放 `SSID` 與 `密碼` ：

```cpp=
const char ssid[] = "SSID名稱";
const char pass[] = "Wifi密碼";
```

建立一個 `Port 80` 的伺服器，

```cpp=
ESP8266WebServer server(80);
```

建立一個首頁用來輸入密碼與執行動作：

```cpp=
void rootRouter()
{
    server.send(200, "text/html", "<form action=\"/door\" method=\"post\"><input type=\"password\" name=\"password\" placeholder=\"Password\"/><input type=\"submit\" name=\"action\" value=\"Open\" /><input type=\"submit\" name=\"action\" value=\"Close\" /></form>");
}
```

建立一個接收請求的頁面，

用於執行硬體相對應的操作：

```cpp=
void doorRouter()
{
    String password = server.arg("password");
    if (password != "密碼")
    {
        server.send(200, "text/html", "Wrong Password! <a href=\"/\">Back</>");
        return;
    }
    String action = server.arg("action");
    if (action == "Open")
    {
        digitalWrite(LED_BUILTIN, LOW);
        server.send(200, "text/html", "Opened! <a href=\"/\">Back</>");
    }
    else if (action == "Close")
    {
        digitalWrite(LED_BUILTIN, HIGH);
        server.send(200, "text/html", "Closed! <a href=\"/\">Back</>");
    }
}
```

伺服器的初始化設定，

包括物聯網 `LED` 的輸出設定，

啟用 `Wifi` 連線與重新連線設定，

伺服器的網頁路由啟用設定：

```cpp=
void setup()
{
    Serial.begin(115200);
    
    pinMode(LED_BUILTIN, OUTPUT);
    digitalWrite(LED_BUILTIN, HIGH);
    
    WiFi.begin(ssid, pass);

    while (WiFi.status() != WL_CONNECTED)
    {
        delay(500);
        Serial.print(".");
    }
    Serial.println("");
    
    server.on("/index.html", rootRouter);
    server.on("/", rootRouter);
    server.on("/door", doorRouter);

    server.onNotFound([]() {
        server.send(404, "text/plain", "Page NOT found!");
    });

    server.begin();
    Serial.println("Server is now running on IP: ");
    Serial.println(WiFi.localIP());
    
}
```

在主函數中不斷的監聽伺服器請求：

```cpp=
void loop()
{
    server.handleClient();
}
```

建立完之後就可以將韌體燒錄到 `ESP8266` 了，

此範例打開後就可以看見簡單的首頁，

輸入密碼後點選就會點亮 `LED` 燈：

![](https://i.imgur.com/5SccFgn.gif)

密碼輸入錯誤也會跳出警告：

![](https://i.imgur.com/jPzUTuA.gif)

大家有學會如何建立 `Wifi` 無線智慧裝置了嗎。