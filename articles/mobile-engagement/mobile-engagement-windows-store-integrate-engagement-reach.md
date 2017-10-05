---
title: "Windows 通用 app Reach SDK 整合"
description: "如何將 Azure Mobile Engagement Reach 與 Windows 通用 app 整合"
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
ms.openlocfilehash: 9311e998e67d8d0d56da68fc9460df32ce7ce5a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="windows-universal-apps-reach-sdk-integration"></a><span data-ttu-id="a06bc-103">Windows 通用 app Reach SDK 整合</span><span class="sxs-lookup"><span data-stu-id="a06bc-103">Windows Universal Apps Reach SDK Integration</span></span>
<span data-ttu-id="a06bc-104">依照本指南進行之前，您必須先遵循 [Windows 通用 Engagement SDK 整合](mobile-engagement-windows-store-integrate-engagement.md) 文件中所述的整合程序。</span><span class="sxs-lookup"><span data-stu-id="a06bc-104">You must follow the integration procedure described in the [Windows Universal Engagement SDK Integration](mobile-engagement-windows-store-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-the-engagement-reach-sdk-into-your-windows-universal-project"></a><span data-ttu-id="a06bc-105">將 Engagement Reach SDK 內嵌至您的 Windows 通用專案</span><span class="sxs-lookup"><span data-stu-id="a06bc-105">Embed the Engagement Reach SDK into your Windows Universal project</span></span>
<span data-ttu-id="a06bc-106">您不需要新增任何項目。</span><span class="sxs-lookup"><span data-stu-id="a06bc-106">You do not have anything to add.</span></span> <span data-ttu-id="a06bc-107">`EngagementReach` 的參考和資源已在您的專案中。</span><span class="sxs-lookup"><span data-stu-id="a06bc-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="a06bc-108">您可以自定專案的 `Resources` 資料夾中的影像，尤其是品牌圖示 (預設為 Engagement 的圖示)。</span><span class="sxs-lookup"><span data-stu-id="a06bc-108">You can customize images located in the `Resources` folder of your project, especially the brand icon (that default to the Engagement icon).</span></span> <span data-ttu-id="a06bc-109">在跨平台 app 上，您也可以移動共用專案上的 `Resources` 資料夾，以便在應用程式間共用其內容；但因為 `Resources\EngagementConfiguration.xml` 檔案和平台相依，所以您必須將它保留在預設位置。</span><span class="sxs-lookup"><span data-stu-id="a06bc-109">On Universal Apps you can also move the `Resources` folder on your shared project to share its content between apps, but you will have to keep the `Resources\EngagementConfiguration.xml` file on its default location as it is platform dependent.</span></span>
> 
> 

## <a name="enable-the-windows-notification-service"></a><span data-ttu-id="a06bc-110">啟用 Windows 通知服務</span><span class="sxs-lookup"><span data-stu-id="a06bc-110">Enable the Windows Notification Service</span></span>
### <a name="windows-8x-and-windows-phone-81-only"></a><span data-ttu-id="a06bc-111">僅 Windows 8.x 和 Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="a06bc-111">Windows 8.x and Windows Phone 8.1 only</span></span>
<span data-ttu-id="a06bc-112">若要在`Application UI` 上的 `Package.appxmanifest` 檔案中使用 **Windows 通知服務** (簡稱 WNS)，請在左邊 bot 方塊中的 `All Image Assets` 上按一下。</span><span class="sxs-lookup"><span data-stu-id="a06bc-112">In order to use the **Windows Notification Service** (referred as WNS) in your `Package.appxmanifest` file on `Application UI` click on `All Image Assets` in the left bot box.</span></span> <span data-ttu-id="a06bc-113">請在 `Notifications` 中方塊的右邊，將 `toast capable` 從 `(not set)` 變更為 `(Yes)`。</span><span class="sxs-lookup"><span data-stu-id="a06bc-113">At the right of the box in `Notifications`, change `toast capable` from `(not set)` to `(Yes)`.</span></span>

### <a name="all-platforms"></a><span data-ttu-id="a06bc-114">所有平台</span><span class="sxs-lookup"><span data-stu-id="a06bc-114">All platforms</span></span>
<span data-ttu-id="a06bc-115">您必須將您的應用程式與您的 Microsoft 帳戶以及 Engagement 平台同步。</span><span class="sxs-lookup"><span data-stu-id="a06bc-115">You need to synchronize your app to your Microsoft account and to the engagement platform.</span></span> <span data-ttu-id="a06bc-116">因此您需要建立一個帳戶或登入 [Windows 開發人員中心](https://dev.windows.com)。</span><span class="sxs-lookup"><span data-stu-id="a06bc-116">For this you need to create an account or log on [windows dev center](https://dev.windows.com).</span></span> <span data-ttu-id="a06bc-117">然後，建立新的應用程式，並且尋找 SID 和秘密金鑰。</span><span class="sxs-lookup"><span data-stu-id="a06bc-117">After that create a new application and find the SID and secret key.</span></span> <span data-ttu-id="a06bc-118">在 Engagement 前端中，繼續應用程式的 `native push` 設定，並貼上您的認證。</span><span class="sxs-lookup"><span data-stu-id="a06bc-118">On the engagement frontend, go on your app setting in `native push` and paste your credentials.</span></span> <span data-ttu-id="a06bc-119">接下來，在您的專案上按一下滑鼠右鍵，依序選取 `store` 和 `Associate App with the Store...`。</span><span class="sxs-lookup"><span data-stu-id="a06bc-119">After that, right click on your project, select `store` and `Associate App with the Store...`.</span></span> <span data-ttu-id="a06bc-120">您只需要在同步處理之前選取您建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="a06bc-120">You just need to select the application you have create before to synchronize it.</span></span>

## <a name="initialize-the-engagement-reach-sdk"></a><span data-ttu-id="a06bc-121">初始化 Engagement Reach SDK</span><span class="sxs-lookup"><span data-stu-id="a06bc-121">Initialize the Engagement Reach SDK</span></span>
<span data-ttu-id="a06bc-122">修改 `App.xaml.cs`：</span><span class="sxs-lookup"><span data-stu-id="a06bc-122">Modify the `App.xaml.cs`:</span></span>

* <span data-ttu-id="a06bc-123">在 `InitEngagement` 方法中，將 `EngagementReach.Instance.Init` 插入 `EngagementAgent.Instance.Init` 後方：</span><span class="sxs-lookup"><span data-stu-id="a06bc-123">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in your `InitEngagement` method:</span></span>
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
        EngagementReach.Instance.Init(e);
      }
  
  <span data-ttu-id="a06bc-124">`EngagementReach.Instance.Init` 會在專用的執行緒中執行。</span><span class="sxs-lookup"><span data-stu-id="a06bc-124">The `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="a06bc-125">您不必自行進行此作業。</span><span class="sxs-lookup"><span data-stu-id="a06bc-125">You do not have to do it yourself.</span></span>

> [!NOTE]
> <span data-ttu-id="a06bc-126">如果您在應用程式的其他地方使用推播通知，則您必須與 Engagement Reach [共用推播通道](#push-channel-sharing) 。</span><span class="sxs-lookup"><span data-stu-id="a06bc-126">If you are using push notifications elsewhere in your application then you have to [share your push channel](#push-channel-sharing) with Engagement Reach.</span></span>
> 
> 

## <a name="integration"></a><span data-ttu-id="a06bc-127">整合</span><span class="sxs-lookup"><span data-stu-id="a06bc-127">Integration</span></span>
<span data-ttu-id="a06bc-128">Engagement 提供兩種方式在應用程式中加入 Reach 應用程式內橫幅，以及宣告和輪詢的插入式檢視：重疊整合和 Web 檢視手動整合。</span><span class="sxs-lookup"><span data-stu-id="a06bc-128">Engagement provides two ways to add the Reach in-app banners and interstitial views for announcements and polls in your application: the overlay integration and the web views manual integration.</span></span> <span data-ttu-id="a06bc-129">您不應該在相同頁面上結合這兩種方法。</span><span class="sxs-lookup"><span data-stu-id="a06bc-129">You should not combine both approach on the same page.</span></span>

<span data-ttu-id="a06bc-130">兩種整合之間的選擇可以如此歸納︰</span><span class="sxs-lookup"><span data-stu-id="a06bc-130">The choice between the two integration could be summarized this way:</span></span>

* <span data-ttu-id="a06bc-131">如果您的頁面已繼承自代理程式 `EngagementPage`，您可以選擇重疊整合，只需在頁面中將 `EngagementPage` 取代為 `EngagementPageOverlay`，將 `xmlns:engagement="using:Microsoft.Azure.Engagement"` 取代為 `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"`。</span><span class="sxs-lookup"><span data-stu-id="a06bc-131">You may choose the overlay integration if your pages already inherits from the Agent `EngagementPage`, it's just a matter of replacing `EngagementPage` by `EngagementPageOverlay` and `xmlns:engagement="using:Microsoft.Azure.Engagement"` by `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` in your pages.</span></span>
* <span data-ttu-id="a06bc-132">如果您想要精確地將 Reach UI 放在頁面中，或是不想在頁面加入另一個繼承層級，可以選擇 Web 檢視手動整合。</span><span class="sxs-lookup"><span data-stu-id="a06bc-132">You may choose the web views manual integration if you want to precisely place the Reach UI within your pages or if you don't want to add another inheritance level to your pages.</span></span> 

### <a name="overlay-integration"></a><span data-ttu-id="a06bc-133">重疊整合</span><span class="sxs-lookup"><span data-stu-id="a06bc-133">Overlay integration</span></span>
<span data-ttu-id="a06bc-134">Engagement 重疊會以動態方式加入用以在頁面中顯示觸達活動的 UI 元素。</span><span class="sxs-lookup"><span data-stu-id="a06bc-134">The Engagement overlay dynamically adds the UI elements used to display Reach campaigns in your page.</span></span> <span data-ttu-id="a06bc-135">如果重疊不符合您的版面配置，您應該改為考慮 Web 檢視手動整合。</span><span class="sxs-lookup"><span data-stu-id="a06bc-135">If the overlay doesn't suit your layout you should consider the web views manual integration instead.</span></span>

<span data-ttu-id="a06bc-136">在您的 .xaml 檔案中，將 `EngagementPage` 參考變更為 `EngagementPageOverlay`</span><span class="sxs-lookup"><span data-stu-id="a06bc-136">In your .xaml file change `EngagementPage` reference to `EngagementPageOverlay`</span></span>

* <span data-ttu-id="a06bc-137">新增至命名空間宣告：</span><span class="sxs-lookup"><span data-stu-id="a06bc-137">Add to your namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"
* <span data-ttu-id="a06bc-138">以 `engagement:EngagementPageOverlay` 取代 `engagement:EngagementPage`：</span><span class="sxs-lookup"><span data-stu-id="a06bc-138">Replace `engagement:EngagementPage` with `engagement:EngagementPageOverlay`:</span></span>

<span data-ttu-id="a06bc-139">**有 EngagementPage：**</span><span class="sxs-lookup"><span data-stu-id="a06bc-139">**With EngagementPage:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">

            <!-- Your layout -->
        </engagement:EngagementPage>

<span data-ttu-id="a06bc-140">**有 EngagementPageOverlay：**</span><span class="sxs-lookup"><span data-stu-id="a06bc-140">**With EngagementPageOverlay:**</span></span>

        <engagement:EngagementPageOverlay 
            xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay">

            <!-- Your layout -->
        </engagement:EngagementPageOverlay>

<span data-ttu-id="a06bc-141">然後在您的 .cs 檔案中以 `EngagementPageOverlay` 而不是 `EngagementPage` 標記頁面，並匯入 `Microsoft.Azure.Engagement.Overlay`。</span><span class="sxs-lookup"><span data-stu-id="a06bc-141">Then in your .cs file tag your page in `EngagementPageOverlay` instead of `EngagementPage` and import `Microsoft.Azure.Engagement.Overlay`.</span></span>

            using Microsoft.Azure.Engagement.Overlay;

* <span data-ttu-id="a06bc-142">以 `EngagementPageOverlay` 取代 `EngagementPage`：</span><span class="sxs-lookup"><span data-stu-id="a06bc-142">Replace `EngagementPage` with `EngagementPageOverlay`:</span></span>

<span data-ttu-id="a06bc-143">**有 EngagementPage：**</span><span class="sxs-lookup"><span data-stu-id="a06bc-143">**With EngagementPage:**</span></span>

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPage
              {
                [...]
              }
            }

