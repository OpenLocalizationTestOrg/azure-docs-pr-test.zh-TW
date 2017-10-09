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
# <a name="send-push-notifications-toochrome-apps-with-azure-notification-hubs"></a>傳送推播通知 tooChrome 應用程式與 Azure 通知中心
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

本主題說明如何 toouse Azure 通知中樞 toosend 推播通知 tooa Chrome 應用程式，將會顯示 hello 內容 hello Google Chrome 瀏覽器中。 在本教學課程中，我們將建立可使用 [Google 雲端通訊 (GCM)](https://developers.google.com/cloud-messaging/)接收推播通知的 Chrome 應用程式。 

> [!NOTE]
> toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F)。
> 
> 

hello 教學課程將引導您完成這些基本步驟 tooenable 推播通知：

* [啟用 Google Cloud Messaging](#register)
* [設定您的通知中樞](#configure-hub)
* [連接您的應用程式 Chrome toohello 的通知中樞](#connect-app)
* [傳送推播通知 tooyour Chrome 應用程式](#send)
* [其他功能與能力](#next-steps)

> [!NOTE]
> Chrome 應用程式的推播通知不是泛型的瀏覽器中通知--它們是特定 toohello 瀏覽器擴充性模型 (請參閱[Chrome 應用程式的概觀]如需詳細資訊)。 此外 toohello 桌面瀏覽器 Chrome 應用程式 （Android 和 iOS） 的行動裝置上透過執行 Apache Cordova。 請參閱[行動裝置上的 Chrome 應用程式]toolearn 更多。
> 
> 

因為設定 GCM 和 Azure 通知中心是適用於 Android 的相同 tooconfiguring [Google Cloud Messaging chrome]已被取代，hello 相同 GCM 現在支援 Android 裝置和 Chrome 的執行個體。

## <a id="register"></a>啟用 Google Cloud Messaging
1. 瀏覽 toohello [Google 雲端主控台]網站，使用您的 Google 帳戶認證登入，然後按一下hello**建立專案** 按鈕。 提供適當**專案名稱**，然後按一下hello**建立** 按鈕。
   
       ![Google Cloud Console - Create Project][1]
2. 請記下 hello**專案編號**上 hello**專案**hello 專案您剛才建立的頁面。 您會使用這個 hello **GCM 寄件者識別碼**hello Chrome 應用程式 tooregister GCM 使用中。
   
       ![Google Cloud Console - Project Number][2]
3. Hello 左窗格中，按一下  **Api & auth**，然後向下捲動並按一下 hello 切換 tooenable**適用於 Android 的 Google Cloud Messaging**。 您不需要 tooenable **Google Cloud Messaging chrome**。
   
       ![Google Cloud Console - Server Key][3]
4. 在 hello 左窗格中，按一下 **認證** > **建立新的金鑰** > **伺服器金鑰** > **建立**.
   
       ![Google Cloud Console - Credentials][4]
5. 請記下 hello 伺服器**API 金鑰**。 您會設定此通知中樞的 下一步，tooenable 中它 toosend 推播通知 tooGCM。
   
       ![Google Cloud Console - API Key][5]

## <a id="configure-hub"></a>設定您的通知中樞
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

&emsp;&emsp;6.   在 hello**設定**刀鋒視窗中，選取**Notification Services**然後**Google (GCM)**。 輸入 hello API 金鑰，並儲存。

&emsp;&emsp;![Azure 通知中樞 - Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

## <a id="connect-app"></a>連接您的應用程式 Chrome toohello 的通知中樞
您的通知中樞現在是設定的 toowork 與 GCM，而且您擁有 hello 的連接字串 tooregister 應用程式 tooboth 接收和傳送推播通知。 LK

### <a name="create-a-new-chrome-app"></a>建立新的 Chrome 應用程式
以下的 hello 範例根據 hello [Chrome 應用程式 GCM 範例]使用 hello 建議的方式 toocreate Chrome 應用程式。 我們將會反白顯示 hello 步驟特別相關的 tooAzure 通知中樞。 

> [!NOTE]
> 我們建議您從這個 Chrome 應用程式下載 hello 來源[Chrome 應用程式通知中樞範例]。
> 
> 

JavaScript 中，透過建立 hello Chrome 應用程式，您可以使用任何慣用的文字編輯器來建立它。 此 Chrome 應用程式如下所示。

![Google Chrome 應用程式][15]

1. 建立資料夾，並將其命名為 `ChromePushApp`。 當然，hello 名稱是任意-如果您將檔案命名不同的項目，請確定您所需的 hello 程式碼區段中的 hello 路徑來取代。
2. 下載 hello [crypto js 程式庫]hello hello 第二個步驟中所建立的資料夾中。 此程式庫資料夾將包含兩個子資料夾：`components` 和 `rollups`。
3. 建立 `manifest.json` 檔案。 所有 Chrome 應用程式都都由資訊清單檔案，其中包含 hello 應用程式中繼資料和最重要的是，所有已授與權限 toohello 應用程式時 hello 使用者進行安裝。
   
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
   
    請注意 hello`permissions`元素，其指定此 Chrome 應用程式將會從 GCM 可以 tooreceive 推播通知。 它也必須指定 hello 而 hello Chrome 應用程式將於其中進行 REST 呼叫 tooregister Azure 通知中樞 URI。
    我們的範例應用程式也會使用的圖示檔`gcm_128.png`，您會發現在 hello 來源 hello 原始 GCM 範例中會重複使用。 您可以替換符合 hello 任何映像[圖示準則](https://developer.chrome.com/apps/manifest/icons)。
4. 建立一個叫做檔案`background.js`以下列程式碼的 hello:
   
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
   
    這是快顯 hello Chrome 應用程式視窗 HTML 的 hello 檔案 (**register.html**)，並且定義 hello 處理常式**messageReceived** toohandle hello 傳入推播通知。
5. 建立一個叫做檔案`register.html`-這會定義 hello hello Chrome 應用程式的 UI。 
   
   > [!NOTE]
   > 此範例使用 **CryptoJS v3.1.2**。 如果您已經下載 hello 文件庫的另一個版本，請確定您正確替代 hello 中的 hello 版本`src`路徑。
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
6. 建立一個叫做檔案`register.js`與 hello 的下列程式碼。 此檔案會指定 hello 指令碼後置`register.html`。 Chrome 應用程式不允許內嵌執行，因此您 ui 有 toocreate 個別備份指令碼。
   
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
   
    上述指令碼的 hello 具有下列索引鍵參數的 hello:
   
   * **window.onload** hello UI 上定義的 hello 兩個按鈕的 hello 按鈕 click 事件。 其中一個登錄 GCM，並 hello 其他使用 GCM tooregister 與 Azure 通知中心註冊後，會傳回的 hello 註冊 ID。
   * **updateLog**是 hello 函式，讓我們 toohandle 簡單的記錄功能。
   * **registerWithGCM** hello 第一個按鈕 click 處理常式，使得 hello`chrome.gcm.register`呼叫 tooGCM tooregister hello 目前 Chrome 應用程式的執行個體。
   * **registerCallback**是 hello hello GCM 註冊呼叫傳回時被呼叫的回呼函式。
   * **registerWithNH** hello 第二個按鈕 click 處理常式，以使用通知中樞註冊。 它會取得`hubName`和`connectionString`（hello 使用者已指定） 和美工 hello 通知中樞註冊 REST API 呼叫。
   * **splitConnectionString**和**generateSaSToken**是代表 hello 的 SaS 權杖的建立程序必須用於所有 REST API 呼叫的 JavaScript 實作的協助程式。 如需詳細資訊，請參閱 [一般概念](http://msdn.microsoft.com/library/dn495627.aspx)。
   * **sendNHRegistrationRequest** hello 函式，讓 HTTP REST 呼叫 tooAzure 通知中樞。
   * **registrationPayload**定義 hello 註冊 XML 裝載。 如需詳細資訊，請參閱 [建立註冊 NH REST API]。 我們會以我們收到來自 GCM 更新中的 hello 註冊 ID。
   * **用戶端**的執行個體**XMLHttpRequest** ，我們會使用 toomake hello HTTP POST 要求。 請注意，我們會更新 hello`Authorization`具有標頭`sasToken`。 成功完成此呼叫後，即會向 Azure 通知中樞註冊此 Chrome 應用程式執行個體。

hello 這個專案的整個資料夾結構看起來應該像這樣： ![Google Chrome 應用程式的資料夾結構][21]

### <a name="set-up-and-test-your-chrome-app"></a>設定和測試 Chrome 應用程式
1. 開啟 Chrome 瀏覽器。 開啟 [Chrome 擴充功能]，並啟用 [開發人員模式]。
   
       ![Google Chrome - Enable Developer Mode][16]
2. 按一下**解除封裝的擴充功能載入**並瀏覽 toohello 資料夾建立 hello 檔案的位置。 您也可以使用 hello **Chrome 應用程式 （& s) 延伸模組的開發人員工具**。 此工具是 Chrome 中的應用程式本身 （從 hello Chrome Web Store 安裝），並提供進階偵錯功能 Chrome 應用程式開發。
   
       ![Google Chrome - Load Unpacked Extension][17]
3. 如果沒有發生任何錯誤，建立 hello Chrome 應用程式，您會看到顯示 Chrome 應用程式。
   
       ![Google Chrome - Chrome App Display][18]
4. 輸入 hello**專案編號**，則您稍早取得從 hello **Google 雲端主控台**為 hello 寄件者識別碼，然後按一下**GCM 註冊**。 您必須查看 hello 訊息**GCM 成功的註冊。**
   
       ![Google Chrome - Chrome App Customization][19]
5. 輸入您**通知中樞名稱**和 hello **DefaultListenSharedAccessSignature**您取得的較舊版本，hello 網站，然後按一下**向 Azure 通知中樞**. 您必須查看 hello 訊息**通知中樞註冊成功 ！** 而且識別碼 hello hello 註冊回應，其中包含 hello Azure 通知中樞註冊詳細資料。
   
       ![Google Chrome - Specify Notification Hub Details][20]  

## <a name="send"></a>傳送通知 tooyour Chrome 應用程式
為了進行測試，我們會使用 .NET 主控台應用程式傳送 Chrome 推播通知。 

> [!NOTE]
> 您可以透過公用 <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST 介面</a>，使用通知中樞從任何後端傳送推播通知。 如需其他跨平台範例，請查看我們的 [說明文件入口網站](https://azure.microsoft.com/documentation/services/notification-hubs/) 。
> 
> 

1. 在 Visual Studio 中，從 hello**檔案**功能表上，選取**新增**然後**專案**。 在 Visual C# 下方，按一下 Windows 和 主控台應用程式，然後按一下確定。  這會建立新的主控台應用程式專案。
2. 從 hello**工具**功能表上，按一下 **程式庫套件管理員**然後**Package Manager Console**。 這會顯示 hello Package Manager Console。
3. 在 hello 主控台視窗中，執行下列命令的 hello:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
       This adds a reference toohello Azure Service Bus SDK with hello <a href="http://nuget.org/packages/  WindowsAzure.ServiceBus/">WindowsAzure.ServiceBus NuGet package</a>.
4. 開啟`Program.cs`並加入下列 hello`using`陳述式：
   
        using Microsoft.Azure.NotificationHubs;
5. 在 hello`Program`類別中，新增下列方法 hello:
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            String message = "{\"data\":{\"message\":\"Hello Chrome from Azure Notification Hubs\"}}";
            await hub.SendGcmNativeNotificationAsync(message);
        }
   
       Make sure tooreplace hello `<hub name>` placeholder with hello name of hello notification hub that appears in hello [portal](https://portal.azure.com) in your Notification Hub blade. Also, replace hello connection string placeholder with hello connection string called `DefaultFullSharedAccessSignature` that you obtained in hello notification hub configuration section.
   
   > [!NOTE]
   > 請確定您使用連接字串 hello**完整**不存取**接聽**存取。 hello**接聽**存取連接字串不授與權限 toosend 推播通知。
   > 
   > 
6. 新增 hello 下列呼叫 hello`Main`方法：
   
         SendNotificationAsync();
         Console.ReadLine();
7. 請確定 Chrome 正在執行，並執行 hello 主控台應用程式。
8. 您應該會看見 hello 下列顯桌面上的通知。
   
       ![Google Chrome - Notification][13]
9. 您也可以查看您的通知 （在 Windows) 使用 hello 工作列中的 hello Chrome 通知視窗 Chrome 正在執行時。
   
       ![Google Chrome - Notifications List][14]

> [!NOTE]
> 您不需要 toohave hello Chrome 應用程式執行中或在 hello 瀏覽器中開啟 （但必須執行 hello Chrome 瀏覽器本身）。 您也可以取得您的通知的彙總的檢視 hello Chrome 通知視窗中。
> 
> 

## <a name="next-steps"> </a>後續步驟
請在 [通知中樞概觀]中進一步了解通知中樞。

tootarget 特定使用者，請參閱 toohello [Azure 通知中樞通知使用者]教學課程。 

如果您希望 toosegment 使用者感興趣的群組，您可以依照 hello [Azure 通知中心最新消息]教學課程。

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
