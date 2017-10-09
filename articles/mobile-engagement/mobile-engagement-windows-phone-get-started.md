---
title: "aaaGet 開始使用 Azure Mobile Engagement 的 Windows Phone Silverlight 應用程式"
description: "深入了解如何 toouse Azure Mobile Engagement 與為 Windows Phone Silverlight 應用程式的分析和推播通知。"
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: aa34692f-87f7-47c6-a20c-a1972750bc25
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b39a838ab03217b2dc845cbf59d7bf8b094dac1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-phone-silverlight-apps"></a>開始使用適用於 Windows Phone Silverlight 應用程式的 Azure Mobile Engagement
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

本主題說明如何 toouse Azure Mobile Engagement toounderstand 您的應用程式使用量和傳送推播通知 toosegmented 使用者的 Windows Phone Silverlight 應用程式。
本教學課程會示範簡單 hello 使用 Mobile Engagement 廣播的案例。 在課程中，您將建立一個空白的 Windows Phone Silverlight 應用程式，以使用 Microsoft 推播通知服務 (MPNS) 來收集基本資料及接收推播通知。

> [!NOTE]
> hello Azure Mobile Engagement 服務將會遭到淘汰年 3 月 2018年，目前只使用 tooexisting 客戶。 如需詳細資訊，請參閱 [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/)。

> [!NOTE]
> Visual Studio 2017 不支援 Windows Phone 8.1 和舊版專案。  如需詳細資訊，請參閱 [Visual Studio 2017 平台目標及相容性](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs)。

> [!NOTE]
> 如果您的目標 Windows Phone 8.1 (非 Silverlight)，請參閱 toohello [Windows 通用的教學課程](mobile-engagement-windows-store-dotnet-get-started.md)。
> 
> 

本教學課程必須 hello 下列需求：

* Visual Studio 2013
* [MicrosoftAzure.MobileEngagement] Nuget 封裝

> [!NOTE]
> toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started)。
> 
> 

## <a id="setup-azme"></a>設定 Windows Phone 應用程式的 Mobile Engagement
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>連接您的應用程式 toohello Mobile Engagement 後端
此教學課程提供 < 基本整合 >，其最小的 hello 設定必要的 toocollect 資料，並傳送推播通知。 hello 完整的整合文件可以在 hello [Mobile Engagement Windows Phone SDK 整合](mobile-engagement-windows-phone-sdk-overview.md)

我們會建立基本應用程式與 Visual Studio toodemonstrate hello 整合。

### <a name="create-a-new-windows-phone-silverlight-project"></a>建立新的 Windows Phone Silverlight 專案
hello 下列步驟假設 hello 使用 Visual Studio 2015 雖然在舊版的 Visual Studio 中的 hello 步驟如下。 

1. 啟動 Visual Studio，並在 hello**首頁**畫面上，選取**新專案**。
2. 在 hello 快顯視窗中，選取  **Windows 8** -> **Windows Phone** -> **空白應用程式 (Windows Phone Silverlight)**。 Hello 應用程式中填滿**名稱**和**方案名稱**，然後按一下**確定**。
   
    ![][1]
3. 您可以選擇 tootarget 或是**Windows Phone 8.0**或**Windows Phone 8.1**。

您現在已建立新的 Windows Phone Silverlight 應用程式，我們將會在其中整合 hello Azure Mobile Engagement SDK。

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a>連接您的應用程式 toohello Mobile Engagement 後端
1. 安裝 hello [MicrosoftAzure.MobileEngagement]專案中的 nuget 封裝。
2. 開啟`WMAppManifest.xml`（hello 屬性 資料夾） 下，並確定 hello 下列宣告 （加入它們如果不是） 在 hello`<Capabilities />`標記：
   
        <Capability Name="ID_CAP_NETWORKING" />
        <Capability Name="ID_CAP_IDENTITY_DEVICE" />
   
    ![][2]
