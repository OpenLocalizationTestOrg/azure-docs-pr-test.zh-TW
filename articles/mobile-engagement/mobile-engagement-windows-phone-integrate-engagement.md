---
title: "aaaWindows Phone Silverlight Engagement SDK 整合"
description: "如何使用 Windows Phone Silverlight 應用程式的 Azure Mobile Engagement tooIntegrate"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 447fea8d-f4e3-4ad4-8ec0-8e3cf1ad3ab0
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f65683a62e5256cea469a3a73d99ade4331cb6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-engagement-sdk-integration"></a>Windows Phone Silverlight Engagement SDK 整合
> [!div class="op_single_selector"]
> * [Windows Universal](mobile-engagement-windows-store-integrate-engagement.md) 
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [iOS](mobile-engagement-ios-integrate-engagement.md) 
> * [Android](mobile-engagement-android-integrate-engagement.md) 
> 
> 

此程序描述 hello 最簡單方式 tooactivate Azure Mobile Engagement 的分析和監視您的 Windows Phone Silverlight 應用程式中的函式。

hello 步驟所記錄的足夠 tooactivate hello 報表所需 toocompute 關於使用者、 工作階段、 活動、 當機和 Technicals 的所有統計資料。 hello 報表的記錄檔所需 toocompute 其他統計資料像是事件、 錯誤和作業必須完成手動使用 hello Engagement 應用程式開發介面 (請參閱[toouse hello 如何進階標記您的 Windows Phone Silverlight 應用程式中的應用程式開發介面的 Mobile Engagement](mobile-engagement-windows-phone-use-engagement-api.md)下面） 因為這些統計資料是應用程式相依。

## <a name="supported-versions"></a>支援的版本
hello Mobile Engagement SDK for Windows Silverlight 只可以整合到應用程式為目標：

* Windows Phone 8.0
* Windows Phone 8.1 Silverlight

> [!NOTE]
> 如果您的目標 Windows Phone 8.1 (非 Silverlight)，請參閱 toohello [Windows 通用整合程序](mobile-engagement-windows-store-integrate-engagement.md)。
> 
> 

## <a name="install-hello-mobile-engagement-silverlight-sdk"></a>安裝 hello Mobile Engagement Silverlight SDK
hello Mobile Engagement SDK for Windows Silverlight 是以 Nuget 套件使用呼叫*MicrosoftAzure.MobileEngagement*。 您可以從 hello Visual Studio 的 Nuget 套件管理員來安裝它。 

## <a name="add-hello-capabilities"></a>加入 hello 功能
hello Engagement SDK 正確需要 hello Windows Phone Silverlight SDK toowork 順序中的某些功能。

開啟您`WMAppManifest.xml`檔案，並確定在 hello 中宣告的下列功能的 hello`Capabilities`面板：

* `ID_CAP_NETWORKING`
* `ID_CAP_IDENTITY_DEVICE`

## <a name="initialize-hello-engagement-sdk"></a>初始化 hello Engagement SDK
### <a name="engagement-configuration"></a>Engagement 組態
hello Engagement 組態會集中在 hello`Resources\EngagementConfiguration.xml`專案檔。

編輯此檔案 toospecify:

* 應用程式在 `<connectionString>` 和 `<\connectionString>` 標記之間的連接字串。

如果您想要在執行階段相反地，您可以呼叫 hello 下列 toospecify hello Engagement 代理程式初始化之前的方法：

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

您的應用程式的 hello 連接字串會顯示在 hello Azure 傳統入口網站。

### <a name="engagement-initialization"></a>Engagement 初始化
當您建立新專案時會產生一份 `App.xaml.cs` 檔案。 這個類別繼承自 `Application` ，且包含的許多重要的方法。 它也會使用的 tooinitialize hello Engagement SDK。

修改 hello `App.xaml.cs`:

* 新增 tooyour`using`陳述式：
  
      using Microsoft.Azure.Engagement;
* 插入`EngagementAgent.Instance.Init`在 hello`Application_Launching`方法：
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
        EngagementAgent.Instance.Init();
      }
* 插入`EngagementAgent.Instance.OnActivated`在 hello`Application_Activated`方法：
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
      }

> [!WARNING]
> 我們強烈建議您 tooadd hello Engagement 初始化應用程式的另一個位置中。 不過，請注意該 hello`EngagementAgent.Instance.Init`專用的執行緒，而不是在 hello UI 執行緒執行方法。
> 
> 

## <a name="basic-reporting"></a>基本報告
### <a name="recommended-method--overload-your-phoneapplicationpage-classes"></a>建議使用的方法：多載您的 `PhoneApplicationPage` 類別
訂單 tooactivate hello Engagement toocompute 使用者、 工作階段、 活動、 當機和技術的統計資料所需的所有 hello 記錄檔的報表，您可以只在所有您`PhoneApplicationPage`子類別是繼承自 hello`EngagementPage`類別。

以下是如何的範例 toodo 這樣的應用程式頁面。 您可以 hello 相同的動作，為您的應用程式的所有頁面。

#### <a name="c-source-file"></a>C# 來源檔案
修改您的頁面 `.xaml.cs` 檔案：

* 新增 tooyour`using`陳述式：
  
      using Microsoft.Azure.Engagement;
* 以 `EngagementPage` 取代 `PhoneApplicationPage`：

**沒有 Engagement：**

        namespace Example
        {
          public partial class ExamplePage : PhoneApplicationPage
          {
            [...]
          }
        }

**有 Engagement：**

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!WARNING]
> 如果您的頁面是繼承自 hello`OnNavigatedTo`方法，要特別小心 toolet hello`base.OnNavigatedTo(e)`呼叫。 否則，將不會報告 hello 活動。 事實上，hello`EngagementPage`呼叫`StartActivity`內 hello`OnNavigatedTo`方法。
> 
> 

#### <a name="xaml-file"></a>XAML 檔案
修改您的頁面 `.xaml` 檔案：

* 加入 tooyour 命名空間宣告：
  
      xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
* 以 `engagement:EngagementPage` 取代 `phone:PhoneApplicationPage`：

**沒有 Engagement：**

        <phone:PhoneApplicationPage>
            <!-- layout -->
        </phone:PhoneApplicationPage>

**有 Engagement：**

        <engagement:EngagementPage 
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP">

            <!-- layout -->
        </engagement:EngagementPage >

#### <a name="override-hello-default-behavior"></a>覆寫 hello 預設行為
根據預設，hello 活動名稱，以及不需額外會報告 hello 頁面 hello 類別名稱。 如果 hello 類別使用 hello"Page"後置詞，Engagement 也會移除它。

如果您想要 hello 名稱 toooverride hello 預設行為，只要加入此 tooyour 程式碼：

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
           /* your code */
           return "new name";
        }

如果您想要 tooreport 一些額外的資訊與您的活動，您可以加入這個 tooyour 程式碼：

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
           /* your code */
           return extra;
        }

這些方法從呼叫 hello 內`OnNavigatedTo`頁面的方法。

### <a name="alternate-method-call-startactivity-manually"></a>替代方法：手動呼叫 `StartActivity()`
如果您無法或不想 toooverload 您`PhoneApplicationPage`類別，您可以改為啟動您的活動藉由呼叫`EngagementAgent`直接的方法。

我們建議您於 PhoneApplicationPage 的 `OnNavigatedTo` 方法內呼叫 `StartActivity`。

        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
           base.OnNavigatedTo(e);
           EngagementAgent.Instance.StartActivity("MyPage");
        }

> [!IMPORTANT]
> 請確定您正確地結束工作階段。
> 
> hello SDK 會自動呼叫 hello `EndActivity` hello 應用程式關閉時的方法。 因此，它是**高**建議 toocall hello`StartActivity`每當 hello 使用者的 hello 活動變更時，方法和太**永不**呼叫 hello`EndActivity`方法。 這個方法會傳送訊息 toohello Engagement 伺服器 hello 目前使用者離開 hello 應用程式，且這會影響所有的應用程式記錄檔。
> 
> 

## <a name="advanced-reporting"></a>進階報告
（選擇性） 您可能會想 tooreport 應用程式特定事件、 錯誤和作業、 toodo 因此、 使用 hello 其他方法位於 hello`EngagementAgent`類別。 hello Engagement 應用程式開發介面可讓 toouse 所有參與的進階功能。

如需詳細資訊，請參閱[toouse hello 如何進階標記您的 Windows Phone Silverlight 應用程式中的應用程式開發介面的 Mobile Engagement](mobile-engagement-windows-phone-use-engagement-api.md)。

## <a name="advanced-configuration"></a>進階組態
### <a name="disable-automatic-crash-reporting"></a>停用自動當機報告
您可以停用報告功能的 Engagement hello 自動損毀。 然後，發生未處理的例外狀況時，Engagement 將不會執行任何動作。

> [!WARNING]
> 如果您計劃 toodisable 這項功能，請注意，當應用程式中，將會發生未處理的損毀，Engagement 不會傳送 hello 損毀**AND** hello 工作階段和工作，就不會關閉它。
> 
> 

toodisable 自動當機報告，也可以自訂您的組態，根據您在宣告的 hello 方式而定：

#### <a name="from-engagementconfigurationxml-file"></a>從 `EngagementConfiguration.xml` 檔案
設定報表損毀太`false`之間`<reportCrash>`和`</reportCrash>`標記。

#### <a name="from-engagementconfiguration-object-at-run-time"></a>於執行階段時從 `EngagementConfiguration` 物件
設定報表損毀 toofalse 使用 EngagementConfiguration 物件。

        /* Engagement configuration. */

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration(); engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";
        /\* Disable Engagement crash reporting. \*/ engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a>高載模式
根據預設，hello Engagement 服務報表會即時記錄。 如果您的應用程式會報告記錄檔頻率很高，是較佳的 toobuffer hello 記錄檔和 tooreport 一次在固定時間基底 （稱為 hello 「 高載模式 」）。

toodo 因此，呼叫 hello 方法：

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

hello 引數是中的值**毫秒**。 在任何時間，如果您想 tooreactivate hello 即時記錄，就會呼叫 hello 方法未使用任何參數，或使用 hello 0 值。

hello 高載模式稍微增加 hello 電池壽命但有 hello Engagement 監視影響： 所有工作階段和作業的持續時間將會捨入的 toohello 高載臨界值 （因此，工作階段和短 hello 高載閾值可能不會顯示作業）。 它會建議 toouse 高載臨界值不會再於 30000 （30 秒）。 您有 toobe 感知儲存記錄檔是有限的 too300 項目。 如果傳送太長，您可能會遺失某些記錄檔。

> [!WARNING]
> hello 高載臨界值不能設定較小者 tooa 期間比一秒。 如果您因此嘗試 toodo，hello SDK 將會顯示追蹤與 hello 錯誤，就會自動重設 toohello 預設值，也就是零秒。 這將會觸發即時 hello SDK tooreport hello 記錄。
> 
> 

