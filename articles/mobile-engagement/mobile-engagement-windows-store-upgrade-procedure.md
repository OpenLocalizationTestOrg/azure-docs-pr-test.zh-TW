---
title: "Windows 通用 app SDK 升級程序"
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
ms.openlocfilehash: fe85a99a92fb39082cafe7422b356de1f20f14bd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="windows-universal-apps-sdk-upgrade-procedures"></a><span data-ttu-id="b76e2-103">Windows 通用 app SDK 升級程序</span><span class="sxs-lookup"><span data-stu-id="b76e2-103">Windows Universal Apps SDK Upgrade Procedures</span></span>
<span data-ttu-id="b76e2-104">如果您已經整合舊版 Engagement 到您的應用程式，在升級 SDK 時您必須考慮以下幾點。</span><span class="sxs-lookup"><span data-stu-id="b76e2-104">If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="b76e2-105">如果您有錯過幾個版本的 SDK，您必須遵循幾個步驟。</span><span class="sxs-lookup"><span data-stu-id="b76e2-105">You may have to follow several procedures if you missed several versions of the SDK.</span></span> <span data-ttu-id="b76e2-106">例如，如果您要從 0.10.1 移轉到 0.11.0，必須先遵循「從 0.9.0 到 0.10.1」的程序，然後「從 0.10.1 到 0.11.0」的程序。</span><span class="sxs-lookup"><span data-stu-id="b76e2-106">For example if you migrate from 0.10.1 to 0.11.0 you have to first follow the "from 0.9.0 to 0.10.1" procedure then the "from 0.10.1 to 0.11.0" procedure.</span></span>

## <a name="from-330-to-340"></a><span data-ttu-id="b76e2-107">從 3.3.0 到 3.4.0</span><span class="sxs-lookup"><span data-stu-id="b76e2-107">From 3.3.0 to 3.4.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="b76e2-108">測試記錄檔</span><span class="sxs-lookup"><span data-stu-id="b76e2-108">Test logs</span></span>
<span data-ttu-id="b76e2-109">SDK 所產生的主控台記錄檔現在可以啟用/停用/篩選。</span><span class="sxs-lookup"><span data-stu-id="b76e2-109">Console logs produced by the SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="b76e2-110">若要自訂這種情況，請將屬性 `EngagementAgent.Instance.TestLogEnabled` 更新為 `EngagementTestLogLevel` 列舉的其中一個可用值，例如︰</span><span class="sxs-lookup"><span data-stu-id="b76e2-110">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="resources"></a><span data-ttu-id="b76e2-111">資源</span><span class="sxs-lookup"><span data-stu-id="b76e2-111">Resources</span></span>
<span data-ttu-id="b76e2-112">已改善 Reach 重疊。</span><span class="sxs-lookup"><span data-stu-id="b76e2-112">The Reach overlay has been improved.</span></span> <span data-ttu-id="b76e2-113">它是 SDK NuGet 封裝資源的一部分。</span><span class="sxs-lookup"><span data-stu-id="b76e2-113">It is part of the SDK NuGet package resources.</span></span>

<span data-ttu-id="b76e2-114">當您升級到新版的 SDK，可以選擇是否要保留資源之重疊資料夾中的現有檔案︰</span><span class="sxs-lookup"><span data-stu-id="b76e2-114">While upgrading to the new version of the SDK you can choose whether you want to keep your existing files from the overlay folder of your resources or not:</span></span>

