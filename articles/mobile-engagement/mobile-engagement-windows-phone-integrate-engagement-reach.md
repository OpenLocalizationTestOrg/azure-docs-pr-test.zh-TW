---
title: "Windows Phone Silverlight Reach SDK 整合"
description: "如何將 Azure Mobile Engagement Reach 與 Windows Phone Silverlight 應用程式整合"
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
ms.openlocfilehash: 0738f33df94d14fbb393bfaaf09e94c6560213cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="windows-phone-silverlight-reach-sdk-integration"></a><span data-ttu-id="c9e42-103">Windows Phone Silverlight Reach SDK 整合</span><span class="sxs-lookup"><span data-stu-id="c9e42-103">Windows Phone Silverlight Reach SDK Integration</span></span>
<span data-ttu-id="c9e42-104">依照本指南進行之前，您必須先遵循 [Windows Phone Silverlight Engagement SDK 整合](mobile-engagement-windows-phone-integrate-engagement.md) 中所述的整合程序。</span><span class="sxs-lookup"><span data-stu-id="c9e42-104">You must follow the integration procedure described in the [Windows Phone Silverlight Engagement SDK Integration](mobile-engagement-windows-phone-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-the-engagement-reach-sdk-into-your-windows-phone-silverlight-project"></a><span data-ttu-id="c9e42-105">將 Engagement Reach SDK 內嵌到您的 Windows Phone Silverlight 專案</span><span class="sxs-lookup"><span data-stu-id="c9e42-105">Embed the Engagement Reach SDK into your Windows Phone Silverlight project</span></span>
<span data-ttu-id="c9e42-106">您不需要新增任何項目。</span><span class="sxs-lookup"><span data-stu-id="c9e42-106">You do not have anything to add.</span></span> <span data-ttu-id="c9e42-107">`EngagementReach` 的參考和資源已在您的專案中。</span><span class="sxs-lookup"><span data-stu-id="c9e42-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="c9e42-108">您可以自定專案的 `Resources` 資料夾中的影像，尤其是品牌圖示 (預設為 Engagement 的圖示)。</span><span class="sxs-lookup"><span data-stu-id="c9e42-108">You can customize images located in the `Resources` folder of your project, especially the brand icon (that default to the Engagement icon).</span></span>
> 
> 

## <a name="add-the-capabilities"></a><span data-ttu-id="c9e42-109">新增功能</span><span class="sxs-lookup"><span data-stu-id="c9e42-109">Add the capabilities</span></span>
<span data-ttu-id="c9e42-110">Engagement Reach SDK 需要一些額外的功能。</span><span class="sxs-lookup"><span data-stu-id="c9e42-110">The Engagement Reach SDK needs some additional capabilities.</span></span>

<span data-ttu-id="c9e42-111">開啟 `WMAppManifest.xml` 檔案，並確定已宣告下列功能：</span><span class="sxs-lookup"><span data-stu-id="c9e42-111">Open your `WMAppManifest.xml` file and be sure that the following capabilities are declared:</span></span>

* `ID_CAP_PUSH_NOTIFICATION`
* `ID_CAP_WEBBROWSERCOMPONENT`

<span data-ttu-id="c9e42-112">第一項是 MPNS 服務用於允許顯示快顯通知的功能。</span><span class="sxs-lookup"><span data-stu-id="c9e42-112">The first one is used by the MPNS service to allow the display of toast notification.</span></span> <span data-ttu-id="c9e42-113">第二項是將瀏覽器工作內嵌到 SDK 的功能。</span><span class="sxs-lookup"><span data-stu-id="c9e42-113">The second one is used to embed a browser task into the SDK.</span></span>

<span data-ttu-id="c9e42-114">編輯 `WMAppManifest.xml` 檔案，並在 `<Capabilities />` 標記內加入：</span><span class="sxs-lookup"><span data-stu-id="c9e42-114">Edit the `WMAppManifest.xml` file and add inside the `<Capabilities />` tag :</span></span>

    <Capability Name="ID_CAP_PUSH_NOTIFICATION" />
    <Capability Name="ID_CAP_WEBBROWSERCOMPONENT" />

## <a name="enable-the-microsoft-push-notification-service"></a><span data-ttu-id="c9e42-115">啟用 Microsoft 推播通知服務</span><span class="sxs-lookup"><span data-stu-id="c9e42-115">Enable the Microsoft Push Notification Service</span></span>
<span data-ttu-id="c9e42-116">若要使用「Microsoft 推播通知服務」(簡稱 MPNS)，您的 `WMAppManifest.xml` 檔案必須包含 `<App />` 標記，且 `Publisher` 屬性設為您專案的名稱。</span><span class="sxs-lookup"><span data-stu-id="c9e42-116">In order to use the **Microsoft Push Notification Service** (referred as MPNS) your `WMAppManifest.xml` file must have an `<App />` tag with a `Publisher` attribute set to the name of your project.</span></span>

## <a name="initialize-the-engagement-reach-sdk"></a><span data-ttu-id="c9e42-117">初始化 Engagement Reach SDK</span><span class="sxs-lookup"><span data-stu-id="c9e42-117">Initialize the Engagement Reach SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="c9e42-118">Engagement 組態</span><span class="sxs-lookup"><span data-stu-id="c9e42-118">Engagement configuration</span></span>
<span data-ttu-id="c9e42-119">Engagement 組態會集中在您專案的 `Resources\EngagementConfiguration.xml` 檔案中。</span><span class="sxs-lookup"><span data-stu-id="c9e42-119">The Engagement configuration is centralized in the `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="c9e42-120">編輯此檔案來指定 Reach 的組態：</span><span class="sxs-lookup"><span data-stu-id="c9e42-120">Edit this file to specify reach configuration :</span></span>

* <span data-ttu-id="c9e42-121">(選擇性) 在 `<enableNativePush>` 和 `</enableNativePush>` 標記之間指定是否啟用原生推送 (MPNS) 的設定 (預設為 `true`)。</span><span class="sxs-lookup"><span data-stu-id="c9e42-121">*Optional*, indicate whether the native push (MPNS) is activated or not between `<enableNativePush>` and `</enableNativePush>` tags, (`true` by default).</span></span>
* <span data-ttu-id="c9e42-122">(選擇性) 在 `<channelName>` 和 `</channelName>` 標記之間指定推送通道的名稱，提供應用程式目前使用的推送通道名稱或保留空白。</span><span class="sxs-lookup"><span data-stu-id="c9e42-122">*Optional*, indicate the name of the push channel between `<channelName>` and `</channelName>` tags, provide the same that your application may currently use or leave it empty.</span></span>

<span data-ttu-id="c9e42-123">若想要改為在執行階段指定它，您可以在 Engagement 代理程式初始化之前呼叫下列方法：</span><span class="sxs-lookup"><span data-stu-id="c9e42-123">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization :</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    engagementConfiguration.Reach.EnableNativePush = true;                  
    /* [Optional] whether the native push (MPNS) is activated or not. */

    engagementConfiguration.Reach.ChannelName = "YOUR_PUSH_CHANNEL_NAME";   
    /* [Optional] Provide the same channel name that your application may currently use. */

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

> [!TIP]
> <span data-ttu-id="c9e42-124">您可以指定應用程式的 MPNS 推播通道之名稱。</span><span class="sxs-lookup"><span data-stu-id="c9e42-124">You can specify the name of the MPNS push channel of your application.</span></span> <span data-ttu-id="c9e42-125">根據預設，Engagement 會依 appId 建立名稱。</span><span class="sxs-lookup"><span data-stu-id="c9e42-125">By default, Engagement creates a name based on the appId.</span></span> <span data-ttu-id="c9e42-126">您不需要自行指定名稱，除非您打算於 Engagement 之外使用該推播通道。</span><span class="sxs-lookup"><span data-stu-id="c9e42-126">You have no need to specify the name yourself, except if you plan to use the push channel outside of Engagement.</span></span>
> 
> 

### <a name="engagement-initialization"></a><span data-ttu-id="c9e42-127">Engagement 初始化</span><span class="sxs-lookup"><span data-stu-id="c9e42-127">Engagement initialization</span></span>
<span data-ttu-id="c9e42-128">修改 `App.xaml.cs`：</span><span class="sxs-lookup"><span data-stu-id="c9e42-128">Modify the `App.xaml.cs`:</span></span>

* <span data-ttu-id="c9e42-129">新增至您的 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="c9e42-129">Add to your `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="c9e42-130">在 `Application_Launching` 中，將 `EngagementReach.Instance.Init` 插入 `EngagementAgent.Instance.Init` 後方：</span><span class="sxs-lookup"><span data-stu-id="c9e42-130">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in `Application_Launching` :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
         EngagementAgent.Instance.Init();
         EngagementReach.Instance.Init();
      }
* <span data-ttu-id="c9e42-131">在 `Application_Activated` 方法中插入 `EngagementReach.Instance.OnActivated`：</span><span class="sxs-lookup"><span data-stu-id="c9e42-131">Insert `EngagementReach.Instance.OnActivated` in the `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
         EngagementReach.Instance.OnActivated(e);
      }

> [!IMPORTANT]
> <span data-ttu-id="c9e42-132">`EngagementReach.Instance.Init` 會在專用的執行緒中執行。</span><span class="sxs-lookup"><span data-stu-id="c9e42-132">The `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="c9e42-133">您不必自行進行此作業。</span><span class="sxs-lookup"><span data-stu-id="c9e42-133">You do not have to do it yourself.</span></span>
> 
> 

## <a name="app-store-submission-considerations"></a><span data-ttu-id="c9e42-134">應用程式商店提交考量事項</span><span class="sxs-lookup"><span data-stu-id="c9e42-134">App store submission considerations</span></span>
<span data-ttu-id="c9e42-135">Microsoft 對於推播通知的使用有一些規定：</span><span class="sxs-lookup"><span data-stu-id="c9e42-135">Microsoft imposes some rules when using the push notifications:</span></span>

<span data-ttu-id="c9e42-136">摘錄自 Microsoft [應用程式原則] 文件，第 2.9 節：</span><span class="sxs-lookup"><span data-stu-id="c9e42-136">From the Microsoft [Application Policies] documentation, section 2.9:</span></span>

