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
# <a name="windows-phone-silverlight-reach-sdk-integration"></a><span data-ttu-id="18d04-103">Windows Phone Silverlight Reach SDK 整合</span><span class="sxs-lookup"><span data-stu-id="18d04-103">Windows Phone Silverlight Reach SDK Integration</span></span>
<span data-ttu-id="18d04-104">您必須遵循 hello 整合程序所述 hello [Windows Phone Silverlight Engagement SDK 整合](mobile-engagement-windows-phone-integrate-engagement.md)之前依照本指南。</span><span class="sxs-lookup"><span data-stu-id="18d04-104">You must follow hello integration procedure described in hello [Windows Phone Silverlight Engagement SDK Integration](mobile-engagement-windows-phone-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-phone-silverlight-project"></a><span data-ttu-id="18d04-105">內嵌至 Windows Phone Silverlight 專案中的 hello Engagement 觸達 SDK</span><span class="sxs-lookup"><span data-stu-id="18d04-105">Embed hello Engagement Reach SDK into your Windows Phone Silverlight project</span></span>
<span data-ttu-id="18d04-106">您沒有任何項目 tooadd。</span><span class="sxs-lookup"><span data-stu-id="18d04-106">You do not have anything tooadd.</span></span> <span data-ttu-id="18d04-107">`EngagementReach` 的參考和資源已在您的專案中。</span><span class="sxs-lookup"><span data-stu-id="18d04-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="18d04-108">您可以自訂映像位於 hello`Resources`專案，特別是 hello 商標圖示 （該預設 toohello Engagement 圖示） 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="18d04-108">You can customize images located in hello `Resources` folder of your project, especially hello brand icon (that default toohello Engagement icon).</span></span>
> 
> 

## <a name="add-hello-capabilities"></a><span data-ttu-id="18d04-109">加入 hello 功能</span><span class="sxs-lookup"><span data-stu-id="18d04-109">Add hello capabilities</span></span>
<span data-ttu-id="18d04-110">hello Engagement 觸達 SDK 需要一些額外的功能。</span><span class="sxs-lookup"><span data-stu-id="18d04-110">hello Engagement Reach SDK needs some additional capabilities.</span></span>

<span data-ttu-id="18d04-111">開啟您`WMAppManifest.xml`檔案，並確定宣告該 hello 下列功能：</span><span class="sxs-lookup"><span data-stu-id="18d04-111">Open your `WMAppManifest.xml` file and be sure that hello following capabilities are declared:</span></span>

* `ID_CAP_PUSH_NOTIFICATION`
* `ID_CAP_WEBBROWSERCOMPONENT`

<span data-ttu-id="18d04-112">hello 先使用其中一個是由 hello MPNS 服務 tooallow hello 顯示快顯通知。</span><span class="sxs-lookup"><span data-stu-id="18d04-112">hello first one is used by hello MPNS service tooallow hello display of toast notification.</span></span> <span data-ttu-id="18d04-113">hello 第二個是使用的 tooembed hello SDK 到瀏覽器工作。</span><span class="sxs-lookup"><span data-stu-id="18d04-113">hello second one is used tooembed a browser task into hello SDK.</span></span>

<span data-ttu-id="18d04-114">編輯 hello`WMAppManifest.xml`檔案，然後加入內 hello`<Capabilities />`標記：</span><span class="sxs-lookup"><span data-stu-id="18d04-114">Edit hello `WMAppManifest.xml` file and add inside hello `<Capabilities />` tag :</span></span>

    <Capability Name="ID_CAP_PUSH_NOTIFICATION" />
    <Capability Name="ID_CAP_WEBBROWSERCOMPONENT" />

## <a name="enable-hello-microsoft-push-notification-service"></a><span data-ttu-id="18d04-115">啟用 hello Microsoft 推播通知服務</span><span class="sxs-lookup"><span data-stu-id="18d04-115">Enable hello Microsoft Push Notification Service</span></span>
<span data-ttu-id="18d04-116">在訂單 toouse hello **Microsoft 推播通知服務**（稱為 MPNS） 您`WMAppManifest.xml`檔案必須具有`<App />`標記`Publisher`設定 toohello 專案名稱的屬性。</span><span class="sxs-lookup"><span data-stu-id="18d04-116">In order toouse hello **Microsoft Push Notification Service** (referred as MPNS) your `WMAppManifest.xml` file must have an `<App />` tag with a `Publisher` attribute set toohello name of your project.</span></span>

## <a name="initialize-hello-engagement-reach-sdk"></a><span data-ttu-id="18d04-117">初始化 hello Engagement 觸達 SDK</span><span class="sxs-lookup"><span data-stu-id="18d04-117">Initialize hello Engagement Reach SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="18d04-118">Engagement 組態</span><span class="sxs-lookup"><span data-stu-id="18d04-118">Engagement configuration</span></span>
<span data-ttu-id="18d04-119">hello Engagement 組態會集中在 hello`Resources\EngagementConfiguration.xml`專案檔。</span><span class="sxs-lookup"><span data-stu-id="18d04-119">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="18d04-120">編輯此檔案 toospecify 觸達設定：</span><span class="sxs-lookup"><span data-stu-id="18d04-120">Edit this file toospecify reach configuration :</span></span>

* <span data-ttu-id="18d04-121">*選擇性*，指出是否啟用 hello 原生推送 (MPNS) 或不介於`<enableNativePush>`和`</enableNativePush>`標記 (`true`依預設)。</span><span class="sxs-lookup"><span data-stu-id="18d04-121">*Optional*, indicate whether hello native push (MPNS) is activated or not between `<enableNativePush>` and `</enableNativePush>` tags, (`true` by default).</span></span>
* <span data-ttu-id="18d04-122">*選擇性*，表示 hello 發送通道之間 hello 名稱`<channelName>`和`</channelName>`標記，提供 hello 相同應用程式可能目前使用，或保持空白。</span><span class="sxs-lookup"><span data-stu-id="18d04-122">*Optional*, indicate hello name of hello push channel between `<channelName>` and `</channelName>` tags, provide hello same that your application may currently use or leave it empty.</span></span>

<span data-ttu-id="18d04-123">如果您想要在執行階段相反地，您可以呼叫 hello 下列 toospecify hello Engagement 代理程式初始化之前的方法：</span><span class="sxs-lookup"><span data-stu-id="18d04-123">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization :</span></span>

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
> <span data-ttu-id="18d04-124">您可以指定 hello hello MPNS 發送通道，您的應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="18d04-124">You can specify hello name of hello MPNS push channel of your application.</span></span> <span data-ttu-id="18d04-125">根據預設，Engagement 會建立 hello appId 為基礎的名稱。</span><span class="sxs-lookup"><span data-stu-id="18d04-125">By default, Engagement creates a name based on hello appId.</span></span> <span data-ttu-id="18d04-126">您有任何需要 toospecify hello 名稱，但如果您計劃外 Engagement toouse hello 推播通道。</span><span class="sxs-lookup"><span data-stu-id="18d04-126">You have no need toospecify hello name yourself, except if you plan toouse hello push channel outside of Engagement.</span></span>
> 
> 

### <a name="engagement-initialization"></a><span data-ttu-id="18d04-127">Engagement 初始化</span><span class="sxs-lookup"><span data-stu-id="18d04-127">Engagement initialization</span></span>
<span data-ttu-id="18d04-128">修改 hello `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="18d04-128">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="18d04-129">新增 tooyour`using`陳述式：</span><span class="sxs-lookup"><span data-stu-id="18d04-129">Add tooyour `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="18d04-130">在 `Application_Launching` 中，將 `EngagementReach.Instance.Init` 插入 `EngagementAgent.Instance.Init` 後方：</span><span class="sxs-lookup"><span data-stu-id="18d04-130">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in `Application_Launching` :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
         EngagementAgent.Instance.Init();
         EngagementReach.Instance.Init();
      }