* <span data-ttu-id="b76e2-115">如果先前的重疊對您而言可以運作，或是您要手動整合 `WebView` 元素，則您可以決定保留現有檔案，這樣仍然可以運作。</span><span class="sxs-lookup"><span data-stu-id="b76e2-115">If the previous overlay is working for you or you are integrating the `WebView` elements manually then you can decide to keep your exiting files, it will still work.</span></span> 
* <span data-ttu-id="b76e2-116">如果您想要更新為新的重疊，那麼只要將資源的整個 `overlay` 資料夾取代為來自 SDK 封裝的新資料夾 (UWP 應用程式︰升級後，您可以從 %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources 取得新的重疊資料夾)。</span><span class="sxs-lookup"><span data-stu-id="b76e2-116">If you want to update to the new overlay, just replace the whole `overlay` folder from your resources with the new one from the SDK package (UWP apps: after the upgrade, you can get the new overlay folder from %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span></span>

> [!WARNING]
> <span data-ttu-id="b76e2-117">使用新的重疊會覆寫先前版本上所做的任何自訂。</span><span class="sxs-lookup"><span data-stu-id="b76e2-117">Using the new overlay will overwrite any customizations made on the previous version.</span></span>
> 
> 

## <a name="from-320-to-330"></a><span data-ttu-id="b76e2-118">從 3.2.0 到 3.3.0</span><span class="sxs-lookup"><span data-stu-id="b76e2-118">From 3.2.0 to 3.3.0</span></span>
### <a name="resources"></a><span data-ttu-id="b76e2-119">資源</span><span class="sxs-lookup"><span data-stu-id="b76e2-119">Resources</span></span>
<span data-ttu-id="b76e2-120">此步驟僅涉及自訂資源。</span><span class="sxs-lookup"><span data-stu-id="b76e2-120">This step concerns customized resources only.</span></span> <span data-ttu-id="b76e2-121">如果您已自訂透過 SDK (html、影像、重疊) 提供的資源，則您必須先備份這些資源，然後在已升級的資源上升級和重新套用您的自訂。</span><span class="sxs-lookup"><span data-stu-id="b76e2-121">If you have customized the resources provided by the SDK (html, images, overlay) then you have to backup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-310-to-320"></a><span data-ttu-id="b76e2-122">從 3.1.0 到 3.2.0</span><span class="sxs-lookup"><span data-stu-id="b76e2-122">From 3.1.0 to 3.2.0</span></span>
### <a name="resources"></a><span data-ttu-id="b76e2-123">資源</span><span class="sxs-lookup"><span data-stu-id="b76e2-123">Resources</span></span>
<span data-ttu-id="b76e2-124">此步驟僅涉及自訂資源。</span><span class="sxs-lookup"><span data-stu-id="b76e2-124">This step concerns customized resources only.</span></span> <span data-ttu-id="b76e2-125">如果您已自訂透過 SDK (html、影像、重疊) 提供的資源，則您必須先備份這些資源，然後在已升級的資源上升級和重新套用您的自訂。</span><span class="sxs-lookup"><span data-stu-id="b76e2-125">If you have customized the resources provided by the SDK (html, images, overlay) then you have to backup them before upgrading and reapply your customization on upgraded resources.</span></span>

### <a name="webview-integration"></a><span data-ttu-id="b76e2-126">Web 檢視整合</span><span class="sxs-lookup"><span data-stu-id="b76e2-126">Webview integration</span></span>
<span data-ttu-id="b76e2-127">部分改善以符合此版本中引進的其他裝置版型規格。</span><span class="sxs-lookup"><span data-stu-id="b76e2-127">Some improvements to match different device form factors were introduced in this version.</span></span> <span data-ttu-id="b76e2-128">確認您的 Web 檢視符合下列條件：</span><span class="sxs-lookup"><span data-stu-id="b76e2-128">Make sure that your integration of the webview match the following:</span></span>

<span data-ttu-id="b76e2-129">在您的 XAML page () 中：</span><span class="sxs-lookup"><span data-stu-id="b76e2-129">In your XAML page ():</span></span>

            <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Right" VerticalAlignment="Top"/>
            <WebView x:Name="engagement_announcement_content" Visibility="Collapsed" HorizontalAlignment="Right" VerticalAlignment="Top"/> 

<span data-ttu-id="b76e2-130">且在您相關聯的 .cs 檔案中：</span><span class="sxs-lookup"><span data-stu-id="b76e2-130">And in your associated .cs file:</span></span>

    using Microsoft.Azure.Engagement;
    using System;
    using Windows.ApplicationModel.Core;
    using Windows.UI.ViewManagement;
    using Windows.UI.Xaml;
    using Windows.UI.Xaml.Navigation;

    namespace My.Namespace.Example
    {
            /// <summary>
            /// An empty page that can be used on its own or navigated to within a Frame.
            /// </summary>
            public sealed partial class ExampleEngagementReachPage : EngagementPage
            {
              public ExampleEngagementReachPage()
              {
                this.InitializeComponent();

                /* Set your webview elements to the correct size. */
                SetWebView(width, height);
              }

              #region to implement
              /* Attach events when page is navigated. */
              protected override void OnNavigatedTo(NavigationEventArgs e)
              {
                /* Update the webview when the app window is resized. */
                Window.Current.SizeChanged += DisplayProperties_OrientationChanged;

                /* Update the webview when the app/status bar is resized. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged += DisplayProperties_VisibleBoundsChanged; 
    #endif
                base.OnNavigatedTo(e);
              }

              /* When page is left ensure to detach SizeChanged handler. */
              protected override void OnNavigatedFrom(NavigationEventArgs e)
              {
                Window.Current.SizeChanged -= DisplayProperties_OrientationChanged;
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged -= DisplayProperties_VisibleBoundsChanged;
    #endif
                base.OnNavigatedFrom(e);
              }

              /* "width" and "height" are the current size of your application display. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
              double width = ApplicationView.GetForCurrentView().VisibleBounds.Width;
              double height = ApplicationView.GetForCurrentView().VisibleBounds.Height;
    #else
              double width =  Window.Current.Bounds.Width;
              double height =  Window.Current.Bounds.Height;
    #endif

              /// <summary>
              /// Set your webview elements to the correct size.
              /// </summary>
              /// <param name="width">The width of your current display.</param>
              /// <param name="height">The height of your current display.</param>
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
              /// Handler that takes the Windows.Current.SizeChanged and indicates that webviews have to be resized.
              /// </summary>
              /// <param name="sender">Original event trigger.</param>
              /// <param name="e">Window Size Changed Event arguments.</param>
              private void DisplayProperties_OrientationChanged(object sender, Windows.UI.Core.WindowSizeChangedEventArgs e)
              {
                double width = e.Size.Width;
                double height = e.Size.Height;

                /* Set your webview elements to the correct size. */
                SetWebView(width, height);
              }

    #if WINDOWS_PHONE_APP || WINDOWS_UWP              
              /// <summary>
              /// Handler that takes the ApplicationView.VisibleBoundsChanged and indicates that webviews have to be resized
              /// </summary>
              /// <param name="sender">The related application view.</param>
              /// <param name="e">Related event arguments.</param>
              private void DisplayProperties_VisibleBoundsChanged(ApplicationView sender, Object e)
              {
                double width = sender.VisibleBounds.Width;
                double height = sender.VisibleBounds.Height;

                /* Set your webview elements to the correct size. */
                SetWebView(width, height);
              }
    #endif
              #endregion
            }
    }

## <a name="from-200-to-300"></a><span data-ttu-id="b76e2-131">從 2.0.0 到 3.0.0</span><span class="sxs-lookup"><span data-stu-id="b76e2-131">From 2.0.0 to 3.0.0</span></span>
### <a name="resources"></a><span data-ttu-id="b76e2-132">資源</span><span class="sxs-lookup"><span data-stu-id="b76e2-132">Resources</span></span>
<span data-ttu-id="b76e2-133">此步驟僅涉及自訂資源。</span><span class="sxs-lookup"><span data-stu-id="b76e2-133">This step concerns customized resources only.</span></span> <span data-ttu-id="b76e2-134">如果您已自訂透過 SDK (html、影像、重疊) 提供的資源，則您必須先備份這些資源，然後在已升級的資源上升級和重新套用您的自訂。</span><span class="sxs-lookup"><span data-stu-id="b76e2-134">If you have customized the resources provided by the SDK (html, images, overlay) then you have to backup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-111-to-200"></a><span data-ttu-id="b76e2-135">從 1.1.1 到 2.0.0</span><span class="sxs-lookup"><span data-stu-id="b76e2-135">From 1.1.1 to 2.0.0</span></span>
<span data-ttu-id="b76e2-136">以下說明如何將 SDK 整合從 Capptain SAS 提供的 Capptain 服務，移轉到由 Azure Mobile Engagement 提供的應用程式內。</span><span class="sxs-lookup"><span data-stu-id="b76e2-136">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="b76e2-137">Capptain 和 Mobile Engagement 是不同的服務，而以下程序只適用於移轉用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="b76e2-137">Capptain and Mobile Engagement are not the same services and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="b76e2-138">移轉應用程式中的 SDK「不會」將您的資料從 Capptain 伺服器移轉到 Mobile Engagement 伺服器</span><span class="sxs-lookup"><span data-stu-id="b76e2-138">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="b76e2-139">如果您要從舊版移轉，請先參閱 Capptain 網站以移轉到 1.1.1，然後再遵循以下程序</span><span class="sxs-lookup"><span data-stu-id="b76e2-139">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 1.1.1 first then apply the following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="b76e2-140">Nuget 封裝</span><span class="sxs-lookup"><span data-stu-id="b76e2-140">Nuget package</span></span>
<span data-ttu-id="b76e2-141">以 **MicrosoftAzure.MobileEngagement** Nuget 套件取代 **Capptain.WindowsPhone**。</span><span class="sxs-lookup"><span data-stu-id="b76e2-141">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="b76e2-142">套用 Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="b76e2-142">Applying Mobile Engagement</span></span>
<span data-ttu-id="b76e2-143">SDK 使用 `Engagement`一詞。</span><span class="sxs-lookup"><span data-stu-id="b76e2-143">The SDK uses the term `Engagement`.</span></span> <span data-ttu-id="b76e2-144">您需要更新您的專案，以符合此變更。</span><span class="sxs-lookup"><span data-stu-id="b76e2-144">You need to update your project to match this change.</span></span>

<span data-ttu-id="b76e2-145">您需要解除安裝目前的 Capptain nuget 封裝。</span><span class="sxs-lookup"><span data-stu-id="b76e2-145">You need to uninstall your current Capptain nuget package.</span></span> <span data-ttu-id="b76e2-146">請考慮您在 [Capptain Resources] 資料夾中所有的變更將會移除。</span><span class="sxs-lookup"><span data-stu-id="b76e2-146">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="b76e2-147">如果您想要保留這些檔案，請將它們複製一份。</span><span class="sxs-lookup"><span data-stu-id="b76e2-147">If you want to keep those files then make a copy of them.</span></span>

<span data-ttu-id="b76e2-148">接下來，在您的專案上安裝新的 Microsoft Azure Engagement nuget 封裝。</span><span class="sxs-lookup"><span data-stu-id="b76e2-148">After that, install the new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="b76e2-149">您可以直接在 [nuget 網站]上找到。</span><span class="sxs-lookup"><span data-stu-id="b76e2-149">You can find it directly on [nuget website].</span></span> <span data-ttu-id="b76e2-150">或此處的索引。</span><span class="sxs-lookup"><span data-stu-id="b76e2-150">or here index.</span></span> <span data-ttu-id="b76e2-151">此動作會取代所有 Engagement 使用的資源檔，並將新的 Engagement DLL 新增到您專案的「參考」。</span><span class="sxs-lookup"><span data-stu-id="b76e2-151">This action replaces all resources files used by Engagement and adds the new Engagement DLL to your project References.</span></span>

<span data-ttu-id="b76e2-152">您必須刪除 Capptain DLL 參考來清除您專案的參考。</span><span class="sxs-lookup"><span data-stu-id="b76e2-152">You have to clean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="b76e2-153">如果沒有這樣做，Capptain 的版本會有衝突並發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="b76e2-153">If you do not make this, the version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="b76e2-154">若您有自訂的 Capptain 資源，請複製您舊檔案的內容，並在新的 Engagement 檔案中貼上它們。</span><span class="sxs-lookup"><span data-stu-id="b76e2-154">If you have customized Capptain resources, copy your old files content and paste them in the new Engagement files.</span></span> <span data-ttu-id="b76e2-155">請注意，xaml 和 cs 檔案兩者都必須更新。</span><span class="sxs-lookup"><span data-stu-id="b76e2-155">Please note that both xaml and cs files have to be updated.</span></span>

<span data-ttu-id="b76e2-156">完成這些步驟之後，您只需要用新的 Engagement 參考取代舊的 Capptain 參考。</span><span class="sxs-lookup"><span data-stu-id="b76e2-156">When those steps are completed you only have to replace old Capptain references by the new Engagement references.</span></span>

1. <span data-ttu-id="b76e2-157">所有的 Capptain 命名空間都必須更新。</span><span class="sxs-lookup"><span data-stu-id="b76e2-157">All Capptain namespaces have to be updated.</span></span>
   
    <span data-ttu-id="b76e2-158">移轉前：</span><span class="sxs-lookup"><span data-stu-id="b76e2-158">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="b76e2-159">移轉後：</span><span class="sxs-lookup"><span data-stu-id="b76e2-159">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="b76e2-160">所有包含 "Capptain" 的 Capptain 類別應該要包含 "Engagement"。</span><span class="sxs-lookup"><span data-stu-id="b76e2-160">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="b76e2-161">移轉前：</span><span class="sxs-lookup"><span data-stu-id="b76e2-161">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="b76e2-162">移轉後：</span><span class="sxs-lookup"><span data-stu-id="b76e2-162">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="b76e2-163">對於 xaml 檔案，Capptain 命名空間和屬性也會變更。</span><span class="sxs-lookup"><span data-stu-id="b76e2-163">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="b76e2-164">移轉前：</span><span class="sxs-lookup"><span data-stu-id="b76e2-164">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="b76e2-165">移轉後：</span><span class="sxs-lookup"><span data-stu-id="b76e2-165">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="b76e2-166">重疊項目頁面變更</span><span class="sxs-lookup"><span data-stu-id="b76e2-166">Overlay page changes</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="b76e2-167">重疊項目也會變更。</span><span class="sxs-lookup"><span data-stu-id="b76e2-167">Overlay also changes.</span></span> <span data-ttu-id="b76e2-168">它的新命名空間為 `Microsoft.Azure.Engagement.Overlay`。</span><span class="sxs-lookup"><span data-stu-id="b76e2-168">Its new namespace is `Microsoft.Azure.Engagement.Overlay`.</span></span> <span data-ttu-id="b76e2-169">在 xaml 和 cs 檔案中都必須使用它。</span><span class="sxs-lookup"><span data-stu-id="b76e2-169">It has to be used in both xaml and cs files.</span></span> <span data-ttu-id="b76e2-170">此外，`CapptainGrid` 命名為 `EngagementGrid`，`capptain_notification_content` 和 `capptain_announcement_content` 命名為 `engagement_notification_content` 和 `engagement_announcement_content`。</span><span class="sxs-lookup"><span data-stu-id="b76e2-170">Moreover `CapptainGrid` is to be named `EngagementGrid`, `capptain_notification_content` and `capptain_announcement_content` are named `engagement_notification_content` and `engagement_announcement_content`.</span></span>
   > 
   > 
   
    <span data-ttu-id="b76e2-171">針對重疊：</span><span class="sxs-lookup"><span data-stu-id="b76e2-171">For overlay :</span></span>
   
        <capptain:CapptainPageOverlay
          xmlns:capptain="using:Capptain.Overlay"
          ...
        </capptain:CapptainPageOverlay>
   
    <span data-ttu-id="b76e2-172">它會變成：</span><span class="sxs-lookup"><span data-stu-id="b76e2-172">It becomes :</span></span>
   
        <EngagementPageOverlay
          engagement="using:Microsoft.Azure.Engagement.Overlay"
          ...
        </engagement:EngagementPageOverlay>
5. <span data-ttu-id="b76e2-173">針對其他資源，例如 Capptain 圖片和 HTML 檔案，請注意它們也已重新命名使用 "Engagement"。</span><span class="sxs-lookup"><span data-stu-id="b76e2-173">For the other resources like Capptain pictures and HTML files, please note that they also have been renamed to use "Engagement".</span></span>

### <a name="project-declaration"></a><span data-ttu-id="b76e2-174">專案宣告</span><span class="sxs-lookup"><span data-stu-id="b76e2-174">Project declaration</span></span>
<span data-ttu-id="b76e2-175">Package.appxmanifest 上的 `File Type Associations` 已經更新自：</span><span class="sxs-lookup"><span data-stu-id="b76e2-175">On Package.appxmanifest `File Type Associations` has been updated from :</span></span>

* <span data-ttu-id="b76e2-176">capptain\_reach\_content to engagement\_reach\_content</span><span class="sxs-lookup"><span data-stu-id="b76e2-176">capptain\_reach\_content to engagement\_reach\_content</span></span>
* <span data-ttu-id="b76e2-177">capptain\_log\_file to engagement\_log\_file</span><span class="sxs-lookup"><span data-stu-id="b76e2-177">capptain\_log\_file to engagement\_log\_file</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="b76e2-178">應用程式 ID / SDK 金鑰</span><span class="sxs-lookup"><span data-stu-id="b76e2-178">Application ID / SDK Key</span></span>
<span data-ttu-id="b76e2-179">Engagement 使用連接字串。</span><span class="sxs-lookup"><span data-stu-id="b76e2-179">Engagement uses a connection string.</span></span> <span data-ttu-id="b76e2-180">您不需要為 Mobile Engagement 指定應用程式 ID 和 SDK 金鑰，您只需要指定連接字串。</span><span class="sxs-lookup"><span data-stu-id="b76e2-180">You don't have to specify an application ID and an SDK key with Mobile Engagement, you only have to specify a connection string.</span></span> <span data-ttu-id="b76e2-181">您可以在您的 EngagementConfiguration 檔案中設定它。</span><span class="sxs-lookup"><span data-stu-id="b76e2-181">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="b76e2-182">您可以在專案的 `Resources\EngagementConfiguration.xml` 檔案中設定 Engagement 組態。</span><span class="sxs-lookup"><span data-stu-id="b76e2-182">The Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="b76e2-183">編輯此檔案來指定：</span><span class="sxs-lookup"><span data-stu-id="b76e2-183">Edit this file to specify:</span></span>

* <span data-ttu-id="b76e2-184">應用程式在 `<connectionString>` 和 `<\connectionString>` 標記之間的連接字串。</span><span class="sxs-lookup"><span data-stu-id="b76e2-184">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="b76e2-185">若想要改為在執行階段指定它，您可以在 Engagement 代理程式初始化之前呼叫下列方法：</span><span class="sxs-lookup"><span data-stu-id="b76e2-185">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(args, engagementConfiguration);

<span data-ttu-id="b76e2-186">應用程式的連接字串會顯示在 Azure 傳統入口網站中。</span><span class="sxs-lookup"><span data-stu-id="b76e2-186">The connection string for your application is displayed on the Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="b76e2-187">項目名稱變更</span><span class="sxs-lookup"><span data-stu-id="b76e2-187">Items name change</span></span>
<span data-ttu-id="b76e2-188">所有名為 capptain 的項目已命名為 engagement。</span><span class="sxs-lookup"><span data-stu-id="b76e2-188">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="b76e2-189">同樣地，Capptain 也已命名為 Engagement。</span><span class="sxs-lookup"><span data-stu-id="b76e2-189">Similarly for *Capptain* to *Engagement*.</span></span>

<span data-ttu-id="b76e2-190">常用 Capptain 項目的範例：</span><span class="sxs-lookup"><span data-stu-id="b76e2-190">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="b76e2-191">CapptainConfiguration 現在名為 EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="b76e2-191">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="b76e2-192">CapptainAgent 現在名為 EngagementAgent</span><span class="sxs-lookup"><span data-stu-id="b76e2-192">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="b76e2-193">CapptainReach 現在名為 EngagementReach</span><span class="sxs-lookup"><span data-stu-id="b76e2-193">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="b76e2-194">CapptainHttpConfig 現在名為 EngagementHttpConfig</span><span class="sxs-lookup"><span data-stu-id="b76e2-194">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="b76e2-195">GetCapptainPageName 現在名為 GetEngagementPageName</span><span class="sxs-lookup"><span data-stu-id="b76e2-195">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="b76e2-196">請注意，重新命名也會影響覆寫方法。</span><span class="sxs-lookup"><span data-stu-id="b76e2-196">Note that rename also affects overridden methods.</span></span>