1) <span data-ttu-id="c9e42-137">您必須詢問使用者是否要接收推播通知。</span><span class="sxs-lookup"><span data-stu-id="c9e42-137">You must ask the user to accept to receive push notifications.</span></span> <span data-ttu-id="c9e42-138">然後，在您的設定中加入停用推播通知的方法。</span><span class="sxs-lookup"><span data-stu-id="c9e42-138">Then, in your settings, add a way to disable the push notifications.</span></span>

<span data-ttu-id="c9e42-139">EngagementReach 物件提供兩種方法來管理加入/退出、`EnableNativePush()` 和 `DisableNativePush()`。</span><span class="sxs-lookup"><span data-stu-id="c9e42-139">The EngagementReach object provides two methods to manage the opt-in/opt-out, `EnableNativePush()` and `DisableNativePush()`.</span></span> <span data-ttu-id="c9e42-140">例如，您可以在設定中建立有開關的選項，以停用或啟用 MPNS。</span><span class="sxs-lookup"><span data-stu-id="c9e42-140">You could, for example, create an option in the settings with a toggle to disable or enable MPNS.</span></span>

<span data-ttu-id="c9e42-141">您也可以選擇透過 Engagement 組態 \<windows-phone-sdk-reach-configuration\> 來停用 MPNS。</span><span class="sxs-lookup"><span data-stu-id="c9e42-141">You can also decide to deactivate MPNS through the Engagement configuration\<windows-phone-sdk-reach-configuration\>.</span></span>

> <span data-ttu-id="c9e42-142">2.9.1) 應用程式必須先描述所提供之通知的內容，並取得使用者明確的許可 (選擇加入)，且必須提供使用者可以選擇退出接收推播通知的機制。</span><span class="sxs-lookup"><span data-stu-id="c9e42-142">2.9.1) The application must first describe the notifications to be provided and **obtain the user’s express permission (opt-in)**, and **must provide a mechanism through which the user can opt out of receiving push notifications**.</span></span> <span data-ttu-id="c9e42-143">使用 Microsoft 推播通知服務提供的所有通知必須與提供給使用者的描述一致，且必須遵守所有適用的[應用程式原則][Content Policies]和[適用於特定應用程式類型的額外需求]。</span><span class="sxs-lookup"><span data-stu-id="c9e42-143">All notifications provided using the Microsoft Push Notification Service must be consistent with the description provided to the user and must comply with all applicable [Application Policies][Content Policies] and [Additional Requirements for Specific Application Types].</span></span>
> 
> 

