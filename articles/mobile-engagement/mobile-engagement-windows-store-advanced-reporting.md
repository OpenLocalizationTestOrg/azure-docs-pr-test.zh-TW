---
title: "通用進階報告功能與 MobileApps Engagement aaaWindows"
description: "如何 tooIntegrate 與 Windows 通用應用程式的 Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ea5030bf-73ac-49b7-bc3e-c25fc10e945a
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 20968f238ef7ae9dc0b8bb6dac3fb8bdb9bc3a10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-hello-windows-universal-apps-engagement-sdk"></a>以 hello Windows 通用應用程式 Engagement SDK 的進階的報告
> [!div class="op_single_selector"]
> * [Universal Windows](mobile-engagement-windows-store-advanced-reporting.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-reporting.md)
> 
> 

本主題說明 Windows 通用應用程式中的其他報告案例。 這些案例包括您可以選擇建立 hello tooapply toohello 應用程式的選項[入門](mobile-engagement-windows-store-dotnet-get-started.md)教學課程。

## <a name="prerequisites"></a>必要條件
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

再開始本教學課程，您必須先完成 hello[入門](mobile-engagement-windows-store-dotnet-get-started.md)教學課程中，已刻意直接且簡單。 本教學課程涵蓋您可以選擇的其他選項。

## <a name="specifying-engagement-configuration-at-runtime"></a>指定執行階段的 Engagement 組態
hello Engagement 組態會集中在 hello`Resources\EngagementConfiguration.xml`檔案的專案，也就是其中指定在 hello[入門](mobile-engagement-windows-store-dotnet-get-started.md)主題。

但是您也可以指定它在執行階段： 您可以呼叫下列方法 hello Engagement 代理程式初始化之前 hello:

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);



## <a name="recommended-method-overload-your-page-classes"></a>建議使用的方法：多載您的 `Page` 類別
tooactivate Engagement toocompute 使用者、 工作階段、 活動、 當機和技術的統計資料所需的所有 hello 記錄檔的 hello reporting 進行所有您`Page`子類別是繼承自 hello`EngagementPage`類別。

以下是您應用程式其中一個頁面的範例。 您可以 hello 相同的動作，為您的應用程式的所有頁面。

### <a name="c-source-file"></a>C# 來源檔案
修改您頁面的 `.xaml.cs` 檔案：

* 新增 tooyour`using`陳述式：
  
      using Microsoft.Azure.Engagement;
* 以 `EngagementPage` 取代 `Page`：

**沒有 Engagement：**

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

**有 Engagement：**

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage
          {
            [...]
          }
        }

> [!IMPORTANT]
> 如果您的頁面會覆寫 hello`OnNavigatedTo`方法，是確定 toocall `base.OnNavigatedTo(e)`。 否則，不會報告 hello 活動 (hello`EngagementPage`呼叫`StartActivity`內其`OnNavigatedTo`方法)。
> 
> 

### <a name="xaml-file"></a>XAML 檔案
修改您頁面的 `.xaml` 檔案：

* 加入 tooyour 命名空間宣告：
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* 以 `engagement:EngagementPage` 取代 `Page`：

**沒有 Engagement：**

        <Page>
            <!-- layout -->
            ...
        </Page>

**有 Engagement：**

        <engagement:EngagementPage
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

### <a name="override-hello-default-behaviour"></a>覆寫預設行為，hello
根據預設，hello 活動名稱，以及不需額外會報告 hello 頁面 hello 類別名稱。 如果 hello 類別使用 hello"Page"後置詞，Engagement 會移除它。

hello 名稱 toooverride hello 預設行為會加入下列程式碼：

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

tooreport 額外的資訊與程式活動中，加入下列程式碼：

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

這些方法從呼叫 hello 內`OnNavigatedTo`頁面的方法。

### <a name="alternate-method-call-startactivity-manually"></a>替代方法：手動呼叫 `StartActivity()`
如果您無法或不想 toooverload 您`Page`類別，您可以改為啟動您的活動藉由呼叫`EngagementAgent`直接的方法。

我們建議您於 Page 的 `OnNavigatedTo` 方法內呼叫 `StartActivity`。

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> 請確定您正確地結束工作階段。
> 
> hello Windows 通用 SDK 會自動呼叫 hello `EndActivity` hello 應用程式關閉時的方法。 因此，它是**高**建議 toocall hello`StartActivity`每當 hello 使用者的 hello 活動變更時，方法和太**永不**呼叫 hello`EndActivity`方法。 這個方法會通知 hello Engagement 伺服器 hello 目前的使用者已離開 hello 應用程式，將會影響所有的應用程式記錄檔。
> 
> 

## <a name="advanced-reporting"></a>進階報告
（選擇性） 您可能會想 tooreport 應用程式特定事件、 錯誤和作業、 toodo 因此、 使用 hello 其他方法位於 hello`EngagementAgent`類別。 hello Engagement 應用程式開發介面可讓您使用所有參與的進階功能。

如需詳細資訊，請參閱[toouse hello 如何進階標記 Windows 通用應用程式中的應用程式開發介面的 Mobile Engagement](mobile-engagement-windows-store-use-engagement-api.md)。

