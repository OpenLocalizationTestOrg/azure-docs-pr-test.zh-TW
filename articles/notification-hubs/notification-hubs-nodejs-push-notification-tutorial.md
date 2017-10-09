---
title: "Azure 通知中樞與 Node.js aaaSending 推播通知"
description: "了解如何 toouse 通知中樞 toosend 推播通知從 Node.js 應用程式。"
keywords: "推播通知, 推播通知, node.js 推播,ios 推播"
services: notification-hubs
documentationcenter: nodejs
author: ysxu
manager: erikre
editor: 
ms.assetid: ded4749c-6c39-4ff8-b2cf-1927b3e92f93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 10/25/2016
ms.author: yuaxu
ms.openlocfilehash: 151d224fa6dd07e4acdc3a4887c4e95ee03168c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-and-nodejs"></a>使用 Azure 通知中樞和 Node.js 傳送推播通知
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

## <a name="overview"></a>概觀
> [!IMPORTANT]
> toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs)。
> 
> 

本指南將說明如何 toosend 推播通知與 hello 說明 Azure 通知中心直接從 Node.js 應用程式。 

涵蓋的 hello 案例包括傳送推播通知 tooapplications hello 下列平台上：

* Android
* iOS
* Windows Phone
* 通用 Windows 平台 

