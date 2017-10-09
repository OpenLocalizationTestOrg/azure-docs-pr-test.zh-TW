---
title: "aaaWindows Phone Silverlight 到達 SDK 整合"
description: "如何 tooIntegrate Azure Mobile Engagement 達到與 Windows Phone Silverlight 應用程式"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: d3516a6b-db9f-4cdb-a475-4148edf81af1
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 09c8767216e11963c5c600755ab8d4d11cd92034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-reach-sdk-integration"></a>Windows Phone Silverlight Reach SDK 整合
您必須遵循 hello 整合程序所述 hello [Windows Phone Silverlight Engagement SDK 整合](mobile-engagement-windows-phone-integrate-engagement.md)之前依照本指南。

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-phone-silverlight-project"></a>內嵌至 Windows Phone Silverlight 專案中的 hello Engagement 觸達 SDK
您沒有任何項目 tooadd。 `EngagementReach` 的參考和資源已在您的專案中。

> [!TIP]
> 您可以自訂映像位於 hello`Resources`專案，特別是 hello 商標圖示 （該預設 toohello Engagement 圖示） 的資料夾。
> 
> 

## <a name="add-hello-capabilities"></a>加入 hello 功能
hello Engagement 觸達 SDK 需要一些額外的功能。

開啟您`WMAppManifest.xml`檔案，並確定宣告該 hello 下列功能：

* `ID_CAP_PUSH_NOTIFICATION`
* `ID_CAP_WEBBROWSERCOMPONENT`

hello 先使用其中一個是由 hello MPNS 服務 tooallow hello 顯示快顯通知。 hello 第二個是使用的 tooembed hello SDK 到瀏覽器工作。

編輯 hello`WMAppManifest.xml`檔案，然後加入內 hello`<Capabilities />`標記：

    <Capability Name="ID_CAP_PUSH_NOTIFICATION" />
    <Capability Name="ID_CAP_WEBBROWSERCOMPONENT" />

## <a name="enable-hello-microsoft-push-notification-service"></a>啟用 hello Microsoft 推播通知服務
在訂單 toouse hello **Microsoft 推播通知服務**（稱為 MPNS） 您`WMAppManifest.xml`檔案必須具有`<App />`標記`Publisher`設定 toohello 專案名稱的屬性。

## <a name="initialize-hello-engagement-reach-sdk"></a>初始化 hello Engagement 觸達 SDK
### <a name="engagement-configuration"></a>Engagement 組態
hello Engagement 組態會集中在 hello`Resources\EngagementConfiguration.xml`專案檔。

編輯此檔案 toospecify 觸達設定：

* *選擇性*，指出是否啟用 hello 原生推送 (MPNS) 或不介於`<enableNativePush>`和`</enableNativePush>`標記 (`true`依預設)。
* *選擇性*，表示 hello 發送通道之間 hello 名稱`<channelName>`和`</channelName>`標記，提供 hello 相同應用程式可能目前使用，或保持空白。

如果您想要在執行階段相反地，您可以呼叫 hello 下列 toospecify hello Engagement 代理程式初始化之前的方法：

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    engagementConfiguration.Reach.EnableNativePush = true;                  
    /* [Optional] whether hello native push (MPNS) is activated or not. */

    engagementConfiguration.Reach.ChannelName = "YOUR_PUSH_CHANNEL_NAME";   
    /* [Optional] Provide hello same channel name that your application may currently use. */

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

> [!TIP]
> 您可以指定 hello hello MPNS 發送通道，您的應用程式的名稱。 根據預設，Engagement 會建立 hello appId 為基礎的名稱。 您有任何需要 toospecify hello 名稱，但如果您計劃外 Engagement toouse hello 推播通道。
> 
> 

### <a name="engagement-initialization"></a>Engagement 初始化
修改 hello `App.xaml.cs`:

* 新增 tooyour`using`陳述式：
  
      using Microsoft.Azure.Engagement;
* 在 `Application_Launching` 中，將 `EngagementReach.Instance.Init` 插入 `EngagementAgent.Instance.Init` 後方：
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
         EngagementAgent.Instance.Init();
         EngagementReach.Instance.Init();
      }
* 插入`EngagementReach.Instance.OnActivated`在 hello`Application_Activated`方法：
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
         EngagementReach.Instance.OnActivated(e);
      }

> [!IMPORTANT]
> hello`EngagementReach.Instance.Init`專用的執行緒中執行。 您不需要 toodo 它自己。
> 
> 

## <a name="app-store-submission-considerations"></a>應用程式商店提交考量事項
使用 hello 推播通知時，Microsoft 會施加某些規則：

從 hello Microsoft[應用程式原則]文件、 2.9 區段：

1) 您必須要求 hello 使用者 tooaccept tooreceive 推播通知。 然後，在您設定中，加入方法 toodisable hello 推播通知。

hello EngagementReach 物件提供兩個方法 toomanage hello 選擇位在/退出，`EnableNativePush()`和`DisableNativePush()`。 例如，您無法切換 toodisable 與 hello 設定中建立選項或啟用 MPNS。

您也可以決定透過 hello Engagement 組態 toodeactivate MPNS\<windows phone-sdk-觸達-設定\>。

> 2.9.1) hello 應用程式必須先說明提供 hello 通知 toobe 和**取得 hello 使用者快速權限 （選擇加入的）**，和**必須提供的機制，透過 hello 哪些使用者可以選擇不接收推播通知**。 提供使用 hello Microsoft 推播通知服務的所有通知的 hello 提供描述 toohello 使用者必須一致，且必須符合所有適用[應用程式原則][ Content Policies]和[特定應用程式類型的其他需求]。
> 
> 

2) 您不應該使用太多推播通知。 Engagement 將為您處理通知。

> 2.9.2) hello 應用程式和其 hello Microsoft 推播通知服務的使用情形必須不過度使用網路容量或頻寬的 hello Microsoft 推播通知服務，或 Windows Phone 或其他 Microsoft 裝置或服務否則過度應用具有過多由 Microsoft 依合理酌情判斷，將推播通知，並不得對系統造成傷害或干擾任何 Microsoft 網路伺服器或任何協力廠商伺服器或網路連線的 toohello Microsoft 推播通知服務。
> 
> 

3) 請勿依賴 MPNS toosend criticals 資訊。 Engagement 使用 MPNS，因此這項規則也適用於建立在 hello Engagement 前端 hello 客群。

> 2.9.3) hello Microsoft 推播通知服務可能無法使用的 toosend 通知是非常重要或其他可能會影響對很重要的生命週期或死亡，包括但不限於重要通知相關的 tooa 醫療裝置或條件。 MICROSOFT 用戶不作任何擔保，hello 使用的 hello MICROSOFT 推播通知服務或傳遞的 MICROSOFT 推播通知服務通知將會是不中斷，錯誤可用或保證 tooOCCUR ON A 即時基礎。
> 
> 

**我們無法保證您的應用程式將會通過 hello 驗證程序，如果您不會採用這些建議。**

## <a name="handle-data-push-optional"></a>處理資料推送 (選擇性)
如果您希望您的應用程式 toobe tooreceive 無法觸達資料推播通知時，您會有 tooimplement 的 hello EngagementReach 類別的兩個事件：

    EngagementReach.Instance.DataPushStringReceived += (body) =>
    {
       Debug.WriteLine("String data push message received: " + body);
       return true;
    };

    EngagementReach.Instance.DataPushBase64Received += (decodedBody, encodedBody) =>
    {
       Debug.WriteLine("Base64 data push message received: " + encodedBody);
       // Do something useful with decodedBody like updating an image view
       return true;
    };

您可以看到 hello 回撥的每個方法會傳回布林值。 Engagement 傳送意見反應 tooits 後端之後分派 hello 資料推送。 如果 hello 回呼傳回 false，hello`exit`意見反應會傳送。 否則將會是 `action`。 如果沒有回呼 hello 事件設定，hello `drop` tooEngagement 將傳回的意見反應。

> [!WARNING]
> Engagement 不能 tooreceive 倍數的意見反應資料推入。 如果您計劃 tooset 數個處理常式事件，請注意 hello 意見反應會對應 toohello 傳送的最後一個。 在此情況下，我們建議 tooalways 傳回 hello 相同的值 tooavoid hello 前端上有令人混淆的意見反應。
> 
> 

## <a name="customize-ui-optional"></a>自訂 UI (選擇性)
### <a name="first-step"></a>第一步
我們可讓您 toocustomize hello 觸達 UI。

toodo 因此，您有 toocreate hello 的子類別`EngagementReachHandler`類別。

**範例程式碼：**

    using Microsoft.Azure.Engagement;

    namespace Example
    {
       internal class ExampleReachHandler : EngagementReachHandler
       {
          // Override EngagementReachHandler methods depending on your needs
       }
    }

然後將設定的 hello hello 內容`EngagementReach.Instance.Handler`欄位中的自訂物件取代您`App.xaml.cs`內 hello 類別`Application_Launching`方法。

**範例程式碼：**

    private void Application_Launching(object sender, LaunchingEventArgs e)
    {
       // your app initialization 
       EngagementReach.Instance.Handler = new ExampleReachHandler();
       // Engagement Agent and Reach initialization
    }

> [!NOTE]
> 根據預設，Engagement 會使用自己的 `EngagementReachHandler` 實作。 您不需要 toocreate 您自己的而且這樣一來，如果您沒有 toooverride 每個方法。 hello 預設行為是 tooselect hello Engagement 基底物件。
> 
> 

### <a name="layouts"></a>版面配置
根據預設，觸達會使用 hello DLL toodisplay hello 通知和網頁的 hello 內嵌的資源。

不過，您可以決定 toouse 您自己的資源 tooreflect 您在這些元件的品牌。

您可以覆寫`EngagementReachHandler`您子類別 tootell Engagement toouse 中的方法的配置：

**範例程式碼：**

    // In your subclass of EngagementReachHandler

    public override string GetTextViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetWebViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetPollUri()
    {
       // return hello path of your own xaml
    }

    public override EngagementNotificationView CreateNotification(EngagementNotificationViewModel viewModel)
    {
       // return a new instance of your own notification
    }

> [!TIP]
> hello`CreateNotification`方法可以傳回 null。 將不會顯示 hello 通知和 hello 觸達活動皆會予以捨棄。
> 
> 

toosimplify 配置實作中，我們也提供自己 xaml，這可以做為基礎的程式碼。 它們位於 hello Engagement SDK 封存中 (/ src/觸達 /)。

> [!WARNING]
> 我們提供的 hello 我們使用的完全相同的 hello 來源。 因此如果您想 toomodify 它們直接，不要忘記 toochange hello 命名空間並 hello 名稱。
> 
> 

### <a name="notification-position"></a>通知的位置
根據預設，應用程式內通知會顯示在 hello 下方左邊 hello 應用程式。 您可以變更此行為，藉由覆寫 hello`GetNotificationPosition`方法 hello`EngagementReachHandler`物件。

    // In your subclass of EngagementReachHandler

    public override EngagementReachHandler.NotificationPosition GetNotificationPosition(EngagementNotificationViewModel viewModel)
    {
       // return a value of hello EngagementReachHandler.NotificationPosition enum (TOP or BOTTOM)
    }

目前，您可以選擇 hello `BOTTOM` （預設值） 和`TOP`位置。

### <a name="launch-message"></a>啟動訊息
當使用者按一下系統通知 （快顯） 時，Engagement 啟動 hello 應用程式、 hello 負載 hello 內容發送訊息，並顯示 hello 對應活動的 hello 頁面。

Hello hello 頁面 （取決於網路 hello 速度） 的應用程式和 hello 顯示 hello 啟動會延遲。

項目正在載入的 tooindicate toohello 使用者，您應該提供視覺化的資訊，例如進度列或進度列指示器。 Engagement 無法自行處理這些，但有提供您幾個處理常式。

tooimplement hello 回撥，請執行：

    /* hello application has launched and hello content is loading.
     * You should display an indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageStarted += () => { [...] };

    /* hello application has finished loading hello content and hello page
     * is about toobe displayed.
     * You should hide hello indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageCompleted += () => { [...] };

    /* hello content has been loaded, but an error has occurred.
     * You can provide an information toohello user.
     * You should hide hello indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageFailed += () => { [...] };

您可以在設定 hello 回呼您`Application_Launching`方法您`App.xaml.cs`檔案，最好是先 hello`EngagementReach.Instance.Init()`呼叫。

> [!TIP]
> 每個處理常式會呼叫 hello UI 執行緒。 使用 MessageBox 或項目與 UI 相關時，您並沒有 tooworry。
> 
> 

[應用程式原則]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx
[Content Policies]:http://msdn.microsoft.com/library/windows/apps/hh184842(v=vs.105).aspx
[特定應用程式類型的其他需求]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx

