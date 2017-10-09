---
title: "aaaWindows 通用應用程式 SDK 升級程序"
description: "適用於 Azure Mobile Engagement 的 Windows 通用 app SDK 升級程序"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 4c898175-2cd6-43db-b350-bb408332f24d
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 95aba5d55cd65d4190aad35737f872414b5ed443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-sdk-upgrade-procedures"></a>Windows 通用 app SDK 升級程序
如果您已經有整合至您的應用程式較舊版本的參與，則必須升級 hello SDK 時，下列點 tooconsider hello。

如果您錯過數個版本的 hello SDK 您可能需要指定 toofollow 數個程序。 例如，如果您從 0.10.1 移轉 too0.11.0 您有遵循 hello toofirst"0.9.0 從 too0.10.1 」 程序然後 hello 」 從 0.10.1 too0.11.0 」 程序。

## <a name="from-330-too340"></a>從 3.3.0 too3.4.0
### <a name="test-logs"></a>測試記錄檔
主控台記錄檔所產生的 hello SDK 現在可以啟用/停用/篩選。 toocustomize，更新 hello 屬性`EngagementAgent.Instance.TestLogEnabled`hello 值可從 hello 的 tooone`EngagementTestLogLevel`列舉型別，例如：

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="resources"></a>資源
已改善 hello 觸達重疊。 它是 hello SDK 的 NuGet 封裝資源的一部分。

升級 toohello hello SDK 新版本時，您可以選擇是否要將 tookeep hello 從現有的檔案覆疊資源的資料夾或不：

* 如果 hello 先前覆疊正在為您或您要整合 hello`WebView`項目手動然後您可以決定 tookeep 您現有的檔案，它仍可運作。 
* 如果您想 tooupdate toohello 新建立的重疊只取代 hello 整個`overlay`從您的資源，以從 hello SDK 套件中的 hello 新資料夾 (UWP 應用程式： hello 升級之後，您可以從 %USERPROFILE%取得新重疊資料夾 hello\\。 nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources)。

> [!WARNING]
> 使用 hello 新覆疊時，將會覆寫 hello 舊版本上所做的任何自訂。
> 
> 

## <a name="from-320-too330"></a>從 3.2.0 too3.3.0
### <a name="resources"></a>資源
此步驟僅涉及自訂資源。 如果您已自訂 hello 資源就會有 toobackup hello （html、 影像、 重疊） 的 SDK 提供他們升級和 reapply 上的自訂升級資源。

## <a name="from-310-too320"></a>從 3.1.0 too3.2.0
### <a name="resources"></a>資源
此步驟僅涉及自訂資源。 如果您已自訂 hello 資源就會有 toobackup hello （html、 影像、 重疊） 的 SDK 提供他們升級和 reapply 上的自訂升級資源。

### <a name="webview-integration"></a>Web 檢視整合
在此版本導入一些改進 toomatch 不同裝置的表單係數。 請確定您的整合的 hello webview 符合 hello 下列：

在您的 XAML page () 中：

            <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Right" VerticalAlignment="Top"/>
            <WebView x:Name="engagement_announcement_content" Visibility="Collapsed" HorizontalAlignment="Right" VerticalAlignment="Top"/> 

且在您相關聯的 .cs 檔案中：

    using Microsoft.Azure.Engagement;
    using System;
    using Windows.ApplicationModel.Core;
    using Windows.UI.ViewManagement;
    using Windows.UI.Xaml;
    using Windows.UI.Xaml.Navigation;

    namespace My.Namespace.Example
    {
            /// <summary>
            /// An empty page that can be used on its own or navigated toowithin a Frame.
            /// </summary>
            public sealed partial class ExampleEngagementReachPage : EngagementPage
            {
              public ExampleEngagementReachPage()
              {
                this.InitializeComponent();

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }

              #region tooimplement
              /* Attach events when page is navigated. */
              protected override void OnNavigatedTo(NavigationEventArgs e)
              {
                /* Update hello webview when hello app window is resized. */
                Window.Current.SizeChanged += DisplayProperties_OrientationChanged;

                /* Update hello webview when hello app/status bar is resized. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged += DisplayProperties_VisibleBoundsChanged; 
    #endif
                base.OnNavigatedTo(e);
              }

              /* When page is left ensure toodetach SizeChanged handler. */
              protected override void OnNavigatedFrom(NavigationEventArgs e)
              {
                Window.Current.SizeChanged -= DisplayProperties_OrientationChanged;
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged -= DisplayProperties_VisibleBoundsChanged;
    #endif
                base.OnNavigatedFrom(e);
              }

              /* "width" and "height" are hello current size of your application display. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
              double width = ApplicationView.GetForCurrentView().VisibleBounds.Width;
              double height = ApplicationView.GetForCurrentView().VisibleBounds.Height;
    #else
              double width =  Window.Current.Bounds.Width;
              double height =  Window.Current.Bounds.Height;
    #endif

              /// <summary>
              /// Set your webview elements toohello correct size.
              /// </summary>
              /// <param name="width">hello width of your current display.</param>
              /// <param name="height">hello height of your current display.</param>
              private void SetWebView(double width, double height)
              {
                #pragma warning disable 4014
                CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal,
                        () =>
                        {
                          this.engagement_notification_content.Width = width;
                          this.engagement_announcement_content.Width = width;
                          this.engagement_announcement_content.Height = height;
                        });
              }

              /// <summary>
              /// Handler that takes hello Windows.Current.SizeChanged and indicates that webviews have toobe resized.
              /// </summary>
              /// <param name="sender">Original event trigger.</param>
              /// <param name="e">Window Size Changed Event arguments.</param>
              private void DisplayProperties_OrientationChanged(object sender, Windows.UI.Core.WindowSizeChangedEventArgs e)
              {
                double width = e.Size.Width;
                double height = e.Size.Height;

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }

    #if WINDOWS_PHONE_APP || WINDOWS_UWP              
              /// <summary>
              /// Handler that takes hello ApplicationView.VisibleBoundsChanged and indicates that webviews have toobe resized
              /// </summary>
              /// <param name="sender">hello related application view.</param>
              /// <param name="e">Related event arguments.</param>
              private void DisplayProperties_VisibleBoundsChanged(ApplicationView sender, Object e)
              {
                double width = sender.VisibleBounds.Width;
                double height = sender.VisibleBounds.Height;

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }
    #endif
              #endregion
            }
    }

## <a name="from-200-too300"></a>從 2.0.0 too3.0.0
### <a name="resources"></a>資源
此步驟僅涉及自訂資源。 如果您已自訂 hello 資源就會有 toobackup hello （html、 影像、 重疊） 的 SDK 提供他們升級和 reapply 上的自訂升級資源。

## <a name="from-111-too200"></a>從 1.1.1 too2.0.0
hello 下列程式碼說明如何 toomigrate hello Capptain 服務從 SDK 整合提供 Capptain SAS 到由 Azure Mobile Engagement 應用程式。 

> [!IMPORTANT]
> Capptain 和 Mobile Engagement 不是 hello 相同的服務和 hello 下列程序只會反白顯示 toomigrate hello 用戶端應用程式的方式。 移轉 hello SDK hello 應用程式中的不會移轉您的資料從 hello Capptain 伺服器 toohello Mobile Engagement 伺服器
> 
> 

如果您從舊版移轉，請先參閱 hello Capptain 網站 toomigrate too1.1.1 則套用 hello 遵循程序

### <a name="nuget-package"></a>Nuget 封裝
以 **MicrosoftAzure.MobileEngagement** Nuget 套件取代 **Capptain.WindowsPhone**。

### <a name="applying-mobile-engagement"></a>套用 Mobile Engagement
hello SDK 會使用 hello 詞彙`Engagement`。 您需要 tooupdate 專案 toomatch 這項變更。

您需要 toouninstall 目前 Capptain nuget 套件。 請考慮您在 [Capptain Resources] 資料夾中所有的變更將會移除。 如果您要 tookeep 那些檔案，請建立一份。

之後，請在您的專案上安裝 hello 新 Microsoft Azure Engagement nuget 封裝。 您可以直接在 [nuget 網站]上找到。 或此處的索引。 這個動作會取代所有的資源檔案由參與，並將新 Engagement DLL tooyour hello 專案參考。

您的 tooclean 您的專案參考刪除 Capptain DLL 的參考。 如果不這樣做，Capptain hello 版本會發生衝突，會發生錯誤。

如果您已自訂 Capptain 資源，複製舊的檔案內容，並將它們貼在 hello 新 Engagement 檔案中。 請注意，xaml 和 cs 檔案有 toobe 更新。

這些步驟都完成之後，您只需要由 hello 新 Engagement 參考 tooreplace 舊 Capptain 參考。

1. 所有 Capptain 命名空間都有 toobe 更新。
   
    移轉前：
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    移轉後：
   
        using Microsoft.Azure.Engagement;
2. 所有包含 "Capptain" 的 Capptain 類別應該要包含 "Engagement"。
   
    移轉前：
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    移轉後：
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. 對於 xaml 檔案，Capptain 命名空間和屬性也會變更。
   
    移轉前：
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    移轉後：
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. 重疊項目頁面變更
   
   > [!IMPORTANT]
   > 重疊項目也會變更。 它的新命名空間為 `Microsoft.Azure.Engagement.Overlay`。 它有 toobe xaml 和 cs 檔案中使用。 此外`CapptainGrid`toobe 名為`EngagementGrid`，`capptain_notification_content`和`capptain_announcement_content`命名`engagement_notification_content`和`engagement_announcement_content`。
   > 
   > 
   
    針對重疊：
   
        <capptain:CapptainPageOverlay
          xmlns:capptain="using:Capptain.Overlay"
          ...
        </capptain:CapptainPageOverlay>
   
    它會變成：
   
        <EngagementPageOverlay
          engagement="using:Microsoft.Azure.Engagement.Overlay"
          ...
        </engagement:EngagementPageOverlay>
5. Hello 的其他資源，例如 Capptain 圖片和 HTML 檔案，請注意，它們也已重新命名的 toouse 「 參與 」。

### <a name="project-declaration"></a>專案宣告
Package.appxmanifest 上的 `File Type Associations` 已經更新自：

* capptain\_到達\_內容 tooengagement\_到達\_內容
* capptain\_記錄\_檔案 tooengagement\_記錄\_檔案

### <a name="application-id--sdk-key"></a>應用程式 ID / SDK 金鑰
Engagement 使用連接字串。 您沒有 toospecify 應用程式識別碼和與 Mobile Engagement SDK 金鑰，您只需要 toospecify 連接字串。 您可以在您的 EngagementConfiguration 檔案中設定它。

hello Engagement 組態可以設定您`Resources\EngagementConfiguration.xml`專案檔。

編輯此檔案 toospecify:

* 應用程式在 `<connectionString>` 和 `<\connectionString>` 標記之間的連接字串。

如果您想要在執行階段相反地，您可以呼叫 hello 下列 toospecify hello Engagement 代理程式初始化之前的方法：

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(args, engagementConfiguration);

您的應用程式的 hello 連接字串會顯示在 hello Azure 傳統入口網站。

### <a name="items-name-change"></a>項目名稱變更
所有名為 capptain 的項目已命名為 engagement。 同樣地針對*Capptain*太*Engagement*。

常用 Capptain 項目的範例：

* CapptainConfiguration 現在名為 EngagementConfiguration
* CapptainAgent 現在名為 EngagementAgent
* CapptainReach 現在名為 EngagementReach
* CapptainHttpConfig 現在名為 EngagementHttpConfig
* GetCapptainPageName 現在名為 GetEngagementPageName

請注意，重新命名也會影響覆寫方法。

