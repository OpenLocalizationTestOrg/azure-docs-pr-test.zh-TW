---
title: "新的 Azure Application Insights 資源 aaaCreate |Microsoft 文件"
description: "針對新的即時應用程式手動設定 Application Insights 監視。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 878b007e-161c-4e36-8ab2-3d7047d8a92d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: bwren
ms.openlocfilehash: 3aba7045e1f8fe43d473f0be01dd52106ab992a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-insights-resource"></a><span data-ttu-id="4b640-103">建立 Application Insights 資源</span><span class="sxs-lookup"><span data-stu-id="4b640-103">Create an Application Insights resource</span></span>
<span data-ttu-id="4b640-104">Azure Application Insights 會在 Microsoft Azure「資源」中顯示您應用程式的相關資料。</span><span class="sxs-lookup"><span data-stu-id="4b640-104">Azure Application Insights displays data about your application in a Microsoft Azure *resource*.</span></span> <span data-ttu-id="4b640-105">建立新的資源屬於因此[新的應用程式設定 Application Insights toomonitor][start]。</span><span class="sxs-lookup"><span data-stu-id="4b640-105">Creating a new resource is therefore part of [setting up Application Insights toomonitor a new application][start].</span></span> <span data-ttu-id="4b640-106">在許多情況下，建立資源即可自動 hello IDE。</span><span class="sxs-lookup"><span data-stu-id="4b640-106">In many cases, creating a resource can be done automatically by hello IDE.</span></span> <span data-ttu-id="4b640-107">但在某些情況下，您手動建立資源-toohave 進行開發和生產環境的個別資源，例如建置應用程式。</span><span class="sxs-lookup"><span data-stu-id="4b640-107">But in some cases, you create a resource manually - for example, toohave separate resources for development and production builds of your application.</span></span>

<span data-ttu-id="4b640-108">建立 hello 資源之後，您會取得其檢測金鑰，並使用該 tooconfigure hello SDK hello 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="4b640-108">After you have created hello resource, you get its instrumentation key and use that tooconfigure hello SDK in hello application.</span></span> <span data-ttu-id="4b640-109">hello 資源的索引鍵連結 hello 遙測 toohello 資源。</span><span class="sxs-lookup"><span data-stu-id="4b640-109">hello resource key links hello telemetry toohello resource.</span></span>

