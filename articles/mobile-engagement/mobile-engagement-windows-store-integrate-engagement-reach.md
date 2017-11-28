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
# <a name="windows-universal-apps-reach-sdk-integration"></a><span data-ttu-id="f8b41-103">Windows 通用 app Reach SDK 整合</span><span class="sxs-lookup"><span data-stu-id="f8b41-103">Windows Universal Apps Reach SDK Integration</span></span>
<span data-ttu-id="f8b41-104">您必須遵循 hello 整合程序所述 hello [Windows 通用 Engagement SDK 整合](mobile-engagement-windows-store-integrate-engagement.md)之前依照本指南。</span><span class="sxs-lookup"><span data-stu-id="f8b41-104">You must follow hello integration procedure described in hello [Windows Universal Engagement SDK Integration](mobile-engagement-windows-store-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-universal-project"></a><span data-ttu-id="f8b41-105">內嵌至 Windows 通用專案中的 hello Engagement 觸達 SDK</span><span class="sxs-lookup"><span data-stu-id="f8b41-105">Embed hello Engagement Reach SDK into your Windows Universal project</span></span>
<span data-ttu-id="f8b41-106">您沒有任何項目 tooadd。</span><span class="sxs-lookup"><span data-stu-id="f8b41-106">You do not have anything tooadd.</span></span> <span data-ttu-id="f8b41-107">`EngagementReach` 的參考和資源已在您的專案中。</span><span class="sxs-lookup"><span data-stu-id="f8b41-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="f8b41-108">您可以自訂映像位於 hello`Resources`專案，特別是 hello 商標圖示 （該預設 toohello Engagement 圖示） 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="f8b41-108">You can customize images located in hello `Resources` folder of your project, especially hello brand icon (that default toohello Engagement icon).</span></span> <span data-ttu-id="f8b41-109">您也可以在通用應用程式上移動 hello`Resources`上其內容之間的應用程式，但您會有您共用的專案 tooshare 資料夾 tookeep hello`Resources\EngagementConfiguration.xml`檔案的預設位置，因為它是平台相依。</span><span class="sxs-lookup"><span data-stu-id="f8b41-109">On Universal Apps you can also move hello `Resources` folder on your shared project tooshare its content between apps, but you will have tookeep hello `Resources\EngagementConfiguration.xml` file on its default location as it is platform dependent.</span></span>
> 
> 

## <a name="enable-hello-windows-notification-service"></a><span data-ttu-id="f8b41-110">啟用 hello Windows 通知服務</span><span class="sxs-lookup"><span data-stu-id="f8b41-110">Enable hello Windows Notification Service</span></span>
### <a name="windows-8x-and-windows-phone-81-only"></a><span data-ttu-id="f8b41-111">僅 Windows 8.x 和 Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="f8b41-111">Windows 8.x and Windows Phone 8.1 only</span></span>
<span data-ttu-id="f8b41-112">在順序 toouse hello **Windows 通知服務**（稱為 WNS） 在您`Package.appxmanifest`上的檔案`Application UI`按一下`All Image Assets`hello bot 左邊的方塊中。</span><span class="sxs-lookup"><span data-stu-id="f8b41-112">In order toouse hello **Windows Notification Service** (referred as WNS) in your `Package.appxmanifest` file on `Application UI` click on `All Image Assets` in hello left bot box.</span></span> <span data-ttu-id="f8b41-113">在 [hello] 方塊中的 hello `Notifications`，變更`toast capable`從`(not set)`太`(Yes)`。</span><span class="sxs-lookup"><span data-stu-id="f8b41-113">At hello right of hello box in `Notifications`, change `toast capable` from `(not set)` too`(Yes)`.</span></span>

### <a name="all-platforms"></a><span data-ttu-id="f8b41-114">所有平台</span><span class="sxs-lookup"><span data-stu-id="f8b41-114">All platforms</span></span>
<span data-ttu-id="f8b41-115">您需要 toosynchronize 您應用程式 tooyour Microsoft 帳戶和 toohello engagement 平台。</span><span class="sxs-lookup"><span data-stu-id="f8b41-115">You need toosynchronize your app tooyour Microsoft account and toohello engagement platform.</span></span> <span data-ttu-id="f8b41-116">這需要 toocreate 帳戶或登入[windows 開發人員中心](https://dev.windows.com)。</span><span class="sxs-lookup"><span data-stu-id="f8b41-116">For this you need toocreate an account or log on [windows dev center](https://dev.windows.com).</span></span> <span data-ttu-id="f8b41-117">之後，建立新的應用程式，並尋找 hello SID 與秘密金鑰。</span><span class="sxs-lookup"><span data-stu-id="f8b41-117">After that create a new application and find hello SID and secret key.</span></span> <span data-ttu-id="f8b41-118">Hello engagement 前端上繼續您的應用程式設定中`native push`並貼上您的認證。</span><span class="sxs-lookup"><span data-stu-id="f8b41-118">On hello engagement frontend, go on your app setting in `native push` and paste your credentials.</span></span> <span data-ttu-id="f8b41-119">接下來，在您的專案上按一下滑鼠右鍵，依序選取 `store` 和 `Associate App with hello Store...`。</span><span class="sxs-lookup"><span data-stu-id="f8b41-119">After that, right click on your project, select `store` and `Associate App with hello Store...`.</span></span> <span data-ttu-id="f8b41-120">您只需要 tooselect hello 應用程式有建立 toosynchronize 之前。</span><span class="sxs-lookup"><span data-stu-id="f8b41-120">You just need tooselect hello application you have create before toosynchronize it.</span></span>

## <a name="initialize-hello-engagement-reach-sdk"></a><span data-ttu-id="f8b41-121">初始化 hello Engagement 觸達 SDK</span><span class="sxs-lookup"><span data-stu-id="f8b41-121">Initialize hello Engagement Reach SDK</span></span>
<span data-ttu-id="f8b41-122">修改 hello `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="f8b41-122">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="f8b41-123">在 `InitEngagement` 方法中，將 `EngagementReach.Instance.Init` 插入 `EngagementAgent.Instance.Init` 後方：</span><span class="sxs-lookup"><span data-stu-id="f8b41-123">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in your `InitEngagement` method:</span></span>
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
        EngagementReach.Instance.Init(e);
      }
  
  <span data-ttu-id="f8b41-124">hello`EngagementReach.Instance.Init`專用的執行緒中執行。</span><span class="sxs-lookup"><span data-stu-id="f8b41-124">hello `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="f8b41-125">您不需要 toodo 它自己。</span><span class="sxs-lookup"><span data-stu-id="f8b41-125">You do not have toodo it yourself.</span></span>

> [!NOTE]
> <span data-ttu-id="f8b41-126">如果您的應用程式中其他地方使用推播通知，則您也有[共用您的推播通道](#push-channel-sharing)與 Engagement 觸達。</span><span class="sxs-lookup"><span data-stu-id="f8b41-126">If you are using push notifications elsewhere in your application then you have too[share your push channel](#push-channel-sharing) with Engagement Reach.</span></span>
> 
> 

## <a name="integration"></a><span data-ttu-id="f8b41-127">整合</span><span class="sxs-lookup"><span data-stu-id="f8b41-127">Integration</span></span>
<span data-ttu-id="f8b41-128">Engagement 提供宣告與輪詢應用程式中的兩種方式 tooadd hello 觸達應用程式內橫幅和插入式檢視： hello 重疊整合以及 hello web 檢視手動整合。</span><span class="sxs-lookup"><span data-stu-id="f8b41-128">Engagement provides two ways tooadd hello Reach in-app banners and interstitial views for announcements and polls in your application: hello overlay integration and hello web views manual integration.</span></span> <span data-ttu-id="f8b41-129">您不應該結合這兩種方法在 hello 上的相同的頁面。</span><span class="sxs-lookup"><span data-stu-id="f8b41-129">You should not combine both approach on hello same page.</span></span>

<span data-ttu-id="f8b41-130">無法彙總之間 hello 兩個整合的 hello 選擇這種方式：</span><span class="sxs-lookup"><span data-stu-id="f8b41-130">hello choice between hello two integration could be summarized this way:</span></span>

* <span data-ttu-id="f8b41-131">如果您的網頁已繼承自 hello 代理程式，您可以選擇 hello 重疊整合`EngagementPage`，它是只需取代`EngagementPage`由`EngagementPageOverlay`和`xmlns:engagement="using:Microsoft.Azure.Engagement"`由`xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"`頁面中。</span><span class="sxs-lookup"><span data-stu-id="f8b41-131">You may choose hello overlay integration if your pages already inherits from hello Agent `EngagementPage`, it's just a matter of replacing `EngagementPage` by `EngagementPageOverlay` and `xmlns:engagement="using:Microsoft.Azure.Engagement"` by `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` in your pages.</span></span>
* <span data-ttu-id="f8b41-132">您可以選擇 hello web 檢視手動整合如果您想在網頁中的 tooprecisely 位置 hello 到達 UI，或如果您不想 tooadd 另一個繼承 tooyour 層級頁面。</span><span class="sxs-lookup"><span data-stu-id="f8b41-132">You may choose hello web views manual integration if you want tooprecisely place hello Reach UI within your pages or if you don't want tooadd another inheritance level tooyour pages.</span></span> 

### <a name="overlay-integration"></a><span data-ttu-id="f8b41-133">重疊整合</span><span class="sxs-lookup"><span data-stu-id="f8b41-133">Overlay integration</span></span>
<span data-ttu-id="f8b41-134">hello Engagement 重疊動態新增 hello UI 項目在網頁中使用 toodisplay 觸達活動。</span><span class="sxs-lookup"><span data-stu-id="f8b41-134">hello Engagement overlay dynamically adds hello UI elements used toodisplay Reach campaigns in your page.</span></span> <span data-ttu-id="f8b41-135">如果 hello 重疊不符合您配置您應該考慮 hello web 檢視手動整合改為。</span><span class="sxs-lookup"><span data-stu-id="f8b41-135">If hello overlay doesn't suit your layout you should consider hello web views manual integration instead.</span></span>

<span data-ttu-id="f8b41-136">在您的.xaml 檔案變更`EngagementPage`太參考`EngagementPageOverlay`</span><span class="sxs-lookup"><span data-stu-id="f8b41-136">In your .xaml file change `EngagementPage` reference too`EngagementPageOverlay`</span></span>

* <span data-ttu-id="f8b41-137">加入 tooyour 命名空間宣告：</span><span class="sxs-lookup"><span data-stu-id="f8b41-137">Add tooyour namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"
* <span data-ttu-id="f8b41-138">以 `engagement:EngagementPageOverlay` 取代 `engagement:EngagementPage`：</span><span class="sxs-lookup"><span data-stu-id="f8b41-138">Replace `engagement:EngagementPage` with `engagement:EngagementPageOverlay`:</span></span>

<span data-ttu-id="f8b41-139">**有 EngagementPage：**</span><span class="sxs-lookup"><span data-stu-id="f8b41-139">**With EngagementPage:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">

            <!-- Your layout -->
        </engagement:EngagementPage>

<span data-ttu-id="f8b41-140">**有 EngagementPageOverlay：**</span><span class="sxs-lookup"><span data-stu-id="f8b41-140">**With EngagementPageOverlay:**</span></span>

        <engagement:EngagementPageOverlay 
            xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay">

            <!-- Your layout -->
        </engagement:EngagementPageOverlay>

<span data-ttu-id="f8b41-141">然後在您的 .cs 檔案中以 `EngagementPageOverlay` 而不是 `EngagementPage` 標記頁面，並匯入 `Microsoft.Azure.Engagement.Overlay`。</span><span class="sxs-lookup"><span data-stu-id="f8b41-141">Then in your .cs file tag your page in `EngagementPageOverlay` instead of `EngagementPage` and import `Microsoft.Azure.Engagement.Overlay`.</span></span>

            using Microsoft.Azure.Engagement.Overlay;

* <span data-ttu-id="f8b41-142">以 `EngagementPageOverlay` 取代 `EngagementPage`：</span><span class="sxs-lookup"><span data-stu-id="f8b41-142">Replace `EngagementPage` with `EngagementPageOverlay`:</span></span>

<span data-ttu-id="f8b41-143">**有 EngagementPage：**</span><span class="sxs-lookup"><span data-stu-id="f8b41-143">**With EngagementPage:**</span></span>

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPage
              {
                [...]
              }
            }

<span data-ttu-id="f8b41-144">**有 EngagementPageOverlay：**</span><span class="sxs-lookup"><span data-stu-id="f8b41-144">**With EngagementPageOverlay:**</span></span>

            using Microsoft.Azure.Engagement.Overlay;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPageOverlay 
              {
                [...]
              }
            }


<span data-ttu-id="f8b41-145">hello Engagement 覆疊新增`Grid`在您的頁面頂端的項目組成的版面配置及 hello 兩`WebView`hello 的項目一個橫幅和 hello hello 插入檢視另一個。</span><span class="sxs-lookup"><span data-stu-id="f8b41-145">hello Engagement overlay adds a `Grid` element on top of your page composed of your layout and hello two `WebView` elements one for hello banner and hello other one for hello interstitial view.</span></span>

<span data-ttu-id="f8b41-146">您可以自訂 hello 重疊項目，直接在 hello`EngagementPageOverlay.cs`檔案。</span><span class="sxs-lookup"><span data-stu-id="f8b41-146">You can customize hello overlay elements directly in hello `EngagementPageOverlay.cs` file.</span></span>

### <a name="web-views-manual-integration"></a><span data-ttu-id="f8b41-147">Web 檢視手動整合</span><span class="sxs-lookup"><span data-stu-id="f8b41-147">Web views manual integration</span></span>
<span data-ttu-id="f8b41-148">觸達搜尋 hello 兩個頁面`WebView`負責顯示 hello 橫幅和 hello 插入式檢視的項目。</span><span class="sxs-lookup"><span data-stu-id="f8b41-148">Reach will be searching your pages for hello two `WebView` elements responsible for displaying hello banner and hello interstitial view.</span></span> <span data-ttu-id="f8b41-149">只有您唯一 toodo tooadd hello 這兩者`WebView`項目位置在頁面中，範例如下：</span><span class="sxs-lookup"><span data-stu-id="f8b41-149">hello only thing you have toodo is tooadd those two `WebView` elements somewhere in your pages, here is an example:</span></span>

    <Grid x:Name="engagementGrid">

      <!-- Your layout -->

      <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Stretch" VerticalAlignment="Top"/>
      <WebView x:Name="engagement_announcement_content" Visibility="Collapsed"  HorizontalAlignment="Stretch"  VerticalAlignment="Stretch"/>
    </Grid>


<span data-ttu-id="f8b41-150">在此範例 hello`WebView`項目會伸展的 toofit 其容器的自動重新調整大小它們螢幕旋轉或視窗大小變更時。</span><span class="sxs-lookup"><span data-stu-id="f8b41-150">In this example hello `WebView` elements are stretched toofit their container which automatically re-sizes them in case of screen rotation or window size change.</span></span>

> [!WARNING]
> <span data-ttu-id="f8b41-151">請務必 tookeep hello 相同命名`engagement_notification_content`和`engagement_announcement_content`hello`WebView`項目。</span><span class="sxs-lookup"><span data-stu-id="f8b41-151">It is important tookeep hello same naming `engagement_notification_content` and `engagement_announcement_content` for hello `WebView` elements.</span></span> <span data-ttu-id="f8b41-152">Reach 依其名稱來識別。</span><span class="sxs-lookup"><span data-stu-id="f8b41-152">Reach is identifying them by their name.</span></span> 
> 
> 

## <a name="handle-datapush-optional"></a><span data-ttu-id="f8b41-153">處理資料推送 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="f8b41-153">Handle datapush (optional)</span></span>
<span data-ttu-id="f8b41-154">如果您希望您的應用程式 toobe tooreceive 無法觸達資料推播通知時，您會有 tooimplement 的 hello EngagementReach 類別的兩個事件：</span><span class="sxs-lookup"><span data-stu-id="f8b41-154">If you want your application toobe able tooreceive Reach data pushes, you have tooimplement two events of hello EngagementReach class:</span></span>

<span data-ttu-id="f8b41-155">在 App.xaml.cs hello App() 建構函式中加入：</span><span class="sxs-lookup"><span data-stu-id="f8b41-155">In App.xaml.cs in hello App() constructor add:</span></span>

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

<span data-ttu-id="f8b41-156">您可以看到 hello 回撥的每個方法會傳回布林值。</span><span class="sxs-lookup"><span data-stu-id="f8b41-156">You can see that hello callback of each method returns a boolean.</span></span> <span data-ttu-id="f8b41-157">Engagement 傳送意見反應 tooits 後端之後分派 hello 資料推送。</span><span class="sxs-lookup"><span data-stu-id="f8b41-157">Engagement sends a feedback tooits back-end after dispatching hello data push.</span></span> <span data-ttu-id="f8b41-158">如果 hello 回呼傳回 false，hello`exit`意見反應會傳送。</span><span class="sxs-lookup"><span data-stu-id="f8b41-158">If hello callback returns false, hello `exit` feedback will be send.</span></span> <span data-ttu-id="f8b41-159">否則將會是 `action`。</span><span class="sxs-lookup"><span data-stu-id="f8b41-159">Otherwise, it will be `action`.</span></span> <span data-ttu-id="f8b41-160">如果沒有回呼 hello 事件設定，hello `drop` tooEngagement 將傳回的意見反應。</span><span class="sxs-lookup"><span data-stu-id="f8b41-160">If no callback is set for hello events, hello `drop` feedback will be returned tooEngagement.</span></span>

> [!WARNING]
> <span data-ttu-id="f8b41-161">Engagement 不能 tooreceive 倍數的意見反應資料推入。</span><span class="sxs-lookup"><span data-stu-id="f8b41-161">Engagement is not able tooreceive multiples feedbacks for a data push.</span></span> <span data-ttu-id="f8b41-162">如果您計劃 tooset 數個處理常式事件，請注意 hello 意見反應會對應 toohello 傳送的最後一個。</span><span class="sxs-lookup"><span data-stu-id="f8b41-162">If you plan tooset several handlers on an event, be aware that hello feedback will correspond toohello last one sent.</span></span> <span data-ttu-id="f8b41-163">在此情況下，我們建議 tooalways 傳回 hello 相同的值 tooavoid hello 前端上有令人混淆的意見反應。</span><span class="sxs-lookup"><span data-stu-id="f8b41-163">In this case, we recommend tooalways returns hello same value tooavoid having confusing feedback on hello front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="f8b41-164">自訂 UI (選擇性)</span><span class="sxs-lookup"><span data-stu-id="f8b41-164">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="f8b41-165">第一步</span><span class="sxs-lookup"><span data-stu-id="f8b41-165">First step</span></span>
<span data-ttu-id="f8b41-166">我們可讓您 toocustomize hello 觸達 UI。</span><span class="sxs-lookup"><span data-stu-id="f8b41-166">We allow you toocustomize hello reach UI.</span></span>

<span data-ttu-id="f8b41-167">toodo 因此，您有 toocreate hello 的子類別`EngagementReachHandler`類別。</span><span class="sxs-lookup"><span data-stu-id="f8b41-167">toodo so, you have toocreate a subclass of hello `EngagementReachHandler` class.</span></span>

<span data-ttu-id="f8b41-168">**範例程式碼：**</span><span class="sxs-lookup"><span data-stu-id="f8b41-168">**Sample Code :**</span></span>

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              internal class ExampleReachHandler : EngagementReachHandler
              {
               // Override EngagementReachHandler methods depending on your needs
              }
            }

<span data-ttu-id="f8b41-169">然後將設定的 hello hello 內容`EngagementReach.Instance.Handler`欄位中的自訂物件取代您`App.xaml.cs`內 hello 類別`App()`方法。</span><span class="sxs-lookup"><span data-stu-id="f8b41-169">Then, set hello content of hello `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within hello `App()` method.</span></span>

<span data-ttu-id="f8b41-170">**範例程式碼：**</span><span class="sxs-lookup"><span data-stu-id="f8b41-170">**Sample Code :**</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs args)
            {
              // your app initialization 
              EngagementReach.Instance.Handler = new ExampleReachHandler();
              // Engagement Agent and Reach initialization
            }

> [!NOTE]
> <span data-ttu-id="f8b41-171">根據預設，Engagement 會使用自己的 `EngagementReachHandler` 實作。</span><span class="sxs-lookup"><span data-stu-id="f8b41-171">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span>
> <span data-ttu-id="f8b41-172">您不需要 toocreate 您自己的而且這樣一來，如果您沒有 toooverride 每個方法。</span><span class="sxs-lookup"><span data-stu-id="f8b41-172">You don't have toocreate your own, and if you do so, you don't have toooverride every method.</span></span> <span data-ttu-id="f8b41-173">hello 預設行為是 tooselect hello Engagement 基底物件。</span><span class="sxs-lookup"><span data-stu-id="f8b41-173">hello default behavior is tooselect hello Engagement base object.</span></span>
> 
> 

### <a name="web-view"></a><span data-ttu-id="f8b41-174">Web 檢視</span><span class="sxs-lookup"><span data-stu-id="f8b41-174">Web View</span></span>
<span data-ttu-id="f8b41-175">根據預設，觸達會使用 hello DLL toodisplay hello 通知和網頁的 hello 內嵌的資源。</span><span class="sxs-lookup"><span data-stu-id="f8b41-175">By default, Reach will use hello embedded resources of hello DLL toodisplay hello notifications and pages.</span></span>

<span data-ttu-id="f8b41-176">tooprovide 完整自訂我們只會使用 web 檢視的項目。</span><span class="sxs-lookup"><span data-stu-id="f8b41-176">tooprovide a full customization possibilities we only use web view.</span></span> <span data-ttu-id="f8b41-177">如果您想 toocustomize 版面配置時，覆寫直接 hello 資源檔`EngagementAnnouncement.html`和`EngagementNotification.html`。</span><span class="sxs-lookup"><span data-stu-id="f8b41-177">If you want toocustomize layouts, override directly hello resources files `EngagementAnnouncement.html` and `EngagementNotification.html`.</span></span> <span data-ttu-id="f8b41-178">Engagement 需要所有的程式碼中`<body></body>`toorun 正確。</span><span class="sxs-lookup"><span data-stu-id="f8b41-178">Engagement needs all code in `<body></body>` toorun correctly.</span></span> <span data-ttu-id="f8b41-179">但您可以在 `engagement_webview_area`之外新增標記。</span><span class="sxs-lookup"><span data-stu-id="f8b41-179">But you can add tag outer `engagement_webview_area`.</span></span>

<span data-ttu-id="f8b41-180">不過，您可以決定 toouse 您自己的資源。</span><span class="sxs-lookup"><span data-stu-id="f8b41-180">However, you can decide toouse your own resources.</span></span>

<span data-ttu-id="f8b41-181">您可以覆寫`EngagementReachHandler`方法在您的子類別 tootell Engagement toouse 的配置，但會採用照護 tooembedded hello engagement 機制：</span><span class="sxs-lookup"><span data-stu-id="f8b41-181">You can override `EngagementReachHandler` methods in your subclass tootell Engagement toouse your layouts, but take care tooembedded hello engagement mechanism:</span></span>

<span data-ttu-id="f8b41-182">**範例程式碼：**</span><span class="sxs-lookup"><span data-stu-id="f8b41-182">**Sample Code :**</span></span>

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


<span data-ttu-id="f8b41-183">根據預設，AnnouncementHTML 是 `ms-appx-web:///Resources/EngagementAnnouncement.html`。</span><span class="sxs-lookup"><span data-stu-id="f8b41-183">By default, AnnouncementHTML is `ms-appx-web:///Resources/EngagementAnnouncement.html`.</span></span> <span data-ttu-id="f8b41-184">它代表 hello 設計 hello 訊息的內容推播 （文字公告、 Web anoucement 和輪詢通知） 的 html 檔案。</span><span class="sxs-lookup"><span data-stu-id="f8b41-184">It represents hello html file that design hello content of a push message (Text announcement, Web anoucement and Poll announcement).</span></span> <span data-ttu-id="f8b41-185">AnnouncementName 是 `engagement_announcement_content`。</span><span class="sxs-lookup"><span data-stu-id="f8b41-185">AnnouncementName is `engagement_announcement_content`.</span></span> <span data-ttu-id="f8b41-186">它是在 xaml 頁面中的 hello webview 設計 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="f8b41-186">It is hello name of hello webview design in your xaml page.</span></span>

