---
title: "aaaWindows 通用應用程式連線到 SDK 整合"
description: "如何 tooIntegrate Azure Mobile Engagement 出現 Windows 通用應用程式"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a31ca1d6-856f-4aec-898a-07969ae5f7ec
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: af311c65940014083333853875a00173b8d6783e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-reach-sdk-integration"></a>Windows 通用 app Reach SDK 整合
您必須遵循 hello 整合程序所述 hello [Windows 通用 Engagement SDK 整合](mobile-engagement-windows-store-integrate-engagement.md)之前依照本指南。

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-universal-project"></a>內嵌至 Windows 通用專案中的 hello Engagement 觸達 SDK
您沒有任何項目 tooadd。 `EngagementReach` 的參考和資源已在您的專案中。

> [!TIP]
> 您可以自訂映像位於 hello`Resources`專案，特別是 hello 商標圖示 （該預設 toohello Engagement 圖示） 的資料夾。 您也可以在通用應用程式上移動 hello`Resources`上其內容之間的應用程式，但您會有您共用的專案 tooshare 資料夾 tookeep hello`Resources\EngagementConfiguration.xml`檔案的預設位置，因為它是平台相依。
> 
> 

## <a name="enable-hello-windows-notification-service"></a>啟用 hello Windows 通知服務
### <a name="windows-8x-and-windows-phone-81-only"></a>僅 Windows 8.x 和 Windows Phone 8.1
在順序 toouse hello **Windows 通知服務**（稱為 WNS） 在您`Package.appxmanifest`上的檔案`Application UI`按一下`All Image Assets`hello bot 左邊的方塊中。 在 [hello] 方塊中的 hello `Notifications`，變更`toast capable`從`(not set)`太`(Yes)`。

### <a name="all-platforms"></a>所有平台
您需要 toosynchronize 您應用程式 tooyour Microsoft 帳戶和 toohello engagement 平台。 這需要 toocreate 帳戶或登入[windows 開發人員中心](https://dev.windows.com)。 之後，建立新的應用程式，並尋找 hello SID 與秘密金鑰。 Hello engagement 前端上繼續您的應用程式設定中`native push`並貼上您的認證。 接下來，在您的專案上按一下滑鼠右鍵，依序選取 `store` 和 `Associate App with hello Store...`。 您只需要 tooselect hello 應用程式有建立 toosynchronize 之前。

## <a name="initialize-hello-engagement-reach-sdk"></a>初始化 hello Engagement 觸達 SDK
修改 hello `App.xaml.cs`:

* 在 `InitEngagement` 方法中，將 `EngagementReach.Instance.Init` 插入 `EngagementAgent.Instance.Init` 後方：
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
        EngagementReach.Instance.Init(e);
      }
  
  hello`EngagementReach.Instance.Init`專用的執行緒中執行。 您不需要 toodo 它自己。

> [!NOTE]
> 如果您的應用程式中其他地方使用推播通知，則您也有[共用您的推播通道](#push-channel-sharing)與 Engagement 觸達。
> 
> 

## <a name="integration"></a>整合
Engagement 提供宣告與輪詢應用程式中的兩種方式 tooadd hello 觸達應用程式內橫幅和插入式檢視： hello 重疊整合以及 hello web 檢視手動整合。 您不應該結合這兩種方法在 hello 上的相同的頁面。

無法彙總之間 hello 兩個整合的 hello 選擇這種方式：

* 如果您的網頁已繼承自 hello 代理程式，您可以選擇 hello 重疊整合`EngagementPage`，它是只需取代`EngagementPage`由`EngagementPageOverlay`和`xmlns:engagement="using:Microsoft.Azure.Engagement"`由`xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"`頁面中。
* 您可以選擇 hello web 檢視手動整合如果您想在網頁中的 tooprecisely 位置 hello 到達 UI，或如果您不想 tooadd 另一個繼承 tooyour 層級頁面。 

### <a name="overlay-integration"></a>重疊整合
hello Engagement 重疊動態新增 hello UI 項目在網頁中使用 toodisplay 觸達活動。 如果 hello 重疊不符合您配置您應該考慮 hello web 檢視手動整合改為。

在您的.xaml 檔案變更`EngagementPage`太參考`EngagementPageOverlay`

* 加入 tooyour 命名空間宣告：
  
      xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"
* 以 `engagement:EngagementPageOverlay` 取代 `engagement:EngagementPage`：

**有 EngagementPage：**

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">

            <!-- Your layout -->
        </engagement:EngagementPage>

**有 EngagementPageOverlay：**

        <engagement:EngagementPageOverlay 
            xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay">

            <!-- Your layout -->
        </engagement:EngagementPageOverlay>

然後在您的 .cs 檔案中以 `EngagementPageOverlay` 而不是 `EngagementPage` 標記頁面，並匯入 `Microsoft.Azure.Engagement.Overlay`。

            using Microsoft.Azure.Engagement.Overlay;

* 以 `EngagementPageOverlay` 取代 `EngagementPage`：

**有 EngagementPage：**

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPage
              {
                [...]
              }
            }

