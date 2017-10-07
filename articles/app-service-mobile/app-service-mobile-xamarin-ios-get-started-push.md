---
title: "aaaAdd 推播通知 tooyour Xamarin.iOS 應用程式使用 Azure App Service"
description: "了解如何 toouse Azure App Service toosend 推播通知 tooyour Xamarin.iOS 應用程式"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 2921214a-49f8-45e1-a306-a85ce21defca
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: glenga
ms.openlocfilehash: 3e6439aee4f3fe0f60b9786d0bbfd74c4f5e52d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinios-app"></a>加入推播通知 tooyour Xamarin.iOS 應用程式
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>概觀
在本教學課程中，您將加入推播通知 toohello [Xamarin.iOS 快速入門](app-service-mobile-xamarin-ios-get-started.md)專案，以便每次將記錄插入推播通知會傳送 toohello 裝置。

如果您不要使用 hello 下載快速入門的伺服器專案，您將需要 hello 推播通知擴充套件。 請參閱[Azure 行動應用程式使用 hello.NET 後端伺服器 SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)如需詳細資訊。

## <a name="prerequisites"></a>必要條件
* 完整的 hello [Xamarin.iOS 快速入門](app-service-mobile-xamarin-ios-get-started.md)教學課程。
* 實體的 iOS 裝置。 推播通知不會受到 hello iOS 模擬器。

## <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a>註冊 Apple 開發人員入口網站上的推播通知的 hello 應用程式
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-your-mobile-app-toosend-push-notifications"></a>設定您的行動裝置應用程式 toosend 推播通知
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a>更新 hello 伺服器專案 toosend 推播通知
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-your-xamarinios-project"></a>設定您的 Xamarin.iOS 專案
[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

## <a name="add-push-notifications-tooyour-app"></a>新增推播通知 tooyour 應用程式
1. 在**QSTodoService**，新增下列屬性的 hello 以便**AppDelegate**可以取得 hello 行動用戶端：
   
            public MobileServiceClient GetClient {
            get
            {
                return client;
            }
            private set
            {
                client = value;
            }
        }
2. 新增下列 hello`using`陳述式 toohello 頂端 hello **d**檔案。
   
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. 在**AppDelegate**，覆寫 hello **FinishedLaunching**事件：
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            // registers for push for iOS8
            var settings = UIUserNotificationSettings.GetSettingsForTypes(
                UIUserNotificationType.Alert
                | UIUserNotificationType.Badge
                | UIUserNotificationType.Sound,
                new NSSet());
   
            UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications();
   
            return true;
        }
4. 在 hello 同一個檔案中覆寫 hello **RegisteredForRemoteNotifications**事件。 這個程式碼中您所註冊依 hello 伺服器會傳送跨所有支援平台為簡單的範本通知。
   
    如需有關通知中樞範本的詳細資訊，請參閱 [範本](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md)。

        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            MobileServiceClient client = QSTodoService.DefaultService.GetClient;

            const string templateBodyAPNS = "{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
                {"body", templateBodyAPNS}
            };

            // Register for push with your mobile app
            var push = client.GetPush();
            push.RegisterAsync(deviceToken, templates);
        }


1. 然後，覆寫 hello **DidReceivedRemoteNotification**事件：
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, Action<UIBackgroundFetchResult> completionHandler)
        {
            NSDictionary aps = userInfo.ObjectForKey(new NSString("aps")) as NSDictionary;
   
            string alert = string.Empty;
            if (aps.ContainsKey(new NSString("alert")))
                alert = (aps [new NSString("alert")] as NSString).ToString();
   
            //show alert
            if (!string.IsNullOrEmpty(alert))
            {
                UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                avAlert.Show();
            }
        }

您的應用程式已更新的 toosupport 推播通知。

## <a name="test"></a>在應用程式中測試推播通知
1. 按 hello**執行**按鈕 toobuild hello 專案並開始 hello 應用程式在 iOS 支援的裝置，然後按一下**確定**tooaccept 推播通知。
   
   > [!NOTE]
   > 您必須明確地接受來自應用程式的推播通知。 此要求才會發生 hello hello 應用程式執行的第一次。
   > 
   > 
2. 在 hello 應用程式，請在類型的工作，，，然後按一下加號 hello (**+**) 圖示。
3. 請確認已收到通知，然後按一下 **確定**toodismiss hello 通知。
4. 重複步驟 2 到立即關閉 hello 應用程式，然後確認已顯示通知。

您已成功完成此教學課程。

<!-- Images. -->

<!-- URLs. -->



