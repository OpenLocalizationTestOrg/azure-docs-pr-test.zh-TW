---
title: "aaaSend 跨平台通知 toousers 與通知中樞 (ASP.NET)"
description: "深入了解如何在單一要求中，所有平台為目標的無從驗證平台通知，toouse 通知中樞範本 toosend。"
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 11d2131b-f683-47fd-a691-4cdfc696f62b
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: multiple
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: f105b871b809e739dd5c05ea819ad135e842ebb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="send-cross-platform-notifications-toousers-with-notification-hubs"></a>傳送跨平台通知 toousers 與通知中樞
Hello 上一個教學課程中[向使用者通知中樞通知]，您學到如何 toopush 通知 tooall 裝置註冊特定的已驗證使用者。 在此教學課程中，在多個要求提供了必要的 toosend 通知支援 tooeach 用戶端平台。 通知中心支援範本，可讓您指定特定的裝置想 tooreceive 通知的方式。 這使得傳送跨平台通知變得更簡單。 本主題示範如何在單一要求中，所有平台為目標的無從驗證平台通知的範本 toosend tootake 優點。 如需這些範本的詳細資訊，請參閱 [Azure 通知中樞概觀][Templates]。
> [!IMPORTANT]
> Windows Phone 8.1 及更早版本的專案不支援使用 Visual Studio 2017。 如需詳細資訊，請參閱 [Visual Studio 2017 平台目標及相容性](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs)。

> [!NOTE]
> 通知中樞可讓裝置 tooregister hello 與多個範本相同的標記。 在此情況下，目標標記，會導致多個通知的內送訊息傳遞 toohello 裝置，一個用於每個範本。 這樣做可讓您 toodisplay hello 相同訊息中多個視覺通知的詳細資訊，例如同時當做徽章和 Windows 市集應用程式中的快顯通知。
> 
> 

完成下列步驟 toosend 跨平台通知使用範本的 hello:

1. 在 hello Visual Studio 中的 方案總管 中，展開 hello**控制器**資料夾，然後開啟 hello RegisterController.cs 檔案。
2. 在 hello 中尋找的程式碼的 hello 區塊**放**建立新註冊的方法取代 hello`switch`內容以下列程式碼的 hello:
   
        switch (deviceUpdate.Platform)
        {
            case "mpns":
                var toastTemplate = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>$(message)</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
                registration = new MpnsTemplateRegistrationDescription(deviceUpdate.Handle, toastTemplate);
                break;
            case "wns":
                toastTemplate = @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(message)</text></binding></visual></toast>";
                registration = new WindowsTemplateRegistrationDescription(deviceUpdate.Handle, toastTemplate);
                break;
            case "apns":
                var alertTemplate = "{\"aps\":{\"alert\":\"$(message)\"}}";
                registration = new AppleTemplateRegistrationDescription(deviceUpdate.Handle, alertTemplate);
                break;
            case "gcm":
                var messageTemplate = "{\"data\":{\"message\":\"$(message)\"}}";
                registration = new GcmTemplateRegistrationDescription(deviceUpdate.Handle, messageTemplate);
                break;
            default:
                throw new HttpResponseException(HttpStatusCode.BadRequest);
        }
   
    此程式碼會呼叫 hello 平台專屬方法 toocreate 範本註冊，而不是原生註冊。 不需要修改現有註冊，因為範本註冊源自原生註冊。
3. 在 hello**通知**控制站，取代 hello **sendNotification**方法，以下列程式碼的 hello:
   
        public async Task<HttpResponseMessage> Post()
        {
            var user = HttpContext.Current.User.Identity.Name;
            var userTag = "username:" + user;
   
            var notification = new Dictionary<string, string> { { "message", "Hello, " + user } };
            await Notifications.Instance.Hub.SendTemplateNotificationAsync(notification, userTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
    此程式碼會傳送通知 tooall 平台在 hello 相同時間，而不需要 toospecify 原生的裝載。 通知中樞建置並傳送 hello 以 hello 提供正確的裝載 tooevery 裝置*標記*hello 註冊範本中所指定的值。
4. 重新發佈您的 WebApi 後端專案。
5. 再次執行 hello 用戶端應用程式，並驗證註冊成功。
6. （選擇性）部署 hello 用戶端應用程式 tooa 第二個裝置，然後執行 hello 應用程式。
   
    請留意到，每個裝置上都會顯示通知。

## <a name="next-steps"></a>後續步驟
您已完成本教學課程，現在可參閱下列主題進一步了解通知中心和範本：

* **[使用通知中樞 toosend 最新消息]** <br/>示範另一個使用範本的案例
* **[Azure 通知中樞概觀][Templates]**<br/>概觀主題包含範本的詳細資訊。

<!-- Anchors. -->

<!-- Images. -->




<!-- URLs. -->
[Push toousers ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Push toousers Mobile Services]: /manage/services/notification-hubs/notify-users/
[Visual Studio 2012 Express for Windows 8]: http://go.microsoft.com/fwlink/?LinkId=257546

[使用通知中樞 toosend 最新消息]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
[Azure Notification Hubs]: http://go.microsoft.com/fwlink/p/?LinkId=314257
[向使用者通知中樞通知]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Templates]: http://go.microsoft.com/fwlink/p/?LinkId=317339
[Notification Hub How toofor Windows Store]: http://msdn.microsoft.com/library/windowsazure/jj927172.aspx