2) <span data-ttu-id="c9e42-144">您不應該使用太多推播通知。</span><span class="sxs-lookup"><span data-stu-id="c9e42-144">You should not use too many push notifications.</span></span> <span data-ttu-id="c9e42-145">Engagement 將為您處理通知。</span><span class="sxs-lookup"><span data-stu-id="c9e42-145">Engagement will handle notifications for you.</span></span>

> <span data-ttu-id="c9e42-146">2.9.2) 應用程式及其對 Microsoft 推播通知服務的使用不得過度使用 Microsoft 推播通知服務的網路容量或頻寬，或以過度的推播通知對 Windows Phone 或其他 Microsoft 裝置或服務造成大量的負荷 (由 Microsoft 之合理的處理權判斷)，且不得傷害或干擾任何 Microsoft 網路或伺服器，或任何協力廠商伺服器或連線至 Microsoft 推播通知服務的網路。</span><span class="sxs-lookup"><span data-stu-id="c9e42-146">2.9.2) The application and its use of the Microsoft Push Notification Service must not excessively use network capacity or bandwidth of the Microsoft Push Notification Service, or otherwise unduly burden a Windows Phone or other Microsoft device or service with excessive push notifications, as determined by Microsoft in its reasonable discretion, and must not harm or interfere with any Microsoft networks or servers or any third party servers or networks connected to the Microsoft Push Notification Service.</span></span>
> 
> 

3) <span data-ttu-id="c9e42-147">請勿依賴 MPNS 傳送重要資訊。</span><span class="sxs-lookup"><span data-stu-id="c9e42-147">Do not rely on MPNS to send criticals information.</span></span> <span data-ttu-id="c9e42-148">Engagement 使用 MPNS，所以此規定也適用於在 Engagement 前端所建立的活動。</span><span class="sxs-lookup"><span data-stu-id="c9e42-148">Engagement uses MPNS, so this rule also applies for the campaigns created inside the Engagement front-end.</span></span>

> <span data-ttu-id="c9e42-149">2.9.3) Microsoft 推播通知服務不得用來傳送緊急或攸關生命安全的通知，包括但不限於與醫療裝置或狀況相關的緊急通知。</span><span class="sxs-lookup"><span data-stu-id="c9e42-149">2.9.3) The Microsoft Push Notification Service may not be used to send notifications that are mission critical or otherwise could affect matters of life or death, including without limitation critical notifications related to a medical device or condition.</span></span> <span data-ttu-id="c9e42-150">Microsoft 清楚聲明對於 Microsoft 推播通知服務或 Microsoft 推播通知服務之通知的傳送，不提供不會有任何中斷、錯誤，或為即時運作的任何擔保。</span><span class="sxs-lookup"><span data-stu-id="c9e42-150">MICROSOFT EXPRESSLY DISCLAIMS ANY WARRANTIES THAT THE USE OF THE MICROSOFT PUSH NOTIFICATION SERVICE OR DELIVERY OF MICROSOFT PUSH NOTIFICATION SERVICE NOTIFICATIONS WILL BE UNINTERRUPTED, ERROR FREE, OR OTHERWISE GUARANTEED TO OCCUR ON A REAL-TIME BASIS.</span></span>
> 
> 

<span data-ttu-id="c9e42-151">**如果您不遵守這些建議，我們無法保證您的應用程式會通過驗證程序。**</span><span class="sxs-lookup"><span data-stu-id="c9e42-151">**We cannot guarantee that your application will pass the validation process if you do not respect these recommendations.**</span></span>