<span data-ttu-id="a06bc-144">**有 EngagementPageOverlay：**</span><span class="sxs-lookup"><span data-stu-id="a06bc-144">**With EngagementPageOverlay:**</span></span>

            using Microsoft.Azure.Engagement.Overlay;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPageOverlay 
              {
                [...]
              }
            }


<span data-ttu-id="a06bc-145">Engagement 重疊會在版面配置組成的頁面頂端加入 `Grid` 元素和兩個 `WebView` 元素，一個用於橫幅，另一個則用於插入式檢視。</span><span class="sxs-lookup"><span data-stu-id="a06bc-145">The Engagement overlay adds a `Grid` element on top of your page composed of your layout and the two `WebView` elements one for the banner and the other one for the interstitial view.</span></span>

<span data-ttu-id="a06bc-146">您可以直接在 `EngagementPageOverlay.cs` 檔案中自訂重疊元素。</span><span class="sxs-lookup"><span data-stu-id="a06bc-146">You can customize the overlay elements directly in the `EngagementPageOverlay.cs` file.</span></span>

### <a name="web-views-manual-integration"></a><span data-ttu-id="a06bc-147">Web 檢視手動整合</span><span class="sxs-lookup"><span data-stu-id="a06bc-147">Web views manual integration</span></span>
<span data-ttu-id="a06bc-148">Reach 會搜尋頁面中負責顯示橫幅和插入式檢視的兩個 `WebView` 元素。</span><span class="sxs-lookup"><span data-stu-id="a06bc-148">Reach will be searching your pages for the two `WebView` elements responsible for displaying the banner and the interstitial view.</span></span> <span data-ttu-id="a06bc-149">您唯一要做的是將這兩個 `WebView` 元素加入頁面中的某處，範例如下︰</span><span class="sxs-lookup"><span data-stu-id="a06bc-149">The only thing you have to do is to add those two `WebView` elements somewhere in your pages, here is an example:</span></span>

    <Grid x:Name="engagementGrid">

      <!-- Your layout -->

      <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Stretch" VerticalAlignment="Top"/>
      <WebView x:Name="engagement_announcement_content" Visibility="Collapsed"  HorizontalAlignment="Stretch"  VerticalAlignment="Stretch"/>
    </Grid>


