---
title: "aaaGet Started with Xamarin.iOS 的 Azure Mobile Engagement"
description: "深入了解如何使用分析及推播通知 Xamarin.iOS 應用程式的 Azure Mobile Engagement toouse。"
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0448209e-fff6-47bd-985c-2cf074bac12f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 02340a744753dcc5cd1b6888a5fa87628be47b68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinios-apps"></a>開始使用適用於 Xamarin.iOS 應用程式的 Azure Mobile Engagement
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

本主題說明如何 toouse Azure Mobile Engagement toounderstand 您的應用程式使用量和傳送推播通知 toosegmented 使用者 Xamarin.iOS 應用程式中。
在本教學課程中，您將使用 Apple 推播通知服務 (APNS)，建立可收集基本資料，並接收推播通知的空白 Xamarin.iOS 應用程式。

> [!NOTE]
> hello Azure Mobile Engagement 服務將會遭到淘汰年 3 月 2018年，目前只使用 tooexisting 客戶。 如需詳細資訊，請參閱 [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/)。

本教學課程必須 hello 下列需求：

* [Xamarin Studio](http://xamarin.com/studio)。 您也可以使用 Visual Studio 搭配 Xamarin，但本教學課程會使用 Xamarin Studio。 如需安裝指示，請參閱[設定和安裝 Visual Studio 和 Xamarin](https://msdn.microsoft.com/library/mt613162.aspx)。 
* [Mobile Engagement Xamarin SDK](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started)。
> 
> 

## <a id="setup-azme"></a>為您的 iOS 應用程式設定 Mobile Engagement
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>連接您的應用程式 toohello Mobile Engagement 後端
此教學課程提供 < 基本整合 > hello 最小設定必要的 toocollect 資料及傳送推播通知。

我們將使用 Xamarin toodemonstrate hello 整合，以建立基本應用程式：

### <a name="create-a-new-xamarinios-project"></a>建立新的 Xamarin.iOS 專案
1. 啟動 Xamarin Studio。 跳過**檔案** -> **新增** -> **方案** 
   
    ![][1]
2. 選取**單一檢視應用程式**，請確定選取的 hello 語言是**C#** ，然後按一下**下一步**。
   
    ![][2]
3. 填寫 hello**應用程式名稱**和 hello**組織識別碼**，然後按一下**下一步**。 
   
    ![][3]
   
   > [!IMPORTANT]
   > 請確定該 hello 發行設定檔，您最終會使用的 toodeploy iOS 應用程式使用與您在這裡有的配套識別碼 hello 完全符合應用程式識別碼。 
   > 
   > 
4. 更新 hello**專案名稱**，**方案名稱**和**位置**如果需要，然後按一下 **建立**。
   
    ![][4]

Xamarin Studio 將會建立在其中，我們將會整合 Mobile Engagement hello 示範應用程式。 

### <a name="connect-your-app-toomobile-engagement-backend"></a>連接您的應用程式 tooMobile Engagement 後端
1. 以滑鼠右鍵按一下 hello**封裝**hello 方案 windows 和選取資料夾**新增套件...**
   
    ![][5]
2. 搜尋 hello **Microsoft Azure Mobile Engagement Xamarin SDK**並將它加入 tooyour 方案。  
   
    ![][6]
3. 開啟**d**並加入 hello 下列 using 陳述式：
   
        using Microsoft.Azure.Engagement.Xamarin;
4. 在 hello **FinishedLaunching**方法中，新增下列 tooinitialize hello 連線與 Mobile Engagement 後端的 hello。 請確定 tooadd 您**ConnectionString**。 此程式碼也會使用假**NotificationIcon** hello Mobile Engagement SDK，您可能想要新增的 tooreplace。 
   
        EngagementConfiguration config = new EngagementConfiguration {
                        ConnectionString = "YourConnectionStringFromAzurePortal",
                        NotificationIcon = UIImage.FromBundle("close")
                    };
        EngagementAgent.Init (config);

## <a id="monitor"></a>啟用即時監視
在訂單 toostart 傳送資料，並確保 hello 的使用者，您必須傳送至少一個螢幕 toohello Mobile Engagement 後端。

1. 開啟**ViewController.cs**並加入 hello 下列 using 陳述式：
   
        using Microsoft.Azure.Engagement.Xamarin;
2. 取代 hello 類別`ViewController`繼承自`UIViewController`太`EngagementViewController`。 

## <a id="monitor"></a>將 App 與即時監視連接
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>啟用推播通知與 App 內傳訊
Mobile Engagement 可讓您與您的使用者 toointeract 和觸達推播通知與應用程式內訊息的活動 hello 內容中。 此模組會呼叫觸達 hello Mobile Engagement 入口網站中。
hello 下列各節將設定您的應用程式 tooreceive 它們。

### <a name="modify-your-application-delegate"></a>修改您的應用程式代理人
1. 開啟 hello **d**並加入 hello 下列 using 陳述式：
   
        using System; 
2. 現在內 hello`FinishedLaunching`方法，加入下列 tooregister 推播訊息之後的 hello`EngagementAgent.init(...)`
   
        if (UIDevice.CurrentDevice.CheckSystemVersion(8,0))
        {
            var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                (UIUserNotificationType.Badge |
                    UIUserNotificationType.Sound |
                    UIUserNotificationType.Alert),
                null);
            UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications ();
        }
        else
        {
            UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (
                UIRemoteNotificationType.Badge |
                UIRemoteNotificationType.Sound |
                UIRemoteNotificationType.Alert);
        }
3. 最後的更新，或新增 hello 下列方法：
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, 
            Action<UIBackgroundFetchResult> completionHandler)
        {
            EngagementAgent.ApplicationDidReceiveRemoteNotification(userInfo, completionHandler);
        }
   
        public override void RegisteredForRemoteNotifications (UIApplication application, NSData deviceToken)
        {
            // Register device token on Engagement
            EngagementAgent.RegisterDeviceToken(deviceToken);
        }
   
        public override void FailedToRegisterForRemoteNotifications(UIApplication application, NSError error)
        {
            Console.WriteLine("Failed tooregister for remote notifications: Error '{0}'", error);
        }
4. 在您**Info.plist** hello 方案中的檔案，請確認該 hello**配套識別碼**符合以 hello**應用程式識別碼**hello Apple 開發人員在您佈建設定檔中有置中。 
   
    ![][7]
5. 在 hello 相同**Info.plist**檔案，請確定您已核取 hello**啟用背景模式**和**遠端通知**。 
   
     ![][8]
6. 在您已經與此發行設定檔關聯的 hello 裝置上執行 hello 應用程式。 

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[1]: ./media/mobile-engagement-xamarin-ios-get-started/new-solution.png
[2]: ./media/mobile-engagement-xamarin-ios-get-started/app-type.png
[3]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-name.png
[4]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-confirm.png
[5]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget.png
[6]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget-azme.png
[7]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-confirm-bundle.png
[8]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-configure-push.png