## <a name="handle-data-push-optional"></a><span data-ttu-id="c9e42-152">處理資料推送 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="c9e42-152">Handle data push (optional)</span></span>
<span data-ttu-id="c9e42-153">如果您希望您的應用程式接收 Reach 資料推送，您必須實作 EngagementReach 類別的兩個事件：</span><span class="sxs-lookup"><span data-stu-id="c9e42-153">If you want your application to be able to receive Reach data pushes, you have to implement two events of the EngagementReach class:</span></span>

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

<span data-ttu-id="c9e42-154">您可以看到每個方法的回呼會傳回布林值。</span><span class="sxs-lookup"><span data-stu-id="c9e42-154">You can see that the callback of each method returns a boolean.</span></span> <span data-ttu-id="c9e42-155">Engagement 會在發送資料推送之後傳送回饋到它的後端。</span><span class="sxs-lookup"><span data-stu-id="c9e42-155">Engagement sends a feedback to its back-end after dispatching the data push.</span></span> <span data-ttu-id="c9e42-156">如果回呼傳回 false，會傳送 `exit` 回饋。</span><span class="sxs-lookup"><span data-stu-id="c9e42-156">If the callback returns false, the `exit` feedback will be send.</span></span> <span data-ttu-id="c9e42-157">否則將會是 `action`。</span><span class="sxs-lookup"><span data-stu-id="c9e42-157">Otherwise, it will be `action`.</span></span> <span data-ttu-id="c9e42-158">如果沒有設定事件的回呼，就會傳送 `drop` 回饋到 Engagement。</span><span class="sxs-lookup"><span data-stu-id="c9e42-158">If no callback is set for the events, the `drop` feedback will be returned to Engagement.</span></span>

> [!WARNING]
> <span data-ttu-id="c9e42-159">Engagement 無法接收單一資料推送的多個回饋。</span><span class="sxs-lookup"><span data-stu-id="c9e42-159">Engagement is not able to receive multiples feedbacks for a data push.</span></span> <span data-ttu-id="c9e42-160">如果計畫在單一事件上設定多個處理常式，請留意回饋將與最後一個傳送的對應。</span><span class="sxs-lookup"><span data-stu-id="c9e42-160">If you plan to set several handlers on an event, be aware that the feedback will correspond to the last one sent.</span></span> <span data-ttu-id="c9e42-161">在此情況下，我們建議一律傳回相同的值，避免在前端有令人困惑的回饋。</span><span class="sxs-lookup"><span data-stu-id="c9e42-161">In this case, we recommend to always returns the same value to avoid having confusing feedback on the front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="c9e42-162">自訂 UI (選擇性)</span><span class="sxs-lookup"><span data-stu-id="c9e42-162">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="c9e42-163">第一步</span><span class="sxs-lookup"><span data-stu-id="c9e42-163">First step</span></span>
<span data-ttu-id="c9e42-164">我們讓您可以自訂 Reach UI。</span><span class="sxs-lookup"><span data-stu-id="c9e42-164">We allow you to customize the reach UI.</span></span>

<span data-ttu-id="c9e42-165">若要這樣做，您必須建立 `EngagementReachHandler` 類別的子類別。</span><span class="sxs-lookup"><span data-stu-id="c9e42-165">To do so, you have to create a subclass of the `EngagementReachHandler` class.</span></span>

<span data-ttu-id="c9e42-166">**範例程式碼：**</span><span class="sxs-lookup"><span data-stu-id="c9e42-166">**Sample Code :**</span></span>

    using Microsoft.Azure.Engagement;

    namespace Example
    {
       internal class ExampleReachHandler : EngagementReachHandler
       {
          // Override EngagementReachHandler methods depending on your needs
       }
    }