<span data-ttu-id="a06bc-150">在此範例中， `WebView` 元素會伸展以符合其容器，容器會在螢幕旋轉或視窗大小變更時自動重新調整大小。</span><span class="sxs-lookup"><span data-stu-id="a06bc-150">In this example the `WebView` elements are stretched to fit their container which automatically re-sizes them in case of screen rotation or window size change.</span></span>

> [!WARNING]
> <span data-ttu-id="a06bc-151">請務必為 `WebView` 元素的 `engagement_notification_content` 和 `engagement_announcement_content` 保留相同的命名。</span><span class="sxs-lookup"><span data-stu-id="a06bc-151">It is important to keep the same naming `engagement_notification_content` and `engagement_announcement_content` for the `WebView` elements.</span></span> <span data-ttu-id="a06bc-152">Reach 依其名稱來識別。</span><span class="sxs-lookup"><span data-stu-id="a06bc-152">Reach is identifying them by their name.</span></span> 
> 
> 

## <a name="handle-datapush-optional"></a><span data-ttu-id="a06bc-153">處理資料推送 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="a06bc-153">Handle datapush (optional)</span></span>
<span data-ttu-id="a06bc-154">如果您希望您的應用程式接收 Reach 資料推送，您必須實作 EngagementReach 類別的兩個事件：</span><span class="sxs-lookup"><span data-stu-id="a06bc-154">If you want your application to be able to receive Reach data pushes, you have to implement two events of the EngagementReach class:</span></span>