如需有關通知中樞的詳細資訊，請參閱 hello[接下來的步驟](#next)> 一節。

## <a name="what-are-notification-hubs"></a>什麼是通知中心？
Azure 通知中樞傳送推播通知 toomobile 裝置提供方便使用、 多平台、 可擴充的基礎結構。 如需 hello 服務基礎結構的詳細資訊，請參閱 hello [Azure 通知中樞](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx)頁面。

## <a name="create-a-nodejs-application"></a>建立 Node.js 應用程式
本教學課程中的 hello 第一個步驟，建立新的空白 Node.js 應用程式。 如需建立 Node.js 應用程式的指示，請參閱[建立及部署 Node.js 應用程式 tooAzure 網站][nodejswebsite]， [Node.js 雲端服務][Node.js Cloud Service]使用 Windows PowerShell 或[使用 WebMatrix 的網站]。

## <a name="configure-your-application-toouse-notification-hubs"></a>設定您的應用程式 tooUse 通知中樞
toouse Azure 通知中樞，您需要 toodownload 和使用 hello Node.js [azure 封裝](https://www.npmjs.com/package/azure)，其中包含一組內建的協助程式程式庫與 hello 推播通知 REST 服務進行通訊。

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>使用節點封裝管理員 (NPM) tooobtain hello 套件
1. 使用命令列介面，例如**PowerShell** (Windows)**終端機**(Mac)，或**撞**(Linux)，瀏覽 toohello 資料夾建立空白的應用程式的位置.
2. 型別**npm 安裝 azure sb** hello 命令視窗中。
3. 您可以手動執行 hello **ls**或**dir**命令 tooverify，**節點\_模組**建立資料夾。 在該資料夾中，找出 hello **azure**包含需要 tooaccess hello 程式庫套件 hello 通知中樞。

> [!NOTE]
> 您可以進一步了解上 hello 官方安裝 NPM [NPM 部落格](http://blog.npmjs.org/post/85484771375/how-to-install-npm)。 
> 
> 

### <a name="import-hello-module"></a>匯入 hello 模組
使用文字編輯器中，加入下列 toohello 頂端 hello hello**立即轉譯 server.js** hello 應用程式檔案：

    var azure = require('azure');

### <a name="setup-an-azure-notification-hub-connection"></a>設定 Azure 通知中樞連線
hello **NotificationHubService**物件可讓您使用通知中樞。 hello 下列程式碼會建立**NotificationHubService**物件名為 hello nofication 中樞**hubname**。 新增 hello hello 頂端附近**立即轉譯 server.js** hello 陳述式 tooimport hello azure 模組之後的檔案：

    var notificationHubService = azure.createNotificationHubService('hubname','connectionstring');

hello 連接**connectionstring**值可以取自 hello [Azure 入口網站]藉由執行下列步驟的 hello:

1. 在 hello 左側瀏覽窗格中，按一下 **瀏覽**。
2. 選取**通知中樞**，，然後尋找 hello 中樞想 toouse hello 範例。 您可以使用參照 toohello [Windows 存放區快速入門教學課程](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)如果您需要建立新的通知中樞的說明。
3. 選取 [Settings] \(設定) 。
4. 按一下 [存取原則] 。 您會看到兩個共用和完整存取連接字串。

![Azure 入口網站 - 通知中樞](./media/notification-hubs-nodejs-how-to-use-notification-hubs/notification-hubs-portal.png)

> [!NOTE]
> 您也可以擷取 hello 連接字串使用 hello **Get AzureSbNamespace**所提供的 cmdlet [Azure PowerShell](/powershell/azureps-cmdlets-docs)或 hello **azure sb 命名空間顯示**命令搭配hello [Azure 命令列介面 (Azure CLI)](../cli-install-nodejs.md)。
> 
> 

## <a name="general-architecture"></a>一般架構
hello **NotificationHubService**物件會公開下列物件來傳送推播通知 toospecific 裝置和應用程式的執行個體的 hello:

* **Android** -使用 hello **GcmService**物件，將會位於**notificationHubService.gcm**
* **iOS** -使用 hello **ApnsService**物件，可存取**notificationHubService.apns**
* **Windows Phone** -使用 hello **MpnsService**物件，將會位於**notificationHubService.mpns**
* **通用 Windows 平台**-使用 hello **WnsService**物件，將會位於**notificationHubService.wns**

### <a name="how-to-send-push-notifications-tooandroid-applications"></a>如何： 傳送推播通知 tooAndroid 應用程式
hello **GcmService**物件提供**傳送**可以是使用的 toosend 推播通知 tooAndroid 應用程式的方法。 hello**傳送**方法可接受下列參數的 hello:

* **標記**-hello 標記識別項。 如果提供沒有標記，則 hello 會傳送通知 tooall 用戶端。
* **裝載**-hello 訊息的 JSON 或原始字串裝載。
* **回呼**-hello 回呼函式。

如需有關 hello 裝載格式的詳細資訊，請參閱 hello**裝載**區段 hello[實作 GCM 伺服器](http://developer.android.com/google/gcm/server.html#payload)文件。

hello 下列程式碼使用 hello **GcmService** hello 所公開的執行個體**NotificationHubService** toosend 推播通知 tooall 註冊用戶端。

    var payload = {
      data: {
        message: 'Hello!'
      }
    };
    notificationHubService.gcm.send(null, payload, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-tooios-applications"></a>如何： 傳送推播通知 tooiOS 應用程式
相同如同上面所述的 Android 應用程式 hello **ApnsService**物件提供**傳送**可以是使用的 toosend 推播通知 tooiOS 應用程式的方法。 hello**傳送**方法可接受下列參數的 hello:

* **標記**-hello 標記識別項。 如果提供沒有標記，則 hello 會傳送通知 tooall 用戶端。
* **裝載**-hello 訊息的 JSON 或字串裝載。
* **回呼**-hello 回呼函式。

如需詳細資訊 hello 裝載格式，請參閱 hello**通知裝載**區段 hello[本機和推播通知程式設計指南](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html)文件。

hello 下列程式碼使用 hello **ApnsService** hello 所公開的執行個體**NotificationHubService** toosend 警示訊息 tooall 用戶端：

    var payload={
        alert: 'Hello!'
      };
    notificationHubService.apns.send(null, payload, function(error){
      if(!error){
         // notification sent
      }
    });

### <a name="how-to-send-push-notifications-toowindows-phone-applications"></a>如何： 傳送推播通知 tooWindows 電話應用程式
hello **MpnsService**物件提供**傳送**可以是使用的 toosend 推播通知 tooWindows 電話應用程式的方法。 hello**傳送**方法可接受下列參數的 hello:

* **標記**-hello 標記識別項。 如果提供沒有標記，則 hello 會傳送通知 tooall 用戶端。
* **裝載**-hello 訊息的 XML 內容。
* **TargetName** - 快顯通知的 `toast`。 `token` 代表磚通知。
* **通知類別**-hello hello 通知的優先順序。 請參閱 hello **HTTP 標頭項目**區段 hello[推播通知從伺服器](http://msdn.microsoft.com/library/hh221551.aspx)文件適用於有效的值。
* **Options** - 選用的要求標頭。
* **回呼**-hello 回呼函式。

取得一份有效**TargetName**，**通知類別**和標頭檔選項，請參閱 hello[推播通知從伺服器](http://msdn.microsoft.com/library/hh221551.aspx)頁面。

下列範例程式碼的 hello 使用 hello **MpnsService** hello 所公開的執行個體**NotificationHubService** toosend 快顯通知推播通知：

    var payload = '<?xml version="1.0" encoding="utf-8"?><wp:Notification xmlns:wp="WPNotification"><wp:Toast><wp:Text1>string</wp:Text1><wp:Text2>string</wp:Text2></wp:Toast></wp:Notification>';
    notificationHubService.mpns.send(null, payload, 'toast', 22, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-toouniversal-windows-platform-uwp-applications"></a>如何： 傳送推播通知 tooUniversal Windows 平台 (UWP) 應用程式
hello **WnsService**物件提供**傳送**可以是使用的 toosend 推播通知 tooUniversal Windows 平台應用程式的方法。  hello**傳送**方法可接受下列參數的 hello:

* **標記**-hello 標記識別項。 如果提供沒有標記，則 hello 會傳送通知 tooall 註冊用戶端。
* **裝載**-hello XML 訊息裝載。
* **型別**-hello 通知類型。
* **Options** - 選用的要求標頭。
* **回呼**-hello 回呼函式。

如需有效類型和要求標頭的清單，請參閱 [推播通知服務要求和回應標頭](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx)。

hello 下列程式碼使用 hello **WnsService** hello 所公開的執行個體**NotificationHubService** toosend 快顯通知推播通知 tooa UWP 應用程式：

    var payload = '<toast><visual><binding template="ToastText01"><text id="1">Hello!</text></binding></visual></toast>';
    notificationHubService.wns.send(null, payload , 'wns/toast', function(error){
      if(!error){
         // notification sent
      }
    });

## <a name="next-steps"></a>後續步驟
可讓您 tooeasily 組建服務基礎結構 toodeliver 推播通知 tooa 各式各樣的裝置 hello 範例程式碼片段上方。 既然您已經學會使用 node.js 通知中樞的 hello 基本概念，請遵循這些連結 toolearn 深入了解如何擴充進一步這些功能。

* 請參閱 hello 的 MSDN 參考[Azure 通知中樞](https://msdn.microsoft.com/library/azure/jj927170.aspx)。
* 請瀏覽 hello [Azure SDK for 節點]GitHub 上的儲存機制，如需詳細的範例和實作詳細資料。

[Azure SDK for 節點]: https://github.com/WindowsAzure/azure-sdk-for-node
[Next Steps]: #nextsteps
[What are Service Bus Topics and Subscriptions?]: #what-are-service-bus-topics
[Create a Service Namespace]: #create-a-service-namespace
[Obtain hello Default Management Credentials for hello Namespace]: #obtain-default-credentials
[Create a Node.js Application]: #Create_a_Nodejs_Application
[Configure Your Application tooUse Service Bus]: #Configure_Your_Application_to_Use_Service_Bus
[How to: Create a Topic]: #How_to_Create_a_Topic
[How to: Create Subscriptions]: #How_to_Create_Subscriptions
[How to: Send Messages tooa Topic]: #How_to_Send_Messages_to_a_Topic
[How to: Receive Messages from a Subscription]: #How_to_Receive_Messages_from_a_Subscription
[How to: Handle Application Crashes and Unreadable Messages]: #How_to_Handle_Application_Crashes_and_Unreadable_Messages
[How to: Delete Topics and Subscriptions]: #How_to_Delete_Topics_and_Subscriptions
[1]: #Next_Steps
[Topic Concepts]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-topics-01.png
[Azure Classic Portal]: http://manage.windowsazure.com
[image]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-03.png
[2]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-04.png
[3]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-05.png
[4]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-06.png
[5]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-07.png
[SqlFilter.SqlExpression]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.sqlexpression.aspx
[Azure Service Bus Notification Hubs]: http://msdn.microsoft.com/library/windowsazure/jj927170.aspx
[SqlFilter]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.aspx
[使用 WebMatrix 的網站]: /develop/nodejs/tutorials/web-site-with-webmatrix/
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Previous Management Portal]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/previous-portal.png
[nodejswebsite]: /develop/nodejs/tutorials/create-a-website-(mac)/
[Node.js Cloud Service with Storage]: /develop/nodejs/tutorials/web-app-with-storage/
[Node.js Web Application with Storage]: /develop/nodejs/tutorials/web-site-with-storage/
[Azure 入口網站]: https://portal.azure.com
