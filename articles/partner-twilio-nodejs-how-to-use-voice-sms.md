---
title: "在 Azure 中透過 Twilio 使用語音、VoIP 和簡訊功能"
description: "了解如何在 Azure 上使用 Twilio API 服務撥打電話及傳送簡訊。 程式碼範例以 Node.js 撰寫。"
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
ms.openlocfilehash: 44ec97812130d41d75be98fc8e2d846b7cb5c913
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="using-twilio-for-voice-voip-and-sms-messaging-in-azure"></a><span data-ttu-id="d5e96-104">在 Azure 中透過 Twilio 使用語音、VoIP 和簡訊功能</span><span class="sxs-lookup"><span data-stu-id="d5e96-104">Using Twilio for Voice, VoIP, and SMS Messaging in Azure</span></span>
<span data-ttu-id="d5e96-105">本指南將說明如何建置可在 Azure 上與 Twilio 和 node.js 通訊的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d5e96-105">This guide demonstrates how to build apps that communicate with Twilio and node.js on Azure.</span></span>

<a id="whatis"/>

## <a name="what-is-twilio"></a><span data-ttu-id="d5e96-106">什麼是 Twilio？</span><span class="sxs-lookup"><span data-stu-id="d5e96-106">What is Twilio?</span></span>
<span data-ttu-id="d5e96-107">Twilio 是一個 API 平台，可協助開發人員撥接電話、收發簡訊，以及在瀏覽器應用程式和原生行動應用程式中內嵌 VoIP 通話。</span><span class="sxs-lookup"><span data-stu-id="d5e96-107">Twilio is an API platform that makes it easy for developers to make and receive phone calls, send and receive text messages, and embed VoIP calling into browser-based and native mobile applications.</span></span> <span data-ttu-id="d5e96-108">在深入說明之前，我們先概略了解其運作方式。</span><span class="sxs-lookup"><span data-stu-id="d5e96-108">Let's briefly go over how this works before diving in.</span></span>

### <a name="receiving-calls-and-text-messages"></a><span data-ttu-id="d5e96-109">接收來電和簡訊</span><span class="sxs-lookup"><span data-stu-id="d5e96-109">Receiving Calls and Text Messages</span></span>
<span data-ttu-id="d5e96-110">Twilio 可讓開發人員[購買可程式化的電話號碼][purchase_phone]，用以收發電話和簡訊。</span><span class="sxs-lookup"><span data-stu-id="d5e96-110">Twilio allows developers to [purchase programmable phone numbers][purchase_phone] which can be used to both send and receive calls and text messages.</span></span> <span data-ttu-id="d5e96-111">當 Twilio 號碼接收到內送的電話或簡訊時，Twilio 會對您的 Web 應用程式傳送 HTTP POST 或 GET 要求，向您請示如何處理來電或簡訊。</span><span class="sxs-lookup"><span data-stu-id="d5e96-111">When a Twilio number receives an inbound call or text, Twilio will send your web application an HTTP POST or GET request, asking you for instructions on how to handle the call or text.</span></span> <span data-ttu-id="d5e96-112">您的伺服器會以 [TwiML][twiml] 回應 Twilio 的 HTTP 要求；這是一組簡單的 XML 標籤，其中包含如何處理來電或簡訊的指示。</span><span class="sxs-lookup"><span data-stu-id="d5e96-112">Your server will respond to Twilio's HTTP request with [TwiML][twiml], a simple set of XML tags that contain instructions on how to handle a call or text.</span></span> <span data-ttu-id="d5e96-113">稍後我們會檢視 TwiML 的範例。</span><span class="sxs-lookup"><span data-stu-id="d5e96-113">We will see examples of TwiML in just a moment.</span></span>

### <a name="making-calls-and-sending-text-messages"></a><span data-ttu-id="d5e96-114">撥打電話和傳送簡訊</span><span class="sxs-lookup"><span data-stu-id="d5e96-114">Making Calls and Sending Text Messages</span></span>
<span data-ttu-id="d5e96-115">開發人員可對 Twilio Web 服務 API 發出 HTTP 要求，以傳送簡訊或向外撥打電話。</span><span class="sxs-lookup"><span data-stu-id="d5e96-115">By making HTTP requests to the Twilio web service API, developers can send text messages or initiate outbound phone calls.</span></span> <span data-ttu-id="d5e96-116">對於外撥電話，開發人員還必須指定一個 URL 以傳回相關指示，說明在接通後應如何處理外撥電話。</span><span class="sxs-lookup"><span data-stu-id="d5e96-116">For outbound calls, the developer must also specify a URL that returns TwiML instructions for how to handle the outbound call once it is connected.</span></span>

### <a name="embedding-voip-capabilities-in-ui-code-javascript-ios-or-android"></a><span data-ttu-id="d5e96-117">在 UI 程式碼中內嵌 VoIP 功能 (JavaScript、iOS 或 Android)</span><span class="sxs-lookup"><span data-stu-id="d5e96-117">Embedding VoIP Capabilities in UI code (JavaScript, iOS, or Android)</span></span>
<span data-ttu-id="d5e96-118">Twilio 提供了一個可將任何桌面 Web 瀏覽器、iOS 應用程式或 Android 應用程式轉換為 VoIP 電話的用戶端 SDK。</span><span class="sxs-lookup"><span data-stu-id="d5e96-118">Twilio provides a client-side SDK which can turn any desktop web browser, iOS app, or Android app into a VoIP phone.</span></span> <span data-ttu-id="d5e96-119">在本文中，我們僅討論如何在瀏覽器中使用 VoIP 通話。</span><span class="sxs-lookup"><span data-stu-id="d5e96-119">In this article, we will focus on how to use VoIP calling in the browser.</span></span> <span data-ttu-id="d5e96-120">除了在瀏覽器中執行 *Twilio JavaScript SDK* 以外，同時也須使用伺服器端應用程式 (node.js 應用程式)，將「功能權杖」發出至 JavaScript 用戶端。</span><span class="sxs-lookup"><span data-stu-id="d5e96-120">In addition to the *Twilio JavaScript SDK* running in the browser, a server-side application (our node.js application) must be used to issue a "capability token" to the JavaScript client.</span></span> <span data-ttu-id="d5e96-121">如需透過 node.js 使用 VoIP 的詳細資訊，請參閱 [Twilio 開發人員部落格][voipnode]。</span><span class="sxs-lookup"><span data-stu-id="d5e96-121">You can read more about using VoIP with node.js [on the Twilio dev blog][voipnode].</span></span>

<a id="signup"/>

## <a name="sign-up-for-twilio-microsoft-discount"></a><span data-ttu-id="d5e96-122">註冊 Twilio (Microsoft 折扣)</span><span class="sxs-lookup"><span data-stu-id="d5e96-122">Sign Up For Twilio (Microsoft Discount)</span></span>
<span data-ttu-id="d5e96-123">在使用 Twilio 服務之前，您必須先[註冊帳戶][signup]。</span><span class="sxs-lookup"><span data-stu-id="d5e96-123">Before using Twilio services, you must first [sign up for an account][signup].</span></span> <span data-ttu-id="d5e96-124">Microsoft Azure 客戶享有特別折扣 - 請[務必在此註冊][signup]！</span><span class="sxs-lookup"><span data-stu-id="d5e96-124">Microsoft Azure customers receive a special discount - [be sure to sign up here][signup]!</span></span>

<a id="azuresite"/>

## <a name="create-and-deploy-a-nodejs-azure-website"></a><span data-ttu-id="d5e96-125">建立及部署 node.js Azure 網站</span><span class="sxs-lookup"><span data-stu-id="d5e96-125">Create and Deploy a node.js Azure Website</span></span>
<span data-ttu-id="d5e96-126">接著，您必須建立在 Azure 上執行的 node.js 網站。</span><span class="sxs-lookup"><span data-stu-id="d5e96-126">Next, you will need to create a node.js website running on Azure.</span></span> <span data-ttu-id="d5e96-127">[此作業的正式指引文件位於此處][azure_new_site]。</span><span class="sxs-lookup"><span data-stu-id="d5e96-127">[The official documentation for doing this is located here][azure_new_site].</span></span> <span data-ttu-id="d5e96-128">概括而言，您將執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="d5e96-128">At a high level, you will be doing the following:</span></span>

* <span data-ttu-id="d5e96-129">註冊 Azure 帳戶 (若您尚無此帳戶)</span><span class="sxs-lookup"><span data-stu-id="d5e96-129">Signing up for an Azure account, if you don't have one already</span></span>
* <span data-ttu-id="d5e96-130">使用 Azure 管理主控台建立新網站</span><span class="sxs-lookup"><span data-stu-id="d5e96-130">Using the Azure admin console to create a new website</span></span>
* <span data-ttu-id="d5e96-131">新增原始檔控制支援 (我們假設您使用 git)</span><span class="sxs-lookup"><span data-stu-id="d5e96-131">Adding source control support (we will assume you used git)</span></span>
* <span data-ttu-id="d5e96-132">使用簡單的 node.js Web 應用程式建立 `server.js` 檔案</span><span class="sxs-lookup"><span data-stu-id="d5e96-132">Creating a file `server.js` with a simple node.js web application</span></span>
* <span data-ttu-id="d5e96-133">將這個簡單的應用程式部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="d5e96-133">Deploying this simple application to Azure</span></span>

<a id="twiliomodule"/>

## <a name="configure-the-twilio-module"></a><span data-ttu-id="d5e96-134">設定 Twilio 模組</span><span class="sxs-lookup"><span data-stu-id="d5e96-134">Configure the Twilio Module</span></span>
<span data-ttu-id="d5e96-135">接著，我們將開始撰寫採用 Twilio API 的簡易 node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d5e96-135">Next, we will begin to write a simple node.js application which makes use of the Twilio API.</span></span> <span data-ttu-id="d5e96-136">開始之前，我們必須設定 Twilio 帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="d5e96-136">Before we begin, we need to configure our Twilio account credentials.</span></span>

### <a name="configuring-twilio-credentials-in-system-environment-variables"></a><span data-ttu-id="d5e96-137">在系統環境變數中設定 Twilio 認證</span><span class="sxs-lookup"><span data-stu-id="d5e96-137">Configuring Twilio Credentials in System Environment Variables</span></span>
<span data-ttu-id="d5e96-138">若要對 Twilio 後端發出已驗證的要求，我們必須要有自己的帳戶 SID 和驗證權杖，以作為 Twilio 帳戶的使用者名稱和密碼集。</span><span class="sxs-lookup"><span data-stu-id="d5e96-138">In order to make authenticated requests against the Twilio back end, we need our account SID and auth token, which function as the username and password set for our Twilio account.</span></span> <span data-ttu-id="d5e96-139">最安全的方式是透過系統環境變數，在 Azure 中設定這些與節點模組搭配使用的項目；您可以直接在 Azure 管理主控台中設定。</span><span class="sxs-lookup"><span data-stu-id="d5e96-139">The most secure way to configure these for use with the node module in Azure is via system environment variables, which you can set directly in the Azure admin console.</span></span>

<span data-ttu-id="d5e96-140">選取您的 node.js 網站，然後按一下 "CONFIGURE" 連結。</span><span class="sxs-lookup"><span data-stu-id="d5e96-140">Select your node.js website, and click the "CONFIGURE" link.</span></span>  <span data-ttu-id="d5e96-141">稍微向下捲動，您會看見一個可讓您為應用程式設定組態屬性的區域。</span><span class="sxs-lookup"><span data-stu-id="d5e96-141">If you scroll down a bit, you will see an area where you can set configuration properties for your application.</span></span>  <span data-ttu-id="d5e96-142">如下所示，輸入您的 Twilio 帳戶認證 ([可在 Twilio 主控台上找到][twilio_console]) - 務必分別將它們命名為 `TWILIO_ACCOUNT_SID` 和 `TWILIO_AUTH_TOKEN`︰</span><span class="sxs-lookup"><span data-stu-id="d5e96-142">Enter your Twilio account credentials ([found on your Twilio Console][twilio_console]) as shown - make sure to name them `TWILIO_ACCOUNT_SID` and `TWILIO_AUTH_TOKEN`, respectively:</span></span>

![Azure admin console][azure-admin-console]

<span data-ttu-id="d5e96-144">這些變數設定完成後，請在 Azure 主控台中重新啟動您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d5e96-144">Once you have configured these variables, restart your application in the Azure console.</span></span>

### <a name="declaring-the-twilio-module-in-packagejson"></a><span data-ttu-id="d5e96-145">在 package.json 中宣告 Twilio 模組</span><span class="sxs-lookup"><span data-stu-id="d5e96-145">Declaring the Twilio module in package.json</span></span>
<span data-ttu-id="d5e96-146">接下來，我們必須建立一個 package.json，以透過 [npm]管理節點模組相依性。</span><span class="sxs-lookup"><span data-stu-id="d5e96-146">Next, we need to create a package.json to manage our node module dependencies via [npm].</span></span> <span data-ttu-id="d5e96-147">在您於 *Azure/node.js* 教學課程中建立的 `server.js` 檔案所屬的相同層級上，建立名為 `package.json` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="d5e96-147">At the same level as the `server.js` file you created in the *Azure/node.js* tutorial, create a file named `package.json`.</span></span>  <span data-ttu-id="d5e96-148">在此檔案中放入下列項目：</span><span class="sxs-lookup"><span data-stu-id="d5e96-148">Inside this file, place the following:</span></span>

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

<span data-ttu-id="d5e96-149">這會將 twilio 模組宣告為相依性，以及常用的 [Express Web 架構][express]和 EJS 範本引擎。</span><span class="sxs-lookup"><span data-stu-id="d5e96-149">This declares the twilio module as a dependency, as well as the popular [Express web framework][express] and the EJS template engine.</span></span>  <span data-ttu-id="d5e96-150">一切都已就緒，可以開始撰寫程式碼了。</span><span class="sxs-lookup"><span data-stu-id="d5e96-150">Okay, now we're all set - let's write some code!</span></span>

<a id="makecall"/>

## <a name="make-an-outbound-call"></a><span data-ttu-id="d5e96-151">向外撥打電話</span><span class="sxs-lookup"><span data-stu-id="d5e96-151">Make an Outbound Call</span></span>
<span data-ttu-id="d5e96-152">我們可以建立簡易表單，以撥打我們選擇的號碼。</span><span class="sxs-lookup"><span data-stu-id="d5e96-152">Let's create a simple form that will place a call to a number we choose.</span></span> <span data-ttu-id="d5e96-153">開啟 `server.js`，並輸入下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="d5e96-153">Open up `server.js`, and enter the following code.</span></span> <span data-ttu-id="d5e96-154">請留意顯示 "CHANGE_ME" 的部分 - 請在該處放入您 Azure 網站的名稱：</span><span class="sxs-lookup"><span data-stu-id="d5e96-154">Note where it says "CHANGE_ME" - put the name of your azure website there:</span></span>

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

// Render an HTML user interface for the application's home page
app.get('/', (request, response) => response.render('index'));

// Handle the form POST to place a call
app.post('/call', (request, response) => {
  var client = twilio(accountSid, authToken);

  client.makeCall({
    // make a call to this number
    to:request.body.number,

    // Change to a Twilio number you bought - see:
    // https://www.twilio.com/console/phone-numbers/incoming
    from:'+15558675309',

    // A URL in our app which generates TwiML
    // Change "CHANGE_ME" to your app's name
    url:'https://CHANGE_ME.azurewebsites.net/outbound_call'
  }, () => {
      // Go back to the home page
      response.redirect('/');
  });
});

// Generate TwiML to handle an outbound call
app.post('/outbound_call', (request, response) => {
  var twiml = new twilio.TwimlResponse();

  // Say a message to the call's receiver
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

<span data-ttu-id="d5e96-155">接著，請建立名為 `views` 的目錄 - 在此目錄中，請以下列內容建立名為 `index.ejs` 的檔案：</span><span class="sxs-lookup"><span data-stu-id="d5e96-155">Next, create a directory called `views` - inside this directory, create a file named `index.ejs` with the following contents:</span></span>

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
      <input type="submit" value="Call the number above"/>
  </form>
</body>
</html>
```

<span data-ttu-id="d5e96-156">現在，將您的網站部署至 Azure，然後開啟您的首頁。</span><span class="sxs-lookup"><span data-stu-id="d5e96-156">Now, deploy your website to Azure and open your home.</span></span> <span data-ttu-id="d5e96-157">您應可在文字欄位中輸入電話號碼，並接聽您 Twilio 號碼的來電。</span><span class="sxs-lookup"><span data-stu-id="d5e96-157">You should be able to enter your phone number in the text field, and receive a call from your Twilio number!</span></span>

<a id="sendmessage"/>

## <a name="send-an-sms-message"></a><span data-ttu-id="d5e96-158">傳送簡訊</span><span class="sxs-lookup"><span data-stu-id="d5e96-158">Send an SMS Message</span></span>
<span data-ttu-id="d5e96-159">現在，我們要設定用以傳送簡訊的使用者介面和表單處理邏輯。</span><span class="sxs-lookup"><span data-stu-id="d5e96-159">Now, let's set up a user interface and form handling logic to send a text message.</span></span> <span data-ttu-id="d5e96-160">開啟 `server.js`，並在對 `app.post` 的最後一個呼叫之後新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="d5e96-160">Open up `server.js`, and add the following code after the last call to `app.post`:</span></span>

```javascript
app.post('/sms', (request, response) => {
  const client = twilio(accountSid, authToken);

  client.sendSms({
      // send a text to this number
      to:request.body.number,

      // A Twilio number you bought - see:
      // https://www.twilio.com/console/phone-numbers/incoming
      from:'+15558675309',

      // The body of the text message
      body: request.body.message

  }, () => {
      // Go back to the home page
      response.redirect('/');
  });
});
```

<span data-ttu-id="d5e96-161">在 `views/index.ejs` 中的第一個項目下新增其他資料表，以便提交號碼及簡訊：</span><span class="sxs-lookup"><span data-stu-id="d5e96-161">In `views/index.ejs`, add another form under the first one to submit a number and a text message:</span></span>

```html
<form action="/sms" method="POST">
  <input placeholder="Enter a phone number" name="number"/>
  <br/>
  <input placeholder="Enter a message to send" name="message"/>
  <br/>
  <input type="submit" value="Send text to the number above"/>
</form>
```

<span data-ttu-id="d5e96-162">將您的應用程式重新部署至 Azure，此時您應可提交該表單，並且將簡訊傳送給自己 (或是您所有的好友)！</span><span class="sxs-lookup"><span data-stu-id="d5e96-162">Re-deploy your application to Azure, and you should now be able to submit that form and send yourself (or any of your closest friends) a text message!</span></span>

<a id="nextsteps"/>

## <a name="next-steps"></a><span data-ttu-id="d5e96-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d5e96-163">Next Steps</span></span>
<span data-ttu-id="d5e96-164">現在，您已了解使用 node.js 和 Twilio 建置通訊應用程式的基本概念。</span><span class="sxs-lookup"><span data-stu-id="d5e96-164">You have now learned the basics of using node.js and Twilio to build apps that communicate.</span></span> <span data-ttu-id="d5e96-165">但前述範例僅只勾勒出 Twilio 和 node.js 功能的大致輪廓。</span><span class="sxs-lookup"><span data-stu-id="d5e96-165">But these examples barely scratch the surface of what's possible with Twilio and node.js.</span></span> <span data-ttu-id="d5e96-166">如需使用 Twilio 和 node.js 的詳細資訊，請參考下列資源：</span><span class="sxs-lookup"><span data-stu-id="d5e96-166">For more information using Twilio with node.js, check out the following resources:</span></span>

* <span data-ttu-id="d5e96-167">[正式模組文件][docs]</span><span class="sxs-lookup"><span data-stu-id="d5e96-167">[Official module docs][docs]</span></span>
* <span data-ttu-id="d5e96-168">[透過 node.js 應用程式使用 VoIP 的教學課程][voipnode]</span><span class="sxs-lookup"><span data-stu-id="d5e96-168">[Tutorial on VoIP with node.js applications][voipnode]</span></span>
* <span data-ttu-id="d5e96-169">[Votr - 使用 node.js 和 CouchDB 的即時簡訊投票應用程式 (三個單元)][votr]</span><span class="sxs-lookup"><span data-stu-id="d5e96-169">[Votr - a real-time SMS voting application with node.js and CouchDB (three parts)][votr]</span></span>
* <span data-ttu-id="d5e96-170">[在瀏覽器中使用 node.js 的配對程式設計][pair]</span><span class="sxs-lookup"><span data-stu-id="d5e96-170">[Pair programming in the browser with node.js][pair]</span></span>

<span data-ttu-id="d5e96-171">祝您在 Azure 上使用 node.js 和 Twilio 時能夠得心應手！</span><span class="sxs-lookup"><span data-stu-id="d5e96-171">We hope you love hacking node.js and Twilio on Azure!</span></span>

[purchase_phone]: https://www.twilio.com/console/phone-numbers/search
[twiml]: https://www.twilio.com/docs/api/twiml
[signup]: http://ahoy.twilio.com/azure
[azure_new_site]: app-service-web/app-service-web-get-started-nodejs.md
[twilio_console]: https://www.twilio.com/console
<span data-ttu-id="d5e96-172">[npm]: http://npmjs.org</span><span class="sxs-lookup"><span data-stu-id="d5e96-172">[npm]: http://npmjs.org</span></span>
[express]: http://expressjs.com
[voipnode]: http://www.twilio.com/blog/2013/04/introduction-to-twilio-client-with-node-js.html
[docs]: http://twilio.github.io/twilio-node/
[votr]: http://www.twilio.com/blog/2012/09/building-a-real-time-sms-voting-app-part-1-node-js-couchdb.html
[pair]: http://www.twilio.com/blog/2013/06/pair-programming-in-the-browser-with-twilio.html
[azure-admin-console]: ./media/partner-twilio-nodejs-how-to-use-voice-sms/twilio_1.png