<span data-ttu-id="a06bc-155">在 App.xaml.cs 的 App() 建構函式中加入︰</span><span class="sxs-lookup"><span data-stu-id="a06bc-155">In App.xaml.cs in the App() constructor add:</span></span>

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

<span data-ttu-id="a06bc-156">您可以看到每個方法的回呼會傳回布林值。</span><span class="sxs-lookup"><span data-stu-id="a06bc-156">You can see that the callback of each method returns a boolean.</span></span> <span data-ttu-id="a06bc-157">Engagement 會在發送資料推送之後傳送回饋到它的後端。</span><span class="sxs-lookup"><span data-stu-id="a06bc-157">Engagement sends a feedback to its back-end after dispatching the data push.</span></span> <span data-ttu-id="a06bc-158">如果回呼傳回 false，會傳送 `exit` 回饋。</span><span class="sxs-lookup"><span data-stu-id="a06bc-158">If the callback returns false, the `exit` feedback will be send.</span></span> <span data-ttu-id="a06bc-159">否則將會是 `action`。</span><span class="sxs-lookup"><span data-stu-id="a06bc-159">Otherwise, it will be `action`.</span></span> <span data-ttu-id="a06bc-160">如果沒有設定事件的回呼，就會傳送 `drop` 回饋到 Engagement。</span><span class="sxs-lookup"><span data-stu-id="a06bc-160">If no callback is set for the events, the `drop` feedback will be returned to Engagement.</span></span>

> [!WARNING]
> <span data-ttu-id="a06bc-161">Engagement 無法接收單一資料推送的多個回饋。</span><span class="sxs-lookup"><span data-stu-id="a06bc-161">Engagement is not able to receive multiples feedbacks for a data push.</span></span> <span data-ttu-id="a06bc-162">如果計畫在單一事件上設定多個處理常式，請留意回饋將與最後一個傳送的對應。</span><span class="sxs-lookup"><span data-stu-id="a06bc-162">If you plan to set several handlers on an event, be aware that the feedback will correspond to the last one sent.</span></span> <span data-ttu-id="a06bc-163">在此情況下，我們建議一律傳回相同的值，避免在前端有令人困惑的回饋。</span><span class="sxs-lookup"><span data-stu-id="a06bc-163">In this case, we recommend to always returns the same value to avoid having confusing feedback on the front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="a06bc-164">自訂 UI (選擇性)</span><span class="sxs-lookup"><span data-stu-id="a06bc-164">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="a06bc-165">第一步</span><span class="sxs-lookup"><span data-stu-id="a06bc-165">First step</span></span>
<span data-ttu-id="a06bc-166">我們讓您可以自訂 Reach UI。</span><span class="sxs-lookup"><span data-stu-id="a06bc-166">We allow you to customize the reach UI.</span></span>

<span data-ttu-id="a06bc-167">若要這樣做，您必須建立 `EngagementReachHandler` 類別的子類別。</span><span class="sxs-lookup"><span data-stu-id="a06bc-167">To do so, you have to create a subclass of the `EngagementReachHandler` class.</span></span>

<span data-ttu-id="a06bc-168">**範例程式碼：**</span><span class="sxs-lookup"><span data-stu-id="a06bc-168">**Sample Code :**</span></span>

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              internal class ExampleReachHandler : EngagementReachHandler
              {
               // Override EngagementReachHandler methods depending on your needs
              }
            }

<span data-ttu-id="a06bc-169">然後，使用 `App()` 方法中 `App.xaml.cs` 類別的自訂物件，設定 `EngagementReach.Instance.Handler` 欄位的內容。</span><span class="sxs-lookup"><span data-stu-id="a06bc-169">Then, set the content of the `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within the `App()` method.</span></span>

<span data-ttu-id="a06bc-170">**範例程式碼：**</span><span class="sxs-lookup"><span data-stu-id="a06bc-170">**Sample Code :**</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs args)
            {
              // your app initialization 
              EngagementReach.Instance.Handler = new ExampleReachHandler();
              // Engagement Agent and Reach initialization
            }

> [!NOTE]
> <span data-ttu-id="a06bc-171">根據預設，Engagement 會使用自己的 `EngagementReachHandler` 實作。</span><span class="sxs-lookup"><span data-stu-id="a06bc-171">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span>
> <span data-ttu-id="a06bc-172">您不需要自己建立，但如果有需要，您不需要覆寫每個方法。</span><span class="sxs-lookup"><span data-stu-id="a06bc-172">You don't have to create your own, and if you do so, you don't have to override every method.</span></span> <span data-ttu-id="a06bc-173">預設行為是選取 Engagement 基底物件。</span><span class="sxs-lookup"><span data-stu-id="a06bc-173">The default behavior is to select the Engagement base object.</span></span>
> 
> 

### <a name="web-view"></a><span data-ttu-id="a06bc-174">Web 檢視</span><span class="sxs-lookup"><span data-stu-id="a06bc-174">Web View</span></span>
<span data-ttu-id="a06bc-175">根據預設，Reach 會使用 DLL 的內嵌資源來顯示通知和頁面。</span><span class="sxs-lookup"><span data-stu-id="a06bc-175">By default, Reach will use the embedded resources of the DLL to display the notifications and pages.</span></span>

<span data-ttu-id="a06bc-176">若要提供完全自訂的可能性，我們只會使用網頁檢視。</span><span class="sxs-lookup"><span data-stu-id="a06bc-176">To provide a full customization possibilities we only use web view.</span></span> <span data-ttu-id="a06bc-177">如果您想要自訂版面配置，請直接覆寫資源檔案 `EngagementAnnouncement.html` 和 `EngagementNotification.html`。</span><span class="sxs-lookup"><span data-stu-id="a06bc-177">If you want to customize layouts, override directly the resources files `EngagementAnnouncement.html` and `EngagementNotification.html`.</span></span> <span data-ttu-id="a06bc-178">Engagement 需要 `<body></body>` 內的所有程式碼正確執行。</span><span class="sxs-lookup"><span data-stu-id="a06bc-178">Engagement needs all code in `<body></body>` to run correctly.</span></span> <span data-ttu-id="a06bc-179">但您可以在 `engagement_webview_area`之外新增標記。</span><span class="sxs-lookup"><span data-stu-id="a06bc-179">But you can add tag outer `engagement_webview_area`.</span></span>

<span data-ttu-id="a06bc-180">不過，您可以決定使用自己的資源。</span><span class="sxs-lookup"><span data-stu-id="a06bc-180">However, you can decide to use your own resources.</span></span>

<span data-ttu-id="a06bc-181">您可以在您的子類別中覆寫 `EngagementReachHandler` 方法，以告訴 Engagement 要使用您的版面配置，但是請小心內嵌的 Engagement 機制：</span><span class="sxs-lookup"><span data-stu-id="a06bc-181">You can override `EngagementReachHandler` methods in your subclass to tell Engagement to use your layouts, but take care to embedded the engagement mechanism:</span></span>

<span data-ttu-id="a06bc-182">**範例程式碼：**</span><span class="sxs-lookup"><span data-stu-id="a06bc-182">**Sample Code :**</span></span>

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


<span data-ttu-id="a06bc-183">根據預設，AnnouncementHTML 是 `ms-appx-web:///Resources/EngagementAnnouncement.html`。</span><span class="sxs-lookup"><span data-stu-id="a06bc-183">By default, AnnouncementHTML is `ms-appx-web:///Resources/EngagementAnnouncement.html`.</span></span> <span data-ttu-id="a06bc-184">它代表設計推播訊息之內容的 html 檔案 (文字宣告、Web 宣告和投票宣告)。</span><span class="sxs-lookup"><span data-stu-id="a06bc-184">It represents the html file that design the content of a push message (Text announcement, Web anoucement and Poll announcement).</span></span> <span data-ttu-id="a06bc-185">AnnouncementName 是 `engagement_announcement_content`。</span><span class="sxs-lookup"><span data-stu-id="a06bc-185">AnnouncementName is `engagement_announcement_content`.</span></span> <span data-ttu-id="a06bc-186">它是您 xaml 頁面中 Web 檢視設計的名稱。</span><span class="sxs-lookup"><span data-stu-id="a06bc-186">It is the name of the webview design in your xaml page.</span></span>

<span data-ttu-id="a06bc-187">NotfificationHTML 是 `ms-appx-web:///Resources/EngagementNotification.html`。</span><span class="sxs-lookup"><span data-stu-id="a06bc-187">NotfificationHTML is `ms-appx-web:///Resources/EngagementNotification.html`.</span></span> <span data-ttu-id="a06bc-188">它代表設計推播訊息通知的 html 檔案。</span><span class="sxs-lookup"><span data-stu-id="a06bc-188">It represents the html file that design the notification of a push message.</span></span> <span data-ttu-id="a06bc-189">NotfificationName 是 `engagement_notification_content`。</span><span class="sxs-lookup"><span data-stu-id="a06bc-189">NotfificationName is `engagement_notification_content`.</span></span> <span data-ttu-id="a06bc-190">它是您 xaml 頁面中 Web 檢視設計的名稱。</span><span class="sxs-lookup"><span data-stu-id="a06bc-190">It is the name of the webview design in your xaml page.</span></span>

### <a name="customization"></a><span data-ttu-id="a06bc-191">自訂</span><span class="sxs-lookup"><span data-stu-id="a06bc-191">Customization</span></span>
<span data-ttu-id="a06bc-192">如果您保留 Engagement 物件，便可以自訂通知和宣告的 Web 檢視。</span><span class="sxs-lookup"><span data-stu-id="a06bc-192">You can customize notification and announcement web view has you want if you preserve Engagement object.</span></span> <span data-ttu-id="a06bc-193">請注意，Web 檢視會說明三次 (第一次在 xaml 中、第二次在 "setwebview()" 內的 .cs 檔案中，而第三次則在 html 檔案中)。</span><span class="sxs-lookup"><span data-stu-id="a06bc-193">Take care that webview object is described three times - the first time in your xaml, second time in your .cs file in the "setwebview()" method, and third time in the html file.</span></span>

* <span data-ttu-id="a06bc-194">在 xaml 中是描述目前的圖形版面配置 Web 檢視元件。</span><span class="sxs-lookup"><span data-stu-id="a06bc-194">In your xaml you describe the current graphical layout webview component.</span></span>
* <span data-ttu-id="a06bc-195">您可以在 .cs 檔案中定義設定兩種 Web 檢視 (通知、宣告) 的維度之 "setwebview()"。</span><span class="sxs-lookup"><span data-stu-id="a06bc-195">In your .cs file you can define "setwebview()" in which you set the dimension of the two webview (notification, announcement).</span></span> <span data-ttu-id="a06bc-196">這在應用程式調整大小時非常有效。</span><span class="sxs-lookup"><span data-stu-id="a06bc-196">It is very effective when the application is resizing.</span></span>
* <span data-ttu-id="a06bc-197">我們在 Engagement html 檔案中描述 Web 檢視的內容、設計，以及各元素之間的位置。</span><span class="sxs-lookup"><span data-stu-id="a06bc-197">In the Engagement html file we describe the webview content, design and the elements positions between each other.</span></span>

### <a name="launch-message"></a><span data-ttu-id="a06bc-198">啟動訊息</span><span class="sxs-lookup"><span data-stu-id="a06bc-198">Launch message</span></span>
<span data-ttu-id="a06bc-199">當使用者按一下系統通知 (快顯通知) 時，Engagement 會啟動該應用程式、載入推播訊息的內容，並顯示對應之活動的頁面。</span><span class="sxs-lookup"><span data-stu-id="a06bc-199">When a user clicks on a system notification (a toast), Engagement launches the application, load the content of the push messages, and display the page for the corresponding campaign.</span></span>

<span data-ttu-id="a06bc-200">啟動應用程式與頁面顯示之間會有延遲 (取決於您的網路速度)。</span><span class="sxs-lookup"><span data-stu-id="a06bc-200">There is a delay between the launch of the application and the display of the page (depending on the speed of your network).</span></span>

<span data-ttu-id="a06bc-201">若要向使用者指示正在載入項目，您應該提供視覺化的資訊，例如進度列或進度列指示器。</span><span class="sxs-lookup"><span data-stu-id="a06bc-201">To indicate to the user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="a06bc-202">Engagement 無法自行處理這些，但有提供您幾個處理常式。</span><span class="sxs-lookup"><span data-stu-id="a06bc-202">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="a06bc-203">若要實作回呼，在 App.xaml.cs 中的 "Public app {}" 新增：</span><span class="sxs-lookup"><span data-stu-id="a06bc-203">To implement the callback, in App.xaml.cs in "Public App(){}" add:</span></span>

            /* The application has launched and the content is loading.
             * You should display an indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageStarted += () => { [...] };

            /* The application has finished loading the content and the page
             * is about to be displayed.
             * You should hide the indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageCompleted += () => { [...] };

            /* The content has been loaded, but an error has occurred.
             * You can provide an information to the user.
             * You should hide the indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageFailed += () => { [...] };

<span data-ttu-id="a06bc-204">您可以在 `App.xaml.cs` 檔案的 "Public App(){}" 方法中設定回呼，最好設定在 `EngagementReach.Instance.Init()` 呼叫之前。</span><span class="sxs-lookup"><span data-stu-id="a06bc-204">You can set the callback in your "Public App(){}" method of your `App.xaml.cs` file, preferably before the `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="a06bc-205">每個處理常式都是由 UI 執行緒呼叫。</span><span class="sxs-lookup"><span data-stu-id="a06bc-205">Each handler is called by the UI Thread.</span></span> <span data-ttu-id="a06bc-206">在使用 MessageBox 或 UI 相關的項目時您不必擔心。</span><span class="sxs-lookup"><span data-stu-id="a06bc-206">You do not have to worry when using a MessageBox or something UI-related.</span></span>
> 
> 

## <span data-ttu-id="a06bc-207"><a id="push-channel-sharing"></a> 推播通道共用</span><span class="sxs-lookup"><span data-stu-id="a06bc-207"><a id="push-channel-sharing"></a> Push channel sharing</span></span>
<span data-ttu-id="a06bc-208">如果您在應用程式中將推播通知用於其他目的，則您必須使用 Engagement SDK 的推播通道共用功能。</span><span class="sxs-lookup"><span data-stu-id="a06bc-208">If you are using push notifications for another purpose in your application then you have to use the push channel sharing feature of the Engagement SDK.</span></span> <span data-ttu-id="a06bc-209">這是為了避免遺失推播。</span><span class="sxs-lookup"><span data-stu-id="a06bc-209">This is to avoid missed push.</span></span>

* <span data-ttu-id="a06bc-210">您可以對 Engagement Reach 初始化提供自己的推播通道。</span><span class="sxs-lookup"><span data-stu-id="a06bc-210">You can provide your own push channel to the Engagement Reach initialization.</span></span> <span data-ttu-id="a06bc-211">SDK 將會使用它而不是要求新的。</span><span class="sxs-lookup"><span data-stu-id="a06bc-211">The SDK will use it instead of requesting a new one.</span></span>

<span data-ttu-id="a06bc-212">使用您在 `App.xaml.cs` 檔案之 `InitEngagement` 方法中的推播通道更新 Engagement Reach 初始化：</span><span class="sxs-lookup"><span data-stu-id="a06bc-212">Update the Engagement Reach initialization with your push channel in the `InitEngagement` method from the `App.xaml.cs` file:</span></span>

    /* Your own push channel logic... */
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    /*...Engagement initialization */
    EngagementAgent.Instance.Init(e);
    EngagementReach.Instance.Init(e,pushChannel);

* <span data-ttu-id="a06bc-213">或者，如果您只是想在 Reach 初始化之後使用推播通道，那麼您可以在 Engagement Reach 上設定回呼，以在 SDK 建立推播通到之後立即取得它。</span><span class="sxs-lookup"><span data-stu-id="a06bc-213">Alternatively, if you just want to consume the push channel after the Reach initialization then you can set a callback on Engagement Reach to get the push channel once it is created by the SDK.</span></span>

<span data-ttu-id="a06bc-214">在 Reach 初始化「之後」  的任何地方設定回呼：</span><span class="sxs-lookup"><span data-stu-id="a06bc-214">Set your callback at any place **after** the Reach initialization :</span></span>

    /* Set action on the SDK push channel. */
    EngagementReach.Instance.SetActionOnPushChannel((PushNotificationChannel channel) => 
    {
      /* The forwarded channel can be null if its creation fails for any reason. */
      if (channel != null)
      {
        /* Your own push channel logic... */
      });
    }

## <a name="custom-scheme-tip"></a><span data-ttu-id="a06bc-215">自訂配置秘訣</span><span class="sxs-lookup"><span data-stu-id="a06bc-215">Custom scheme tip</span></span>
<span data-ttu-id="a06bc-216">我們提供使用自訂配置。</span><span class="sxs-lookup"><span data-stu-id="a06bc-216">We provide custom scheme use.</span></span> <span data-ttu-id="a06bc-217">您可以從 Engagement 前端傳送您 Engagement 應用程式使用的不同類型之 URI。</span><span class="sxs-lookup"><span data-stu-id="a06bc-217">You can send different type of URI from engagement frontend to be used in your engagement application.</span></span> <span data-ttu-id="a06bc-218">如果裝置上沒有安裝預設的應用程式，預設配置 (例如，由 Windows 管理 `http, ftp, ...` ) 便會出現視窗提示。</span><span class="sxs-lookup"><span data-stu-id="a06bc-218">Default scheme like `http, ftp, ...` are manage by Windows, a window will prompt if they are no default application installed on device.</span></span> <span data-ttu-id="a06bc-219">您也可以在您的應用程式中使用自訂配置。</span><span class="sxs-lookup"><span data-stu-id="a06bc-219">You can also create your own custom scheme for your application.</span></span>

<span data-ttu-id="a06bc-220">若要在您的應用程式中設定自訂配置，最簡單的方式就是開啟 `Package.appxmanifest`，然後進入 `Declarations` 面板。</span><span class="sxs-lookup"><span data-stu-id="a06bc-220">The simple way to set a custom scheme in your application is to open your `Package.appxmanifest` go in `Declarations` panel.</span></span> <span data-ttu-id="a06bc-221">在 [可用宣告] 捲動方塊中選取 `Protocol` 並將它新增。</span><span class="sxs-lookup"><span data-stu-id="a06bc-221">Select `Protocol` in the Available Declarations scroll box and add it.</span></span> <span data-ttu-id="a06bc-222">以您想要的新通訊協定名稱來編輯 `Name` 欄位。</span><span class="sxs-lookup"><span data-stu-id="a06bc-222">Edit the `Name` field with your new protocol desired name.</span></span>

<span data-ttu-id="a06bc-223">現在若要使用此通訊協定，請使用 `OnActivated` 方法編輯您的 `App.xaml.cs`，並請不要忘記也在此初始化 Engagement：</span><span class="sxs-lookup"><span data-stu-id="a06bc-223">Now to use this protocol, edit your `App.xaml.cs` with the `OnActivated` method, and don't forget to initialize engagement here also:</span></span>

            /// <summary>
            /// Enter point when app his called by another way than user click
            /// </summary>
            /// <param name="args">Activation args</param>
            protected override void OnActivated(IActivatedEventArgs args)
            {
              /* Init engagement like it was launch by a custom uri scheme */
              EngagementAgent.Instance.Init(args);
              EngagementReach.Instance.Init(args);

              //TODO design action to do when app is launch

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