<span data-ttu-id="f8b41-187">NotfificationHTML 是 `ms-appx-web:///Resources/EngagementNotification.html`。</span><span class="sxs-lookup"><span data-stu-id="f8b41-187">NotfificationHTML is `ms-appx-web:///Resources/EngagementNotification.html`.</span></span> <span data-ttu-id="f8b41-188">它代表 hello 設計 hello 通知推播訊息的 html 檔案。</span><span class="sxs-lookup"><span data-stu-id="f8b41-188">It represents hello html file that design hello notification of a push message.</span></span> <span data-ttu-id="f8b41-189">NotfificationName 是 `engagement_notification_content`。</span><span class="sxs-lookup"><span data-stu-id="f8b41-189">NotfificationName is `engagement_notification_content`.</span></span> <span data-ttu-id="f8b41-190">它是在 xaml 頁面中的 hello webview 設計 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="f8b41-190">It is hello name of hello webview design in your xaml page.</span></span>

### <a name="customization"></a><span data-ttu-id="f8b41-191">自訂</span><span class="sxs-lookup"><span data-stu-id="f8b41-191">Customization</span></span>
<span data-ttu-id="f8b41-192">如果您保留 Engagement 物件，便可以自訂通知和宣告的 Web 檢視。</span><span class="sxs-lookup"><span data-stu-id="f8b41-192">You can customize notification and announcement web view has you want if you preserve Engagement object.</span></span> <span data-ttu-id="f8b41-193">請小心 webview 物件會描述三次-hello 第一次在 xaml 中，第二個時間在 hello"setwebview()"方法中，您的.cs 檔案中與第三次 hello html 檔案中。</span><span class="sxs-lookup"><span data-stu-id="f8b41-193">Take care that webview object is described three times - hello first time in your xaml, second time in your .cs file in hello "setwebview()" method, and third time in hello html file.</span></span>

* <span data-ttu-id="f8b41-194">在 xaml 中，您會描述 hello 目前圖形配置 webview 元件。</span><span class="sxs-lookup"><span data-stu-id="f8b41-194">In your xaml you describe hello current graphical layout webview component.</span></span>
* <span data-ttu-id="f8b41-195">您可以在.cs 檔案定義"setwebview()"集中的兩個 hello webview （通知，通知） 的 hello 維度。</span><span class="sxs-lookup"><span data-stu-id="f8b41-195">In your .cs file you can define "setwebview()" in which you set hello dimension of hello two webview (notification, announcement).</span></span> <span data-ttu-id="f8b41-196">Hello 應用程式是調整大小時，它是非常有效。</span><span class="sxs-lookup"><span data-stu-id="f8b41-196">It is very effective when hello application is resizing.</span></span>
* <span data-ttu-id="f8b41-197">Hello Engagement html 檔案中，我們說明 hello webview 內容，設計並 hello 彼此之間的項目位置。</span><span class="sxs-lookup"><span data-stu-id="f8b41-197">In hello Engagement html file we describe hello webview content, design and hello elements positions between each other.</span></span>

### <a name="launch-message"></a><span data-ttu-id="f8b41-198">啟動訊息</span><span class="sxs-lookup"><span data-stu-id="f8b41-198">Launch message</span></span>
<span data-ttu-id="f8b41-199">當使用者按一下系統通知 （快顯） 時，Engagement 啟動 hello 應用程式、 hello 負載 hello 內容發送訊息，並顯示 hello 頁面 hello 對應的活動。</span><span class="sxs-lookup"><span data-stu-id="f8b41-199">When a user clicks on a system notification (a toast), Engagement launches hello application, load hello content of hello push messages, and display hello page for hello corresponding campaign.</span></span>

<span data-ttu-id="f8b41-200">Hello hello 頁面 （取決於網路 hello 速度） 的應用程式和 hello 顯示 hello 啟動會延遲。</span><span class="sxs-lookup"><span data-stu-id="f8b41-200">There is a delay between hello launch of hello application and hello display of hello page (depending on hello speed of your network).</span></span>

<span data-ttu-id="f8b41-201">項目正在載入的 tooindicate toohello 使用者，您應該提供視覺化的資訊，例如進度列或進度列指示器。</span><span class="sxs-lookup"><span data-stu-id="f8b41-201">tooindicate toohello user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="f8b41-202">Engagement 無法自行處理這些，但有提供您幾個處理常式。</span><span class="sxs-lookup"><span data-stu-id="f8b41-202">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="f8b41-203">tooimplement hello 回呼，在 「 公用 App() {}"App.xaml.cs 加入：</span><span class="sxs-lookup"><span data-stu-id="f8b41-203">tooimplement hello callback, in App.xaml.cs in "Public App(){}" add:</span></span>

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

<span data-ttu-id="f8b41-204">您可以在 「 公用 App() {}"的方法中設定 hello 回呼您`App.xaml.cs`檔案，最好是先 hello`EngagementReach.Instance.Init()`呼叫。</span><span class="sxs-lookup"><span data-stu-id="f8b41-204">You can set hello callback in your "Public App(){}" method of your `App.xaml.cs` file, preferably before hello `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="f8b41-205">每個處理常式會呼叫 hello UI 執行緒。</span><span class="sxs-lookup"><span data-stu-id="f8b41-205">Each handler is called by hello UI Thread.</span></span> <span data-ttu-id="f8b41-206">使用 MessageBox 或項目與 UI 相關時，您並沒有 tooworry。</span><span class="sxs-lookup"><span data-stu-id="f8b41-206">You do not have tooworry when using a MessageBox or something UI-related.</span></span>
> 
> 

## <span data-ttu-id="f8b41-207"><a id="push-channel-sharing"></a> 推播通道共用</span><span class="sxs-lookup"><span data-stu-id="f8b41-207"><a id="push-channel-sharing"></a> Push channel sharing</span></span>
<span data-ttu-id="f8b41-208">如果您應用程式中用於其他用途使用推播通知您有 toouse hello 推播通道共用 hello Engagement SDK 的功能。</span><span class="sxs-lookup"><span data-stu-id="f8b41-208">If you are using push notifications for another purpose in your application then you have toouse hello push channel sharing feature of hello Engagement SDK.</span></span> <span data-ttu-id="f8b41-209">這是遺漏 tooavoid 推入。</span><span class="sxs-lookup"><span data-stu-id="f8b41-209">This is tooavoid missed push.</span></span>

* <span data-ttu-id="f8b41-210">您可以提供您自己發送通道 toohello Engagement 觸達初始化。</span><span class="sxs-lookup"><span data-stu-id="f8b41-210">You can provide your own push channel toohello Engagement Reach initialization.</span></span> <span data-ttu-id="f8b41-211">hello SDK 會使用它而不是一個新的要求。</span><span class="sxs-lookup"><span data-stu-id="f8b41-211">hello SDK will use it instead of requesting a new one.</span></span>

<span data-ttu-id="f8b41-212">更新您的推播通道在 hello hello Engagement 觸達初始化`InitEngagement`方法從 hello`App.xaml.cs`檔案：</span><span class="sxs-lookup"><span data-stu-id="f8b41-212">Update hello Engagement Reach initialization with your push channel in hello `InitEngagement` method from hello `App.xaml.cs` file:</span></span>

    /* Your own push channel logic... */
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    /*...Engagement initialization */
    EngagementAgent.Instance.Init(e);
    EngagementReach.Instance.Init(e,pushChannel);

* <span data-ttu-id="f8b41-213">或者，如果您只想 tooconsume hello 推送通道 hello 觸達初始化之後則 hello SDK 建立之後，您可以在 Engagement 觸達 tooget hello 發送通道將回呼。</span><span class="sxs-lookup"><span data-stu-id="f8b41-213">Alternatively, if you just want tooconsume hello push channel after hello Reach initialization then you can set a callback on Engagement Reach tooget hello push channel once it is created by hello SDK.</span></span>

<span data-ttu-id="f8b41-214">在任何地方設定回呼**之後**hello 觸達初始化：</span><span class="sxs-lookup"><span data-stu-id="f8b41-214">Set your callback at any place **after** hello Reach initialization :</span></span>

    /* Set action on hello SDK push channel. */
    EngagementReach.Instance.SetActionOnPushChannel((PushNotificationChannel channel) => 
    {
      /* hello forwarded channel can be null if its creation fails for any reason. */
      if (channel != null)
      {
        /* Your own push channel logic... */
      });
    }