* <span data-ttu-id="18d04-131">插入`EngagementReach.Instance.OnActivated`在 hello`Application_Activated`方法：</span><span class="sxs-lookup"><span data-stu-id="18d04-131">Insert `EngagementReach.Instance.OnActivated` in hello `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
         EngagementReach.Instance.OnActivated(e);
      }

> [!IMPORTANT]
> <span data-ttu-id="18d04-132">hello`EngagementReach.Instance.Init`專用的執行緒中執行。</span><span class="sxs-lookup"><span data-stu-id="18d04-132">hello `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="18d04-133">您不需要 toodo 它自己。</span><span class="sxs-lookup"><span data-stu-id="18d04-133">You do not have toodo it yourself.</span></span>
> 
> 

## <a name="app-store-submission-considerations"></a><span data-ttu-id="18d04-134">應用程式商店提交考量事項</span><span class="sxs-lookup"><span data-stu-id="18d04-134">App store submission considerations</span></span>
<span data-ttu-id="18d04-135">使用 hello 推播通知時，Microsoft 會施加某些規則：</span><span class="sxs-lookup"><span data-stu-id="18d04-135">Microsoft imposes some rules when using hello push notifications:</span></span>

<span data-ttu-id="18d04-136">從 hello Microsoft[應用程式原則]文件、 2.9 區段：</span><span class="sxs-lookup"><span data-stu-id="18d04-136">From hello Microsoft [Application Policies] documentation, section 2.9:</span></span>