3. 現在貼上您先前複製您的 Mobile Engagement 應用程式的 hello 連接字串，並將它貼在 hello `Resources\EngagementConfiguration.xml` hello 之間的檔案，`<connectionString>`和`</connectionString>`標記：
   
    ![][3]
4. 在 hello`App.xaml.cs`檔案：
   
    a. 新增 hello`using`陳述式：
   
            using Microsoft.Azure.Engagement;
   
    b. 初始化 hello SDK 中 hello`Application_Launching`方法：
   
            private void Application_Launching(object sender, LaunchingEventArgs e)
            {
              EngagementAgent.Instance.Init();
            }
   
    c. 在 hello 中插入下列 hello `Application_Activated`:
   
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
               EngagementAgent.Instance.OnActivated(e);
            }

## <a id="monitor"></a>啟用即時監視
在順序 toostart 傳送資料，並確保 hello 使用者使用中，您必須傳送至少一個螢幕 （活動） toohello Mobile Engagement 後端。

1. 在 hello MainPage.xaml.cs，新增 hello`using`陳述式：
   
        using Microsoft.Azure.Engagement;
2. 取代 hello 基底類別**MainPage**，這是之前**PhoneApplicationPage**，與**EngagementPage**。
   
        class MainPage : EngagementPage 
3. 在您的 `MainPage.xml` 檔案中：
   
    a. 加入 tooyour 命名空間宣告：
   
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
   
    b. 取代`phone:PhoneApplicationPage`hello XML 標記名稱與`engagement:EngagementPage`。

## <a id="monitor"></a>將 App 與即時監視連接
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>啟用推播通知與 App 內傳訊
Mobile Engagement 可讓您 toointeract，並連線到您推播通知與 hello 內容的活動中的應用程式內訊息的使用者。 此模組會呼叫觸達 hello Mobile Engagement 入口網站中。
hello 下列各節將設定您的應用程式 tooreceive 它們。

### <a name="enable-your-app-tooreceive-mpns-push-notifications"></a>啟用您的應用程式 tooreceive MPNS 的推播通知
加入新的功能 tooyour`WMAppManifest.xml`檔案：

        ID_CAP_PUSH_NOTIFICATION
        ID_CAP_WEBBROWSERCOMPONENT

   ![][5]

### <a name="initialize-hello-reach-sdk"></a>初始化 hello REACH SDK
1. 在`App.xaml.cs`，呼叫`EngagementReach.Instance.Init();`在 hello **Application_Launching**函式，後面 hello 代理程式初始化：
   
        private void Application_Launching(object sender, LaunchingEventArgs e)
        {
           EngagementAgent.Instance.Init();
           EngagementReach.Instance.Init();
        }
2. 在`App.xaml.cs`，呼叫`EngagementReach.Instance.OnActivated(e);`在 hello **Application_Activated**函式，後面 hello 代理程式初始化：
   
        private void Application_Activated(object sender, ActivatedEventArgs e)
        {
           EngagementAgent.Instance.OnActivated(e);
           EngagementReach.Instance.OnActivated(e);
        }

您全都準備好了。 現在我們要驗證您已正確完成這項基本整合。

## <a id="send"></a>傳送通知 tooyour 應用程式
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

您現在應該會看到通知將會顯示您裝置上以應用程式內通知是否 hello 應用程式開啟否則當做快顯通知 hello 如下： 

![][6]

<!-- URLs. -->
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9874664
[Mobile Engagement Windows Phone SDK documentation]: ../mobile-engagement-windows-phone-integrate-engagement/

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-phone-get-started/project-properties.png
[2]: ./media/mobile-engagement-windows-phone-get-started/wmappmanifest-capabilities.png
[3]: ./media/mobile-engagement-windows-phone-get-started/add-connection-string.png
[5]: ./media/mobile-engagement-windows-phone-get-started/reach-capabilities.png
[6]: ./media/mobile-engagement-windows-phone-get-started/push-screenshot.png