## <a name="sign-up-toomicrosoft-azure"></a><span data-ttu-id="4b640-110">註冊 Azure tooMicrosoft</span><span class="sxs-lookup"><span data-stu-id="4b640-110">Sign up tooMicrosoft Azure</span></span>
<span data-ttu-id="4b640-111">如果您還沒有 [Microsoft 帳戶，請立即申請](http://live.com)。</span><span class="sxs-lookup"><span data-stu-id="4b640-111">If you haven't got a [Microsoft account, get one now](http://live.com).</span></span> <span data-ttu-id="4b640-112">(如果您使用 Outlook.com、OneDrive、Windows Phone 或 XBox Live 等服務，就會有 Microsoft 帳戶)。</span><span class="sxs-lookup"><span data-stu-id="4b640-112">(If you use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, you already have a Microsoft account.)</span></span>

<span data-ttu-id="4b640-113">您也需要訂用帳戶太[Microsoft Azure](http://azure.com)。</span><span class="sxs-lookup"><span data-stu-id="4b640-113">You also need a subscription too[Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="4b640-114">如果您的小組或組織有 Azure 訂用帳戶，hello 擁有者可以將您加入 tooit，使用您的 Windows Live id。</span><span class="sxs-lookup"><span data-stu-id="4b640-114">If your team or organization has an Azure subscription, hello owner can add you tooit, using your Windows Live ID.</span></span> <span data-ttu-id="4b640-115">您只需針對使用的項目付費。</span><span class="sxs-lookup"><span data-stu-id="4b640-115">You're only charged for what you use.</span></span> <span data-ttu-id="4b640-116">hello 基本計劃可讓您免費的實驗使用數量。</span><span class="sxs-lookup"><span data-stu-id="4b640-116">hello default basic plan allows for a certain amount of experimental use free of charge.</span></span>

<span data-ttu-id="4b640-117">當您有存取 tooa 訂用帳戶時，登入在 tooApplication Insights [http://portal.azure.com](https://portal.azure.com)，並使用您的 Live ID toologin。</span><span class="sxs-lookup"><span data-stu-id="4b640-117">When you've got access tooa subscription, log in tooApplication Insights at [http://portal.azure.com](https://portal.azure.com), and use your Live ID toologin.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="4b640-118">建立 Application Insights 資源</span><span class="sxs-lookup"><span data-stu-id="4b640-118">Create an Application Insights resource</span></span>
<span data-ttu-id="4b640-119">在 hello [portal.azure.com](https://portal.azure.com)，加入 Application Insights 資源：</span><span class="sxs-lookup"><span data-stu-id="4b640-119">In hello [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![按一下 新增，然後按一下Application Insights](./media/app-insights-create-new-resource/01-new.png)

* <span data-ttu-id="4b640-121">**應用程式類型**會影響您在 hello 概觀刀鋒視窗，然後 hello 中可用的屬性上看到[度量總管][metrics]。</span><span class="sxs-lookup"><span data-stu-id="4b640-121">**Application type** affects what you see on hello overview blade and hello properties available in [metric explorer][metrics].</span></span> <span data-ttu-id="4b640-122">如果沒有看到您的應用程式類型，請選擇 [一般]。</span><span class="sxs-lookup"><span data-stu-id="4b640-122">If you don't see your type of app, choose General.</span></span>
* <span data-ttu-id="4b640-123">**訂用帳戶** 是您在 Azure 中的付款帳戶。</span><span class="sxs-lookup"><span data-stu-id="4b640-123">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="4b640-124">**資源群組** 可讓您輕鬆管理屬性，例如存取控制。</span><span class="sxs-lookup"><span data-stu-id="4b640-124">**Resource group** is a convenience for managing properties like access control.</span></span> <span data-ttu-id="4b640-125">如果您已經建立其他 Azure 資源，您可以選擇 tooput 這個新的資源中 hello 相同的群組。</span><span class="sxs-lookup"><span data-stu-id="4b640-125">If you have already created other Azure resources, you can choose tooput this new resource in hello same group.</span></span>
* <span data-ttu-id="4b640-126">**位置** 是我們保留您資料的地方。</span><span class="sxs-lookup"><span data-stu-id="4b640-126">**Location** is where we keep your data.</span></span>
* <span data-ttu-id="4b640-127">**Pin toodashboard**可以在 Azure 首頁上放置快速存取磚以取得您的資源。</span><span class="sxs-lookup"><span data-stu-id="4b640-127">**Pin toodashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> <span data-ttu-id="4b640-128">建議使用。</span><span class="sxs-lookup"><span data-stu-id="4b640-128">Recommended.</span></span>

<span data-ttu-id="4b640-129">建立您的應用程式後，會開啟新的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="4b640-129">When your app has been created, a new blade opens.</span></span> <span data-ttu-id="4b640-130">此刀鋒視窗是您會在其中看到應用程式的效能和使用情況資料的位置。</span><span class="sxs-lookup"><span data-stu-id="4b640-130">This blade is where you see performance and usage data about your app.</span></span> 

<span data-ttu-id="4b640-131">tooget 後 tooit 下次您登入 tooAzure，尋找您的應用程式快速入門圖格上 hello 開始面板 （主畫面）。</span><span class="sxs-lookup"><span data-stu-id="4b640-131">tooget back tooit next time you log in tooAzure, look for your app's quick-start tile on hello start board (home screen).</span></span> <span data-ttu-id="4b640-132">或按一下瀏覽 toofind 它。</span><span class="sxs-lookup"><span data-stu-id="4b640-132">Or click Browse toofind it.</span></span>

## <a name="copy-hello-instrumentation-key"></a><span data-ttu-id="4b640-133">複製 hello 檢測金鑰</span><span class="sxs-lookup"><span data-stu-id="4b640-133">Copy hello instrumentation key</span></span>
<span data-ttu-id="4b640-134">hello 檢測金鑰會識別您所建立的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="4b640-134">hello instrumentation key identifies hello resource that you created.</span></span> <span data-ttu-id="4b640-135">您需要 toogive toohello SDK。</span><span class="sxs-lookup"><span data-stu-id="4b640-135">You need it toogive toohello SDK.</span></span>

![按一下 Essentials，請按一下 hello 檢測金鑰 CTRL + C](./media/app-insights-create-new-resource/02-props.png)

## <a name="install-hello-sdk-in-your-app"></a><span data-ttu-id="4b640-137">安裝應用程式中的 hello SDK</span><span class="sxs-lookup"><span data-stu-id="4b640-137">Install hello SDK in your app</span></span>
<span data-ttu-id="4b640-138">安裝應用程式中的 hello Application Insights SDK。</span><span class="sxs-lookup"><span data-stu-id="4b640-138">Install hello Application Insights SDK in your app.</span></span> <span data-ttu-id="4b640-139">此步驟中有很大取決於您的應用程式的 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="4b640-139">This step depends heavily on hello type of your application.</span></span> 

<span data-ttu-id="4b640-140">使用 hello 檢測金鑰 tooconfigure [hello 您安裝應用程式中的 SDK][start]。</span><span class="sxs-lookup"><span data-stu-id="4b640-140">Use hello instrumentation key tooconfigure [hello SDK that you install in your application][start].</span></span>

<span data-ttu-id="4b640-141">hello SDK 包含標準不需要您 toowrite 任何程式碼傳送遙測的模組。</span><span class="sxs-lookup"><span data-stu-id="4b640-141">hello SDK includes standard modules that send telemetry without you having toowrite any code.</span></span> <span data-ttu-id="4b640-142">tootrack 使用者動作或診斷問題的詳細資料，[使用 hello API] [ api] toosend 您自己的遙測。</span><span class="sxs-lookup"><span data-stu-id="4b640-142">tootrack user actions or diagnose issues in more detail, [use hello API][api] toosend your own telemetry.</span></span>

## <span data-ttu-id="4b640-143"><a name="monitor"></a>查看遙測資料</span><span class="sxs-lookup"><span data-stu-id="4b640-143"><a name="monitor"></a>See telemetry data</span></span>
<span data-ttu-id="4b640-144">關閉 hello 快速啟動刀鋒視窗 tooreturn tooyour 應用程式 刀鋒視窗中 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="4b640-144">Close hello quick start blade tooreturn tooyour application blade in hello Azure portal.</span></span>

<span data-ttu-id="4b640-145">按一下 hello 搜尋磚 toosee[診斷搜尋][diagnostic]、 hello 第一個事件的出現位置。</span><span class="sxs-lookup"><span data-stu-id="4b640-145">Click hello Search tile toosee [Diagnostic Search][diagnostic], where hello first events appear.</span></span> 

<span data-ttu-id="4b640-146">如果您預期有更多資料，請在幾秒之後按一下 [重新整理]。</span><span class="sxs-lookup"><span data-stu-id="4b640-146">If you're expecting more data, click **Refresh** after a few seconds  .</span></span>

## <a name="creating-a-resource-automatically"></a><span data-ttu-id="4b640-147">自動建立資源</span><span class="sxs-lookup"><span data-stu-id="4b640-147">Creating a resource automatically</span></span>
<span data-ttu-id="4b640-148">您可以撰寫[PowerShell 指令碼](app-insights-powershell.md)toocreate 資源自動。</span><span class="sxs-lookup"><span data-stu-id="4b640-148">You can write a [PowerShell script](app-insights-powershell.md) toocreate a resource automatically.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b640-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4b640-149">Next steps</span></span>
* [<span data-ttu-id="4b640-150">建立儀表板</span><span class="sxs-lookup"><span data-stu-id="4b640-150">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="4b640-151">診斷搜尋</span><span class="sxs-lookup"><span data-stu-id="4b640-151">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="4b640-152">探索度量</span><span class="sxs-lookup"><span data-stu-id="4b640-152">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="4b640-153">撰寫分析查詢</span><span class="sxs-lookup"><span data-stu-id="4b640-153">Write Analytics queries</span></span>](app-insights-analytics.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[diagnostic]: app-insights-diagnostic-search.md
[metrics]: app-insights-metrics-explorer.md
[start]: app-insights-overview.md

