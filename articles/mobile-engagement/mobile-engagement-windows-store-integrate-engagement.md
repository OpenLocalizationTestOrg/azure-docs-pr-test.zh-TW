---
title: "Windows 通用 app Engagement SDK 整合"
description: "如何將 Azure Mobile Engagement 與 Windows 通用 app 整合"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 71236b68-5ebd-44aa-8c82-c7ca8098ea05
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 56a382a348609df1d1d308aeac39f47ca82ac4c8
ms.sourcegitcommit: 821b6306aab244d2feacbd722f60d99881e9d2a4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/18/2017
---
# <a name="windows-universal-apps-engagement-sdk-integration"></a>Windows 通用 app Engagement SDK 整合
> [!div class="op_single_selector"]
> * [Universal Windows](mobile-engagement-windows-store-integrate-engagement.md) 
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [iOS](mobile-engagement-ios-integrate-engagement.md) 
> * [Android](mobile-engagement-android-integrate-engagement.md) 
> 
> 

本程序說明如何以最簡單的方式啟用 Windows 通用 app 內 Engagement 的分析與監視功能。

下列步驟便足以啟用計算使用者、工作階段、活動、當機和技術等所有統計資料時需要的記錄檔報告。 用來計算其他統計資料 (例如事件、錯誤及工作) 所需的記錄檔報告必須使用 Engagement API 來手動完成 (請參閱 [如何在 Windows 通用 app 中使用進階的 Mobile Engagement 標記 API](mobile-engagement-windows-store-use-engagement-api.md) )，因為這些是應用程式相依的統計資料。

## <a name="supported-versions"></a>支援的版本
適用於 Windows 通用 app 的 Mobile Engagement SDK 只能整合至目標為以下作業系統的 Windows 執行階段和通用 Windows 平台應用程式：

* Windows 8
* Windows 8.1
* Windows Phone 8.1
* Windows 10 (桌上型電腦和行動裝置系列)

> [!NOTE]
> 如果您是以 Windows Phone Silverlight 為目標，則請參考 [Windows Phone Silverlight 整合程序](mobile-engagement-windows-phone-integrate-engagement.md)。
> 
> 

## <a name="install-the-mobile-engagement-universal-apps-sdk"></a>安裝 Mobile Engagement 跨平台 app SDK
### <a name="all-platforms"></a>所有平台
提供適用於 Windows 通用 app 的 Mobile Engagement SDK 時會使用稱為 *MicrosoftAzure.MobileEngagement*的 Nuget 封裝。 您可以從 Visual Studio Nuget 封裝管理員安裝該封裝。

### <a name="windows-8x-and-windows-phone-81"></a>Windows 8.x 和 Windows Phone 8.1
NuGet 會自動在您的應用程式專案根目錄 `Resources` 資料夾中部署 SDK 資源。

### <a name="windows-10-universal-windows-platform-applications"></a>Windows 10 通用 Windows 平台應用程式
NuGet 目前還不會自動在您的 UWP 應用程式部署 SDK 資源。 您必須手動執行，直到 NuGet 重新引進資源部署：

1. 開啟 [檔案總管]。
2. 瀏覽至以下位置 (**x.x.x** 是您安裝的 Engagement 版本)：*%USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\\**x.x.x**\\content\win81*
3. 從檔案總管將 [Resources]  資料夾拖放到您的專案在 Visual Studio 中的根目錄。
4. 在 Visual Studio 中，選取您的專案並啟動 [方案總管] 上方的 [顯示所有檔案] 圖示。
5. 部分檔案未包含在專案中。 若要將它們一次匯入，請在 [Resources] 資料夾上按一下滑鼠右鍵，[從專案移除] 然後再次在 [Resources] 資料夾上按一次滑鼠右鍵，[加入至專案] 以重新包含整個資料夾。 所有來自 [Resources]  資料夾的檔案現在已經包含在您的專案中。

## <a name="add-the-capabilities"></a>新增功能
Engagement SDK 需要一些 Windows SDK 的功能以正常運作。

開啟 `Package.appxmanifest` 檔案，並確定已宣告下列功能：

* `Internet (Client)`

## <a name="initialize-the-engagement-sdk"></a>初始化 Engagement SDK
### <a name="engagement-configuration"></a>Engagement 組態
Engagement 組態會集中在您專案的 `Resources\EngagementConfiguration.xml` 檔案中。

編輯此檔案來指定：

* 應用程式在 `<connectionString>` 和 `<\connectionString>` 標記之間的連接字串。

若想要改為在執行階段指定它，您可以在 Engagement 代理程式初始化之前呼叫下列方法：

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set the Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);

您的應用程式的連接字串會顯示在 Azure 入口網站。

### <a name="engagement-initialization"></a>Engagement 初始化
當您建立新專案時會產生一份 `App.xaml.cs` 檔案。 這個類別繼承自 `Application` ，且包含的許多重要的方法。 它將會用來初始化 Engagement SDK。

修改 `App.xaml.cs`：

* 新增至您的 `using` 陳述式：
  
      using Microsoft.Azure.Engagement;
* 定義一個方法以針對所有呼叫一次共用 Engagement 初始化：
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
  
        // or
  
        EngagementAgent.Instance.Init(e, engagementConfiguration);
      }
* 呼叫 `OnLaunched` 方法中的 `InitEngagement`：
  
      protected override void OnLaunched(LaunchActivatedEventArgs e)
      {
        InitEngagement(e);
      }
* 當您的應用程式使用自訂配置、其他應用程式或命令列啟動時，會呼叫 `OnActivated` 方法。 您也需要在您的應用程式啟動時初始化 Engagement SDK。 若要這樣做，請覆寫 `OnActivated` 方法：
  
      protected override void OnActivated(IActivatedEventArgs args)
      {
        InitEngagement(args);
      }

> [!IMPORTANT]
> 我們強烈地建議您不要在應用程式的其他地方新增 Engagement 初始化。
> 
> 

## <a name="basic-reporting"></a>基本報告
### <a name="recommended-method-overload-your-page-classes"></a>建議使用的方法：多載您的 `Page` 類別
為了啟用 Engagement 計算使用者、工作階段、活動、當機和技術的統計資料所需的所有記錄檔報告，您可讓所有的 `Page` 子類別繼承自 `EngagementPage` 類別。

以下是如何在您應用程式其中一個頁面使用此方法的範例。 您可以將相同的方法用於您應用程式的所有頁面。

#### <a name="c-source-file"></a>C# 來源檔案
修改您頁面的 `.xaml.cs` 檔案：

* 新增至您的 `using` 陳述式：
  
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
> 如果您的頁面會覆寫 `OnNavigatedTo` 方法，請務必呼叫 `base.OnNavigatedTo(e)`。 否則不會報告活動 (`EngagementPage` 會在其 `OnNavigatedTo` 方法內呼叫 `StartActivity`)。
> 
> 

#### <a name="xaml-file"></a>XAML 檔案
修改您頁面的 `.xaml` 檔案：

* 新增命名空間宣告：
  
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

#### <a name="override-the-default-behaviour"></a>覆寫預設行為
根據預設，頁面的類別名稱會在報告時做為活動名稱 (沒有額外的名稱)。 如果類別使用 "Page" 尾碼，Engagement 也會移除它。

如果想要覆寫名稱的預設行為，您只需將下列新增至您的程式碼：

        // in the .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

如果想要報告活動的一些額外資訊，您可以將下列新增至您的程式碼：

        // in the .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

系統會從您頁面的 `OnNavigatedTo` 方法中呼叫這些方法。

### <a name="alternate-method-call-startactivity-manually"></a>替代方法：手動呼叫 `StartActivity()`
如果您無法或不想要多載您的 `Page` 類別，您可以改為透過直接呼叫 `EngagementAgent` 方法來啟動活動。

我們建議您於 Page 的 `OnNavigatedTo` 方法內呼叫 `StartActivity`。

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> 請確定您正確地結束工作階段。
> 
> 應用程式關閉時，Windows 通用 SDK 會自動呼叫 `EndActivity` 方法。 因此，「強烈」建議每當使用者的活動變更時便叫呼叫 `StartActivity` 方法，並且「絕對不要」呼叫 `EndActivity` 方法，此方法會傳送至 Engagement 伺服器，目前的使用者已離開應用程式，這會影響所有應用程式記錄檔。
> 
> 

## <a name="advanced-reporting"></a>進階報告
(選擇性) 您可以報告應用程式的特定事件、錯誤和工作；若要這樣做，請使用 `EngagementAgent` 類別中找到的其他方法。 Engagement API 允許使用所有 Engagement 的進階功能。

如需詳細資訊，請參閱 [如何在 Windows 通用 app 中使用進階的 Mobile Engagement 標記 API](mobile-engagement-windows-store-use-engagement-api.md)。

## <a name="advanced-configuration"></a>進階組態
### <a name="disable-automatic-crash-reporting"></a>停用自動當機報告
您可以停用 Engagement 的自動當機報告功能。 然後，發生未處理的例外狀況時，Engagement 將不會執行任何動作。

> [!WARNING]
> 如果您打算停用此功能，請注意當您的應用程式中將發生未處理的當機時，Engagement 將不會傳送該當機，「且」亦不會關閉工作階段和工作。
> 
> 

若要停用自動當機報告，只要依照您宣告的方式自訂您的組態即可：

#### <a name="from-engagementconfigurationxml-file"></a>從 `EngagementConfiguration.xml` 檔案
在 `<reportCrash>` 和 `</reportCrash>` 標記之間，將報告當機設為 `false`。

#### <a name="from-engagementconfiguration-object-at-run-time"></a>於執行階段時從 `EngagementConfiguration` 物件
使用 EngagementConfiguration 物件將報告當機設為 false。

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a>高載模式
根據預設，Engagement 服務會即時報告記錄檔。 如果應用程式報告記錄檔的頻率很高，最好先緩衝處理記錄檔，再定期一次報告它們 (此稱為「高載模式」)。

若要這樣做，請呼叫方法：

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

該引數是以 「毫秒」為單位的值。 如果您想要重新啟動及時記錄，您隨時可以呼叫該方法，而不需要使用任何參數 (或使用 0 為值)。

高載模式可以稍微延長電池使用時間但對 Engagement 監視器會有影響： 所有工作階段和工作持續時間將調整為高載閾值 (因此，可能將看不到時間比高載閾值短的工作階段和作業)。 建議使用低於 30000 (30 秒) 的閾值。 您必須留意儲存記錄檔僅限於 300 個項目。 如果傳送太長，您可能會遺失某些記錄檔。

> [!WARNING]
> 高載閾值無法設定為小於 1 秒的時間間隔。 如果您嘗試這樣做，SDK 會顯示含錯誤訊息的追蹤，並且會自動重設為預設值 (0 秒)。 這樣會觸發 SDK 以即時的方式報告記錄檔。
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview

