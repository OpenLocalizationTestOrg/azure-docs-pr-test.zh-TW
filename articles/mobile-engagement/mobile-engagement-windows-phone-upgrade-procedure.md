---
title: "aaaWindows Phone Silverlight SDK 升級程序"
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
ms.openlocfilehash: d72e7b8a59ef2c0a95b22efbf1e5257271399ddc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-sdk-upgrade-procedures"></a><span data-ttu-id="66f5b-103">Windows Phone Silverlight SDK 升級程序</span><span class="sxs-lookup"><span data-stu-id="66f5b-103">Windows Phone Silverlight SDK Upgrade Procedures</span></span>
<span data-ttu-id="66f5b-104">如果您已經有整合至您的應用程式較舊版本的我們 SDK，您必須升級 hello SDK 時，下列點 tooconsider hello。</span><span class="sxs-lookup"><span data-stu-id="66f5b-104">If you already have integrated an older version of our SDK into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="66f5b-105">如果您錯過數個版本的 hello SDK 您可能需要指定 toofollow 數個程序。</span><span class="sxs-lookup"><span data-stu-id="66f5b-105">You may have toofollow several procedures if you missed several versions of hello SDK.</span></span> <span data-ttu-id="66f5b-106">例如，如果您從 0.10.1 移轉 too0.11.0 您有遵循 hello toofirst"0.9.0 從 too0.10.1 」 程序然後 hello 」 從 0.10.1 too0.11.0 」 程序。</span><span class="sxs-lookup"><span data-stu-id="66f5b-106">For example if you migrate from 0.10.1 too0.11.0 you have toofirst follow hello "from 0.9.0 too0.10.1" procedure then hello "from 0.10.1 too0.11.0" procedure.</span></span>

## <a name="from-200-too330"></a><span data-ttu-id="66f5b-107">從 2.0.0 too3.3.0</span><span class="sxs-lookup"><span data-stu-id="66f5b-107">From 2.0.0 too3.3.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="66f5b-108">測試記錄檔</span><span class="sxs-lookup"><span data-stu-id="66f5b-108">Test logs</span></span>
<span data-ttu-id="66f5b-109">主控台記錄檔所產生的 hello SDK 現在可以啟用/停用/篩選。</span><span class="sxs-lookup"><span data-stu-id="66f5b-109">Console logs produced by hello SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="66f5b-110">toocustomize，更新 hello 屬性`EngagementAgent.Instance.TestLogEnabled`hello 值可從 hello 的 tooone`EngagementTestLogLevel`列舉型別，例如：</span><span class="sxs-lookup"><span data-stu-id="66f5b-110">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

## <a name="from-111-too200"></a><span data-ttu-id="66f5b-111">從 1.1.1 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="66f5b-111">From 1.1.1 too2.0.0</span></span>
<span data-ttu-id="66f5b-112">hello 下列程式碼說明如何 toomigrate hello Capptain 服務從 SDK 整合提供 Capptain SAS 到由 Azure Mobile Engagement 應用程式。</span><span class="sxs-lookup"><span data-stu-id="66f5b-112">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="66f5b-113">Capptain 和 Mobile Engagement 不是 hello 相同的服務和 hello 下列程序只會反白顯示 toomigrate hello 用戶端應用程式的方式。</span><span class="sxs-lookup"><span data-stu-id="66f5b-113">Capptain and Mobile Engagement are not hello same services and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="66f5b-114">移轉 hello SDK hello 應用程式中的不會移轉您的資料從 hello Capptain 伺服器 toohello Mobile Engagement 伺服器</span><span class="sxs-lookup"><span data-stu-id="66f5b-114">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="66f5b-115">如果您從舊版移轉，請先參閱 hello Capptain 網站 toomigrate too1.1.1 則套用 hello 遵循程序</span><span class="sxs-lookup"><span data-stu-id="66f5b-115">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too1.1.1 first then apply hello following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="66f5b-116">Nuget 封裝</span><span class="sxs-lookup"><span data-stu-id="66f5b-116">Nuget package</span></span>
<span data-ttu-id="66f5b-117">以 **MicrosoftAzure.MobileEngagement** Nuget 套件取代 **Capptain.WindowsPhone**。</span><span class="sxs-lookup"><span data-stu-id="66f5b-117">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="66f5b-118">套用 Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="66f5b-118">Applying Mobile Engagement</span></span>
<span data-ttu-id="66f5b-119">hello SDK 會使用 hello 詞彙`Engagement`。</span><span class="sxs-lookup"><span data-stu-id="66f5b-119">hello SDK uses hello term `Engagement`.</span></span> <span data-ttu-id="66f5b-120">您需要 tooupdate 專案 toomatch 這項變更。</span><span class="sxs-lookup"><span data-stu-id="66f5b-120">You need tooupdate your project toomatch this change.</span></span>

