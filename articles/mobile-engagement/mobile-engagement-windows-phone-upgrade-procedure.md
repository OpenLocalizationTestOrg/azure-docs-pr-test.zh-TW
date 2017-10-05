---
title: "Windows Phone Silverlight SDK 升級程序"
description: "Azure Mobile Engagement 的 Windows Phone Silverlight SDK 升級程序"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 87130026-9759-4659-9184-788a3627a165
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f87f65788075c7f4067e77946e1bcbc8f3709317
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="windows-phone-silverlight-sdk-upgrade-procedures"></a><span data-ttu-id="5bc97-103">Windows Phone Silverlight SDK 升級程序</span><span class="sxs-lookup"><span data-stu-id="5bc97-103">Windows Phone Silverlight SDK Upgrade Procedures</span></span>
<span data-ttu-id="5bc97-104">如果您已經整合我們的舊版 SDK 到您的應用程式，在升級 SDK 時您必須考慮以下幾點。</span><span class="sxs-lookup"><span data-stu-id="5bc97-104">If you already have integrated an older version of our SDK into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="5bc97-105">如果您有錯過幾個版本的 SDK，您必須遵循幾個步驟。</span><span class="sxs-lookup"><span data-stu-id="5bc97-105">You may have to follow several procedures if you missed several versions of the SDK.</span></span> <span data-ttu-id="5bc97-106">例如，如果您要從 0.10.1 移轉到 0.11.0，必須先遵循「從 0.9.0 到 0.10.1」的程序，然後「從 0.10.1 到 0.11.0」的程序。</span><span class="sxs-lookup"><span data-stu-id="5bc97-106">For example if you migrate from 0.10.1 to 0.11.0 you have to first follow the "from 0.9.0 to 0.10.1" procedure then the "from 0.10.1 to 0.11.0" procedure.</span></span>

## <a name="from-200-to-330"></a><span data-ttu-id="5bc97-107">從 2.0.0 到 3.3.0</span><span class="sxs-lookup"><span data-stu-id="5bc97-107">From 2.0.0 to 3.3.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="5bc97-108">測試記錄檔</span><span class="sxs-lookup"><span data-stu-id="5bc97-108">Test logs</span></span>
<span data-ttu-id="5bc97-109">SDK 所產生的主控台記錄檔現在可以啟用/停用/篩選。</span><span class="sxs-lookup"><span data-stu-id="5bc97-109">Console logs produced by the SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="5bc97-110">若要自訂這種情況，請將屬性 `EngagementAgent.Instance.TestLogEnabled` 更新為 `EngagementTestLogLevel` 列舉的其中一個可用值，例如︰</span><span class="sxs-lookup"><span data-stu-id="5bc97-110">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

## <a name="from-111-to-200"></a><span data-ttu-id="5bc97-111">從 1.1.1 到 2.0.0</span><span class="sxs-lookup"><span data-stu-id="5bc97-111">From 1.1.1 to 2.0.0</span></span>
<span data-ttu-id="5bc97-112">以下說明如何將 SDK 整合從 Capptain SAS 提供的 Capptain 服務，移轉到由 Azure Mobile Engagement 提供的應用程式內。</span><span class="sxs-lookup"><span data-stu-id="5bc97-112">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="5bc97-113">Capptain 和 Mobile Engagement 是不同的服務，而以下程序只適用於移轉用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="5bc97-113">Capptain and Mobile Engagement are not the same services and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="5bc97-114">移轉應用程式中的 SDK「不會」將您的資料從 Capptain 伺服器移轉到 Mobile Engagement 伺服器</span><span class="sxs-lookup"><span data-stu-id="5bc97-114">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="5bc97-115">如果您要從舊版移轉，請先參閱 Capptain 網站以移轉到 1.1.1，然後再遵循以下程序</span><span class="sxs-lookup"><span data-stu-id="5bc97-115">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 1.1.1 first then apply the following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="5bc97-116">Nuget 封裝</span><span class="sxs-lookup"><span data-stu-id="5bc97-116">Nuget package</span></span>
<span data-ttu-id="5bc97-117">以 **MicrosoftAzure.MobileEngagement** Nuget 套件取代 **Capptain.WindowsPhone**。</span><span class="sxs-lookup"><span data-stu-id="5bc97-117">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="5bc97-118">套用 Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="5bc97-118">Applying Mobile Engagement</span></span>
<span data-ttu-id="5bc97-119">SDK 使用 `Engagement`一詞。</span><span class="sxs-lookup"><span data-stu-id="5bc97-119">The SDK uses the term `Engagement`.</span></span> <span data-ttu-id="5bc97-120">您需要更新您的專案，以符合此變更。</span><span class="sxs-lookup"><span data-stu-id="5bc97-120">You need to update your project to match this change.</span></span>