**有 EngagementPageOverlay：**

            using Microsoft.Azure.Engagement.Overlay;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPageOverlay 
              {
                [...]
              }
            }


hello Engagement 覆疊新增`Grid`在您的頁面頂端的項目組成的版面配置及 hello 兩`WebView`hello 的項目一個橫幅和 hello hello 插入檢視另一個。

您可以自訂 hello 重疊項目，直接在 hello`EngagementPageOverlay.cs`檔案。

### <a name="web-views-manual-integration"></a>Web 檢視手動整合
觸達搜尋 hello 兩個頁面`WebView`負責顯示 hello 橫幅和 hello 插入式檢視的項目。 只有您唯一 toodo tooadd hello 這兩者`WebView`項目位置在頁面中，範例如下：

    <Grid x:Name="engagementGrid">

      <!-- Your layout -->

      <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Stretch" VerticalAlignment="Top"/>
      <WebView x:Name="engagement_announcement_content" Visibility="Collapsed"  HorizontalAlignment="Stretch"  VerticalAlignment="Stretch"/>
    </Grid>


在此範例 hello`WebView`項目會伸展的 toofit 其容器的自動重新調整大小它們螢幕旋轉或視窗大小變更時。

> [!WARNING]
> 請務必 tookeep hello 相同命名`engagement_notification_content`和`engagement_announcement_content`hello`WebView`項目。 Reach 依其名稱來識別。 
> 
> 

## <a name="handle-datapush-optional"></a>處理資料推送 (選擇性)
如果您希望您的應用程式 toobe tooreceive 無法觸達資料推播通知時，您會有 tooimplement 的 hello EngagementReach 類別的兩個事件：

在 App.xaml.cs hello App() 建構函式中加入：

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

然後將設定的 hello hello 內容`EngagementReach.Instance.Handler`欄位中的自訂物件取代您`App.xaml.cs`內 hello 類別`App()`方法。

**範例程式碼：**

            protected override void OnLaunched(LaunchActivatedEventArgs args)
            {
              // your app initialization 
              EngagementReach.Instance.Handler = new ExampleReachHandler();
              // Engagement Agent and Reach initialization
            }

> [!NOTE]
> 根據預設，Engagement 會使用自己的 `EngagementReachHandler` 實作。
> 您不需要 toocreate 您自己的而且這樣一來，如果您沒有 toooverride 每個方法。 hello 預設行為是 tooselect hello Engagement 基底物件。
> 
> 

### <a name="web-view"></a>Web 檢視
根據預設，觸達會使用 hello DLL toodisplay hello 通知和網頁的 hello 內嵌的資源。

tooprovide 完整自訂我們只會使用 web 檢視的項目。 如果您想 toocustomize 版面配置時，覆寫直接 hello 資源檔`EngagementAnnouncement.html`和`EngagementNotification.html`。 Engagement 需要所有的程式碼中`<body></body>`toorun 正確。 但您可以在 `engagement_webview_area`之外新增標記。

不過，您可以決定 toouse 您自己的資源。

您可以覆寫`EngagementReachHandler`方法在您的子類別 tootell Engagement toouse 的配置，但會採用照護 tooembedded hello engagement 機制：

**範例程式碼：**

            // In your subclass of EngagementReachHandler

            public override string GetAnnouncementHTML()
            {
              return base.GetAnnouncementHTML();
            }
            public override string GetAnnouncementName()
            {
              return base.GetAnnouncementName();
            }
            public override string GetNotfificationHTML()
            {
              return base.GetNotfificationHTML();
            }
            public override string GetNotfificationName()
            {
              return base.GetNotfificationName();
            }


根據預設，AnnouncementHTML 是 `ms-appx-web:///Resources/EngagementAnnouncement.html`。 它代表 hello 設計 hello 訊息的內容推播 （文字公告、 Web anoucement 和輪詢通知） 的 html 檔案。 AnnouncementName 是 `engagement_announcement_content`。 它是在 xaml 頁面中的 hello webview 設計 hello 名稱。

NotfificationHTML 是 `ms-appx-web:///Resources/EngagementNotification.html`。 它代表 hello 設計 hello 通知推播訊息的 html 檔案。 NotfificationName 是 `engagement_notification_content`。 它是在 xaml 頁面中的 hello webview 設計 hello 名稱。

### <a name="customization"></a>自訂
如果您保留 Engagement 物件，便可以自訂通知和宣告的 Web 檢視。 請小心 webview 物件會描述三次-hello 第一次在 xaml 中，第二個時間在 hello"setwebview()"方法中，您的.cs 檔案中與第三次 hello html 檔案中。

* 在 xaml 中，您會描述 hello 目前圖形配置 webview 元件。
* 您可以在.cs 檔案定義"setwebview()"集中的兩個 hello webview （通知，通知） 的 hello 維度。 Hello 應用程式是調整大小時，它是非常有效。
* Hello Engagement html 檔案中，我們說明 hello webview 內容，設計並 hello 彼此之間的項目位置。

### <a name="launch-message"></a>啟動訊息
當使用者按一下系統通知 （快顯） 時，Engagement 啟動 hello 應用程式、 hello 負載 hello 內容發送訊息，並顯示 hello 頁面 hello 對應的活動。

Hello hello 頁面 （取決於網路 hello 速度） 的應用程式和 hello 顯示 hello 啟動會延遲。

項目正在載入的 tooindicate toohello 使用者，您應該提供視覺化的資訊，例如進度列或進度列指示器。 Engagement 無法自行處理這些，但有提供您幾個處理常式。

tooimplement hello 回呼，在 「 公用 App() {}"App.xaml.cs 加入：

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

您可以在 「 公用 App() {}"的方法中設定 hello 回呼您`App.xaml.cs`檔案，最好是先 hello`EngagementReach.Instance.Init()`呼叫。

> [!TIP]
> 每個處理常式會呼叫 hello UI 執行緒。 使用 MessageBox 或項目與 UI 相關時，您並沒有 tooworry。
> 
> 

## <a id="push-channel-sharing"></a> 推播通道共用
如果您應用程式中用於其他用途使用推播通知您有 toouse hello 推播通道共用 hello Engagement SDK 的功能。 這是遺漏 tooavoid 推入。

* 您可以提供您自己發送通道 toohello Engagement 觸達初始化。 hello SDK 會使用它而不是一個新的要求。

更新您的推播通道在 hello hello Engagement 觸達初始化`InitEngagement`方法從 hello`App.xaml.cs`檔案：

    /* Your own push channel logic... */
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    /*...Engagement initialization */
    EngagementAgent.Instance.Init(e);
    EngagementReach.Instance.Init(e,pushChannel);

* 或者，如果您只想 tooconsume hello 推送通道 hello 觸達初始化之後則 hello SDK 建立之後，您可以在 Engagement 觸達 tooget hello 發送通道將回呼。

在任何地方設定回呼**之後**hello 觸達初始化：

    /* Set action on hello SDK push channel. */
    EngagementReach.Instance.SetActionOnPushChannel((PushNotificationChannel channel) => 
    {
      /* hello forwarded channel can be null if its creation fails for any reason. */
      if (channel != null)
      {
        /* Your own push channel logic... */
      });
    }

## <a name="custom-scheme-tip"></a>自訂配置秘訣
我們提供使用自訂配置。 您可以從您的行動應用程式中使用 engagement 前端 toobe 傳送不同類型的 URI。 如果裝置上沒有安裝預設的應用程式，預設配置 (例如，由 Windows 管理 `http, ftp, ...` ) 便會出現視窗提示。 您也可以在您的應用程式中使用自訂配置。

hello 簡單的方式 tooset 自訂應用程式中的配置是 tooopen 您`Package.appxmanifest`中移`Declarations`面板。 選取`Protocol`在 hello 可用宣告捲動方塊，並將它加入。 編輯 hello`Name`欄位與新的通訊協定所需的名稱。

現在 toouse 此通訊協定，編輯您`App.xaml.cs`以 hello`OnActivated`方法，另外也不要忘記 tooinitialize engagement 這裡：

            /// <summary>
            /// Enter point when app his called by another way than user click
            /// </summary>
            /// <param name="args">Activation args</param>
            protected override void OnActivated(IActivatedEventArgs args)
            {
              /* Init engagement like it was launch by a custom uri scheme */
              EngagementAgent.Instance.Init(args);
              EngagementReach.Instance.Init(args);

              //TODO design action toodo when app is launch

              #region Custom scheme use
              if (args.Kind == ActivationKind.Protocol)
              {
                ProtocolActivatedEventArgs myProtocol = (ProtocolActivatedEventArgs)args;

                if (myProtocol.Uri.Scheme.Equals("protocolName"))
                {
                  string path = myProtocol.Uri.AbsolutePath;
                }
              }
              #endregion

