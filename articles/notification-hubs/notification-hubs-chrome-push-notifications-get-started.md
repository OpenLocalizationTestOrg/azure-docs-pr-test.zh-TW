---
title: "使用 Azure 通知中樞將推播通知傳送至 Chrome 應用程式 | Microsoft Docs"
description: "了解如何使用 Azure 通知中樞將推播通知傳送至 Chrome 應用程式。"
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
ms.openlocfilehash: 600b1b7e5f3987c9a0acc33b7049f7118442b931
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="send-push-notifications-to-chrome-apps-with-azure-notification-hubs"></a><span data-ttu-id="7b1a7-104">使用 Azure 通知中樞將推播通知傳送至 Chrome 應用程式</span><span class="sxs-lookup"><span data-stu-id="7b1a7-104">Send push notifications to Chrome apps with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

<span data-ttu-id="7b1a7-105">本主題說明如何使用 Azure 通知中樞將推播通知傳送至 Chrome 應用程式，以顯示於 Google Chrome 瀏覽器的內容中。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-105">This topic shows you how to use Azure Notification Hubs to send push notifications to a Chrome App, which will be displayed within the context of the Google Chrome browser.</span></span> <span data-ttu-id="7b1a7-106">在本教學課程中，我們將建立可使用 [Google 雲端通訊 (GCM)](https://developers.google.com/cloud-messaging/)接收推播通知的 Chrome 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-106">In this tutorial, we will create a Chrome app that receives push notifications by using [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/).</span></span> 

> [!NOTE]
> <span data-ttu-id="7b1a7-107">若要完成此教學課程，您必須具備有效的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-107">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="7b1a7-108">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="7b1a7-109">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F)。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-109">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).</span></span>
> 
> 

<span data-ttu-id="7b1a7-110">本教學課程將逐步引導您完成下列啟用推播通知的基本步驟：</span><span class="sxs-lookup"><span data-stu-id="7b1a7-110">The tutorial walks you through these basic steps to enable push notifications:</span></span>

* [<span data-ttu-id="7b1a7-111">啟用 Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="7b1a7-111">Enable Google Cloud Messaging</span></span>](#register)
* [<span data-ttu-id="7b1a7-112">設定您的通知中樞</span><span class="sxs-lookup"><span data-stu-id="7b1a7-112">Configure your notification hub</span></span>](#configure-hub)
* [<span data-ttu-id="7b1a7-113">將您的 Chrome 應用程式連接到通知中樞</span><span class="sxs-lookup"><span data-stu-id="7b1a7-113">Connect your Chrome App to the notification hub</span></span>](#connect-app)
* [<span data-ttu-id="7b1a7-114">傳送推播通知給您的 Chrome 應用程式</span><span class="sxs-lookup"><span data-stu-id="7b1a7-114">Send a push notification to your Chrome App</span></span>](#send)
* [<span data-ttu-id="7b1a7-115">其他功能與能力</span><span class="sxs-lookup"><span data-stu-id="7b1a7-115">Additional functionality & capabilities</span></span>](#next-steps)

> [!NOTE]
> <span data-ttu-id="7b1a7-116">Chrome 應用程式的推播通知不是一般的瀏覽器中通知，而是瀏覽器擴充性模型所特有 (如需詳細資訊，請參閱 [Chrome 應用程式概觀] )。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-116">Chrome app push notifications are not generic in-browser notifications - they are specific to the browser extensibility model (see [Chrome Apps Overview] for details).</span></span> <span data-ttu-id="7b1a7-117">Chrome 應用程式除了在桌面瀏覽器中執行外，也可透過 Apache Cordova 在行動裝置 (Android 和 iOS) 上執行。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-117">In addition to the desktop browser, Chrome apps run on mobile (Android and iOS) through Apache Cordova.</span></span> <span data-ttu-id="7b1a7-118">若要深入了解，請參閱 [行動裝置上的 Chrome 應用程式] 。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-118">See [Chrome Apps on Mobile] to learn more.</span></span>
> 
> 

<span data-ttu-id="7b1a7-119">設定 GCM 和 Azure 通知中樞的程序與 Android 的設定程序相同，因為 [Google Cloud Messaging for Chrome] 已停用，而相同的 GCM 現在可同時支援 Android 裝置和 Chrome 執行個體。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-119">Configuring GCM and Azure Notification Hubs is identical to configuring for Android, since [Google Cloud Messaging for Chrome] has been deprecated and the same GCM now supports both Android devices and Chrome instances.</span></span>

## <span data-ttu-id="7b1a7-120"><a id="register"></a>啟用 Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="7b1a7-120"><a id="register"></a>Enable Google Cloud Messaging</span></span>
1. <span data-ttu-id="7b1a7-121">瀏覽至 [Google 雲端主控台]網站，並使用 Google 帳戶認證登入，然後按一下 **[建立專案]** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-121">Navigate to the [Google Cloud Console] website, sign in with your Google account credentials, and then click the **Create Project** button.</span></span> <span data-ttu-id="7b1a7-122">提供適當的 [專案名稱]，然後按一下 [建立] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-122">Provide an appropriate **Project Name**, and then click the **Create** button.</span></span>
   
       ![Google Cloud Console - Create Project][1]
2. <span data-ttu-id="7b1a7-123">在 [專案] 頁面上，記下您剛才建立之專案的 [專案編號]。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-123">Make a note of the **Project Number** on the **Projects** page for the project that you just created.</span></span> <span data-ttu-id="7b1a7-124">您將以此編號做為 Chrome 應用程式中的 [GCM 寄件者識別碼]  ，向 GCM 註冊。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-124">You will use this as the **GCM Sender ID** in the Chrome App to register with GCM.</span></span>
   
       ![Google Cloud Console - Project Number][2]
3. <span data-ttu-id="7b1a7-125">在左窗格中按一下 [API 與驗證]，然後向下捲動並按一下切換開關，以啟用 [Google Cloud Messaging for Android]。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-125">In the left pane, click **APIs & auth**, and then scroll down and click the toggle to enable **Google Cloud Messaging for Android**.</span></span> <span data-ttu-id="7b1a7-126">您不需要啟用 Google Cloud Messaging for Chrome 。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-126">You don't have to enable **Google Cloud Messaging for Chrome**.</span></span>
   
       ![Google Cloud Console - Server Key][3]
4. <span data-ttu-id="7b1a7-127">在左窗格中，按一下 [認證] > [建立新的金鑰] > [伺服器金鑰] > [建立]。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-127">In the left pane, click **Credentials** > **Create New Key** > **Server Key** > **Create**.</span></span>
   
       ![Google Cloud Console - Credentials][4]
5. <span data-ttu-id="7b1a7-128">記下伺服器的 [API 金鑰] 。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-128">Make a note of the server **API Key**.</span></span> <span data-ttu-id="7b1a7-129">您後續將會在通知中樞裡設定此金鑰，讓它能夠將推播通知傳送至 GCM。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-129">You will configure this in your notification hub next, to enable it to send push notifications to GCM.</span></span>
   
       ![Google Cloud Console - API Key][5]

## <span data-ttu-id="7b1a7-130"><a id="configure-hub"></a>設定您的通知中樞</span><span class="sxs-lookup"><span data-stu-id="7b1a7-130"><a id="configure-hub"></a>Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="7b1a7-131">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="7b1a7-131">&emsp;&emsp;6.</span></span>   <span data-ttu-id="7b1a7-132">在 [設定] 刀鋒視窗中，選取 [通知服務]，然後選取 [Google (GCM)]。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-132">In the **Settings** blade, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="7b1a7-133">輸入 API 金鑰並儲存。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-133">Enter the API key and save.</span></span>

&emsp;&emsp;![Azure 通知中樞 - Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

## <span data-ttu-id="7b1a7-135"><a id="connect-app"></a>將您的 Chrome 應用程式連接到通知中樞</span><span class="sxs-lookup"><span data-stu-id="7b1a7-135"><a id="connect-app"></a>Connect your Chrome App to the notification hub</span></span>
<span data-ttu-id="7b1a7-136">現在已將您的通知中樞設定成使用 GCM，而且您已擁有可用來註冊應用程式以接收和傳送推播通知的連接字串。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-136">Your notification hub is now configured to work with GCM, and you have the connection strings to register your app to both receive and send push notifications.</span></span> <span data-ttu-id="7b1a7-137">LK</span><span class="sxs-lookup"><span data-stu-id="7b1a7-137">LK</span></span>

### <a name="create-a-new-chrome-app"></a><span data-ttu-id="7b1a7-138">建立新的 Chrome 應用程式</span><span class="sxs-lookup"><span data-stu-id="7b1a7-138">Create a new Chrome App</span></span>
<span data-ttu-id="7b1a7-139">下列範例以 [Chrome 應用程式 GCM 範例] 為基礎，並使用建議的方式建立 Chrome 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-139">The sample below is based on the [Chrome App GCM Sample] and uses the recommended way to create a Chrome App.</span></span> <span data-ttu-id="7b1a7-140">我們將加強說明 Azure 通知中樞的相關具體步驟。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-140">We will highlight the steps specifically related to Azure Notification Hubs.</span></span> 

> [!NOTE]
> <span data-ttu-id="7b1a7-141">我們建議您從 [Chrome 應用程式通知中樞範例]下載此 Chrome 應用程式的原始碼。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-141">We recommend that you download the source for this Chrome App from [Chrome App Notification Hub Sample].</span></span>
> 
> 

<span data-ttu-id="7b1a7-142">Chrome 應用程式是透過 JavaScript 建立的，您可以使用任何慣用的文字編輯器加以建立。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-142">The Chrome App is created via JavaScript, and you can use any of your preferred word editors for creating it.</span></span> <span data-ttu-id="7b1a7-143">此 Chrome 應用程式如下所示。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-143">Below is what this Chrome App will look like.</span></span>

![Google Chrome 應用程式][15]

1. <span data-ttu-id="7b1a7-145">建立資料夾，並將其命名為 `ChromePushApp`。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-145">Create a folder and name it `ChromePushApp`.</span></span> <span data-ttu-id="7b1a7-146">當然，您不一定要取為這個名稱，但如果您將其命名為不同名稱，請務必要替換掉必要程式碼片段中的路徑。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-146">Of course, the name is arbitrary - if you name it something different, make sure you substitute the path in the required code segments.</span></span>
2. <span data-ttu-id="7b1a7-147">在第二個步驟建立的資料夾中，下載 [crypto-js 程式庫] 。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-147">Download the [crypto-js library] in the folder you created in the second step.</span></span> <span data-ttu-id="7b1a7-148">此程式庫資料夾將包含兩個子資料夾：`components` 和 `rollups`。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-148">This library folder will contain two subfolders: `components` and `rollups`.</span></span>
3. <span data-ttu-id="7b1a7-149">建立 `manifest.json` 檔案。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-149">Create a `manifest.json` file.</span></span> <span data-ttu-id="7b1a7-150">所有 Chrome 應用程式都會受到包含應用程式中繼資料的資訊清單檔案，以及最重要的是，使用者安裝應用程式時授與應用程式的所有權限所支援。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-150">All Chrome Apps are backed by a manifest file that contains the app metadata and, most importantly, all permissions that are granted to the app when the user installs it.</span></span>
   
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
   
    <span data-ttu-id="7b1a7-151">請留意 `permissions` 元素，它會指定此 Chrome 應用程式能夠從 GCM 接收推播通知。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-151">Notice the `permissions` element, which specifies that this Chrome App will be able to receive push notifications from GCM.</span></span> <span data-ttu-id="7b1a7-152">它也必須指定 Azure 通知中樞 URI，其中 Chrome 應用程式將呼叫 REST 以進行註冊。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-152">It must also specify the Azure Notification Hubs URI where the Chrome App will make a REST call to register.</span></span>
    <span data-ttu-id="7b1a7-153">我們的範例應用程式也會使用圖示檔案 `gcm_128.png`，您會在取自原始 GCM 範例的重複使用原始碼中發現此檔案。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-153">Our sample app also uses an icon file, `gcm_128.png`, that you will find at the source that's reused from the original GCM sample.</span></span> <span data-ttu-id="7b1a7-154">您可以用此圖示檔案來替換任何符合 [圖示準則](https://developer.chrome.com/apps/manifest/icons)的影像。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-154">You can substitute it for any image that fits the [icon criteria](https://developer.chrome.com/apps/manifest/icons).</span></span>
4. <span data-ttu-id="7b1a7-155">建立名為 `background.js` 的檔案並加入下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="7b1a7-155">Create a file called `background.js` with the following code:</span></span>
   
        // Returns a new notification ID used in the notification.
        function getNotificationId() {
          var id = Math.floor(Math.random() * 9007199254740992) + 1;
          return id.toString();
        }
   
        function messageReceived(message) {
          // A message is an object with a data property that
          // consists of key-value pairs.
   
          // Concatenate all key-value pairs to form a display string.
          var messageString = "";
          for (var key in message.data) {
            if (messageString != "")
              messageString += ", "
            messageString += key + ":" + message.data[key];
          }
          console.log("Message received: " + messageString);
   
          // Pop up a notification to show the GCM message.
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
   
        // Set up listeners to trigger the first-time registration.
        chrome.runtime.onInstalled.addListener(firstTimeRegistration);
        chrome.runtime.onStartup.addListener(firstTimeRegistration);
   
    <span data-ttu-id="7b1a7-156">這是快顯 Chrome 應用程式視窗 HTML (**register.html**) 的檔案，且該檔案也會定義處理常式 **messageReceived** 來處理內送的推播通知。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-156">This is the file that pops up the Chrome App window HTML (**register.html**) and also defines the handler **messageReceived** to handle the incoming push notification.</span></span>
5. <span data-ttu-id="7b1a7-157">建立名為 `register.html` 的檔案，此檔案會定義 Chrome 應用程式的 UI。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-157">Create a file called `register.html` - this defines the UI of the Chrome App.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="7b1a7-158">此範例使用 **CryptoJS v3.1.2**。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-158">This sample uses **CryptoJS v3.1.2**.</span></span> <span data-ttu-id="7b1a7-159">如果您下載了另一個版本的程式庫，請務必要正確替換 `src` 路徑中的版本。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-159">If you downloaded another version of the library, make sure you properly substitute the version in the `src` path.</span></span>
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
6. <span data-ttu-id="7b1a7-160">使用下列程式碼，建立名為 `register.js` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-160">Create a file called `register.js` with the code below.</span></span> <span data-ttu-id="7b1a7-161">此檔案會指定 `register.html`後面的指令碼。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-161">This file specifies the script behind `register.html`.</span></span> <span data-ttu-id="7b1a7-162">Chrome 應用程式並不允許內嵌執行，因此您必須為 UI 建立個別的備份指令碼。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-162">Chrome Apps do not allow inline execution, so you have to create a separate backing script for your UI.</span></span>
   
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
   
          // Prevent register button from being clicked again before the registration finishes.
          document.getElementById("registerWithGCM").disabled = true;
        }
   
        function registerCallback(regId) {
          registrationId = regId;
          document.getElementById("registerWithGCM").disabled = false;
   
          if (chrome.runtime.lastError) {
            // When the registration fails, handle the error and retry the
            // registration later.
            updateLog("Registration failed: " + chrome.runtime.lastError.message);
            return;
          }
   
          updateLog("Registration with GCM succeeded.");
          document.getElementById("registerWithNH").disabled = false;
   
          // Mark that the first-time registration is done.
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
   
          // Update the payload with the registration ID obtained earlier.
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
   
    <span data-ttu-id="7b1a7-163">上述指令碼具有下列重要參數：</span><span class="sxs-lookup"><span data-stu-id="7b1a7-163">The above script has the following key parameters:</span></span>
   
   * <span data-ttu-id="7b1a7-164">**window.onload** 會在 UI 上定義兩個按鈕的按鈕點擊事件。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-164">**window.onload** defines the button-click events of the two buttons on the UI.</span></span> <span data-ttu-id="7b1a7-165">其中一個向 GCM 註冊，另一個使用向 GCM 註冊後所傳回的註冊識別碼來向 Azure 通知中樞註冊。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-165">One registers with GCM, and the other uses the registration ID that's returned after registration with GCM to register with Azure Notification Hubs.</span></span>
   * <span data-ttu-id="7b1a7-166">**updateLog** 是可讓我們處理簡單記錄功能的函式。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-166">**updateLog** is the function that allows us to handle simple logging capabilities.</span></span>
   * <span data-ttu-id="7b1a7-167">**registerWithGCM** 是第一個按鈕點擊處理常式，可向 GCM 進行 `chrome.gcm.register` 呼叫，以註冊目前的 Chrome 應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-167">**registerWithGCM** is the first button-click handler, which makes the `chrome.gcm.register` call to GCM to register the current Chrome App instance.</span></span>
   * <span data-ttu-id="7b1a7-168">**registerCallback** 是回呼函數，會在 GCM 註冊呼叫傳回時受到呼叫。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-168">**registerCallback** is the callback function that gets called when the GCM registration call returns.</span></span>
   * <span data-ttu-id="7b1a7-169">**registerWithNH** 是第二個按鈕點擊處理常式，會向通知中樞進行註冊。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-169">**registerWithNH** is the second button-click handler, which registers with Notification Hubs.</span></span> <span data-ttu-id="7b1a7-170">它會取得使用者已指定的 `hubName` 和 `connectionString`，並製作通知中樞註冊 REST API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-170">It gets `hubName` and `connectionString` (which the user has specified) and crafts the Notification Hubs Registration REST API call.</span></span>
   * <span data-ttu-id="7b1a7-171">**splitConnectionString** 和 **generateSaSToken** 是代表 SaS 權杖建立程序之 JavaScript 實作的協助程式，其必須用於所有 REST API 呼叫中。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-171">**splitConnectionString** and **generateSaSToken** are helpers that represent the JavaScript implementation of a SaS token creation process, that must be used in all REST API calls.</span></span> <span data-ttu-id="7b1a7-172">如需詳細資訊，請參閱 [一般概念](http://msdn.microsoft.com/library/dn495627.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-172">For more information, see [Common Concepts](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
   * <span data-ttu-id="7b1a7-173">**sendNHRegistrationRequest** 是對 Azure 通知中樞發出 HTTP REST 呼叫的函式。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-173">**sendNHRegistrationRequest** is the function that makes a HTTP REST call to Azure Notification Hubs.</span></span>
   * <span data-ttu-id="7b1a7-174">**registrationPayload** 會定義註冊 XML 裝載。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-174">**registrationPayload** defines the registration XML payload.</span></span> <span data-ttu-id="7b1a7-175">如需詳細資訊，請參閱 [建立註冊 NH REST API]。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-175">For more information, see [Create Registration NH REST API].</span></span> <span data-ttu-id="7b1a7-176">我們會以接收自 GCM 的項目來更新其中的註冊識別碼。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-176">We update the registration ID in it with what we received from GCM.</span></span>
   * <span data-ttu-id="7b1a7-177">**client** 是我們用來發出 HTTP POST 要求的 **XMLHttpRequest** 執行個體。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-177">**client** is an instance of **XMLHttpRequest** that we use to make the HTTP POST request.</span></span> <span data-ttu-id="7b1a7-178">請注意，我們會使用 `sasToken` 更新 `Authorization` 標頭。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-178">Note that we update the `Authorization` header with `sasToken`.</span></span> <span data-ttu-id="7b1a7-179">成功完成此呼叫後，即會向 Azure 通知中樞註冊此 Chrome 應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-179">Successful completion of this call will register this Chrome App instance with Azure Notification Hubs.</span></span>

<span data-ttu-id="7b1a7-180">此專案的整體資料夾結構應該會與下圖類似︰![Google Chrome 應用程式 - 資料夾結構][21]</span><span class="sxs-lookup"><span data-stu-id="7b1a7-180">The overall folder structure for this project should resemble this: ![Google Chrome App - Folder Structure][21]</span></span>

### <a name="set-up-and-test-your-chrome-app"></a><span data-ttu-id="7b1a7-181">設定和測試 Chrome 應用程式</span><span class="sxs-lookup"><span data-stu-id="7b1a7-181">Set up and test your Chrome App</span></span>
1. <span data-ttu-id="7b1a7-182">開啟 Chrome 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-182">Open your Chrome browser.</span></span> <span data-ttu-id="7b1a7-183">開啟 [Chrome 擴充功能]，並啟用 [開發人員模式]。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-183">Open **Chrome extensions** and enable **Developer mode**.</span></span>
   
       ![Google Chrome - Enable Developer Mode][16]
2. <span data-ttu-id="7b1a7-184">按一下 [載入未封裝的擴充功能]，並瀏覽至您在其中建立檔案的資料夾。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-184">Click **Load unpacked extension** and navigate to the folder where you created the files.</span></span> <span data-ttu-id="7b1a7-185">您也可以選擇性地使用 **Chrome Apps & Extensions Developer Tool**。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-185">You can also optionally use the **Chrome Apps & Extensions Developer Tool**.</span></span> <span data-ttu-id="7b1a7-186">此工具本身為 Chrome 應用程式 (從 Chrome 線上應用程式商店進行安裝)，且提供 Chrome 應用程式開發進階偵錯功能。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-186">This tool is a Chrome App in itself (installed from the Chrome Web Store) and provides advanced debugging capabilities for your Chrome App development.</span></span>
   
       ![Google Chrome - Load Unpacked Extension][17]
3. <span data-ttu-id="7b1a7-187">如果該 Chrome 應用程式在建立時未發生任何錯誤，則您將會看見該應用程式顯示。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-187">If the Chrome App is created without any errors, then you will see your Chrome App show up.</span></span>
   
       ![Google Chrome - Chrome App Display][18]
4. <span data-ttu-id="7b1a7-188">輸入您先前從 **Google 雲端主控台** 取得的 **[專案編號]**，做為寄件者識別碼，然後按一下 **[向 GCM 註冊]**。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-188">Enter the **Project Number** that you got earlier from the **Google Cloud Console** as the sender ID, and click **Register with GCM**.</span></span> <span data-ttu-id="7b1a7-189">您必須看見 **Registration with GCM succeeded.** 訊息。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-189">You must see the message **Registration with GCM succeeded.**</span></span>
   
       ![Google Chrome - Chrome App Customization][19]
5. <span data-ttu-id="7b1a7-190">輸入您先前從 Azure 傳統入口網站取得的 [通知中樞名稱] 和 [DefaultListenSharedAccessSignature]，然後按一下 [向 Azure 通知中樞註冊]。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-190">Enter your **Notification Hub Name** and the **DefaultListenSharedAccessSignature** that you obtained from the portal earlier, and click **Register with Azure Notification Hub**.</span></span> <span data-ttu-id="7b1a7-191">您必須看見 **Registration with GCM succeeded.** 訊息</span><span class="sxs-lookup"><span data-stu-id="7b1a7-191">You must see the message **Notification Hub Registration successful!**</span></span> <span data-ttu-id="7b1a7-192">和註冊回應的詳細資料，其中包含 Azure 通知中樞註冊識別碼。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-192">and the details of the registration response, which contains the Azure Notification Hubs registration ID.</span></span>
   
       ![Google Chrome - Specify Notification Hub Details][20]  

## <span data-ttu-id="7b1a7-193"><a name="send"></a>傳送通知給您的 Chrome 應用程式</span><span class="sxs-lookup"><span data-stu-id="7b1a7-193"><a name="send"></a>Send a notification to your Chrome App</span></span>
<span data-ttu-id="7b1a7-194">為了進行測試，我們會使用 .NET 主控台應用程式傳送 Chrome 推播通知。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-194">For testing purposes, we will send Chrome push notifications by using a .NET console application.</span></span> 

> [!NOTE]
> <span data-ttu-id="7b1a7-195">您可以透過公用 <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST 介面</a>，使用通知中樞從任何後端傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-195">You can send push notifications with Notification Hubs from any backend via our public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span></span> <span data-ttu-id="7b1a7-196">如需其他跨平台範例，請查看我們的 [說明文件入口網站](https://azure.microsoft.com/documentation/services/notification-hubs/) 。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-196">Check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/) for more cross-platform examples.</span></span>
> 
> 

1. <span data-ttu-id="7b1a7-197">在 Visual Studio 的 [檔案] 功能表中，選取 [新增]，然後選取 [專案]。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-197">In Visual Studio, from the **File** menu, select **New** and then **Project**.</span></span> <span data-ttu-id="7b1a7-198">在 [Visual C#] 下方，按一下 [Windows] 和 [主控台應用程式]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-198">Under **Visual C#**, click **Windows** and **Console Application**, and then click **OK**.</span></span>  <span data-ttu-id="7b1a7-199">這會建立新的主控台應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-199">This creates a new console application project.</span></span>
2. <span data-ttu-id="7b1a7-200">在 [工具] 功能表中，依序按一下 [程式庫套件管理員] 和 [套件管理器主控台]。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-200">From the **Tools** menu, click **Library Package Manager** and then **Package Manager Console**.</span></span> <span data-ttu-id="7b1a7-201">這會顯示 [Package Manager Console]。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-201">This displays the Package Manager Console.</span></span>
3. <span data-ttu-id="7b1a7-202">在主控台視窗中，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="7b1a7-202">In the console window, execute the following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
       This adds a reference to the Azure Service Bus SDK with the <a href="http://nuget.org/packages/  WindowsAzure.ServiceBus/">WindowsAzure.ServiceBus NuGet package</a>.
4. <span data-ttu-id="7b1a7-203">開啟 `Program.cs` 並新增下列 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="7b1a7-203">Open `Program.cs` and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="7b1a7-204">在 `Program` 類別中，新增下列方法：</span><span class="sxs-lookup"><span data-stu-id="7b1a7-204">In the `Program` class, add the following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            String message = "{\"data\":{\"message\":\"Hello Chrome from Azure Notification Hubs\"}}";
            await hub.SendGcmNativeNotificationAsync(message);
        }
   
       Make sure to replace the `<hub name>` placeholder with the name of the notification hub that appears in the [portal](https://portal.azure.com) in your Notification Hub blade. Also, replace the connection string placeholder with the connection string called `DefaultFullSharedAccessSignature` that you obtained in the notification hub configuration section.
   
   > [!NOTE]
   > <span data-ttu-id="7b1a7-205">請確定您使用的連接字串具有 [完整] 存取權，而非 [接聽] 存取權。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-205">Make sure that you use the connection string with **Full** access, not **Listen** access.</span></span> <span data-ttu-id="7b1a7-206">[接聽]  存取權連接字串未授與傳送推播通知的權限。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-206">The **Listen** access connection string does not grant permissions to send push notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="7b1a7-207">在 `Main` 方法中新增下列呼叫︰</span><span class="sxs-lookup"><span data-stu-id="7b1a7-207">Add the following calls in the `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="7b1a7-208">確定 Chrome 正在執行，並執行主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-208">Make sure that Chrome is running, and run the console application.</span></span>
8. <span data-ttu-id="7b1a7-209">您應該會在桌面上看見下列通知快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-209">You should see the following notification pop up on your desktop.</span></span>
   
       ![Google Chrome - Notification][13]
9. <span data-ttu-id="7b1a7-210">當 Chrome 執行時，您也可以使用工作列 (在 Windows 中) 內的 [Chrome 通知] 視窗來查看所有的通知。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-210">You can also see all your notifications by using the Chrome Notifications window in the taskbar (in Windows) when Chrome is running.</span></span>
   
       ![Google Chrome - Notifications List][14]

> [!NOTE]
> <span data-ttu-id="7b1a7-211">您不需要執行 Chrome 應用程式，也不需要在瀏覽器中開啟 (但 Chrome 瀏覽器本身必須為執行狀態)。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-211">You don't need to have the Chrome App running or open in the browser (though the Chrome browser itself must be running).</span></span> <span data-ttu-id="7b1a7-212">您也可以在 [Chrome 通知] 視窗中整合檢視您所有的通知。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-212">You also get a consolidated view of all your notifications in the Chrome Notifications window.</span></span>
> 
> 

## <span data-ttu-id="7b1a7-213"><a name="next-steps"> </a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="7b1a7-213"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="7b1a7-214">請在 [通知中樞概觀]中進一步了解通知中樞。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-214">Learn more about Notification Hubs in [Notification Hubs Overview].</span></span>

<span data-ttu-id="7b1a7-215">若要針對特定使用者，請參閱 [Azure 通知中樞通知使用者] 教學課程。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-215">To target specific users, refer to the [Azure Notification Hubs Notify Users] tutorial.</span></span> 

<span data-ttu-id="7b1a7-216">如果您想要按興趣群組分隔使用者，可按照 [Azure 通知中樞即時新聞] 教學課程的指示進行。</span><span class="sxs-lookup"><span data-stu-id="7b1a7-216">If you want to segment your users by interest groups, you can follow the [Azure Notification Hubs breaking news] tutorial.</span></span>

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
<span data-ttu-id="7b1a7-217">[Chrome 應用程式通知中樞範例]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToChromeApps</span><span class="sxs-lookup"><span data-stu-id="7b1a7-217">[Chrome App Notification Hub Sample]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToChromeApps</span></span>
<span data-ttu-id="7b1a7-218">[Google 雲端主控台]: http://cloud.google.com/console</span><span class="sxs-lookup"><span data-stu-id="7b1a7-218">[Google Cloud Console]: http://cloud.google.com/console</span></span>
[Azure Classic Portal]: https://manage.windowsazure.com/
<span data-ttu-id="7b1a7-219">[通知中樞概觀]: notification-hubs-push-notification-overview.md</span><span class="sxs-lookup"><span data-stu-id="7b1a7-219">[Notification Hubs Overview]: notification-hubs-push-notification-overview.md</span></span>
<span data-ttu-id="7b1a7-220">[Chrome 應用程式概觀]: https://developer.chrome.com/apps/about_apps</span><span class="sxs-lookup"><span data-stu-id="7b1a7-220">[Chrome Apps Overview]: https://developer.chrome.com/apps/about_apps</span></span>
<span data-ttu-id="7b1a7-221">[Chrome 應用程式 GCM 範例]: https://github.com/GoogleChrome/chrome-app-samples/tree/master/samples/gcm-notifications</span><span class="sxs-lookup"><span data-stu-id="7b1a7-221">[Chrome App GCM Sample]: https://github.com/GoogleChrome/chrome-app-samples/tree/master/samples/gcm-notifications</span></span>
[Installable Web Apps]: https://developers.google.com/chrome/apps/docs/
<span data-ttu-id="7b1a7-222">[行動裝置上的 Chrome 應用程式]: https://developer.chrome.com/apps/chrome_apps_on_mobile</span><span class="sxs-lookup"><span data-stu-id="7b1a7-222">[Chrome Apps on Mobile]: https://developer.chrome.com/apps/chrome_apps_on_mobile</span></span>
<span data-ttu-id="7b1a7-223">[建立註冊 NH REST API]: http://msdn.microsoft.com/library/azure/dn223265.aspx</span><span class="sxs-lookup"><span data-stu-id="7b1a7-223">[Create Registration NH REST API]: http://msdn.microsoft.com/library/azure/dn223265.aspx</span></span>
<span data-ttu-id="7b1a7-224">[crypto-js 程式庫]: http://code.google.com/p/crypto-js/</span><span class="sxs-lookup"><span data-stu-id="7b1a7-224">[crypto-js library]: http://code.google.com/p/crypto-js/</span></span>
[GCM with Chrome Apps]: https://developer.chrome.com/apps/cloudMessaging
<span data-ttu-id="7b1a7-225">[Google Cloud Messaging for Chrome]: https://developer.chrome.com/apps/cloudMessagingV1</span><span class="sxs-lookup"><span data-stu-id="7b1a7-225">[Google Cloud Messaging for Chrome]: https://developer.chrome.com/apps/cloudMessagingV1</span></span>
<span data-ttu-id="7b1a7-226">[Azure 通知中樞通知使用者]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span><span class="sxs-lookup"><span data-stu-id="7b1a7-226">[Azure Notification Hubs Notify Users]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span></span>
<span data-ttu-id="7b1a7-227">[Azure 通知中樞即時新聞]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span><span class="sxs-lookup"><span data-stu-id="7b1a7-227">[Azure Notification Hubs breaking news]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span></span>