<span data-ttu-id="5bc97-121">您需要解除安裝目前的 Capptain nuget 封裝。</span><span class="sxs-lookup"><span data-stu-id="5bc97-121">You need to uninstall your current Capptain nuget package.</span></span> <span data-ttu-id="5bc97-122">請考慮您在 [Capptain Resources] 資料夾中所有的變更將會移除。</span><span class="sxs-lookup"><span data-stu-id="5bc97-122">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="5bc97-123">如果您想要保留這些檔案，請將它們複製一份。</span><span class="sxs-lookup"><span data-stu-id="5bc97-123">If you want to keep those files then make a copy of them.</span></span>

<span data-ttu-id="5bc97-124">接下來，在您的專案上安裝新的 Microsoft Azure Engagement nuget 封裝。</span><span class="sxs-lookup"><span data-stu-id="5bc97-124">After that, install the new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="5bc97-125">您可以直接在 [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement)上找到。</span><span class="sxs-lookup"><span data-stu-id="5bc97-125">You can find it directly on [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span></span> <span data-ttu-id="5bc97-126">此動作會取代所有 Engagement 使用的資源檔，並將新的 Engagement DLL 新增到您專案的「參考」。</span><span class="sxs-lookup"><span data-stu-id="5bc97-126">This action replaces all resources files used by Engagement and adds the new Engagement DLL to your project References.</span></span>

<span data-ttu-id="5bc97-127">您必須刪除 Capptain DLL 參考來清除您專案的參考。</span><span class="sxs-lookup"><span data-stu-id="5bc97-127">You have to clean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="5bc97-128">如果沒有這樣做，Capptain 的版本會有衝突並發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="5bc97-128">If you do not make this, the version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="5bc97-129">若您有自訂的 Capptain 資源，請複製您舊檔案的內容，並在新的 Engagement 檔案中貼上它們。</span><span class="sxs-lookup"><span data-stu-id="5bc97-129">If you have customized Capptain resources, copy your old files content and paste them in the new Engagement files.</span></span> <span data-ttu-id="5bc97-130">請注意，xaml 和 cs 檔案兩者都必須更新。</span><span class="sxs-lookup"><span data-stu-id="5bc97-130">Please note that both xaml and cs files have to be updated.</span></span>

<span data-ttu-id="5bc97-131">完成這些步驟之後，您只需要用新的 Engagement 參考取代舊的 Capptain 參考。</span><span class="sxs-lookup"><span data-stu-id="5bc97-131">When those steps are completed you only have to replace old Capptain references by the new Engagement references.</span></span>

1. <span data-ttu-id="5bc97-132">所有的 Capptain 命名空間都必須更新。</span><span class="sxs-lookup"><span data-stu-id="5bc97-132">All Capptain namespaces have to be updated.</span></span>
   
    <span data-ttu-id="5bc97-133">移轉前：</span><span class="sxs-lookup"><span data-stu-id="5bc97-133">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="5bc97-134">移轉後：</span><span class="sxs-lookup"><span data-stu-id="5bc97-134">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="5bc97-135">所有包含 "Capptain" 的 Capptain 類別應該要包含 "Engagement"。</span><span class="sxs-lookup"><span data-stu-id="5bc97-135">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="5bc97-136">移轉前：</span><span class="sxs-lookup"><span data-stu-id="5bc97-136">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="5bc97-137">移轉後：</span><span class="sxs-lookup"><span data-stu-id="5bc97-137">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="5bc97-138">對於 xaml 檔案，Capptain 命名空間和屬性也會變更。</span><span class="sxs-lookup"><span data-stu-id="5bc97-138">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="5bc97-139">移轉前：</span><span class="sxs-lookup"><span data-stu-id="5bc97-139">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="5bc97-140">移轉後：</span><span class="sxs-lookup"><span data-stu-id="5bc97-140">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="5bc97-141">針對其他資源，例如 Capptain 圖片，請注意它們也已重新命名使用 "Engagement"。</span><span class="sxs-lookup"><span data-stu-id="5bc97-141">For the other resources like Capptain pictures, please note that they also have been renamed to use "Engagement".</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="5bc97-142">應用程式 ID / SDK 金鑰</span><span class="sxs-lookup"><span data-stu-id="5bc97-142">Application ID / SDK Key</span></span>
<span data-ttu-id="5bc97-143">Engagement 使用連接字串。</span><span class="sxs-lookup"><span data-stu-id="5bc97-143">Engagement uses a connection string.</span></span> <span data-ttu-id="5bc97-144">您不需要為 Mobile Engagement 指定應用程式 ID 和 SDK 金鑰，您只需要指定連接字串。</span><span class="sxs-lookup"><span data-stu-id="5bc97-144">You don't have to specify an application ID and an SDK key with Mobile Engagement, you only have to specify a connection string.</span></span> <span data-ttu-id="5bc97-145">您可以在您的 EngagementConfiguration 檔案中設定它。</span><span class="sxs-lookup"><span data-stu-id="5bc97-145">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="5bc97-146">您可以在專案的 `Resources\EngagementConfiguration.xml` 檔案中設定 Engagement 組態。</span><span class="sxs-lookup"><span data-stu-id="5bc97-146">The Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="5bc97-147">編輯此檔案來指定：</span><span class="sxs-lookup"><span data-stu-id="5bc97-147">Edit this file to specify:</span></span>

* <span data-ttu-id="5bc97-148">應用程式在 `<connectionString>` 和 `<\connectionString>` 標記之間的連接字串。</span><span class="sxs-lookup"><span data-stu-id="5bc97-148">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="5bc97-149">若想要改為在執行階段指定它，您可以在 Engagement 代理程式初始化之前呼叫下列方法：</span><span class="sxs-lookup"><span data-stu-id="5bc97-149">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Initialize Engagement angent with above configuration. */
        EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="5bc97-150">應用程式的連接字串會顯示在 Azure 傳統入口網站中。</span><span class="sxs-lookup"><span data-stu-id="5bc97-150">The connection string for your application is displayed in the Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="5bc97-151">項目名稱變更</span><span class="sxs-lookup"><span data-stu-id="5bc97-151">Items name change</span></span>
<span data-ttu-id="5bc97-152">所有名為 capptain 的項目已命名為 engagement。</span><span class="sxs-lookup"><span data-stu-id="5bc97-152">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="5bc97-153">同樣地，Capptain 也已命名為 Engagement。</span><span class="sxs-lookup"><span data-stu-id="5bc97-153">Similarly for *Capptain* to *Engagement*.</span></span>

<span data-ttu-id="5bc97-154">常用 Capptain 項目的範例：</span><span class="sxs-lookup"><span data-stu-id="5bc97-154">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="5bc97-155">CapptainConfiguration 現在名為 EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="5bc97-155">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="5bc97-156">CapptainAgent 現在名為 EngagementAgent</span><span class="sxs-lookup"><span data-stu-id="5bc97-156">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="5bc97-157">CapptainReach 現在名為 EngagementReach</span><span class="sxs-lookup"><span data-stu-id="5bc97-157">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="5bc97-158">CapptainHttpConfig 現在名為 EngagementHttpConfig</span><span class="sxs-lookup"><span data-stu-id="5bc97-158">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="5bc97-159">GetCapptainPageName 現在名為 GetEngagementPageName</span><span class="sxs-lookup"><span data-stu-id="5bc97-159">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="5bc97-160">請注意，重新命名也會影響覆寫方法。</span><span class="sxs-lookup"><span data-stu-id="5bc97-160">Note that rename also affects overridden methods.</span></span>