1) <span data-ttu-id="18d04-137">您必須要求 hello 使用者 tooaccept tooreceive 推播通知。</span><span class="sxs-lookup"><span data-stu-id="18d04-137">You must ask hello user tooaccept tooreceive push notifications.</span></span> <span data-ttu-id="18d04-138">然後，在您設定中，加入方法 toodisable hello 推播通知。</span><span class="sxs-lookup"><span data-stu-id="18d04-138">Then, in your settings, add a way toodisable hello push notifications.</span></span>

<span data-ttu-id="18d04-139">hello EngagementReach 物件提供兩個方法 toomanage hello 選擇位在/退出，`EnableNativePush()`和`DisableNativePush()`。</span><span class="sxs-lookup"><span data-stu-id="18d04-139">hello EngagementReach object provides two methods toomanage hello opt-in/opt-out, `EnableNativePush()` and `DisableNativePush()`.</span></span> <span data-ttu-id="18d04-140">例如，您無法切換 toodisable 與 hello 設定中建立選項或啟用 MPNS。</span><span class="sxs-lookup"><span data-stu-id="18d04-140">You could, for example, create an option in hello settings with a toggle toodisable or enable MPNS.</span></span>

<span data-ttu-id="18d04-141">您也可以決定透過 hello Engagement 組態 toodeactivate MPNS\<windows phone-sdk-觸達-設定\>。</span><span class="sxs-lookup"><span data-stu-id="18d04-141">You can also decide toodeactivate MPNS through hello Engagement configuration\<windows-phone-sdk-reach-configuration\>.</span></span>

> <span data-ttu-id="18d04-142">2.9.1) hello 應用程式必須先說明提供 hello 通知 toobe 和**取得 hello 使用者快速權限 （選擇加入的）**，和**必須提供的機制，透過 hello 哪些使用者可以選擇不接收推播通知**。</span><span class="sxs-lookup"><span data-stu-id="18d04-142">2.9.1) hello application must first describe hello notifications toobe provided and **obtain hello user’s express permission (opt-in)**, and **must provide a mechanism through which hello user can opt out of receiving push notifications**.</span></span> <span data-ttu-id="18d04-143">提供使用 hello Microsoft 推播通知服務的所有通知的 hello 提供描述 toohello 使用者必須一致，且必須符合所有適用[應用程式原則][ Content Policies]和[特定應用程式類型的其他需求]。</span><span class="sxs-lookup"><span data-stu-id="18d04-143">All notifications provided using hello Microsoft Push Notification Service must be consistent with hello description provided toohello user and must comply with all applicable [Application Policies][Content Policies] and [Additional Requirements for Specific Application Types].</span></span>
> 
> 

