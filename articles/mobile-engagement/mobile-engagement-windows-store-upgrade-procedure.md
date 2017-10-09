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
# <a name="windows-universal-apps-sdk-upgrade-procedures"></a><span data-ttu-id="d4462-103">Windows 通用 app SDK 升級程序</span><span class="sxs-lookup"><span data-stu-id="d4462-103">Windows Universal Apps SDK Upgrade Procedures</span></span>
<span data-ttu-id="d4462-104">如果您已經有整合至您的應用程式較舊版本的參與，則必須升級 hello SDK 時，下列點 tooconsider hello。</span><span class="sxs-lookup"><span data-stu-id="d4462-104">If you already have integrated an older version of Engagement into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="d4462-105">如果您錯過數個版本的 hello SDK 您可能需要指定 toofollow 數個程序。</span><span class="sxs-lookup"><span data-stu-id="d4462-105">You may have toofollow several procedures if you missed several versions of hello SDK.</span></span> <span data-ttu-id="d4462-106">例如，如果您從 0.10.1 移轉 too0.11.0 您有遵循 hello toofirst"0.9.0 從 too0.10.1 」 程序然後 hello 」 從 0.10.1 too0.11.0 」 程序。</span><span class="sxs-lookup"><span data-stu-id="d4462-106">For example if you migrate from 0.10.1 too0.11.0 you have toofirst follow hello "from 0.9.0 too0.10.1" procedure then hello "from 0.10.1 too0.11.0" procedure.</span></span>

## <a name="from-330-too340"></a><span data-ttu-id="d4462-107">從 3.3.0 too3.4.0</span><span class="sxs-lookup"><span data-stu-id="d4462-107">From 3.3.0 too3.4.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="d4462-108">測試記錄檔</span><span class="sxs-lookup"><span data-stu-id="d4462-108">Test logs</span></span>
<span data-ttu-id="d4462-109">主控台記錄檔所產生的 hello SDK 現在可以啟用/停用/篩選。</span><span class="sxs-lookup"><span data-stu-id="d4462-109">Console logs produced by hello SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="d4462-110">toocustomize，更新 hello 屬性`EngagementAgent.Instance.TestLogEnabled`hello 值可從 hello 的 tooone`EngagementTestLogLevel`列舉型別，例如：</span><span class="sxs-lookup"><span data-stu-id="d4462-110">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="resources"></a><span data-ttu-id="d4462-111">資源</span><span class="sxs-lookup"><span data-stu-id="d4462-111">Resources</span></span>
<span data-ttu-id="d4462-112">已改善 hello 觸達重疊。</span><span class="sxs-lookup"><span data-stu-id="d4462-112">hello Reach overlay has been improved.</span></span> <span data-ttu-id="d4462-113">它是 hello SDK 的 NuGet 封裝資源的一部分。</span><span class="sxs-lookup"><span data-stu-id="d4462-113">It is part of hello SDK NuGet package resources.</span></span>

<span data-ttu-id="d4462-114">升級 toohello hello SDK 新版本時，您可以選擇是否要將 tookeep hello 從現有的檔案覆疊資源的資料夾或不：</span><span class="sxs-lookup"><span data-stu-id="d4462-114">While upgrading toohello new version of hello SDK you can choose whether you want tookeep your existing files from hello overlay folder of your resources or not:</span></span>