<span data-ttu-id="66f5b-121">您需要 toouninstall 目前 Capptain nuget 套件。</span><span class="sxs-lookup"><span data-stu-id="66f5b-121">You need toouninstall your current Capptain nuget package.</span></span> <span data-ttu-id="66f5b-122">請考慮您在 [Capptain Resources] 資料夾中所有的變更將會移除。</span><span class="sxs-lookup"><span data-stu-id="66f5b-122">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="66f5b-123">如果您要 tookeep 那些檔案，請建立一份。</span><span class="sxs-lookup"><span data-stu-id="66f5b-123">If you want tookeep those files then make a copy of them.</span></span>

<span data-ttu-id="66f5b-124">之後，請在您的專案上安裝 hello 新 Microsoft Azure Engagement nuget 封裝。</span><span class="sxs-lookup"><span data-stu-id="66f5b-124">After that, install hello new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="66f5b-125">您可以直接在 [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement)上找到。</span><span class="sxs-lookup"><span data-stu-id="66f5b-125">You can find it directly on [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span></span> <span data-ttu-id="66f5b-126">這個動作會取代所有的資源檔案由參與，並將新 Engagement DLL tooyour hello 專案參考。</span><span class="sxs-lookup"><span data-stu-id="66f5b-126">This action replaces all resources files used by Engagement and adds hello new Engagement DLL tooyour project References.</span></span>

<span data-ttu-id="66f5b-127">您的 tooclean 您的專案參考刪除 Capptain DLL 的參考。</span><span class="sxs-lookup"><span data-stu-id="66f5b-127">You have tooclean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="66f5b-128">如果不這樣做，Capptain hello 版本會發生衝突，會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="66f5b-128">If you do not make this, hello version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="66f5b-129">如果您已自訂 Capptain 資源，複製舊的檔案內容，並將它們貼在 hello 新 Engagement 檔案中。</span><span class="sxs-lookup"><span data-stu-id="66f5b-129">If you have customized Capptain resources, copy your old files content and paste them in hello new Engagement files.</span></span> <span data-ttu-id="66f5b-130">請注意，xaml 和 cs 檔案有 toobe 更新。</span><span class="sxs-lookup"><span data-stu-id="66f5b-130">Please note that both xaml and cs files have toobe updated.</span></span>

<span data-ttu-id="66f5b-131">這些步驟都完成之後，您只需要由 hello 新 Engagement 參考 tooreplace 舊 Capptain 參考。</span><span class="sxs-lookup"><span data-stu-id="66f5b-131">When those steps are completed you only have tooreplace old Capptain references by hello new Engagement references.</span></span>

1. <span data-ttu-id="66f5b-132">所有 Capptain 命名空間都有 toobe 更新。</span><span class="sxs-lookup"><span data-stu-id="66f5b-132">All Capptain namespaces have toobe updated.</span></span>
   
    <span data-ttu-id="66f5b-133">移轉前：</span><span class="sxs-lookup"><span data-stu-id="66f5b-133">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="66f5b-134">移轉後：</span><span class="sxs-lookup"><span data-stu-id="66f5b-134">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="66f5b-135">所有包含 "Capptain" 的 Capptain 類別應該要包含 "Engagement"。</span><span class="sxs-lookup"><span data-stu-id="66f5b-135">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="66f5b-136">移轉前：</span><span class="sxs-lookup"><span data-stu-id="66f5b-136">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="66f5b-137">移轉後：</span><span class="sxs-lookup"><span data-stu-id="66f5b-137">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="66f5b-138">對於 xaml 檔案，Capptain 命名空間和屬性也會變更。</span><span class="sxs-lookup"><span data-stu-id="66f5b-138">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="66f5b-139">移轉前：</span><span class="sxs-lookup"><span data-stu-id="66f5b-139">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="66f5b-140">移轉後：</span><span class="sxs-lookup"><span data-stu-id="66f5b-140">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="66f5b-141">Hello 的其他資源，例如 Capptain 圖片，請注意，它們也已重新命名的 toouse 「 參與 」。</span><span class="sxs-lookup"><span data-stu-id="66f5b-141">For hello other resources like Capptain pictures, please note that they also have been renamed toouse "Engagement".</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="66f5b-142">應用程式 ID / SDK 金鑰</span><span class="sxs-lookup"><span data-stu-id="66f5b-142">Application ID / SDK Key</span></span>
<span data-ttu-id="66f5b-143">Engagement 使用連接字串。</span><span class="sxs-lookup"><span data-stu-id="66f5b-143">Engagement uses a connection string.</span></span> <span data-ttu-id="66f5b-144">您沒有 toospecify 應用程式識別碼和與 Mobile Engagement SDK 金鑰，您只需要 toospecify 連接字串。</span><span class="sxs-lookup"><span data-stu-id="66f5b-144">You don't have toospecify an application ID and an SDK key with Mobile Engagement, you only have toospecify a connection string.</span></span> <span data-ttu-id="66f5b-145">您可以在您的 EngagementConfiguration 檔案中設定它。</span><span class="sxs-lookup"><span data-stu-id="66f5b-145">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="66f5b-146">hello Engagement 組態可以設定您`Resources\EngagementConfiguration.xml`專案檔。</span><span class="sxs-lookup"><span data-stu-id="66f5b-146">hello Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="66f5b-147">編輯此檔案 toospecify:</span><span class="sxs-lookup"><span data-stu-id="66f5b-147">Edit this file toospecify:</span></span>

* <span data-ttu-id="66f5b-148">應用程式在 `<connectionString>` 和 `<\connectionString>` 標記之間的連接字串。</span><span class="sxs-lookup"><span data-stu-id="66f5b-148">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="66f5b-149">如果您想要在執行階段相反地，您可以呼叫 hello 下列 toospecify hello Engagement 代理程式初始化之前的方法：</span><span class="sxs-lookup"><span data-stu-id="66f5b-149">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Initialize Engagement angent with above configuration. */
        EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="66f5b-150">您的應用程式的 hello 連接字串會顯示在 [hello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="66f5b-150">hello connection string for your application is displayed in hello Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="66f5b-151">項目名稱變更</span><span class="sxs-lookup"><span data-stu-id="66f5b-151">Items name change</span></span>
<span data-ttu-id="66f5b-152">所有名為 capptain 的項目已命名為 engagement。</span><span class="sxs-lookup"><span data-stu-id="66f5b-152">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="66f5b-153">同樣地針對*Capptain*太*Engagement*。</span><span class="sxs-lookup"><span data-stu-id="66f5b-153">Similarly for *Capptain* too*Engagement*.</span></span>

<span data-ttu-id="66f5b-154">常用 Capptain 項目的範例：</span><span class="sxs-lookup"><span data-stu-id="66f5b-154">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="66f5b-155">CapptainConfiguration 現在名為 EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="66f5b-155">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="66f5b-156">CapptainAgent 現在名為 EngagementAgent</span><span class="sxs-lookup"><span data-stu-id="66f5b-156">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="66f5b-157">CapptainReach 現在名為 EngagementReach</span><span class="sxs-lookup"><span data-stu-id="66f5b-157">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="66f5b-158">CapptainHttpConfig 現在名為 EngagementHttpConfig</span><span class="sxs-lookup"><span data-stu-id="66f5b-158">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="66f5b-159">GetCapptainPageName 現在名為 GetEngagementPageName</span><span class="sxs-lookup"><span data-stu-id="66f5b-159">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="66f5b-160">請注意，重新命名也會影響覆寫方法。</span><span class="sxs-lookup"><span data-stu-id="66f5b-160">Note that rename also affects overridden methods.</span></span>