<span data-ttu-id="c9e42-167">然後，使用 `Application_Launching` 方法中 `App.xaml.cs` 類別的自訂物件，設定 `EngagementReach.Instance.Handler` 欄位的內容。</span><span class="sxs-lookup"><span data-stu-id="c9e42-167">Then, set the content of the `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within the `Application_Launching` method.</span></span>

<span data-ttu-id="c9e42-168">**範例程式碼：**</span><span class="sxs-lookup"><span data-stu-id="c9e42-168">**Sample Code :**</span></span>

    private void Application_Launching(object sender, LaunchingEventArgs e)
    {
       // your app initialization 
       EngagementReach.Instance.Handler = new ExampleReachHandler();
       // Engagement Agent and Reach initialization
    }

> [!NOTE]
> <span data-ttu-id="c9e42-169">根據預設，Engagement 會使用自己的 `EngagementReachHandler` 實作。</span><span class="sxs-lookup"><span data-stu-id="c9e42-169">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span> <span data-ttu-id="c9e42-170">您不需要自己建立，但如果有需要，您不需要覆寫每個方法。</span><span class="sxs-lookup"><span data-stu-id="c9e42-170">You don't have to create your own, and if you do so, you don't have to override every method.</span></span> <span data-ttu-id="c9e42-171">預設行為是選取 Engagement 基底物件。</span><span class="sxs-lookup"><span data-stu-id="c9e42-171">The default behavior is to select the Engagement base object.</span></span>
> 
> 

### <a name="layouts"></a><span data-ttu-id="c9e42-172">版面配置</span><span class="sxs-lookup"><span data-stu-id="c9e42-172">Layouts</span></span>
<span data-ttu-id="c9e42-173">根據預設，Reach 會使用 DLL 的內嵌資源來顯示通知和頁面。</span><span class="sxs-lookup"><span data-stu-id="c9e42-173">By default, Reach will use the embedded resources of the DLL to display the notifications and pages.</span></span>

<span data-ttu-id="c9e42-174">不過，您可以在這些元件中使用自己的資源以反映您的品牌。</span><span class="sxs-lookup"><span data-stu-id="c9e42-174">However, you can decide to use your own resources to reflect your brand in these components.</span></span>

<span data-ttu-id="c9e42-175">您可以在您的子類別中覆寫 `EngagementReachHandler` 方法，藉此告訴 Engagement 要使用您的版面配置：</span><span class="sxs-lookup"><span data-stu-id="c9e42-175">You can override `EngagementReachHandler` methods in your subclass to tell Engagement to use your layouts :</span></span>

<span data-ttu-id="c9e42-176">**範例程式碼：**</span><span class="sxs-lookup"><span data-stu-id="c9e42-176">**Sample Code :**</span></span>

    // In your subclass of EngagementReachHandler

    public override string GetTextViewAnnouncementUri()
    {
       // return the path of your own xaml
    }

    public override string GetWebViewAnnouncementUri()
    {
       // return the path of your own xaml
    }

    public override string GetPollUri()
    {
       // return the path of your own xaml
    }

    public override EngagementNotificationView CreateNotification(EngagementNotificationViewModel viewModel)
    {
       // return a new instance of your own notification
    }

> [!TIP]
> <span data-ttu-id="c9e42-177">`CreateNotification` 方法可以傳回 Null。</span><span class="sxs-lookup"><span data-stu-id="c9e42-177">The `CreateNotification` method can return null.</span></span> <span data-ttu-id="c9e42-178">通知將無法顯示，且觸達活動將會被捨棄。</span><span class="sxs-lookup"><span data-stu-id="c9e42-178">The notification won't be displayed and the reach campaign will be dropped.</span></span>
> 
> 

<span data-ttu-id="c9e42-179">若要簡化您的版面配置實作，我們也提供可讓您做為程式碼基礎的 xaml。</span><span class="sxs-lookup"><span data-stu-id="c9e42-179">To simplify your layout implementation, we also provide our own xaml which can serve as a basis for your code.</span></span> <span data-ttu-id="c9e42-180">它們在 Engagement SDK 封存內 (/src/reach/)。</span><span class="sxs-lookup"><span data-stu-id="c9e42-180">They are located in the Engagement SDK archive (/src/reach/).</span></span>

> [!WARNING]
> <span data-ttu-id="c9e42-181">我們提供的來源與我們使用的完全相同。</span><span class="sxs-lookup"><span data-stu-id="c9e42-181">The sources that we provide are the exact same ones that we use.</span></span> <span data-ttu-id="c9e42-182">因此，如果您想要直接修改它們，別忘了變更命名空間和名稱。</span><span class="sxs-lookup"><span data-stu-id="c9e42-182">So if you want to modify them directly, don't forget to change the namespace and the name.</span></span>
> 
> 

### <a name="notification-position"></a><span data-ttu-id="c9e42-183">通知的位置</span><span class="sxs-lookup"><span data-stu-id="c9e42-183">Notification position</span></span>
<span data-ttu-id="c9e42-184">根據預設，應用程式內通知會顯示在應用程式底部的左側。</span><span class="sxs-lookup"><span data-stu-id="c9e42-184">By default, an in-app notification is displayed at the bottom left side of the application.</span></span> <span data-ttu-id="c9e42-185">您可以透過覆寫 `EngagementReachHandler` 物件的 `GetNotificationPosition` 方法來變更此行為。</span><span class="sxs-lookup"><span data-stu-id="c9e42-185">You can change this behavior by overriding the `GetNotificationPosition` method of the `EngagementReachHandler` object.</span></span>

    // In your subclass of EngagementReachHandler

    public override EngagementReachHandler.NotificationPosition GetNotificationPosition(EngagementNotificationViewModel viewModel)
    {
       // return a value of the EngagementReachHandler.NotificationPosition enum (TOP or BOTTOM)
    }

<span data-ttu-id="c9e42-186">您目前可以選擇 `BOTTOM` (預設) 或 `TOP` 兩種位置。</span><span class="sxs-lookup"><span data-stu-id="c9e42-186">Currently, you can choose between the `BOTTOM` (default) and `TOP` positions.</span></span>

### <a name="launch-message"></a><span data-ttu-id="c9e42-187">啟動訊息</span><span class="sxs-lookup"><span data-stu-id="c9e42-187">Launch message</span></span>
<span data-ttu-id="c9e42-188">當使用者按一下系統通知 (快顯通知) 時，Engagement 會啟動該應用程式、載入推播訊息的內容，並顯示對應之活動的頁面。</span><span class="sxs-lookup"><span data-stu-id="c9e42-188">When a user clicks on a system notification (a toast), Engagement launches the app, load the content of the push messages, and display the page for the corresponding campaign.</span></span>

<span data-ttu-id="c9e42-189">啟動應用程式與頁面顯示之間會有延遲 (取決於您的網路速度)。</span><span class="sxs-lookup"><span data-stu-id="c9e42-189">There is a delay between the launch of the application and the display of the page (depending on the speed of your network).</span></span>

<span data-ttu-id="c9e42-190">若要向使用者指示正在載入項目，您應該提供視覺化的資訊，例如進度列或進度列指示器。</span><span class="sxs-lookup"><span data-stu-id="c9e42-190">To indicate to the user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="c9e42-191">Engagement 無法自行處理這些，但有提供您幾個處理常式。</span><span class="sxs-lookup"><span data-stu-id="c9e42-191">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="c9e42-192">若要實作回呼，請執行：</span><span class="sxs-lookup"><span data-stu-id="c9e42-192">To implement the callback, do:</span></span>

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

<span data-ttu-id="c9e42-193">您可以在 `App.xaml.cs` 檔案的 `Application_Launching` 方法中設定回呼，最好設定在 `EngagementReach.Instance.Init()` 呼叫之前。</span><span class="sxs-lookup"><span data-stu-id="c9e42-193">You can set the callback in your `Application_Launching` method of your `App.xaml.cs` file, preferably before the `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="c9e42-194">每個處理常式都是由 UI 執行緒呼叫。</span><span class="sxs-lookup"><span data-stu-id="c9e42-194">Each handler is called by the UI Thread.</span></span> <span data-ttu-id="c9e42-195">在使用 MessageBox 或 UI 相關的項目時您不必擔心。</span><span class="sxs-lookup"><span data-stu-id="c9e42-195">You do not have to worry when using a MessageBox or something UI-related.</span></span>
> 
> 

<span data-ttu-id="c9e42-196">[應用程式原則]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx</span><span class="sxs-lookup"><span data-stu-id="c9e42-196">[Application Policies]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx</span></span>
[Content Policies]:http://msdn.microsoft.com/library/windows/apps/hh184842(v=vs.105).aspx
<span data-ttu-id="c9e42-197">[適用於特定應用程式類型的額外需求]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx</span><span class="sxs-lookup"><span data-stu-id="c9e42-197">[Additional Requirements for Specific Application Types]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx</span></span>