2) <span data-ttu-id="18d04-144">您不應該使用太多推播通知。</span><span class="sxs-lookup"><span data-stu-id="18d04-144">You should not use too many push notifications.</span></span> <span data-ttu-id="18d04-145">Engagement 將為您處理通知。</span><span class="sxs-lookup"><span data-stu-id="18d04-145">Engagement will handle notifications for you.</span></span>

> <span data-ttu-id="18d04-146">2.9.2) hello 應用程式和其 hello Microsoft 推播通知服務的使用情形必須不過度使用網路容量或頻寬的 hello Microsoft 推播通知服務，或 Windows Phone 或其他 Microsoft 裝置或服務否則過度應用具有過多由 Microsoft 依合理酌情判斷，將推播通知，並不得對系統造成傷害或干擾任何 Microsoft 網路伺服器或任何協力廠商伺服器或網路連線的 toohello Microsoft 推播通知服務。</span><span class="sxs-lookup"><span data-stu-id="18d04-146">2.9.2) hello application and its use of hello Microsoft Push Notification Service must not excessively use network capacity or bandwidth of hello Microsoft Push Notification Service, or otherwise unduly burden a Windows Phone or other Microsoft device or service with excessive push notifications, as determined by Microsoft in its reasonable discretion, and must not harm or interfere with any Microsoft networks or servers or any third party servers or networks connected toohello Microsoft Push Notification Service.</span></span>
> 
> 

3) <span data-ttu-id="18d04-147">請勿依賴 MPNS toosend criticals 資訊。</span><span class="sxs-lookup"><span data-stu-id="18d04-147">Do not rely on MPNS toosend criticals information.</span></span> <span data-ttu-id="18d04-148">Engagement 使用 MPNS，因此這項規則也適用於建立在 hello Engagement 前端 hello 客群。</span><span class="sxs-lookup"><span data-stu-id="18d04-148">Engagement uses MPNS, so this rule also applies for hello campaigns created inside hello Engagement front-end.</span></span>

> <span data-ttu-id="18d04-149">2.9.3) hello Microsoft 推播通知服務可能無法使用的 toosend 通知是非常重要或其他可能會影響對很重要的生命週期或死亡，包括但不限於重要通知相關的 tooa 醫療裝置或條件。</span><span class="sxs-lookup"><span data-stu-id="18d04-149">2.9.3) hello Microsoft Push Notification Service may not be used toosend notifications that are mission critical or otherwise could affect matters of life or death, including without limitation critical notifications related tooa medical device or condition.</span></span> <span data-ttu-id="18d04-150">MICROSOFT 用戶不作任何擔保，hello 使用的 hello MICROSOFT 推播通知服務或傳遞的 MICROSOFT 推播通知服務通知將會是不中斷，錯誤可用或保證 tooOCCUR ON A 即時基礎。</span><span class="sxs-lookup"><span data-stu-id="18d04-150">MICROSOFT EXPRESSLY DISCLAIMS ANY WARRANTIES THAT hello USE OF hello MICROSOFT PUSH NOTIFICATION SERVICE OR DELIVERY OF MICROSOFT PUSH NOTIFICATION SERVICE NOTIFICATIONS WILL BE UNINTERRUPTED, ERROR FREE, OR OTHERWISE GUARANTEED tooOCCUR ON A REAL-TIME BASIS.</span></span>
> 
> 

<span data-ttu-id="18d04-151">**我們無法保證您的應用程式將會通過 hello 驗證程序，如果您不會採用這些建議。**</span><span class="sxs-lookup"><span data-stu-id="18d04-151">**We cannot guarantee that your application will pass hello validation process if you do not respect these recommendations.**</span></span>

## <a name="handle-data-push-optional"></a><span data-ttu-id="18d04-152">處理資料推送 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="18d04-152">Handle data push (optional)</span></span>
<span data-ttu-id="18d04-153">如果您希望您的應用程式 toobe tooreceive 無法觸達資料推播通知時，您會有 tooimplement 的 hello EngagementReach 類別的兩個事件：</span><span class="sxs-lookup"><span data-stu-id="18d04-153">If you want your application toobe able tooreceive Reach data pushes, you have tooimplement two events of hello EngagementReach class:</span></span>

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

<span data-ttu-id="18d04-154">您可以看到 hello 回撥的每個方法會傳回布林值。</span><span class="sxs-lookup"><span data-stu-id="18d04-154">You can see that hello callback of each method returns a boolean.</span></span> <span data-ttu-id="18d04-155">Engagement 傳送意見反應 tooits 後端之後分派 hello 資料推送。</span><span class="sxs-lookup"><span data-stu-id="18d04-155">Engagement sends a feedback tooits back-end after dispatching hello data push.</span></span> <span data-ttu-id="18d04-156">如果 hello 回呼傳回 false，hello`exit`意見反應會傳送。</span><span class="sxs-lookup"><span data-stu-id="18d04-156">If hello callback returns false, hello `exit` feedback will be send.</span></span> <span data-ttu-id="18d04-157">否則將會是 `action`。</span><span class="sxs-lookup"><span data-stu-id="18d04-157">Otherwise, it will be `action`.</span></span> <span data-ttu-id="18d04-158">如果沒有回呼 hello 事件設定，hello `drop` tooEngagement 將傳回的意見反應。</span><span class="sxs-lookup"><span data-stu-id="18d04-158">If no callback is set for hello events, hello `drop` feedback will be returned tooEngagement.</span></span>

> [!WARNING]
> <span data-ttu-id="18d04-159">Engagement 不能 tooreceive 倍數的意見反應資料推入。</span><span class="sxs-lookup"><span data-stu-id="18d04-159">Engagement is not able tooreceive multiples feedbacks for a data push.</span></span> <span data-ttu-id="18d04-160">如果您計劃 tooset 數個處理常式事件，請注意 hello 意見反應會對應 toohello 傳送的最後一個。</span><span class="sxs-lookup"><span data-stu-id="18d04-160">If you plan tooset several handlers on an event, be aware that hello feedback will correspond toohello last one sent.</span></span> <span data-ttu-id="18d04-161">在此情況下，我們建議 tooalways 傳回 hello 相同的值 tooavoid hello 前端上有令人混淆的意見反應。</span><span class="sxs-lookup"><span data-stu-id="18d04-161">In this case, we recommend tooalways returns hello same value tooavoid having confusing feedback on hello front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="18d04-162">自訂 UI (選擇性)</span><span class="sxs-lookup"><span data-stu-id="18d04-162">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="18d04-163">第一步</span><span class="sxs-lookup"><span data-stu-id="18d04-163">First step</span></span>
<span data-ttu-id="18d04-164">我們可讓您 toocustomize hello 觸達 UI。</span><span class="sxs-lookup"><span data-stu-id="18d04-164">We allow you toocustomize hello reach UI.</span></span>

<span data-ttu-id="18d04-165">toodo 因此，您有 toocreate hello 的子類別`EngagementReachHandler`類別。</span><span class="sxs-lookup"><span data-stu-id="18d04-165">toodo so, you have toocreate a subclass of hello `EngagementReachHandler` class.</span></span>

<span data-ttu-id="18d04-166">**範例程式碼：**</span><span class="sxs-lookup"><span data-stu-id="18d04-166">**Sample Code :**</span></span>

    using Microsoft.Azure.Engagement;

    namespace Example
    {
       internal class ExampleReachHandler : EngagementReachHandler
       {
          // Override EngagementReachHandler methods depending on your needs
       }
    }