* <span data-ttu-id="d4462-115">如果 hello 先前覆疊正在為您或您要整合 hello`WebView`項目手動然後您可以決定 tookeep 您現有的檔案，它仍可運作。</span><span class="sxs-lookup"><span data-stu-id="d4462-115">If hello previous overlay is working for you or you are integrating hello `WebView` elements manually then you can decide tookeep your exiting files, it will still work.</span></span> 
* <span data-ttu-id="d4462-116">如果您想 tooupdate toohello 新建立的重疊只取代 hello 整個`overlay`從您的資源，以從 hello SDK 套件中的 hello 新資料夾 (UWP 應用程式： hello 升級之後，您可以從 %USERPROFILE%取得新重疊資料夾 hello\\。 nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources)。</span><span class="sxs-lookup"><span data-stu-id="d4462-116">If you want tooupdate toohello new overlay, just replace hello whole `overlay` folder from your resources with hello new one from hello SDK package (UWP apps: after hello upgrade, you can get hello new overlay folder from %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span></span>

> [!WARNING]
> <span data-ttu-id="d4462-117">使用 hello 新覆疊時，將會覆寫 hello 舊版本上所做的任何自訂。</span><span class="sxs-lookup"><span data-stu-id="d4462-117">Using hello new overlay will overwrite any customizations made on hello previous version.</span></span>
> 
> 

## <a name="from-320-too330"></a><span data-ttu-id="d4462-118">從 3.2.0 too3.3.0</span><span class="sxs-lookup"><span data-stu-id="d4462-118">From 3.2.0 too3.3.0</span></span>
### <a name="resources"></a><span data-ttu-id="d4462-119">資源</span><span class="sxs-lookup"><span data-stu-id="d4462-119">Resources</span></span>
<span data-ttu-id="d4462-120">此步驟僅涉及自訂資源。</span><span class="sxs-lookup"><span data-stu-id="d4462-120">This step concerns customized resources only.</span></span> <span data-ttu-id="d4462-121">如果您已自訂 hello 資源就會有 toobackup hello （html、 影像、 重疊） 的 SDK 提供他們升級和 reapply 上的自訂升級資源。</span><span class="sxs-lookup"><span data-stu-id="d4462-121">If you have customized hello resources provided by hello SDK (html, images, overlay) then you have toobackup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-310-too320"></a><span data-ttu-id="d4462-122">從 3.1.0 too3.2.0</span><span class="sxs-lookup"><span data-stu-id="d4462-122">From 3.1.0 too3.2.0</span></span>
### <a name="resources"></a><span data-ttu-id="d4462-123">資源</span><span class="sxs-lookup"><span data-stu-id="d4462-123">Resources</span></span>
<span data-ttu-id="d4462-124">此步驟僅涉及自訂資源。</span><span class="sxs-lookup"><span data-stu-id="d4462-124">This step concerns customized resources only.</span></span> <span data-ttu-id="d4462-125">如果您已自訂 hello 資源就會有 toobackup hello （html、 影像、 重疊） 的 SDK 提供他們升級和 reapply 上的自訂升級資源。</span><span class="sxs-lookup"><span data-stu-id="d4462-125">If you have customized hello resources provided by hello SDK (html, images, overlay) then you have toobackup them before upgrading and reapply your customization on upgraded resources.</span></span>

### <a name="webview-integration"></a><span data-ttu-id="d4462-126">Web 檢視整合</span><span class="sxs-lookup"><span data-stu-id="d4462-126">Webview integration</span></span>
<span data-ttu-id="d4462-127">在此版本導入一些改進 toomatch 不同裝置的表單係數。</span><span class="sxs-lookup"><span data-stu-id="d4462-127">Some improvements toomatch different device form factors were introduced in this version.</span></span> <span data-ttu-id="d4462-128">請確定您的整合的 hello webview 符合 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="d4462-128">Make sure that your integration of hello webview match hello following:</span></span>

<span data-ttu-id="d4462-129">在您的 XAML page () 中：</span><span class="sxs-lookup"><span data-stu-id="d4462-129">In your XAML page ():</span></span>

            <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Right" VerticalAlignment="Top"/>
            <WebView x:Name="engagement_announcement_content" Visibility="Collapsed" HorizontalAlignment="Right" VerticalAlignment="Top"/> 

<span data-ttu-id="d4462-130">且在您相關聯的 .cs 檔案中：</span><span class="sxs-lookup"><span data-stu-id="d4462-130">And in your associated .cs file:</span></span>

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

## <a name="from-200-too300"></a><span data-ttu-id="d4462-131">從 2.0.0 too3.0.0</span><span class="sxs-lookup"><span data-stu-id="d4462-131">From 2.0.0 too3.0.0</span></span>
### <a name="resources"></a><span data-ttu-id="d4462-132">資源</span><span class="sxs-lookup"><span data-stu-id="d4462-132">Resources</span></span>
<span data-ttu-id="d4462-133">此步驟僅涉及自訂資源。</span><span class="sxs-lookup"><span data-stu-id="d4462-133">This step concerns customized resources only.</span></span> <span data-ttu-id="d4462-134">如果您已自訂 hello 資源就會有 toobackup hello （html、 影像、 重疊） 的 SDK 提供他們升級和 reapply 上的自訂升級資源。</span><span class="sxs-lookup"><span data-stu-id="d4462-134">If you have customized hello resources provided by hello SDK (html, images, overlay) then you have toobackup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-111-too200"></a><span data-ttu-id="d4462-135">從 1.1.1 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="d4462-135">From 1.1.1 too2.0.0</span></span>
<span data-ttu-id="d4462-136">hello 下列程式碼說明如何 toomigrate hello Capptain 服務從 SDK 整合提供 Capptain SAS 到由 Azure Mobile Engagement 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d4462-136">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d4462-137">Capptain 和 Mobile Engagement 不是 hello 相同的服務和 hello 下列程序只會反白顯示 toomigrate hello 用戶端應用程式的方式。</span><span class="sxs-lookup"><span data-stu-id="d4462-137">Capptain and Mobile Engagement are not hello same services and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="d4462-138">移轉 hello SDK hello 應用程式中的不會移轉您的資料從 hello Capptain 伺服器 toohello Mobile Engagement 伺服器</span><span class="sxs-lookup"><span data-stu-id="d4462-138">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="d4462-139">如果您從舊版移轉，請先參閱 hello Capptain 網站 toomigrate too1.1.1 則套用 hello 遵循程序</span><span class="sxs-lookup"><span data-stu-id="d4462-139">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too1.1.1 first then apply hello following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="d4462-140">Nuget 封裝</span><span class="sxs-lookup"><span data-stu-id="d4462-140">Nuget package</span></span>
<span data-ttu-id="d4462-141">以 **MicrosoftAzure.MobileEngagement** Nuget 套件取代 **Capptain.WindowsPhone**。</span><span class="sxs-lookup"><span data-stu-id="d4462-141">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="d4462-142">套用 Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="d4462-142">Applying Mobile Engagement</span></span>
<span data-ttu-id="d4462-143">hello SDK 會使用 hello 詞彙`Engagement`。</span><span class="sxs-lookup"><span data-stu-id="d4462-143">hello SDK uses hello term `Engagement`.</span></span> <span data-ttu-id="d4462-144">您需要 tooupdate 專案 toomatch 這項變更。</span><span class="sxs-lookup"><span data-stu-id="d4462-144">You need tooupdate your project toomatch this change.</span></span>

<span data-ttu-id="d4462-145">您需要 toouninstall 目前 Capptain nuget 套件。</span><span class="sxs-lookup"><span data-stu-id="d4462-145">You need toouninstall your current Capptain nuget package.</span></span> <span data-ttu-id="d4462-146">請考慮您在 [Capptain Resources] 資料夾中所有的變更將會移除。</span><span class="sxs-lookup"><span data-stu-id="d4462-146">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="d4462-147">如果您要 tookeep 那些檔案，請建立一份。</span><span class="sxs-lookup"><span data-stu-id="d4462-147">If you want tookeep those files then make a copy of them.</span></span>

<span data-ttu-id="d4462-148">之後，請在您的專案上安裝 hello 新 Microsoft Azure Engagement nuget 封裝。</span><span class="sxs-lookup"><span data-stu-id="d4462-148">After that, install hello new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="d4462-149">您可以直接在 [nuget 網站]上找到。</span><span class="sxs-lookup"><span data-stu-id="d4462-149">You can find it directly on [nuget website].</span></span> <span data-ttu-id="d4462-150">或此處的索引。</span><span class="sxs-lookup"><span data-stu-id="d4462-150">or here index.</span></span> <span data-ttu-id="d4462-151">這個動作會取代所有的資源檔案由參與，並將新 Engagement DLL tooyour hello 專案參考。</span><span class="sxs-lookup"><span data-stu-id="d4462-151">This action replaces all resources files used by Engagement and adds hello new Engagement DLL tooyour project References.</span></span>

<span data-ttu-id="d4462-152">您的 tooclean 您的專案參考刪除 Capptain DLL 的參考。</span><span class="sxs-lookup"><span data-stu-id="d4462-152">You have tooclean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="d4462-153">如果不這樣做，Capptain hello 版本會發生衝突，會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="d4462-153">If you do not make this, hello version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="d4462-154">如果您已自訂 Capptain 資源，複製舊的檔案內容，並將它們貼在 hello 新 Engagement 檔案中。</span><span class="sxs-lookup"><span data-stu-id="d4462-154">If you have customized Capptain resources, copy your old files content and paste them in hello new Engagement files.</span></span> <span data-ttu-id="d4462-155">請注意，xaml 和 cs 檔案有 toobe 更新。</span><span class="sxs-lookup"><span data-stu-id="d4462-155">Please note that both xaml and cs files have toobe updated.</span></span>

<span data-ttu-id="d4462-156">這些步驟都完成之後，您只需要由 hello 新 Engagement 參考 tooreplace 舊 Capptain 參考。</span><span class="sxs-lookup"><span data-stu-id="d4462-156">When those steps are completed you only have tooreplace old Capptain references by hello new Engagement references.</span></span>

1. <span data-ttu-id="d4462-157">所有 Capptain 命名空間都有 toobe 更新。</span><span class="sxs-lookup"><span data-stu-id="d4462-157">All Capptain namespaces have toobe updated.</span></span>
   
    <span data-ttu-id="d4462-158">移轉前：</span><span class="sxs-lookup"><span data-stu-id="d4462-158">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="d4462-159">移轉後：</span><span class="sxs-lookup"><span data-stu-id="d4462-159">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="d4462-160">所有包含 "Capptain" 的 Capptain 類別應該要包含 "Engagement"。</span><span class="sxs-lookup"><span data-stu-id="d4462-160">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="d4462-161">移轉前：</span><span class="sxs-lookup"><span data-stu-id="d4462-161">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="d4462-162">移轉後：</span><span class="sxs-lookup"><span data-stu-id="d4462-162">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="d4462-163">對於 xaml 檔案，Capptain 命名空間和屬性也會變更。</span><span class="sxs-lookup"><span data-stu-id="d4462-163">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="d4462-164">移轉前：</span><span class="sxs-lookup"><span data-stu-id="d4462-164">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="d4462-165">移轉後：</span><span class="sxs-lookup"><span data-stu-id="d4462-165">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="d4462-166">重疊項目頁面變更</span><span class="sxs-lookup"><span data-stu-id="d4462-166">Overlay page changes</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="d4462-167">重疊項目也會變更。</span><span class="sxs-lookup"><span data-stu-id="d4462-167">Overlay also changes.</span></span> <span data-ttu-id="d4462-168">它的新命名空間為 `Microsoft.Azure.Engagement.Overlay`。</span><span class="sxs-lookup"><span data-stu-id="d4462-168">Its new namespace is `Microsoft.Azure.Engagement.Overlay`.</span></span> <span data-ttu-id="d4462-169">它有 toobe xaml 和 cs 檔案中使用。</span><span class="sxs-lookup"><span data-stu-id="d4462-169">It has toobe used in both xaml and cs files.</span></span> <span data-ttu-id="d4462-170">此外`CapptainGrid`toobe 名為`EngagementGrid`，`capptain_notification_content`和`capptain_announcement_content`命名`engagement_notification_content`和`engagement_announcement_content`。</span><span class="sxs-lookup"><span data-stu-id="d4462-170">Moreover `CapptainGrid` is toobe named `EngagementGrid`, `capptain_notification_content` and `capptain_announcement_content` are named `engagement_notification_content` and `engagement_announcement_content`.</span></span>
   > 
   > 
   
    <span data-ttu-id="d4462-171">針對重疊：</span><span class="sxs-lookup"><span data-stu-id="d4462-171">For overlay :</span></span>
   
        <capptain:CapptainPageOverlay
          xmlns:capptain="using:Capptain.Overlay"
          ...
        </capptain:CapptainPageOverlay>
   
    <span data-ttu-id="d4462-172">它會變成：</span><span class="sxs-lookup"><span data-stu-id="d4462-172">It becomes :</span></span>
   
        <EngagementPageOverlay
          engagement="using:Microsoft.Azure.Engagement.Overlay"
          ...
        </engagement:EngagementPageOverlay>
5. <span data-ttu-id="d4462-173">Hello 的其他資源，例如 Capptain 圖片和 HTML 檔案，請注意，它們也已重新命名的 toouse 「 參與 」。</span><span class="sxs-lookup"><span data-stu-id="d4462-173">For hello other resources like Capptain pictures and HTML files, please note that they also have been renamed toouse "Engagement".</span></span>

### <a name="project-declaration"></a><span data-ttu-id="d4462-174">專案宣告</span><span class="sxs-lookup"><span data-stu-id="d4462-174">Project declaration</span></span>
<span data-ttu-id="d4462-175">Package.appxmanifest 上的 `File Type Associations` 已經更新自：</span><span class="sxs-lookup"><span data-stu-id="d4462-175">On Package.appxmanifest `File Type Associations` has been updated from :</span></span>

* <span data-ttu-id="d4462-176">capptain\_到達\_內容 tooengagement\_到達\_內容</span><span class="sxs-lookup"><span data-stu-id="d4462-176">capptain\_reach\_content tooengagement\_reach\_content</span></span>
* <span data-ttu-id="d4462-177">capptain\_記錄\_檔案 tooengagement\_記錄\_檔案</span><span class="sxs-lookup"><span data-stu-id="d4462-177">capptain\_log\_file tooengagement\_log\_file</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="d4462-178">應用程式 ID / SDK 金鑰</span><span class="sxs-lookup"><span data-stu-id="d4462-178">Application ID / SDK Key</span></span>
<span data-ttu-id="d4462-179">Engagement 使用連接字串。</span><span class="sxs-lookup"><span data-stu-id="d4462-179">Engagement uses a connection string.</span></span> <span data-ttu-id="d4462-180">您沒有 toospecify 應用程式識別碼和與 Mobile Engagement SDK 金鑰，您只需要 toospecify 連接字串。</span><span class="sxs-lookup"><span data-stu-id="d4462-180">You don't have toospecify an application ID and an SDK key with Mobile Engagement, you only have toospecify a connection string.</span></span> <span data-ttu-id="d4462-181">您可以在您的 EngagementConfiguration 檔案中設定它。</span><span class="sxs-lookup"><span data-stu-id="d4462-181">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="d4462-182">hello Engagement 組態可以設定您`Resources\EngagementConfiguration.xml`專案檔。</span><span class="sxs-lookup"><span data-stu-id="d4462-182">hello Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="d4462-183">編輯此檔案 toospecify:</span><span class="sxs-lookup"><span data-stu-id="d4462-183">Edit this file toospecify:</span></span>

* <span data-ttu-id="d4462-184">應用程式在 `<connectionString>` 和 `<\connectionString>` 標記之間的連接字串。</span><span class="sxs-lookup"><span data-stu-id="d4462-184">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="d4462-185">如果您想要在執行階段相反地，您可以呼叫 hello 下列 toospecify hello Engagement 代理程式初始化之前的方法：</span><span class="sxs-lookup"><span data-stu-id="d4462-185">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(args, engagementConfiguration);

<span data-ttu-id="d4462-186">您的應用程式的 hello 連接字串會顯示在 hello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="d4462-186">hello connection string for your application is displayed on hello Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="d4462-187">項目名稱變更</span><span class="sxs-lookup"><span data-stu-id="d4462-187">Items name change</span></span>
<span data-ttu-id="d4462-188">所有名為 capptain 的項目已命名為 engagement。</span><span class="sxs-lookup"><span data-stu-id="d4462-188">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="d4462-189">同樣地針對*Capptain*太*Engagement*。</span><span class="sxs-lookup"><span data-stu-id="d4462-189">Similarly for *Capptain* too*Engagement*.</span></span>

<span data-ttu-id="d4462-190">常用 Capptain 項目的範例：</span><span class="sxs-lookup"><span data-stu-id="d4462-190">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="d4462-191">CapptainConfiguration 現在名為 EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="d4462-191">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="d4462-192">CapptainAgent 現在名為 EngagementAgent</span><span class="sxs-lookup"><span data-stu-id="d4462-192">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="d4462-193">CapptainReach 現在名為 EngagementReach</span><span class="sxs-lookup"><span data-stu-id="d4462-193">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="d4462-194">CapptainHttpConfig 現在名為 EngagementHttpConfig</span><span class="sxs-lookup"><span data-stu-id="d4462-194">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="d4462-195">GetCapptainPageName 現在名為 GetEngagementPageName</span><span class="sxs-lookup"><span data-stu-id="d4462-195">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="d4462-196">請注意，重新命名也會影響覆寫方法。</span><span class="sxs-lookup"><span data-stu-id="d4462-196">Note that rename also affects overridden methods.</span></span>

