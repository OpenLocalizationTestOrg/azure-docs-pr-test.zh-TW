---
title: "aaaSend 推播通知 tooChrome 應用程式與 Azure 通知中心 |Microsoft 文件"
description: "了解如何 toouse Azure 通知中樞 toosend 推播通知 tooa Chrome 應用程式。"
services: notification-hubs
keywords: "行動推播通知,推播通知,推播通知,chrome 推播通知"
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 75d4ff59-d04a-455f-bd44-0130a68e641f
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-chrome
ms.devlang: JavaScript
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 7dec8ab02622563bc3730a2e96820da8932d22f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="send-push-notifications-toochrome-apps-with-azure-notification-hubs"></a><span data-ttu-id="8bf29-104">傳送推播通知 tooChrome 應用程式與 Azure 通知中心</span><span class="sxs-lookup"><span data-stu-id="8bf29-104">Send push notifications tooChrome apps with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

<span data-ttu-id="8bf29-105">本主題說明如何 toouse Azure 通知中樞 toosend 推播通知 tooa Chrome 應用程式，將會顯示 hello 內容 hello Google Chrome 瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="8bf29-105">This topic shows you how toouse Azure Notification Hubs toosend push notifications tooa Chrome App, which will be displayed within hello context of hello Google Chrome browser.</span></span> <span data-ttu-id="8bf29-106">在本教學課程中，我們將建立可使用 [Google 雲端通訊 (GCM)](https://developers.google.com/cloud-messaging/)接收推播通知的 Chrome 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8bf29-106">In this tutorial, we will create a Chrome app that receives push notifications by using [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/).</span></span> 

> [!NOTE]
> <span data-ttu-id="8bf29-107">toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8bf29-107">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="8bf29-108">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8bf29-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="8bf29-109">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F)。</span><span class="sxs-lookup"><span data-stu-id="8bf29-109">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).</span></span>
> 
> 

<span data-ttu-id="8bf29-110">hello 教學課程將引導您完成這些基本步驟 tooenable 推播通知：</span><span class="sxs-lookup"><span data-stu-id="8bf29-110">hello tutorial walks you through these basic steps tooenable push notifications:</span></span>

* [<span data-ttu-id="8bf29-111">啟用 Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="8bf29-111">Enable Google Cloud Messaging</span></span>](#register)
* [<span data-ttu-id="8bf29-112">設定您的通知中樞</span><span class="sxs-lookup"><span data-stu-id="8bf29-112">Configure your notification hub</span></span>](#configure-hub)
* [<span data-ttu-id="8bf29-113">連接您的應用程式 Chrome toohello 的通知中樞</span><span class="sxs-lookup"><span data-stu-id="8bf29-113">Connect your Chrome App toohello notification hub</span></span>](#connect-app)
* [<span data-ttu-id="8bf29-114">傳送推播通知 tooyour Chrome 應用程式</span><span class="sxs-lookup"><span data-stu-id="8bf29-114">Send a push notification tooyour Chrome App</span></span>](#send)
* [<span data-ttu-id="8bf29-115">其他功能與能力</span><span class="sxs-lookup"><span data-stu-id="8bf29-115">Additional functionality & capabilities</span></span>](#next-steps)

> [!NOTE]
> <span data-ttu-id="8bf29-116">Chrome 應用程式的推播通知不是泛型的瀏覽器中通知--它們是特定 toohello 瀏覽器擴充性模型 (請參閱[Chrome 應用程式的概觀]如需詳細資訊)。</span><span class="sxs-lookup"><span data-stu-id="8bf29-116">Chrome app push notifications are not generic in-browser notifications - they are specific toohello browser extensibility model (see [Chrome Apps Overview] for details).</span></span> <span data-ttu-id="8bf29-117">此外 toohello 桌面瀏覽器 Chrome 應用程式 （Android 和 iOS） 的行動裝置上透過執行 Apache Cordova。</span><span class="sxs-lookup"><span data-stu-id="8bf29-117">In addition toohello desktop browser, Chrome apps run on mobile (Android and iOS) through Apache Cordova.</span></span> <span data-ttu-id="8bf29-118">請參閱[行動裝置上的 Chrome 應用程式]toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="8bf29-118">See [Chrome Apps on Mobile] toolearn more.</span></span>
> 
> 

<span data-ttu-id="8bf29-119">因為設定 GCM 和 Azure 通知中心是適用於 Android 的相同 tooconfiguring [Google Cloud Messaging chrome]已被取代，hello 相同 GCM 現在支援 Android 裝置和 Chrome 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="8bf29-119">Configuring GCM and Azure Notification Hubs is identical tooconfiguring for Android, since [Google Cloud Messaging for Chrome] has been deprecated and hello same GCM now supports both Android devices and Chrome instances.</span></span>

## <span data-ttu-id="8bf29-120"><a id="register"></a>啟用 Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="8bf29-120"><a id="register"></a>Enable Google Cloud Messaging</span></span>
1. <span data-ttu-id="8bf29-121">瀏覽 toohello [Google 雲端主控台]網站，使用您的 Google 帳戶認證登入，然後按一下hello**建立專案** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8bf29-121">Navigate toohello [Google Cloud Console] website, sign in with your Google account credentials, and then click hello **Create Project** button.</span></span> <span data-ttu-id="8bf29-122">提供適當**專案名稱**，然後按一下hello**建立** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8bf29-122">Provide an appropriate **Project Name**, and then click hello **Create** button.</span></span>
   
       ![Google Cloud Console - Create Project][1]
2. <span data-ttu-id="8bf29-123">請記下 hello**專案編號**上 hello**專案**hello 專案您剛才建立的頁面。</span><span class="sxs-lookup"><span data-stu-id="8bf29-123">Make a note of hello **Project Number** on hello **Projects** page for hello project that you just created.</span></span> <span data-ttu-id="8bf29-124">您會使用這個 hello **GCM 寄件者識別碼**hello Chrome 應用程式 tooregister GCM 使用中。</span><span class="sxs-lookup"><span data-stu-id="8bf29-124">You will use this as hello **GCM Sender ID** in hello Chrome App tooregister with GCM.</span></span>
   
       ![Google Cloud Console - Project Number][2]
3. <span data-ttu-id="8bf29-125">Hello 左窗格中，按一下  **Api & auth**，然後向下捲動並按一下 hello 切換 tooenable**適用於 Android 的 Google Cloud Messaging**。</span><span class="sxs-lookup"><span data-stu-id="8bf29-125">In hello left pane, click **APIs & auth**, and then scroll down and click hello toggle tooenable **Google Cloud Messaging for Android**.</span></span> <span data-ttu-id="8bf29-126">您不需要 tooenable **Google Cloud Messaging chrome**。</span><span class="sxs-lookup"><span data-stu-id="8bf29-126">You don't have tooenable **Google Cloud Messaging for Chrome**.</span></span>
   
       ![Google Cloud Console - Server Key][3]
4. <span data-ttu-id="8bf29-127">在 hello 左窗格中，按一下 **認證** > **建立新的金鑰** > **伺服器金鑰** > **建立**.</span><span class="sxs-lookup"><span data-stu-id="8bf29-127">In hello left pane, click **Credentials** > **Create New Key** > **Server Key** > **Create**.</span></span>
   
       ![Google Cloud Console - Credentials][4]
5. <span data-ttu-id="8bf29-128">請記下 hello 伺服器**API 金鑰**。</span><span class="sxs-lookup"><span data-stu-id="8bf29-128">Make a note of hello server **API Key**.</span></span> <span data-ttu-id="8bf29-129">您會設定此通知中樞的 下一步，tooenable 中它 toosend 推播通知 tooGCM。</span><span class="sxs-lookup"><span data-stu-id="8bf29-129">You will configure this in your notification hub next, tooenable it toosend push notifications tooGCM.</span></span>
   
       ![Google Cloud Console - API Key][5]

## <span data-ttu-id="8bf29-130"><a id="configure-hub"></a>設定您的通知中樞</span><span class="sxs-lookup"><span data-stu-id="8bf29-130"><a id="configure-hub"></a>Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="8bf29-131">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="8bf29-131">&emsp;&emsp;6.</span></span>   <span data-ttu-id="8bf29-132">在 hello**設定**刀鋒視窗中，選取**Notification Services**然後**Google (GCM)**。</span><span class="sxs-lookup"><span data-stu-id="8bf29-132">In hello **Settings** blade, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="8bf29-133">輸入 hello API 金鑰，並儲存。</span><span class="sxs-lookup"><span data-stu-id="8bf29-133">Enter hello API key and save.</span></span>

&emsp;&emsp;![Azure 通知中樞 - Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

## <span data-ttu-id="8bf29-135"><a id="connect-app"></a>連接您的應用程式 Chrome toohello 的通知中樞</span><span class="sxs-lookup"><span data-stu-id="8bf29-135"><a id="connect-app"></a>Connect your Chrome App toohello notification hub</span></span>
<span data-ttu-id="8bf29-136">您的通知中樞現在是設定的 toowork 與 GCM，而且您擁有 hello 的連接字串 tooregister 應用程式 tooboth 接收和傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="8bf29-136">Your notification hub is now configured toowork with GCM, and you have hello connection strings tooregister your app tooboth receive and send push notifications.</span></span> <span data-ttu-id="8bf29-137">LK</span><span class="sxs-lookup"><span data-stu-id="8bf29-137">LK</span></span>

### <a name="create-a-new-chrome-app"></a><span data-ttu-id="8bf29-138">建立新的 Chrome 應用程式</span><span class="sxs-lookup"><span data-stu-id="8bf29-138">Create a new Chrome App</span></span>
<span data-ttu-id="8bf29-139">以下的 hello 範例根據 hello [Chrome 應用程式 GCM 範例]使用 hello 建議的方式 toocreate Chrome 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8bf29-139">hello sample below is based on hello [Chrome App GCM Sample] and uses hello recommended way toocreate a Chrome App.</span></span> <span data-ttu-id="8bf29-140">我們將會反白顯示 hello 步驟特別相關的 tooAzure 通知中樞。</span><span class="sxs-lookup"><span data-stu-id="8bf29-140">We will highlight hello steps specifically related tooAzure Notification Hubs.</span></span> 

> [!NOTE]
> <span data-ttu-id="8bf29-141">我們建議您從這個 Chrome 應用程式下載 hello 來源[Chrome 應用程式通知中樞範例]。</span><span class="sxs-lookup"><span data-stu-id="8bf29-141">We recommend that you download hello source for this Chrome App from [Chrome App Notification Hub Sample].</span></span>
> 
> 

<span data-ttu-id="8bf29-142">JavaScript 中，透過建立 hello Chrome 應用程式，您可以使用任何慣用的文字編輯器來建立它。</span><span class="sxs-lookup"><span data-stu-id="8bf29-142">hello Chrome App is created via JavaScript, and you can use any of your preferred word editors for creating it.</span></span> <span data-ttu-id="8bf29-143">此 Chrome 應用程式如下所示。</span><span class="sxs-lookup"><span data-stu-id="8bf29-143">Below is what this Chrome App will look like.</span></span>

![Google Chrome 應用程式][15]

1. <span data-ttu-id="8bf29-145">建立資料夾，並將其命名為 `ChromePushApp`。</span><span class="sxs-lookup"><span data-stu-id="8bf29-145">Create a folder and name it `ChromePushApp`.</span></span> <span data-ttu-id="8bf29-146">當然，hello 名稱是任意-如果您將檔案命名不同的項目，請確定您所需的 hello 程式碼區段中的 hello 路徑來取代。</span><span class="sxs-lookup"><span data-stu-id="8bf29-146">Of course, hello name is arbitrary - if you name it something different, make sure you substitute hello path in hello required code segments.</span></span>
2. <span data-ttu-id="8bf29-147">下載 hello [crypto js 程式庫]hello hello 第二個步驟中所建立的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="8bf29-147">Download hello [crypto-js library] in hello folder you created in hello second step.</span></span> <span data-ttu-id="8bf29-148">此程式庫資料夾將包含兩個子資料夾：`components` 和 `rollups`。</span><span class="sxs-lookup"><span data-stu-id="8bf29-148">This library folder will contain two subfolders: `components` and `rollups`.</span></span>
3. <span data-ttu-id="8bf29-149">建立 `manifest.json` 檔案。</span><span class="sxs-lookup"><span data-stu-id="8bf29-149">Create a `manifest.json` file.</span></span> <span data-ttu-id="8bf29-150">所有 Chrome 應用程式都都由資訊清單檔案，其中包含 hello 應用程式中繼資料和最重要的是，所有已授與權限 toohello 應用程式時 hello 使用者進行安裝。</span><span class="sxs-lookup"><span data-stu-id="8bf29-150">All Chrome Apps are backed by a manifest file that contains hello app metadata and, most importantly, all permissions that are granted toohello app when hello user installs it.</span></span>
   
        {
          "name": "NH-GCM Notifications",
          "description": "Chrome platform app.",
          "manifest_version": 2,
          "version": "0.1",
          "app": {
            "background": {
              "scripts": ["background.js"]
            }
          },
          "permissions": ["gcm", "storage", "notifications", "https://*.servicebus.windows.net/*"],
          "icons": { "128": "gcm_128.png" }
        }
   
    <span data-ttu-id="8bf29-151">請注意 hello`permissions`元素，其指定此 Chrome 應用程式將會從 GCM 可以 tooreceive 推播通知。</span><span class="sxs-lookup"><span data-stu-id="8bf29-151">Notice hello `permissions` element, which specifies that this Chrome App will be able tooreceive push notifications from GCM.</span></span> <span data-ttu-id="8bf29-152">它也必須指定 hello 而 hello Chrome 應用程式將於其中進行 REST 呼叫 tooregister Azure 通知中樞 URI。</span><span class="sxs-lookup"><span data-stu-id="8bf29-152">It must also specify hello Azure Notification Hubs URI where hello Chrome App will make a REST call tooregister.</span></span>
    <span data-ttu-id="8bf29-153">我們的範例應用程式也會使用的圖示檔`gcm_128.png`，您會發現在 hello 來源 hello 原始 GCM 範例中會重複使用。</span><span class="sxs-lookup"><span data-stu-id="8bf29-153">Our sample app also uses an icon file, `gcm_128.png`, that you will find at hello source that's reused from hello original GCM sample.</span></span> <span data-ttu-id="8bf29-154">您可以替換符合 hello 任何映像[圖示準則](https://developer.chrome.com/apps/manifest/icons)。</span><span class="sxs-lookup"><span data-stu-id="8bf29-154">You can substitute it for any image that fits hello [icon criteria](https://developer.chrome.com/apps/manifest/icons).</span></span>
4. <span data-ttu-id="8bf29-155">建立一個叫做檔案`background.js`以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="8bf29-155">Create a file called `background.js` with hello following code:</span></span>
   
        // Returns a new notification ID used in hello notification.
        function getNotificationId() {
          var id = Math.floor(Math.random() * 9007199254740992) + 1;
          return id.toString();
        }
   
        function messageReceived(message) {
          // A message is an object with a data property that
          // consists of key-value pairs.
   
          // Concatenate all key-value pairs tooform a display string.
          var messageString = "";
          for (var key in message.data) {
            if (messageString != "")
              messageString += ", "
            messageString += key + ":" + message.data[key];
          }
          console.log("Message received: " + messageString);
   
          // Pop up a notification tooshow hello GCM message.
          chrome.notifications.create(getNotificationId(), {
            title: 'GCM Message',
            iconUrl: 'gcm_128.png',
            type: 'basic',
            message: messageString
          }, function() {});
        }
   
        var registerWindowCreated = false;
   
        function firstTimeRegistration() {
          chrome.storage.local.get("registered", function(result) {
   
            registerWindowCreated = true;
            chrome.app.window.create(
              "register.html",
              {  width: 520,
                 height: 500,
                 frame: 'chrome'
              },
              function(appWin) {}
            );
          });
        }
   
        // Set up a listener for GCM message event.
        chrome.gcm.onMessage.addListener(messageReceived);
   
        // Set up listeners tootrigger hello first-time registration.
        chrome.runtime.onInstalled.addListener(firstTimeRegistration);
        chrome.runtime.onStartup.addListener(firstTimeRegistration);
   
    <span data-ttu-id="8bf29-156">這是快顯 hello Chrome 應用程式視窗 HTML 的 hello 檔案 (**register.html**)，並且定義 hello 處理常式**messageReceived** toohandle hello 傳入推播通知。</span><span class="sxs-lookup"><span data-stu-id="8bf29-156">This is hello file that pops up hello Chrome App window HTML (**register.html**) and also defines hello handler **messageReceived** toohandle hello incoming push notification.</span></span>
5. <span data-ttu-id="8bf29-157">建立一個叫做檔案`register.html`-這會定義 hello hello Chrome 應用程式的 UI。</span><span class="sxs-lookup"><span data-stu-id="8bf29-157">Create a file called `register.html` - this defines hello UI of hello Chrome App.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="8bf29-158">此範例使用 **CryptoJS v3.1.2**。</span><span class="sxs-lookup"><span data-stu-id="8bf29-158">This sample uses **CryptoJS v3.1.2**.</span></span> <span data-ttu-id="8bf29-159">如果您已經下載 hello 文件庫的另一個版本，請確定您正確替代 hello 中的 hello 版本`src`路徑。</span><span class="sxs-lookup"><span data-stu-id="8bf29-159">If you downloaded another version of hello library, make sure you properly substitute hello version in hello `src` path.</span></span>
   > 
   > 
   
        <html>
   
        <head>
        <title>GCM Registration</title>
        <script src="register.js"></script>
        <script src="CryptoJS v3.1.2/rollups/hmac-sha256.js"></script>
        <script src="CryptoJS v3.1.2/components/enc-base64-min.js"></script>
        </head>
   
        <body>
   
        Sender ID:<br/><input id="senderId" type="TEXT" size="20"><br/>
        <button id="registerWithGCM">Register with GCM</button>
        <br/>
        <br/>
        <br/>
   
        Notification Hub Name:<br/><input id="hubName" type="TEXT" style="width:400px"><br/><br/>
        Connection String:<br/><textarea id="connectionString" type="TEXT" style="width:400px;height:60px"></textarea>
   
        <br/>
   
        <button id="registerWithNH" disabled="true">Register with Azure Notification Hubs</button>
   
        <br/>
        <br/>
   
        <textarea id="console" type="TEXT" readonly style="width:500px;height:200px;background-color:#e5e5e5;padding:5px"></textarea>
   
        </body>
   
        </html>
6. <span data-ttu-id="8bf29-160">建立一個叫做檔案`register.js`與 hello 的下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="8bf29-160">Create a file called `register.js` with hello code below.</span></span> <span data-ttu-id="8bf29-161">此檔案會指定 hello 指令碼後置`register.html`。</span><span class="sxs-lookup"><span data-stu-id="8bf29-161">This file specifies hello script behind `register.html`.</span></span> <span data-ttu-id="8bf29-162">Chrome 應用程式不允許內嵌執行，因此您 ui 有 toocreate 個別備份指令碼。</span><span class="sxs-lookup"><span data-stu-id="8bf29-162">Chrome Apps do not allow inline execution, so you have toocreate a separate backing script for your UI.</span></span>
   
        var registrationId = "";
        var hubName        = "", connectionString = "";
        var originalUri    = "", targetUri = "", endpoint = "", sasKeyName = "", sasKeyValue = "", sasToken = "";
   
        window.onload = function() {
           document.getElementById("registerWithGCM").onclick = registerWithGCM;  
           document.getElementById("registerWithNH").onclick = registerWithNH;
           updateLog("You have not registered yet. Please provider sender ID and register with GCM and then with  Notification Hubs.");
        }
   
        function updateLog(status) {
          currentStatus = document.getElementById("console").innerHTML;
          if (currentStatus != "") {
            currentStatus = currentStatus + "\n\n";
          }
   
          document.getElementById("console").innerHTML = currentStatus  + status;
        }
   
        function registerWithGCM() {
          var senderId = document.getElementById("senderId").value.trim();
          chrome.gcm.register([senderId], registerCallback);
   
          // Prevent register button from being clicked again before hello registration finishes.
          document.getElementById("registerWithGCM").disabled = true;
        }
   
        function registerCallback(regId) {
          registrationId = regId;
          document.getElementById("registerWithGCM").disabled = false;
   
          if (chrome.runtime.lastError) {
            // When hello registration fails, handle hello error and retry the
            // registration later.
            updateLog("Registration failed: " + chrome.runtime.lastError.message);
            return;
          }
   
          updateLog("Registration with GCM succeeded.");
          document.getElementById("registerWithNH").disabled = false;
   
          // Mark that hello first-time registration is done.
          chrome.storage.local.set({registered: true});
        }
   
        function registerWithNH() {
          hubName = document.getElementById("hubName").value.trim();
          connectionString = document.getElementById("connectionString").value.trim();
          splitConnectionString();
          generateSaSToken();
          sendNHRegistrationRequest();
        }
   
        // From http://msdn.microsoft.com/library/dn495627.aspx
        function splitConnectionString()
        {
          var parts = connectionString.split(';');
          if (parts.length != 3)
          throw "Error parsing connection string";
   
          parts.forEach(function(part) {
            if (part.indexOf('Endpoint') == 0) {
            endpoint = 'https' + part.substring(11);
            } else if (part.indexOf('SharedAccessKeyName') == 0) {
            sasKeyName = part.substring(20);
            } else if (part.indexOf('SharedAccessKey') == 0) {
            sasKeyValue = part.substring(16);
            }
          });
   
          originalUri = endpoint + hubName;
        }
   
        function generateSaSToken()
        {
          targetUri = encodeURIComponent(originalUri.toLowerCase()).toLowerCase();
          var expiresInMins = 10; // 10 minute expiration
   
          // Set expiration in seconds.
          var expireOnDate = new Date();
          expireOnDate.setMinutes(expireOnDate.getMinutes() + expiresInMins);
          var expires = Date.UTC(expireOnDate.getUTCFullYear(), expireOnDate
            .getUTCMonth(), expireOnDate.getUTCDate(), expireOnDate
            .getUTCHours(), expireOnDate.getUTCMinutes(), expireOnDate
            .getUTCSeconds()) / 1000;
          var tosign = targetUri + '\n' + expires;
   
          // Using CryptoJS.
          var signature = CryptoJS.HmacSHA256(tosign, sasKeyValue);
          var base64signature = signature.toString(CryptoJS.enc.Base64);
          var base64UriEncoded = encodeURIComponent(base64signature);
   
          // Construct authorization string.
          sasToken = "SharedAccessSignature sr=" + targetUri + "&sig="
                          + base64UriEncoded + "&se=" + expires + "&skn=" + sasKeyName;
        }
   
        function sendNHRegistrationRequest()
        {
          var registrationPayload =
          "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
          "<entry xmlns=\"http://www.w3.org/2005/Atom\">" +
              "<content type=\"application/xml\">" +
                  "<GcmRegistrationDescription xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/netservices/2010/10/servicebus/connect\">" +
                      "<GcmRegistrationId>{GCMRegistrationId}</GcmRegistrationId>" +
                  "</GcmRegistrationDescription>" +
              "</content>" +
          "</entry>";
   
          // Update hello payload with hello registration ID obtained earlier.
          registrationPayload = registrationPayload.replace("{GCMRegistrationId}", registrationId);
   
          var url = originalUri + "/registrations/?api-version=2014-09";
          var client = new XMLHttpRequest();
   
          client.onload = function () {
            if (client.readyState == 4) {
              if (client.status == 200) {
                updateLog("Notification Hub Registration succesful!");
                updateLog(client.responseText);
              } else {
                updateLog("Notification Hub Registration did not succeed!");
                updateLog("HTTP Status: " + client.status + " : " + client.statusText);
                updateLog("HTTP Response: " + "\n" + client.responseText);
              }
            }
          };
   
          client.onerror = function () {
                updateLog("ERROR - Notification Hub Registration did not succeed!");
          }
   
          client.open("POST", url, true);
          client.setRequestHeader("Content-Type", "application/atom+xml;type=entry;charset=utf-8");
          client.setRequestHeader("Authorization", sasToken);
          client.setRequestHeader("x-ms-version", "2014-09");
   
          try {
              client.send(registrationPayload);
          }
          catch(err) {
              updateLog(err.message);
          }
        }
   
    <span data-ttu-id="8bf29-163">上述指令碼的 hello 具有下列索引鍵參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="8bf29-163">hello above script has hello following key parameters:</span></span>
   
   * <span data-ttu-id="8bf29-164">**window.onload** hello UI 上定義的 hello 兩個按鈕的 hello 按鈕 click 事件。</span><span class="sxs-lookup"><span data-stu-id="8bf29-164">**window.onload** defines hello button-click events of hello two buttons on hello UI.</span></span> <span data-ttu-id="8bf29-165">其中一個登錄 GCM，並 hello 其他使用 GCM tooregister 與 Azure 通知中心註冊後，會傳回的 hello 註冊 ID。</span><span class="sxs-lookup"><span data-stu-id="8bf29-165">One registers with GCM, and hello other uses hello registration ID that's returned after registration with GCM tooregister with Azure Notification Hubs.</span></span>
   * <span data-ttu-id="8bf29-166">**updateLog**是 hello 函式，讓我們 toohandle 簡單的記錄功能。</span><span class="sxs-lookup"><span data-stu-id="8bf29-166">**updateLog** is hello function that allows us toohandle simple logging capabilities.</span></span>
   * <span data-ttu-id="8bf29-167">**registerWithGCM** hello 第一個按鈕 click 處理常式，使得 hello`chrome.gcm.register`呼叫 tooGCM tooregister hello 目前 Chrome 應用程式的執行個體。</span><span class="sxs-lookup"><span data-stu-id="8bf29-167">**registerWithGCM** is hello first button-click handler, which makes hello `chrome.gcm.register` call tooGCM tooregister hello current Chrome App instance.</span></span>
   * <span data-ttu-id="8bf29-168">**registerCallback**是 hello hello GCM 註冊呼叫傳回時被呼叫的回呼函式。</span><span class="sxs-lookup"><span data-stu-id="8bf29-168">**registerCallback** is hello callback function that gets called when hello GCM registration call returns.</span></span>
   * <span data-ttu-id="8bf29-169">**registerWithNH** hello 第二個按鈕 click 處理常式，以使用通知中樞註冊。</span><span class="sxs-lookup"><span data-stu-id="8bf29-169">**registerWithNH** is hello second button-click handler, which registers with Notification Hubs.</span></span> <span data-ttu-id="8bf29-170">它會取得`hubName`和`connectionString`（hello 使用者已指定） 和美工 hello 通知中樞註冊 REST API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="8bf29-170">It gets `hubName` and `connectionString` (which hello user has specified) and crafts hello Notification Hubs Registration REST API call.</span></span>
   * <span data-ttu-id="8bf29-171">**splitConnectionString**和**generateSaSToken**是代表 hello 的 SaS 權杖的建立程序必須用於所有 REST API 呼叫的 JavaScript 實作的協助程式。</span><span class="sxs-lookup"><span data-stu-id="8bf29-171">**splitConnectionString** and **generateSaSToken** are helpers that represent hello JavaScript implementation of a SaS token creation process, that must be used in all REST API calls.</span></span> <span data-ttu-id="8bf29-172">如需詳細資訊，請參閱 [一般概念](http://msdn.microsoft.com/library/dn495627.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8bf29-172">For more information, see [Common Concepts](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
   * <span data-ttu-id="8bf29-173">**sendNHRegistrationRequest** hello 函式，讓 HTTP REST 呼叫 tooAzure 通知中樞。</span><span class="sxs-lookup"><span data-stu-id="8bf29-173">**sendNHRegistrationRequest** is hello function that makes a HTTP REST call tooAzure Notification Hubs.</span></span>
   * <span data-ttu-id="8bf29-174">**registrationPayload**定義 hello 註冊 XML 裝載。</span><span class="sxs-lookup"><span data-stu-id="8bf29-174">**registrationPayload** defines hello registration XML payload.</span></span> <span data-ttu-id="8bf29-175">如需詳細資訊，請參閱 [建立註冊 NH REST API]。</span><span class="sxs-lookup"><span data-stu-id="8bf29-175">For more information, see [Create Registration NH REST API].</span></span> <span data-ttu-id="8bf29-176">我們會以我們收到來自 GCM 更新中的 hello 註冊 ID。</span><span class="sxs-lookup"><span data-stu-id="8bf29-176">We update hello registration ID in it with what we received from GCM.</span></span>
   * <span data-ttu-id="8bf29-177">**用戶端**的執行個體**XMLHttpRequest** ，我們會使用 toomake hello HTTP POST 要求。</span><span class="sxs-lookup"><span data-stu-id="8bf29-177">**client** is an instance of **XMLHttpRequest** that we use toomake hello HTTP POST request.</span></span> <span data-ttu-id="8bf29-178">請注意，我們會更新 hello`Authorization`具有標頭`sasToken`。</span><span class="sxs-lookup"><span data-stu-id="8bf29-178">Note that we update hello `Authorization` header with `sasToken`.</span></span> <span data-ttu-id="8bf29-179">成功完成此呼叫後，即會向 Azure 通知中樞註冊此 Chrome 應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="8bf29-179">Successful completion of this call will register this Chrome App instance with Azure Notification Hubs.</span></span>

<span data-ttu-id="8bf29-180">hello 這個專案的整個資料夾結構看起來應該像這樣： ![Google Chrome 應用程式的資料夾結構][21]</span><span class="sxs-lookup"><span data-stu-id="8bf29-180">hello overall folder structure for this project should resemble this: ![Google Chrome App - Folder Structure][21]</span></span>

### <a name="set-up-and-test-your-chrome-app"></a><span data-ttu-id="8bf29-181">設定和測試 Chrome 應用程式</span><span class="sxs-lookup"><span data-stu-id="8bf29-181">Set up and test your Chrome App</span></span>
1. <span data-ttu-id="8bf29-182">開啟 Chrome 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="8bf29-182">Open your Chrome browser.</span></span> <span data-ttu-id="8bf29-183">開啟 [Chrome 擴充功能]，並啟用 [開發人員模式]。</span><span class="sxs-lookup"><span data-stu-id="8bf29-183">Open **Chrome extensions** and enable **Developer mode**.</span></span>
   
       ![Google Chrome - Enable Developer Mode][16]
2. <span data-ttu-id="8bf29-184">按一下**解除封裝的擴充功能載入**並瀏覽 toohello 資料夾建立 hello 檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="8bf29-184">Click **Load unpacked extension** and navigate toohello folder where you created hello files.</span></span> <span data-ttu-id="8bf29-185">您也可以使用 hello **Chrome 應用程式 （& s) 延伸模組的開發人員工具**。</span><span class="sxs-lookup"><span data-stu-id="8bf29-185">You can also optionally use hello **Chrome Apps & Extensions Developer Tool**.</span></span> <span data-ttu-id="8bf29-186">此工具是 Chrome 中的應用程式本身 （從 hello Chrome Web Store 安裝），並提供進階偵錯功能 Chrome 應用程式開發。</span><span class="sxs-lookup"><span data-stu-id="8bf29-186">This tool is a Chrome App in itself (installed from hello Chrome Web Store) and provides advanced debugging capabilities for your Chrome App development.</span></span>
   
       ![Google Chrome - Load Unpacked Extension][17]
3. <span data-ttu-id="8bf29-187">如果沒有發生任何錯誤，建立 hello Chrome 應用程式，您會看到顯示 Chrome 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8bf29-187">If hello Chrome App is created without any errors, then you will see your Chrome App show up.</span></span>
   
       ![Google Chrome - Chrome App Display][18]
4. <span data-ttu-id="8bf29-188">輸入 hello**專案編號**，則您稍早取得從 hello **Google 雲端主控台**為 hello 寄件者識別碼，然後按一下**GCM 註冊**。</span><span class="sxs-lookup"><span data-stu-id="8bf29-188">Enter hello **Project Number** that you got earlier from hello **Google Cloud Console** as hello sender ID, and click **Register with GCM**.</span></span> <span data-ttu-id="8bf29-189">您必須查看 hello 訊息**GCM 成功的註冊。**</span><span class="sxs-lookup"><span data-stu-id="8bf29-189">You must see hello message **Registration with GCM succeeded.**</span></span>
   
       ![Google Chrome - Chrome App Customization][19]
5. <span data-ttu-id="8bf29-190">輸入您**通知中樞名稱**和 hello **DefaultListenSharedAccessSignature**您取得的較舊版本，hello 網站，然後按一下**向 Azure 通知中樞**.</span><span class="sxs-lookup"><span data-stu-id="8bf29-190">Enter your **Notification Hub Name** and hello **DefaultListenSharedAccessSignature** that you obtained from hello portal earlier, and click **Register with Azure Notification Hub**.</span></span> <span data-ttu-id="8bf29-191">您必須查看 hello 訊息**通知中樞註冊成功 ！**</span><span class="sxs-lookup"><span data-stu-id="8bf29-191">You must see hello message **Notification Hub Registration successful!**</span></span> <span data-ttu-id="8bf29-192">而且識別碼 hello hello 註冊回應，其中包含 hello Azure 通知中樞註冊詳細資料。</span><span class="sxs-lookup"><span data-stu-id="8bf29-192">and hello details of hello registration response, which contains hello Azure Notification Hubs registration ID.</span></span>
   
       ![Google Chrome - Specify Notification Hub Details][20]  

## <span data-ttu-id="8bf29-193"><a name="send"></a>傳送通知 tooyour Chrome 應用程式</span><span class="sxs-lookup"><span data-stu-id="8bf29-193"><a name="send"></a>Send a notification tooyour Chrome App</span></span>
<span data-ttu-id="8bf29-194">為了進行測試，我們會使用 .NET 主控台應用程式傳送 Chrome 推播通知。</span><span class="sxs-lookup"><span data-stu-id="8bf29-194">For testing purposes, we will send Chrome push notifications by using a .NET console application.</span></span> 

> [!NOTE]
> <span data-ttu-id="8bf29-195">您可以透過公用 <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST 介面</a>，使用通知中樞從任何後端傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="8bf29-195">You can send push notifications with Notification Hubs from any backend via our public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span></span> <span data-ttu-id="8bf29-196">如需其他跨平台範例，請查看我們的 [說明文件入口網站](https://azure.microsoft.com/documentation/services/notification-hubs/) 。</span><span class="sxs-lookup"><span data-stu-id="8bf29-196">Check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/) for more cross-platform examples.</span></span>
> 
> 

1. <span data-ttu-id="8bf29-197">在 Visual Studio 中，從 hello**檔案**功能表上，選取**新增**然後**專案**。</span><span class="sxs-lookup"><span data-stu-id="8bf29-197">In Visual Studio, from hello **File** menu, select **New** and then **Project**.</span></span> <span data-ttu-id="8bf29-198">在 Visual C# 下方，按一下 Windows 和 主控台應用程式，然後按一下確定。</span><span class="sxs-lookup"><span data-stu-id="8bf29-198">Under **Visual C#**, click **Windows** and **Console Application**, and then click **OK**.</span></span>  <span data-ttu-id="8bf29-199">這會建立新的主控台應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="8bf29-199">This creates a new console application project.</span></span>
2. <span data-ttu-id="8bf29-200">從 hello**工具**功能表上，按一下 **程式庫套件管理員**然後**Package Manager Console**。</span><span class="sxs-lookup"><span data-stu-id="8bf29-200">From hello **Tools** menu, click **Library Package Manager** and then **Package Manager Console**.</span></span> <span data-ttu-id="8bf29-201">這會顯示 hello Package Manager Console。</span><span class="sxs-lookup"><span data-stu-id="8bf29-201">This displays hello Package Manager Console.</span></span>
3. <span data-ttu-id="8bf29-202">在 hello 主控台視窗中，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="8bf29-202">In hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
       This adds a reference toohello Azure Service Bus SDK with hello <a href="http://nuget.org/packages/  WindowsAzure.ServiceBus/">WindowsAzure.ServiceBus NuGet package</a>.
4. <span data-ttu-id="8bf29-203">開啟`Program.cs`並加入下列 hello`using`陳述式：</span><span class="sxs-lookup"><span data-stu-id="8bf29-203">Open `Program.cs` and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="8bf29-204">在 hello`Program`類別中，新增下列方法 hello:</span><span class="sxs-lookup"><span data-stu-id="8bf29-204">In hello `Program` class, add hello following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            String message = "{\"data\":{\"message\":\"Hello Chrome from Azure Notification Hubs\"}}";
            await hub.SendGcmNativeNotificationAsync(message);
        }
   
       Make sure tooreplace hello `<hub name>` placeholder with hello name of hello notification hub that appears in hello [portal](https://portal.azure.com) in your Notification Hub blade. Also, replace hello connection string placeholder with hello connection string called `DefaultFullSharedAccessSignature` that you obtained in hello notification hub configuration section.
   
   > [!NOTE]
   > <span data-ttu-id="8bf29-205">請確定您使用連接字串 hello**完整**不存取**接聽**存取。</span><span class="sxs-lookup"><span data-stu-id="8bf29-205">Make sure that you use hello connection string with **Full** access, not **Listen** access.</span></span> <span data-ttu-id="8bf29-206">hello**接聽**存取連接字串不授與權限 toosend 推播通知。</span><span class="sxs-lookup"><span data-stu-id="8bf29-206">hello **Listen** access connection string does not grant permissions toosend push notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="8bf29-207">新增 hello 下列呼叫 hello`Main`方法：</span><span class="sxs-lookup"><span data-stu-id="8bf29-207">Add hello following calls in hello `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="8bf29-208">請確定 Chrome 正在執行，並執行 hello 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="8bf29-208">Make sure that Chrome is running, and run hello console application.</span></span>
8. <span data-ttu-id="8bf29-209">您應該會看見 hello 下列顯桌面上的通知。</span><span class="sxs-lookup"><span data-stu-id="8bf29-209">You should see hello following notification pop up on your desktop.</span></span>
   
       ![Google Chrome - Notification][13]
9. <span data-ttu-id="8bf29-210">您也可以查看您的通知 （在 Windows) 使用 hello 工作列中的 hello Chrome 通知視窗 Chrome 正在執行時。</span><span class="sxs-lookup"><span data-stu-id="8bf29-210">You can also see all your notifications by using hello Chrome Notifications window in hello taskbar (in Windows) when Chrome is running.</span></span>
   
       ![Google Chrome - Notifications List][14]

> [!NOTE]
> <span data-ttu-id="8bf29-211">您不需要 toohave hello Chrome 應用程式執行中或在 hello 瀏覽器中開啟 （但必須執行 hello Chrome 瀏覽器本身）。</span><span class="sxs-lookup"><span data-stu-id="8bf29-211">You don't need toohave hello Chrome App running or open in hello browser (though hello Chrome browser itself must be running).</span></span> <span data-ttu-id="8bf29-212">您也可以取得您的通知的彙總的檢視 hello Chrome 通知視窗中。</span><span class="sxs-lookup"><span data-stu-id="8bf29-212">You also get a consolidated view of all your notifications in hello Chrome Notifications window.</span></span>
> 
> 

## <span data-ttu-id="8bf29-213"><a name="next-steps"> </a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="8bf29-213"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="8bf29-214">請在 [通知中樞概觀]中進一步了解通知中樞。</span><span class="sxs-lookup"><span data-stu-id="8bf29-214">Learn more about Notification Hubs in [Notification Hubs Overview].</span></span>

<span data-ttu-id="8bf29-215">tootarget 特定使用者，請參閱 toohello [Azure 通知中樞通知使用者]教學課程。</span><span class="sxs-lookup"><span data-stu-id="8bf29-215">tootarget specific users, refer toohello [Azure Notification Hubs Notify Users] tutorial.</span></span> 

<span data-ttu-id="8bf29-216">如果您希望 toosegment 使用者感興趣的群組，您可以依照 hello [Azure 通知中心最新消息]教學課程。</span><span class="sxs-lookup"><span data-stu-id="8bf29-216">If you want toosegment your users by interest groups, you can follow hello [Azure Notification Hubs breaking news] tutorial.</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-chrome-get-started/GoogleConsoleCreateProject.PNG
[2]: ./media/notification-hubs-chrome-get-started/GoogleProjectNumber.png
[3]: ./media/notification-hubs-chrome-get-started/EnableGCM.png
[4]: ./media/notification-hubs-chrome-get-started/CreateServerKey.png
[5]: ./media/notification-hubs-chrome-get-started/ServerKey.png
[6]: ./media/notification-hubs-chrome-get-started/CreateNH.png
[7]: ./media/notification-hubs-chrome-get-started/NHNamespace.png
[8]: ./media/notification-hubs-chrome-get-started/NamespaceConfigure.png
[9]: ./media/notification-hubs-chrome-get-started/NHConfigure.png
[10]: ./media/notification-hubs-chrome-get-started/NHConfigureGCM.png
[11]: ./media/notification-hubs-chrome-get-started/NHDashboard.png
[12]: ./media/notification-hubs-chrome-get-started/NHConnString.png
[13]: ./media/notification-hubs-chrome-get-started/ChromeNotification.png
[14]: ./media/notification-hubs-chrome-get-started/ChromeNotificationWindow.png
[15]: ./media/notification-hubs-chrome-get-started/ChromeApp.png
[16]: ./media/notification-hubs-chrome-get-started/ChromeExtensions.png
[17]: ./media/notification-hubs-chrome-get-started/ChromeLoadExtension.png
[18]: ./media/notification-hubs-chrome-get-started/ChromeAppLoaded.png
[19]: ./media/notification-hubs-chrome-get-started/ChromeAppGCM.png
[20]: ./media/notification-hubs-chrome-get-started/ChromeAppNH.png
[21]: ./media/notification-hubs-chrome-get-started/FinalFolderView.png

<!-- URLs. -->
[Chrome 應用程式通知中樞範例]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToChromeApps
[Google 雲端主控台]: http://cloud.google.com/console
[Azure Classic Portal]: https://manage.windowsazure.com/
[通知中樞概觀]: notification-hubs-push-notification-overview.md
[Chrome 應用程式的概觀]: https://developer.chrome.com/apps/about_apps
[Chrome 應用程式 GCM 範例]: https://github.com/GoogleChrome/chrome-app-samples/tree/master/samples/gcm-notifications
[Installable Web Apps]: https://developers.google.com/chrome/apps/docs/
[行動裝置上的 Chrome 應用程式]: https://developer.chrome.com/apps/chrome_apps_on_mobile
[建立註冊 NH REST API]: http://msdn.microsoft.com/library/azure/dn223265.aspx
[crypto js 程式庫]: http://code.google.com/p/crypto-js/
[GCM with Chrome Apps]: https://developer.chrome.com/apps/cloudMessaging
[Google Cloud Messaging chrome]: https://developer.chrome.com/apps/cloudMessagingV1
[Azure 通知中樞通知使用者]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Azure 通知中心最新消息]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