## <a name="custom-scheme-tip"></a><span data-ttu-id="f8b41-215">自訂配置秘訣</span><span class="sxs-lookup"><span data-stu-id="f8b41-215">Custom scheme tip</span></span>
<span data-ttu-id="f8b41-216">我們提供使用自訂配置。</span><span class="sxs-lookup"><span data-stu-id="f8b41-216">We provide custom scheme use.</span></span> <span data-ttu-id="f8b41-217">您可以從您的行動應用程式中使用 engagement 前端 toobe 傳送不同類型的 URI。</span><span class="sxs-lookup"><span data-stu-id="f8b41-217">You can send different type of URI from engagement frontend toobe used in your engagement application.</span></span> <span data-ttu-id="f8b41-218">如果裝置上沒有安裝預設的應用程式，預設配置 (例如，由 Windows 管理 `http, ftp, ...` ) 便會出現視窗提示。</span><span class="sxs-lookup"><span data-stu-id="f8b41-218">Default scheme like `http, ftp, ...` are manage by Windows, a window will prompt if they are no default application installed on device.</span></span> <span data-ttu-id="f8b41-219">您也可以在您的應用程式中使用自訂配置。</span><span class="sxs-lookup"><span data-stu-id="f8b41-219">You can also create your own custom scheme for your application.</span></span>

<span data-ttu-id="f8b41-220">hello 簡單的方式 tooset 自訂應用程式中的配置是 tooopen 您`Package.appxmanifest`中移`Declarations`面板。</span><span class="sxs-lookup"><span data-stu-id="f8b41-220">hello simple way tooset a custom scheme in your application is tooopen your `Package.appxmanifest` go in `Declarations` panel.</span></span> <span data-ttu-id="f8b41-221">選取`Protocol`在 hello 可用宣告捲動方塊，並將它加入。</span><span class="sxs-lookup"><span data-stu-id="f8b41-221">Select `Protocol` in hello Available Declarations scroll box and add it.</span></span> <span data-ttu-id="f8b41-222">編輯 hello`Name`欄位與新的通訊協定所需的名稱。</span><span class="sxs-lookup"><span data-stu-id="f8b41-222">Edit hello `Name` field with your new protocol desired name.</span></span>

<span data-ttu-id="f8b41-223">現在 toouse 此通訊協定，編輯您`App.xaml.cs`以 hello`OnActivated`方法，另外也不要忘記 tooinitialize engagement 這裡：</span><span class="sxs-lookup"><span data-stu-id="f8b41-223">Now toouse this protocol, edit your `App.xaml.cs` with hello `OnActivated` method, and don't forget tooinitialize engagement here also:</span></span>

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