<span data-ttu-id="18d04-167">然後將設定的 hello hello 內容`EngagementReach.Instance.Handler`欄位中的自訂物件取代您`App.xaml.cs`內 hello 類別`Application_Launching`方法。</span><span class="sxs-lookup"><span data-stu-id="18d04-167">Then, set hello content of hello `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within hello `Application_Launching` method.</span></span>

<span data-ttu-id="18d04-168">**範例程式碼：**</span><span class="sxs-lookup"><span data-stu-id="18d04-168">**Sample Code :**</span></span>

    private void Application_Launching(object sender, LaunchingEventArgs e)
    {
       // your app initialization 
       EngagementReach.Instance.Handler = new ExampleReachHandler();
       // Engagement Agent and Reach initialization
    }

> [!NOTE]
> <span data-ttu-id="18d04-169">根據預設，Engagement 會使用自己的 `EngagementReachHandler` 實作。</span><span class="sxs-lookup"><span data-stu-id="18d04-169">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span> <span data-ttu-id="18d04-170">您不需要 toocreate 您自己的而且這樣一來，如果您沒有 toooverride 每個方法。</span><span class="sxs-lookup"><span data-stu-id="18d04-170">You don't have toocreate your own, and if you do so, you don't have toooverride every method.</span></span> <span data-ttu-id="18d04-171">hello 預設行為是 tooselect hello Engagement 基底物件。</span><span class="sxs-lookup"><span data-stu-id="18d04-171">hello default behavior is tooselect hello Engagement base object.</span></span>
> 
> 

### <a name="layouts"></a><span data-ttu-id="18d04-172">版面配置</span><span class="sxs-lookup"><span data-stu-id="18d04-172">Layouts</span></span>
<span data-ttu-id="18d04-173">根據預設，觸達會使用 hello DLL toodisplay hello 通知和網頁的 hello 內嵌的資源。</span><span class="sxs-lookup"><span data-stu-id="18d04-173">By default, Reach will use hello embedded resources of hello DLL toodisplay hello notifications and pages.</span></span>

<span data-ttu-id="18d04-174">不過，您可以決定 toouse 您自己的資源 tooreflect 您在這些元件的品牌。</span><span class="sxs-lookup"><span data-stu-id="18d04-174">However, you can decide toouse your own resources tooreflect your brand in these components.</span></span>

<span data-ttu-id="18d04-175">您可以覆寫`EngagementReachHandler`您子類別 tootell Engagement toouse 中的方法的配置：</span><span class="sxs-lookup"><span data-stu-id="18d04-175">You can override `EngagementReachHandler` methods in your subclass tootell Engagement toouse your layouts :</span></span>

<span data-ttu-id="18d04-176">**範例程式碼：**</span><span class="sxs-lookup"><span data-stu-id="18d04-176">**Sample Code :**</span></span>

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
> <span data-ttu-id="18d04-177">hello`CreateNotification`方法可以傳回 null。</span><span class="sxs-lookup"><span data-stu-id="18d04-177">hello `CreateNotification` method can return null.</span></span> <span data-ttu-id="18d04-178">將不會顯示 hello 通知和 hello 觸達活動皆會予以捨棄。</span><span class="sxs-lookup"><span data-stu-id="18d04-178">hello notification won't be displayed and hello reach campaign will be dropped.</span></span>
> 
> 

<span data-ttu-id="18d04-179">toosimplify 配置實作中，我們也提供自己 xaml，這可以做為基礎的程式碼。</span><span class="sxs-lookup"><span data-stu-id="18d04-179">toosimplify your layout implementation, we also provide our own xaml which can serve as a basis for your code.</span></span> <span data-ttu-id="18d04-180">它們位於 hello Engagement SDK 封存中 (/ src/觸達 /)。</span><span class="sxs-lookup"><span data-stu-id="18d04-180">They are located in hello Engagement SDK archive (/src/reach/).</span></span>

> [!WARNING]
> <span data-ttu-id="18d04-181">我們提供的 hello 我們使用的完全相同的 hello 來源。</span><span class="sxs-lookup"><span data-stu-id="18d04-181">hello sources that we provide are hello exact same ones that we use.</span></span> <span data-ttu-id="18d04-182">因此如果您想 toomodify 它們直接，不要忘記 toochange hello 命名空間並 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="18d04-182">So if you want toomodify them directly, don't forget toochange hello namespace and hello name.</span></span>
> 
> 

### <a name="notification-position"></a><span data-ttu-id="18d04-183">通知的位置</span><span class="sxs-lookup"><span data-stu-id="18d04-183">Notification position</span></span>
<span data-ttu-id="18d04-184">根據預設，應用程式內通知會顯示在 hello 下方左邊 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="18d04-184">By default, an in-app notification is displayed at hello bottom left side of hello application.</span></span> <span data-ttu-id="18d04-185">您可以變更此行為，藉由覆寫 hello`GetNotificationPosition`方法 hello`EngagementReachHandler`物件。</span><span class="sxs-lookup"><span data-stu-id="18d04-185">You can change this behavior by overriding hello `GetNotificationPosition` method of hello `EngagementReachHandler` object.</span></span>

    // In your subclass of EngagementReachHandler

    public override EngagementReachHandler.NotificationPosition GetNotificationPosition(EngagementNotificationViewModel viewModel)
    {
       // return a value of hello EngagementReachHandler.NotificationPosition enum (TOP or BOTTOM)
    }

<span data-ttu-id="18d04-186">目前，您可以選擇 hello `BOTTOM` （預設值） 和`TOP`位置。</span><span class="sxs-lookup"><span data-stu-id="18d04-186">Currently, you can choose between hello `BOTTOM` (default) and `TOP` positions.</span></span>

### <a name="launch-message"></a><span data-ttu-id="18d04-187">啟動訊息</span><span class="sxs-lookup"><span data-stu-id="18d04-187">Launch message</span></span>
<span data-ttu-id="18d04-188">當使用者按一下系統通知 （快顯） 時，Engagement 啟動 hello 應用程式、 hello 負載 hello 內容發送訊息，並顯示 hello 對應活動的 hello 頁面。</span><span class="sxs-lookup"><span data-stu-id="18d04-188">When a user clicks on a system notification (a toast), Engagement launches hello app, load hello content of hello push messages, and display hello page for hello corresponding campaign.</span></span>

<span data-ttu-id="18d04-189">Hello hello 頁面 （取決於網路 hello 速度） 的應用程式和 hello 顯示 hello 啟動會延遲。</span><span class="sxs-lookup"><span data-stu-id="18d04-189">There is a delay between hello launch of hello application and hello display of hello page (depending on hello speed of your network).</span></span>

<span data-ttu-id="18d04-190">項目正在載入的 tooindicate toohello 使用者，您應該提供視覺化的資訊，例如進度列或進度列指示器。</span><span class="sxs-lookup"><span data-stu-id="18d04-190">tooindicate toohello user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="18d04-191">Engagement 無法自行處理這些，但有提供您幾個處理常式。</span><span class="sxs-lookup"><span data-stu-id="18d04-191">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="18d04-192">tooimplement hello 回撥，請執行：</span><span class="sxs-lookup"><span data-stu-id="18d04-192">tooimplement hello callback, do:</span></span>

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

<span data-ttu-id="18d04-193">您可以在設定 hello 回呼您`Application_Launching`方法您`App.xaml.cs`檔案，最好是先 hello`EngagementReach.Instance.Init()`呼叫。</span><span class="sxs-lookup"><span data-stu-id="18d04-193">You can set hello callback in your `Application_Launching` method of your `App.xaml.cs` file, preferably before hello `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="18d04-194">每個處理常式會呼叫 hello UI 執行緒。</span><span class="sxs-lookup"><span data-stu-id="18d04-194">Each handler is called by hello UI Thread.</span></span> <span data-ttu-id="18d04-195">使用 MessageBox 或項目與 UI 相關時，您並沒有 tooworry。</span><span class="sxs-lookup"><span data-stu-id="18d04-195">You do not have tooworry when using a MessageBox or something UI-related.</span></span>
> 
> 

[應用程式原則]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx
[Content Policies]:http://msdn.microsoft.com/library/windows/apps/hh184842(v=vs.105).aspx
[特定應用程式類型的其他需求]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx

