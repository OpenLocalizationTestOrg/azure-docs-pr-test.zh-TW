---
title: "開始使用 Windows 通用應用程式 Azure Mobile Engagement aaaGet"
description: "深入了解如何 toouse Azure Mobile Engagement 與為 Windows 通用應用程式的分析和推播通知。"
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: 48103867-7f64-4646-b019-42bd797d38e2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 8224a6d3789cfe4784bbc9472005f9eddb94a8b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-universal-apps"></a>開始使用適用於 Windows 通用 App 的 Azure Mobile Engagement
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

本主題說明如何 toouse Azure Mobile Engagement toounderstand 您的應用程式使用量和傳送推播通知 toosegmented 使用者的 Windows 通用應用程式。
本教學課程會示範簡單 hello 使用 Mobile Engagement 廣播的案例。 您建立一個空白的 Windows 通用應用程式，以使用 Windows 通知服務 (WNS) 來收集基本的應用程式使用資料及接收推播通知。

> [!NOTE]
> hello Azure Mobile Engagement 服務將會遭到淘汰年 3 月 2018年，目前只使用 tooexisting 客戶。 如需詳細資訊，請參閱 [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/)。

## <a name="prerequisites"></a>必要條件
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="set-up-mobile-engagement-for-your-windows-universal-app"></a>設定 Windows 通用應用程式的 Mobile Engagement
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>連接您的應用程式 toohello Mobile Engagement 後端
此教學課程提供 < 基本整合，"hello 最小設定必要的 toocollect 資料及傳送推播通知。 hello 完整的整合文件可以在 hello [Mobile Engagement Windows 通用 SDK 整合](mobile-engagement-windows-store-sdk-overview.md)。

您可以建立基本應用程式與 Visual Studio toodemonstrate hello 整合。

### <a name="create-a-windows-universal-app-project"></a>建立一個 Windows 通用應用程式專案
hello 下列步驟假設 hello 使用 Visual Studio 2015 雖然在舊版的 Visual Studio 中的 hello 步驟如下。

1. 啟動 Visual Studio，並在 hello**首頁**畫面上，選取**新專案**。
2. 在 hello 快顯視窗中，選取  **Windows** -> **通用** -> **空白應用程式 (通用 Windows)**。 Hello 應用程式中填滿**名稱**和**方案名稱**，然後按一下**確定**。

    ![][1]

您現在已建立在其中您接下來整合 hello Azure Mobile Engagement SDK 的 Windows 通用應用程式專案。

### <a name="connect-your-app-toomobile-engagement-backend"></a>連接您的應用程式 tooMobile Engagement 後端
1. 安裝 hello [MicrosoftAzure.MobileEngagement]專案中的 Nuget 封裝。 如果您將目標設定 Windows 和 Windows Phone 平台，您需要 toodo 這兩個專案。 適用於 Windows 8.x 和 Windows Phone 8.1，hello 相同 Nuget 封裝上的芳鄰 hello 正確平台專屬的二進位檔案中的每個專案。
2. 開啟**Package.appxmanifest**並確定已那里加入該 hello 下列功能：

        Internet (Client)

    ![][2]
3. 現在將 hello 您之前複製您的 Mobile Engagement 應用程式的連接字串複製並貼入 hello `Resources\EngagementConfiguration.xml` hello 之間的檔案，`<connectionString>`和`</connectionString>`標記：

    ![][3]

    > [!TIP]
    > 如果您的應用程式以 Windows 和 Windows Phone 兩個平台為目標，那麼您仍應該建立兩個 Mobile Engagment 應用程式，讓每個支援的平台各使用一個。 有兩個應用程式，可確保您可以建立正確的分割 hello 對象，並將每個平台的適當目標的通知傳送。

    > [!IMPORTANT]
    > NuGet 不會自動複製 hello SDK 資源，以在 Windows 10 UWP 應用程式中。 您將 toodo 它手動遵循 (readme.txt) hello Nuget 封裝安裝時，顯示 hello 步驟。  

1. 在 hello`App.xaml.cs`檔案：

    a. 新增 hello`using`陳述式：

            using Microsoft.Azure.Engagement;

    b. 加入的方法，初始化 hello Engagement:

           private void InitEngagement(IActivatedEventArgs e)
           {
             EngagementAgent.Instance.Init(e);

             //... rest of hello code
           }

    c. 初始化 hello SDK 中 hello **OnLaunched**方法：

            protected override void OnLaunched(LaunchActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

    c. 插入 hello hello 下列**OnActivated**方法並加入 hello 方法，如果尚不存在：

            protected override void OnActivated(IActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

## <a id="monitor"></a>啟用即時監視
toostart 傳送資料和 hello 使用者都已使用中，您必須傳送至少一個螢幕 （活動） toohello Mobile Engagement 後端。

1. 在 hello **MainPage.xaml.cs**，加入下列 hello`using`陳述式：

    using Microsoft.Azure.Engagement.Overlay;
2. 變更 hello 基底類別**MainPage**從**頁面**太**EngagementPageOverlay**:

        class MainPage : EngagementPageOverlay
3. 在 hello`MainPage.xaml`檔案：

    a. 加入 tooyour 命名空間宣告：

        xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"

    b. 取代 hello**頁面**hello XML 標記名稱與**engagement: EngagementPageOverlay**

> [!IMPORTANT]
> 如果您的頁面會覆寫 hello`OnNavigatedTo`方法，是確定 toocall `base.OnNavigatedTo(e)`。 否則，hello 活動不會報告`EngagementPage`呼叫`StartActivity`內其`OnNavigatedTo`方法)。 這點特別重要，在 Windows Phone 專案顯示 hello 預設範本已`OnNavigatedTo`方法。
>
> **Windows 10 通用應用程式**，使用 hello 方法建議 hello"建議使用的方法： 多載網頁類別 」 一節[進階報告功能與 hello Windows 通用應用程式 Engagement SDK](mobile-engagement-windows-store-advanced-reporting.md)而不是 hello 其中一個上面所述。

## <a id="monitor"></a>將 App 與即時監視連接
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>啟用推播通知與 App 內傳訊
Mobile Engagement 可讓您 toointeract，並連線到您的推播通知及應用程式內訊息的活動 hello 內容中的使用者。 此模組會呼叫觸達 hello Mobile Engagement 入口網站中。
hello 下列各節將設定您的應用程式 tooreceive 它們。

### <a name="enable-your-app-tooreceive-wns-push-notifications"></a>啟用您的應用程式 tooreceive WNS 推播通知
1. 在 hello`Package.appxmanifest`檔案，請在 hello**應用程式**索引標籤，在**通知**，將**支援快顯通知：**太**是**

    ![][5]

### <a name="initialize-hello-reach-sdk"></a>初始化 hello REACH SDK
在`App.xaml.cs`，呼叫**EngagementReach.Instance.Init(e);**在 hello **InitEngagement** hello 代理程式初始化之後函式：

        private void InitEngagement(IActivatedEventArgs e)
        {
           EngagementAgent.Instance.Init(e);
           EngagementReach.Instance.Init(e);
        }

您已準備好 toosend 快顯通知。 接下來我們要驗證您已正確完成這項基本整合。

### <a name="grant-access-toomobile-engagement-toosend-notifications"></a>授與存取 tooMobile Engagement toosend 通知
1. 在網頁瀏覽器中開啟 [Windows 市集開發人員中心] ，視需要登入和建立帳戶。
2. 按一下**儀表板**在 hello 右上角，然後按一下**建立新的應用程式**hello 左的面板功能表。

    ![][9]
3. 建立您的應用程式並保留其名稱。

    ![][10]
4. 一旦建立 hello 應用程式之後，瀏覽過**服務]-> [推播通知**hello 左側功能表中。

    ![][11]
5. 在 [hello 推播通知] 區段中，按一下 hello **Live 服務 」 站台**連結。

    ![][12]
6. 您瀏覽 toohello 推播認證 > 一節。 請確定您是在 hello**應用程式設定**區段，然後複製您**封裝 SID**和**用戶端密碼**

    ![][13]
7. 瀏覽 toohello**設定**Mobile Engagement 入口網站，按一下 hello**原生推送**hello 左側的 > 一節。 然後，按一下 hello**編輯**按鈕 tooenter 您**封裝安全性識別碼 (SID)**和您**秘密金鑰**所示：

    ![][6]
8. 最後請確定您已經與 hello 應用程式存放區中此建立應用程式關聯您的 Visual Studio 應用程式。 按一下 Visual Studio 中的 [建立應用程式與市集關聯]  。

    ![][7]

## <a id="send"></a>傳送通知 tooyour 應用程式
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

如果 hello 應用程式正在執行，您會看到應用程式內通知。 否則如果 hello 應用程式已關閉，您會看到快顯通知。
如果您看到的應用程式內通知，但不是快顯通知，而且您在 Visual Studio 中偵錯模式執行 hello 應用程式，然後再試一次**生命週期事件]-> [暫止**hello 工具列 tooensure 該 hello 應用程式會暫停。 如果您在偵錯 Visual Studio 中的 hello 應用程式時按一下 hello 首頁 按鈕，然後它不會永遠被暫停，而您為應用程式中看到 hello 通知，它不會顯示為快顯通知。  

![][8]

<!-- URLs. -->
[Mobile Engagement Windows Universal SDK documentation]: ../mobile-engagement-windows-store-integrate-engagement/
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9864592
[Windows 市集開發人員中心]: https://dev.windows.com
[Windows Universal Apps - Overlay integration]: ../mobile-engagement-windows-store-integrate-engagement-reach/#overlay-integration

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-store-dotnet-get-started/universal-app-creation.png
[2]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-capabilities.png
[3]: ./media/mobile-engagement-windows-store-dotnet-get-started/add-connection-info.png
[5]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-toast.png
[6]: ./media/mobile-engagement-windows-store-dotnet-get-started/enter-credentials.png
[7]: ./media/mobile-engagement-windows-store-dotnet-get-started/associate-app-store.png
[8]: ./media/mobile-engagement-windows-store-dotnet-get-started/vs-suspend.png
[9]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_create_app.png
[10]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_app_name.png
[11]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push.png
[12]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_1.png
[13]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_creds.png
