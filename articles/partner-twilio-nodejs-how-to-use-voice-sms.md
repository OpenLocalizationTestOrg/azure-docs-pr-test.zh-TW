---
title: "aaaUsing Twilio 語音、 VoIP，和在 Azure 中的 SMS 訊息"
description: "了解如何 toomake 電話及傳送 SMS 訊息 hello Twilio API 服務在 Azure 上。 程式碼範例以 Node.js 撰寫。"
services: 
documentationcenter: nodejs
author: devinrader
manager: wpickett
editor: 
ms.assetid: f558cbbd-13d2-416f-b9b1-33a99c426af9
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 11/25/2014
ms.author: wpickett
ms.openlocfilehash: 6c44d60e217fcdf51e69fd2a8197f979afbb507a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-twilio-for-voice-voip-and-sms-messaging-in-azure"></a>在 Azure 中透過 Twilio 使用語音、VoIP 和簡訊功能
本指南示範如何 toobuild 應用程式的通訊使用 Twilio 和 Azure 上的 node.js。

<a id="whatis"/>

## <a name="what-is-twilio"></a>什麼是 Twilio？
Twilio 是 API 平台，可讓開發人員 toomake 輕鬆與接聽電話、 傳送及接收文字訊息和內嵌 VoIP 撥號到瀏覽器為基礎和原生行動應用程式。 在深入說明之前，我們先概略了解其運作方式。

### <a name="receiving-calls-and-text-messages"></a>接收來電和簡訊
Twilio 可讓開發人員太[購買可程式化的電話號碼][ purchase_phone]可能會使用的 tooboth 傳送和接收通話和文字訊息。 當 Twilio 數接收輸入的通話或簡訊時，Twilio 會傳送 web 應用程式 HTTP POST 或 GET 要求，要求您提供的指示上 toohandle hello 通話或簡訊的方式。 您的伺服器會回應 tooTwilio 的 HTTP 要求與[TwiML][twiml]，一組簡單的 XML 標記包含指示 toohandle 通話或簡訊。 稍後我們會檢視 TwiML 的範例。

### <a name="making-calls-and-sending-text-messages"></a>撥打電話和傳送簡訊
藉由進行 HTTP 要求 toohello Twilio web 服務 API，開發人員可以傳送簡訊或起始輸出撥打電話。 之傳出呼叫，hello 開發人員也必須指定傳回 TwiML 指示如何 toohandle hello 傳出呼叫一旦它所連接的 URL。

### <a name="embedding-voip-capabilities-in-ui-code-javascript-ios-or-android"></a>在 UI 程式碼中內嵌 VoIP 功能 (JavaScript、iOS 或 Android)
Twilio 提供了一個可將任何桌面 Web 瀏覽器、iOS 應用程式或 Android 應用程式轉換為 VoIP 電話的用戶端 SDK。 在本文中，我們將著重在如何 toouse VoIP 呼叫 hello 瀏覽器中。 在加法 toohello *Twilio JavaScript SDK* hello 瀏覽器中執行，伺服器端應用程式 （我們 node.js 應用程式） 必須使用的 tooissue 」 功能語彙基元"toohello JavaScript 用戶端。 閱讀更多關於使用 node.js VoIP [hello Twilio 開發人員部落格上][voipnode]。

<a id="signup"/>

## <a name="sign-up-for-twilio-microsoft-discount"></a>註冊 Twilio (Microsoft 折扣)
在使用 Twilio 服務之前，您必須先[註冊帳戶][signup]。 Microsoft Azure 客戶獲得的特殊折扣-[是確定 toosign 這裡][signup]！

<a id="azuresite"/>

## <a name="create-and-deploy-a-nodejs-azure-website"></a>建立及部署 node.js Azure 網站
接下來，您將需要 toocreate node.js 網站在 Azure 上執行。 [執行此作業的 hello 官方文件位於此處][azure_new_site]。 在高層級，您將執行 hello 下列：

* 註冊 Azure 帳戶 (若您尚無此帳戶)
* 使用 hello Azure 系統管理員主控台 toocreate 新網站
* 新增原始檔控制支援 (我們假設您使用 git)
* 使用簡單的 node.js Web 應用程式建立 `server.js` 檔案
* 部署這個簡單的應用程式 tooAzure

<a id="twiliomodule"/>

## <a name="configure-hello-twilio-module"></a>設定 hello Twilio 模組
接下來，我們將開始的 toowrite 簡單 node.js 應用程式可使用的 hello Twilio API。 開始之前，我們需要 tooconfigure 我們 Twilio 帳戶的認證。

### <a name="configuring-twilio-credentials-in-system-environment-variables"></a>在系統環境變數中設定 Twilio 認證
在針對 hello Twilio 後端訂單 toomake 驗證要求，我們需要我們帳戶 SID 和驗證權杖中，哪些函式做為 hello 使用者名稱和密碼為我們的 Twilio 帳戶設定。 最安全的方式 tooconfigure hello 這些用於在 Azure 中的 hello 節點模組是透過系統環境變數，您可以直接在 hello Azure 管理主控台中設定。

選取您 node.js 的網站，然後按一下 hello 「 設定 」 連結。  稍微向下捲動，您會看見一個可讓您為應用程式設定組態屬性的區域。  輸入您 Twilio 帳戶的認證 ([Twilio 主控台上找到][twilio_console]) 所示-請確定 tooname 它們`TWILIO_ACCOUNT_SID`和`TWILIO_AUTH_TOKEN`分別：

![Azure admin console][azure-admin-console]

您一次設定這些變數，在 hello Azure 主控台中重新啟動您的應用程式。

### <a name="declaring-hello-twilio-module-in-packagejson"></a>宣告 package.json 中的 hello Twilio 模組
接下來，我們需要 toocreate package.json toomanage 透過我們節點模組相依性[npm]。 相同層級在 hello 與 hello`server.js`檔案建立 hello *Azure/node.js*教學課程中，建立名為`package.json`。  在此檔案中，放置 hello 下列：

```json
{
  "name": "application-name",
  "version": "0.0.1",
  "private": true,
  "scripts": {
    "start": "node server"
  },
  "dependencies": {
    "body-parser": "^1.16.1",
    "ejs": "^2.5.5",
    "errorhandler": "^1.5.0",
    "express": "^4.14.1",
    "morgan": "^1.8.1",
    "twilio": "^2.11.1"
  }
}
```

這會宣告 hello twilio 模組相依性，以及 hello 熱門[Express web 架構][ express]和 hello EJS 範本引擎。  一切都已就緒，可以開始撰寫程式碼了。

<a id="makecall"/>

## <a name="make-an-outbound-call"></a>向外撥打電話
讓我們來建立簡單的表單，會將呼叫 tooa 的數字，我們選擇。 開啟  `server.js`，並輸入下列程式碼的 hello。 請注意，其中，該處會指示"CHANGE_ME"-放 hello azure 網站名稱：

```javascript
// Module dependencies
const express = require('express');
const path = require('path');
const http = require('http');
const twilio = require('twilio');
const logger = require('morgan');
const bodyParser = require('body-parser');
const errorHandler = require('errorhandler');
const accountSid = process.env.TWILIO_ACCOUNT_SID;
const authToken = process.env.TWILIO_AUTH_TOKEN;
// Create Express web application
const app = express();

// Express configuration
app.set('port', process.env.PORT || 3000);
app.set('views', __dirname + '/views');
app.set('view engine', 'ejs');
app.use(logger('tiny'));
app.use(bodyParser.urlencoded({ extended: false }))
app.use(bodyParser.json())
app.use(express.static(path.join(__dirname, 'public')));

if (app.get('env') !== 'production') {
  app.use(errorHandler());
}

// Render an HTML user interface for hello application's home page
app.get('/', (request, response) => response.render('index'));

// Handle hello form POST tooplace a call
app.post('/call', (request, response) => {
  var client = twilio(accountSid, authToken);

  client.makeCall({
    // make a call toothis number
    to:request.body.number,

    // Change tooa Twilio number you bought - see:
    // https://www.twilio.com/console/phone-numbers/incoming
    from:'+15558675309',

    // A URL in our app which generates TwiML
    // Change "CHANGE_ME" tooyour app's name
    url:'https://CHANGE_ME.azurewebsites.net/outbound_call'
  }, () => {
      // Go back toohello home page
      response.redirect('/');
  });
});

// Generate TwiML toohandle an outbound call
app.post('/outbound_call', (request, response) => {
  var twiml = new twilio.TwimlResponse();

  // Say a message toohello call's receiver
  twiml.say('hello - thanks for checking out Twilio and Azure', {
      voice:'woman'
  });

  response.set('Content-Type', 'text/xml');
  response.send(twiml.toString());
});

// Start server
app.listen(app.get('port'), function(){
  console.log(`Express server listening on port ${app.get('port')}`);
});
```

接下來，建立名為目錄`views`-在此目錄中，建立名為`index.ejs`以 hello 下列內容：

```html
<!DOCTYPE html>
<html>
<head>
  <title>Twilio Test</title>
  <style>
    input { height:20px; width:300px; font-size:18px; margin:5px; padding:5px; }
  </style>
</head>
<body>
  <h1>Twilio Test</h1>
  <form action="/call" method="POST">
      <input placeholder="Enter a phone number" name="number"/>
      <br/>
      <input type="submit" value="Call hello number above"/>
  </form>
</body>
</html>
```

現在，部署網站 tooAzure 並開啟您的首頁。 您也應該能夠 tooenter 在 hello 文字欄位中，您的電話號碼並從您的 Twilio 號碼接收呼叫 ！

<a id="sendmessage"/>

## <a name="send-an-sms-message"></a>傳送簡訊
現在，接著要設定使用者介面和處理邏輯 toosend 表單的文字訊息。 開啟  `server.js`，並新增下列程式碼 hello 最後一次呼叫之後，太 hello`app.post`:

```javascript
app.post('/sms', (request, response) => {
  const client = twilio(accountSid, authToken);

  client.sendSms({
      // send a text toothis number
      to:request.body.number,

      // A Twilio number you bought - see:
      // https://www.twilio.com/console/phone-numbers/incoming
      from:'+15558675309',

      // hello body of hello text message
      body: request.body.message

  }, () => {
      // Go back toohello home page
      response.redirect('/');
  });
});
```

在`views/index.ejs`，新增另一種形式下 hello toosubmit 第一個數字和文字訊息：

```html
<form action="/sms" method="POST">
  <input placeholder="Enter a phone number" name="number"/>
  <br/>
  <input placeholder="Enter a message toosend" name="message"/>
  <br/>
  <input type="submit" value="Send text toohello number above"/>
</form>
```

重新部署您的應用程式 tooAzure，，您現在應該能夠 toosubmit 會形成，然後傳送簡訊自己 （或任何您最接近的朋友） ！

<a id="nextsteps"/>

## <a name="next-steps"></a>後續步驟
您現在已經學會使用 node.js 和 Twilio toobuild 應用程式進行通訊的 hello 基本概念。 但是，這些範例幾乎 scratch hello 介面使用 Twilio 和 node.js 可行。 如 Twilio 使用 node.js 的詳細資訊，請參閱下列資源的 hello:

* [正式模組文件][docs]
* [透過 node.js 應用程式使用 VoIP 的教學課程][voipnode]
* [Votr - 使用 node.js 和 CouchDB 的即時簡訊投票應用程式 (三個單元)][votr]
* [在 node.js hello 瀏覽器中的組程式設計][pair]

祝您在 Azure 上使用 node.js 和 Twilio 時能夠得心應手！

[purchase_phone]: https://www.twilio.com/console/phone-numbers/search
[twiml]: https://www.twilio.com/docs/api/twiml
[signup]: http://ahoy.twilio.com/azure
[azure_new_site]: app-service-web/app-service-web-get-started-nodejs.md
[twilio_console]: https://www.twilio.com/console
[npm]: http://npmjs.org
[express]: http://expressjs.com
[voipnode]: http://www.twilio.com/blog/2013/04/introduction-to-twilio-client-with-node-js.html
[docs]: http://twilio.github.io/twilio-node/
[votr]: http://www.twilio.com/blog/2012/09/building-a-real-time-sms-voting-app-part-1-node-js-couchdb.html
[pair]: http://www.twilio.com/blog/2013/06/pair-programming-in-the-browser-with-twilio.html
[azure-admin-console]: ./media/partner-twilio-nodejs-how-to-use-voice-sms/twilio_1.png
