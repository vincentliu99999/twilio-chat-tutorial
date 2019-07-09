# twilio-chat-tutorial

## 簡介

提供 API 服務，企業文化： 一旦開始，就要不斷學習和改善，做好剩下的工作

* 提供服務
  * Email
  * 簡訊
  * 電話
  * 傳真
  * 聊天機器人
* 活躍的 [平台傳教者](https://www.twilio.com/blog/tag/evangelism), EX [Phil Nash@Github](https://github.com/philnash), [Phil Nash@Stack Overflow](https://stackoverflow.com/users/28376/philnash)
* 基礎架構: AWS

## Programmable Chat

運用跨平台 SDK(iOS, Android, Web, REST API) 賦予多人聊天功能、權限控管、Push notifications，Client side, Server side API 提供開發者運用

### 帳號資訊

* [Service Instance SID](https://www.twilio.com/docs/chat/rest/services) application data, scope
* [Account SID](https://www.twilio.com/console)
* [API Key](https://www.twilio.com/console/chat/dev-tools/api-keys)
* [API Secret](https://www.twilio.com/console/chat/dev-tools/api-keys)

### [資料類型](https://www.twilio.com/docs/chat/fundamentals)

* Service
* Users
* Roles
* Channels: private or public
* Members
* Messages

### Javascript 設定

```shell
npm install --save twilio-chat
npm install --save twilio
npm install --save twilio-common
```

### Java 設定

```xml
    <dependency>
        <groupId>com.twilio.sdk</groupId>
        <artifactId>twilio</artifactId>
        <version>7.37.3</version>
    </dependency>
```

### [Token](https://www.twilio.com/docs/chat/tutorials/chat-application-node-express#token-generation)

1. 建立 Token, identity
1. 初始化 Client
1. TTL 預設 3600 秒(1 小時)
1. Token 小於三分鐘內將過期時會有 `tokenAboutToExpire` 通知，取新的 token 再更新即可
1. Token 過期 `tokenExpired` 就只有 Error

### [頻道及訊息](https://www.twilio.com/docs/chat/channels)

物件

* `Channel Descriptors`: 查看資訊用, `Channel SID`, `友善名稱`, `獨特名稱`, `XX日期`...等等
* `Channels`: 實際互動用, `建立小圈圈`, `查看小圈圈`, `加入小圈圈`, `聊天說笑`, `邀請別人加入`, `監聽小圈圈事件`, `對方有在理我嗎`...等等
* Event 請參閱 [SDK](http://media.twiliocdn.com/sdk/js/chat/releases/3.2.4/docs/Channel.html#toc34__anchor)

### [多媒體支援](https://www.twilio.com/docs/chat/media-support)

* 圖片、影片 等 [MIME type](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types) 皆支援
* User Role 需要有 `sendMediaMessage`, `sendMessage` 的權限
* 內容不可變，其他屬性才可以
* 檔案大小上限: 150MB
* Media 暫時 URL 僅存在 300 秒，可重新取得

### [分頁](https://www.twilio.com/docs/chat/result-paging)

* Object: Channels, Member list, Messages
* 判斷是否還有資料: `hasPrevPage`, `hasNextPage`

### [權限控管](https://www.twilio.com/docs/chat/permissions)

* 服務層: User 可以看到哪些小圈圈、加入、建立
* Channel 層: User 可以在小圈圈做哪些事

### [訊息輸入提示](https://www.twilio.com/docs/chat/typing-indicator)

* 需由 Client 端發送，而非 SDK 內建幫你做好好
* 為了優化網路, chat client 僅會每 5 秒發送

### [訊息讀取進度](https://www.twilio.com/docs/chat/consumption-horizon)

狀態在多個 device 間是同步的，基於 `lastConsumedMessageIndex`，但他有可能是 `0` 或 `null`，讀取狀態每 10 秒才會發送，可透過 REST API 設定 `ConsumptionReportInterval`

* 功能
  * 有沒有讀？
  * 讀到哪了？
* 設定方式
  * 全部已讀取
  * 全部未讀取
  * 讀到某一則 by `message index`

### [推播通知](https://www.twilio.com/docs/chat/push-notification-configuration)

整合 APN (iOS), GCM/FCM (Android and browsers)，可指定[哪一類通知要發送](https://www.twilio.com/docs/chat/push-notification-configuration#push-types)，以及[發送訊息的樣板](https://www.twilio.com/docs/chat/push-notification-configuration#push-templates)，樣板皆有預設值，可自行 override。通知的 payload 最多 110 字元，超過的會截斷

* 類型
  * `New Message`
  * `Added to Channel`
  * `Invited to Channel`
  * `Removed from Channel`

* [Push Notifications on Web](https://www.twilio.com/docs/chat/javascript/push-notifications-web)

### [Webhook Events](https://www.twilio.com/docs/chat/webhook-events)

可用來監控或互動

## [Twilio Console](https://www.twilio.com/console/chat/dashboard)

### 儀表板

* Account SID
* Auth token
* Services

![dashboard](/images/1-dashboard.png)

### 用量

* users
* messages

![usage](/images/2-usage.png)

### 角色/權限

可自行新增

![roles](/images/3-roles.png)

### 使用者

![users](/images/4-users.png)

### 推播

可客製化推播訊息

![push](/images/5-push.png)

### 聊天室

![channels](/images/6-channels.png)

## [REST API](https://www.twilio.com/docs/chat/rest)

* 必備資料
  * Account SID
  * Auth token
  * Service SID
* 搭配 curl 使用就是 Debug 好工具
* Application 使用時記得設定到環境變數

## 參考資料

* [從零到五億: Twilio – CEO勞森傳奇故事錄](https://tenten.co/blog/twilio-jeff-lawson/)
* [價目表](https://www.twilio.com/pricing)
  * [Chat Pricing](https://www.twilio.com/chat/pricing)
* [Javascript API Reference](https://www.twilio.com/docs/chat/sdk-javascript)
* [REST API Reference](https://www.twilio.com/docs/api/chat/rest)
* [User Identity & Access Tokens](https://www.twilio.com/docs/chat/identity)
* [Twilio 限制](https://www.twilio.com/docs/chat/chat-limits)
* [Secure and Scale Programmable Chat Applications](https://www.twilio.com/docs/chat/secure-and-scale-programmable-chat-applications)
* [Chat with Node.js and Express](https://www.twilio.com/docs/chat/tutorials/chat-application-node-express)
