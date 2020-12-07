## Day 27 : HA 串接 Google Home

### Google Home 設定

其實官方網站在設定流程方面寫得很完整，

雖然 Google 申請畫面稍微有改版，

但對於整體流程來說還不至於影響太大，

看得懂的朋友不妨直接看英文的說明：

[https://www.home-assistant.io/integrations/google_assistant/](https://www.home-assistant.io/integrations/google_assistant/)

如果妳跟筆者一樣英文破爛那就跟著教學做吧！

### 步驟 1 : 建立 Actions on Google 專案

1. 首先點選 `New Project` 設定一個妳喜歡的名稱，選擇 `Chinese (Traditional)` 與 `Taiwan` 
2. 選擇 `Smart Home` 並點擊 `Start Building`
3. 點選 `Build your Action` 再點擊 `Add Action(s)`
4. `Fulfillment URL` 填入 `HA` 的 `API` 網址 `https://{妳的HA網址:連接埠}/api/google_assistant`
5. 點選 `Save` 以儲存

### 步驟 2 : 設定 Account linking 用來與 HA 溝通

1. 點選 `Account linking` 進入設定頁面
2. 填寫 `OAuth Client Information` 設定
    1. `Client ID` 填入 `https://oauth-redirect.googleusercontent.com/r/{妳的Project ID}` ， `Project ID` 可以在右上角三個點的選單內，點選 `Project settings` 後的頁面內找到。
    2. `Client secret` 隨便填寫，因為 `HA` 用不到這個參數
    3. `Authorization URL` 填入 `https://{妳的HA網址:連接埠}/auth/authorize`
    4. `Token URL` 填入 `https://{妳的HA網址:連接埠}/auth/token`

![](https://i.imgur.com/lyouDth.png)

3. 跳過第2步來到第3步 `Configure your client`
    1. 首先在 `Scopes` 填入妳的 `email`
    2. 按 `Add scope` 後再填入妳的 `name`
    3. 注意這項不能是勾選的狀態 `Google to transmit clientID and secret via HTTP basic auth header` 

![](https://i.imgur.com/aestrTc.png)

### 步驟 3 : 確保裝置狀態測試中

1. 點選 `Develop` 頁面
2. 於右上角點選 `Test` 按鈕以產生 `Test App`
3. 如果沒有看到選項的話，則進入 `Test` 頁面，點選 `Settings` 按鈕，啟用 `On device testing` 選項

### 步驟 4 : 在 yaml 設定中新增 Google Assistant

接下來需要在 `configuration.yaml` 內新增 `google_assistant` 設定，

以下是官方提供的範例設定：

```yaml=
# Example configuration.yaml entry
google_assistant:
  project_id: YOUR_PROJECT_ID
  service_account: !include SERVICE_ACCOUNT.JSON
  report_state: true
  exposed_domains:
    - switch
    - light
  entity_config:
    switch.kitchen:
      name: CUSTOM_NAME_FOR_GOOGLE_ASSISTANT
      aliases:
        - BRIGHT_LIGHTS
        - ENTRY_LIGHTS
    light.living_room:
      expose: false
      room: LIVING_ROOM
```

詳細參數可以參考官方手冊：

[https://www.home-assistant.io/integrations/google_assistant/#configuration](https://www.home-assistant.io/integrations/google_assistant/#configuration)

### 步驟 5 : 設定 Google Home

1. 打開手機內的 `Google Home App`
2. 按 `+` 新增裝置，點選 `設定裝置` ，選擇 `Google 的合作夥伴` ，找到一個服務叫做 `[test] 妳的APP名稱`
3. 接下來就可以新增妳的智慧裝置了

### 結語

這篇教學算是比較進階的整合設定，

如果覺得太困難也可以選擇跳過這篇，

但如果能把 `Google Home` 整合進來，

就可以方便地在寶寶快睡著時 `OK Google 燈光調暗一點` ！