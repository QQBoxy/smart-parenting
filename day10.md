## Day 10 : 第一個育兒小工具

### 預產期小工具

時間就是金錢，我想沒有人會反對，

然而老婆的預產期也非常的重要，

預產期其實就是小寶寶預計出生的時間，

它是根據月經的時間來往前推算受孕的日期，

如果已經照過超音波則醫生會再根據胎兒的大小修正預產期，

先不論那些因各種意外而提早報到的小朋友們，

有了預產期的參考資訊才能好好做孕期規劃，

包括先買好寶寶的必需品以及了解何時需要做定期超音波檢查，

或是知道可能是什麼生肖星座也是蠻有趣的，

生產時才比較能帶著輕鬆的心情來迎接小寶貝的出生。

### 開始動手做

當你有了需求以後，

能不能實際動手做就非常重要，

有的人就是缺少了那麼一點點動力，

或是像我今天邊寫鐵人賽還要邊帶6個月的女兒，

導致連一個簡單的計時器可能都要難產許久，

所以那怕是多麼簡單的小程式也是一種練習，

趕快打開妳的編輯器開始撰寫吧。

### 預產期倒數計時器

首先建立 HTML 內容

```htmlembedded=
<span id="countboxy"></span>
```

接著引用 Moment 時間函數，加上 JavaScript 程式碼

```javascript=
const countboxy = document.getElementById("countboxy");
window.setInterval(function() {
  const diffTime = moment('2021-07-18T00:00:00+08:00').diff(moment());
  const duration = moment.duration(diffTime);
  const month = duration.months();
  const day = duration.days();
  const hour = duration.hours();
  const min = duration.minutes();
  const sec = duration.seconds();
  countboxy.innerHTML = `距離預產期還有 ${month} 個月又 ${day} 天 ${hour} 時 ${min} 分 ${sec} 秒`;
}, 1000);
```

範例結果

![](https://i.imgur.com/uQNEcs9.gif)

#### Source Code

[https://codepen.io/QQBoxy/pen/mdPjXOx?editors=1010](https://codepen.io/QQBoxy/pen/mdPjXOx?editors=1010)

有沒有覺得開始踏出第一步後，

好像什麼都難不倒自己了呢?

那麼就給自己一個掌聲鼓勵吧，

大家也不妨試試看寫一個孩子的年齡計時器，

當你的孩子出生後一定會很期待這件事，

每天看著她現在多大了? 經過幾個月又幾天?

那麼希望下一次還能繼續看到你唷。