---
title: "aaaGet Started with Xamarin.Android 的 Azure Mobile Engagement"
description: "深入了解如何使用分析及推播通知 Xamarin.Android 應用程式的 Azure Mobile Engagement toouse。"
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: fb68cf98-08a2-41b5-8e59-757469de3fe7
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/16/2016
ms.author: piyushjo
ms.openlocfilehash: 9d584fea8e8153d511258cf9b6f87f31dac6aeca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinandroid-apps"></a>開始使用適用於 Xamarin.Android 應用程式的 Azure Mobile Engagement
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

本主題說明如何 toouse Azure Mobile Engagement toounderstand 應用程式使用量和 toosend 推播通知 toosegmented 使用者 Xamarin.Android 應用程式的方式。
本教學課程會示範簡單 hello 使用 Mobile Engagement 廣播的案例。 在本教學課程中，您將使用 Google 雲端通訊 (GCM)，建立可收集基本資料和接收推播通知的空白 Xamarin.Android 應用程式。

> [!NOTE]
> hello Azure Mobile Engagement 服務將會遭到淘汰年 3 月 2018年，目前只使用 tooexisting 客戶。 如需詳細資訊，請參閱 [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/)。

本教學課程必須 hello 下列需求：

* [Xamarin Studio](http://xamarin.com/studio)。 您也可以使用 Visual Studio 搭配 Xamarin，但本教學課程會使用 Xamarin Studio。 如需安裝指示，請參閱[設定和安裝 Visual Studio 和 Xamarin](https://msdn.microsoft.com/library/mt613162.aspx)。
* [Mobile Engagement Xamarin SDK](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started)。
> 
> 

## <a id="setup-azme"></a>為您的 Android 應用程式設定 Mobile Engagement
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>連接您的應用程式 toohello Mobile Engagement 後端
此教學課程提供 < 基本整合 >，其最小的 hello 設定必要的 toocollect 資料，並傳送推播通知。 

我們將使用 Xamarin Studio toodemonstrate hello 整合來建立基本應用程式。

### <a name="create-a-new-xamarinandroid-project"></a>建立新的 Xamarin.Android 專案
1. 啟動**Xamarin Studio**太移**檔案** -> **新增** -> **方案** 
   
    ![][1]
2. 選取**Android 應用程式**確定選取的 hello 語言是**C#**按一下**下一步**。
   
    ![][2]
3. 填寫 hello**應用程式名稱**和 hello**組織識別碼**。 請確定 toocheckmark **Google Play 服務**，然後按一下**下一步**。 
   
    ![][3]
4. 更新 hello**專案名稱**，**方案名稱**和**位置**如果需要，然後按一下 **建立**。
   
    ![][4]

Xamarin Studio 將會建立在其中，我們將會整合 Mobile Engagement hello 應用程式。 

### <a name="connect-your-app-toomobile-engagement-backend"></a>連接您的應用程式 tooMobile Engagement 後端
1. 以滑鼠右鍵按一下 hello**封裝**hello 方案 windows 和選取資料夾**新增套件...**
   
    ![][5]
2. 搜尋 hello **Microsoft Azure Mobile Engagement Xamarin SDK**並將它加入 tooyour 方案。  
   
    ![][6]
3. 開啟**Weatherapp**並加入 hello 下列 using 陳述式：
   
        using Microsoft.Azure.Engagement;
        using Microsoft.Azure.Engagement.Activity;
4. 在 hello`OnCreate`方法中，新增下列 tooinitialize hello 連線與 Mobile Engagement 後端的 hello。 請確定 tooadd 您**ConnectionString**。 
   
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.ConnectionString = "YourConnectionStringFromAzurePortal";
        EngagementAgent.Init(engagementConfiguration);

### <a name="add-permissions-and-a-service-declaration"></a>新增權限和服務宣告
1. 開啟 [hello **Manifest.xml** hello 屬性] 資料夾下的檔案。 選取來源 索引標籤，好讓您直接更新 hello XML 來源。
2. 加入這些權限 toohello Manifest.xml (這可以在 hello 下找到**屬性**資料夾) 的專案之前或之後 hello`<application>`標記：
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
3. 新增 hello 下列之間 hello`<application>`和`</application>`標記 toodeclare hello 代理程式服務：
   
        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
4. 在您剛才貼上 hello 程式碼，取代`"<Your application name>"`hello 標籤中。 這會顯示在 hello**設定**功能表的使用者可以查看 hello 裝置上執行服務的位置。 您可以加入 hello word 「 服務 」，例如在該標籤。

### <a name="send-a-screen-toomobile-engagement"></a>傳送螢幕 tooMobile Engagement
在訂單 toostart 傳送資料，並確保 hello 的使用者，您必須傳送至少一個螢幕 toohello Mobile Engagement 後端。 執行此作業-請確認該 hello`MainActivity`繼承自`EngagementActivity`而不是`Activity`。

    public class MainActivity : EngagementActivity

或者，如果您無法繼承自 `EngagementActivity`，則必須分別在 `OnResume` 和 `OnPause` 中新增 `.StartActivity` 和 `.EndActivity` 方法。  

        protected override void OnResume()
            {
                EngagementAgent.StartActivity(EngagementAgentUtils.BuildEngagementActivityName(Java.Lang.Class.FromType(this.GetType())), null);
                base.OnResume();             
            }

            protected override void OnPause()
            {
                EngagementAgent.EndActivity();
                base.OnPause();            
            }

## <a id="monitor"></a>將 App 與即時監視連接
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>啟用推播通知與 App 內傳訊
Mobile Engagement 可讓您與 toointeract，並連線到您的推播通知及應用程式內訊息的活動 hello 內容中的使用者。 此模組會呼叫觸達 hello Mobile Engagement 入口網站中。
下列各節的 hello 設定您的應用程式 tooreceive 它們。

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[1]: ./media/mobile-engagement-xamarin-android-get-started/1.png
[2]: ./media/mobile-engagement-xamarin-android-get-started/2.png
[3]: ./media/mobile-engagement-xamarin-android-get-started/3.png
[4]: ./media/mobile-engagement-xamarin-android-get-started/4.png
[5]: ./media/mobile-engagement-xamarin-android-get-started/5.png
[6]: ./media/mobile-engagement-xamarin-android-get-started/6.png
