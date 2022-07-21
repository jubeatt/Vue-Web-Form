# Vue－表單練習

來自 [Build Web Apps with Vue JS 3 & Firebase](https://www.udemy.com/course/build-web-apps-with-vuejs-firebase/) 的其中一項專案。

這份專案是用來練習 Vue 的基本表單操作，包含：

- `v-model` 的使用（Input、Select、Checkbox）
- `modifier` 的使用（prevent、ctrl）
- 表單驗證（密碼長度）

總之只是份簡單的練習，不過表單確實是常會遇到的需求，所以才留個紀錄。

網站連結：https://jubeatt.github.io/Vue-Web-Form

![demo](demo.png)

附註：表單送出後可以到 console 中查看資料，另外左下角是 `data` 的即時資料，這樣能更快理解什麼是「雙向綁定」。

## 運行方式

1. 把專案 clone 下來後安裝依賴項目：

```bash
npm install
```

2. 啟動開發環境：

```bash
npm run serve
```

## 打包

```bash
npm run build
```

之後再透過 live-sever 的方式打開 `/dist/index.html` 即可
