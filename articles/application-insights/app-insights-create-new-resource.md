---
title: "建立新的 Azure Application Insights 資源 | Microsoft Docs"
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
ms.openlocfilehash: 5f8814ee943424c1c278ab3732129d4459f83819
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-insights-resource"></a><span data-ttu-id="fe7b6-103">建立 Application Insights 資源</span><span class="sxs-lookup"><span data-stu-id="fe7b6-103">Create an Application Insights resource</span></span>
<span data-ttu-id="fe7b6-104">Azure Application Insights 會在 Microsoft Azure「資源」中顯示您應用程式的相關資料。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-104">Azure Application Insights displays data about your application in a Microsoft Azure *resource*.</span></span> <span data-ttu-id="fe7b6-105">因此，建立新的資源是屬於[設定 Application Insights 以監視新應用程式][start]的一環。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-105">Creating a new resource is therefore part of [setting up Application Insights to monitor a new application][start].</span></span> <span data-ttu-id="fe7b6-106">在許多情況下，建立資源可以由 IDE 自動完成。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-106">In many cases, creating a resource can be done automatically by the IDE.</span></span> <span data-ttu-id="fe7b6-107">但在某些情況下，您需要手動建立資源 - 例如，讓應用程式的開發和生產組建有各自可用的資源。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-107">But in some cases, you create a resource manually - for example, to have separate resources for development and production builds of your application.</span></span>

<span data-ttu-id="fe7b6-108">建立資源後，您會取得其檢測金鑰，並將該金鑰用來設定應用程式中的 SDK。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-108">After you have created the resource, you get its instrumentation key and use that to configure the SDK in the application.</span></span> <span data-ttu-id="fe7b6-109">資源索引鍵會將遙測連結到資源。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-109">The resource key links the telemetry to the resource.</span></span>

## <a name="sign-up-to-microsoft-azure"></a><span data-ttu-id="fe7b6-110">註冊 Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="fe7b6-110">Sign up to Microsoft Azure</span></span>
<span data-ttu-id="fe7b6-111">如果您還沒有 [Microsoft 帳戶，請立即申請](http://live.com)。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-111">If you haven't got a [Microsoft account, get one now](http://live.com).</span></span> <span data-ttu-id="fe7b6-112">(如果您使用 Outlook.com、OneDrive、Windows Phone 或 XBox Live 等服務，就會有 Microsoft 帳戶)。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-112">(If you use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, you already have a Microsoft account.)</span></span>

<span data-ttu-id="fe7b6-113">此外您也需要 [Microsoft Azure](http://azure.com) 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-113">You also need a subscription to [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="fe7b6-114">如果您的小組或組織擁有 Azure 訂用帳戶，則擁有者就可以使用您的 Windows Live ID 將您加入該訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-114">If your team or organization has an Azure subscription, the owner can add you to it, using your Windows Live ID.</span></span> <span data-ttu-id="fe7b6-115">您只需針對使用的項目付費。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-115">You're only charged for what you use.</span></span> <span data-ttu-id="fe7b6-116">預設的基本方案有一定的免費數量可作為實驗用途。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-116">The default basic plan allows for a certain amount of experimental use free of charge.</span></span>

<span data-ttu-id="fe7b6-117">當您可以存取訂用帳戶時，請在 [http://portal.azure.com](https://portal.azure.com) 中使用您的 Live ID 登入 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-117">When you've got access to a subscription, log in to Application Insights at [http://portal.azure.com](https://portal.azure.com), and use your Live ID to login.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="fe7b6-118">建立 Application Insights 資源</span><span class="sxs-lookup"><span data-stu-id="fe7b6-118">Create an Application Insights resource</span></span>
<span data-ttu-id="fe7b6-119">在 [portal.azure.com](https://portal.azure.com)中新增 Application Insights 資源：</span><span class="sxs-lookup"><span data-stu-id="fe7b6-119">In the [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![按一下 [新增]，然後按一下 [Application Insights]](./media/app-insights-create-new-resource/01-new.png)

* <span data-ttu-id="fe7b6-121">**應用程式類型**會影響您在 [概觀] 刀鋒視窗中看到的內容，以及[計量瀏覽器][metrics]中提供的屬性。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-121">**Application type** affects what you see on the overview blade and the properties available in [metric explorer][metrics].</span></span> <span data-ttu-id="fe7b6-122">如果沒有看到您的應用程式類型，請選擇 [一般]。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-122">If you don't see your type of app, choose General.</span></span>
* <span data-ttu-id="fe7b6-123">**訂用帳戶** 是您在 Azure 中的付款帳戶。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-123">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="fe7b6-124">**資源群組** 可讓您輕鬆管理屬性，例如存取控制。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-124">**Resource group** is a convenience for managing properties like access control.</span></span> <span data-ttu-id="fe7b6-125">如果您已經建立其他 Azure 資源，可以選擇將這個新的資源放到同一個群組。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-125">If you have already created other Azure resources, you can choose to put this new resource in the same group.</span></span>
* <span data-ttu-id="fe7b6-126">**位置** 是我們保留您資料的地方。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-126">**Location** is where we keep your data.</span></span>
* <span data-ttu-id="fe7b6-127">**釘選到儀表板板** 可在 Azure 首頁上放置資源的快速存取圖格。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-127">**Pin to dashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> <span data-ttu-id="fe7b6-128">建議使用。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-128">Recommended.</span></span>

<span data-ttu-id="fe7b6-129">建立您的應用程式後，會開啟新的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-129">When your app has been created, a new blade opens.</span></span> <span data-ttu-id="fe7b6-130">此刀鋒視窗是您會在其中看到應用程式的效能和使用情況資料的位置。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-130">This blade is where you see performance and usage data about your app.</span></span> 

<span data-ttu-id="fe7b6-131">若要在下次登入 Azure 時返回該應用程式，請在開始面板 (主畫面) 上尋找應用程式的快速啟動圖格。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-131">To get back to it next time you log in to Azure, look for your app's quick-start tile on the start board (home screen).</span></span> <span data-ttu-id="fe7b6-132">或按一下 [瀏覽] 以尋找它。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-132">Or click Browse to find it.</span></span>

## <a name="copy-the-instrumentation-key"></a><span data-ttu-id="fe7b6-133">複製檢測金鑰</span><span class="sxs-lookup"><span data-stu-id="fe7b6-133">Copy the instrumentation key</span></span>
<span data-ttu-id="fe7b6-134">檢測金鑰會識別您所建立的資源。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-134">The instrumentation key identifies the resource that you created.</span></span> <span data-ttu-id="fe7b6-135">您需要它以提供給 SDK。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-135">You need it to give to the SDK.</span></span>

![按一下 [基本功能]，按一下 [檢測金鑰]，CTRL+C](./media/app-insights-create-new-resource/02-props.png)

## <a name="install-the-sdk-in-your-app"></a><span data-ttu-id="fe7b6-137">在應用程式中安裝 SDK</span><span class="sxs-lookup"><span data-stu-id="fe7b6-137">Install the SDK in your app</span></span>
<span data-ttu-id="fe7b6-138">在應用程式中安裝 Application Insights SDK 核心。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-138">Install the Application Insights SDK in your app.</span></span> <span data-ttu-id="fe7b6-139">此步驟高度仰賴於應用程式的類型。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-139">This step depends heavily on the type of your application.</span></span> 

<span data-ttu-id="fe7b6-140">使用檢測金鑰來設定[您在應用程式中安裝的 SDK][start]。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-140">Use the instrumentation key to configure [the SDK that you install in your application][start].</span></span>

<span data-ttu-id="fe7b6-141">SDK 包含不需撰寫任何程式碼，即可傳送遙測資料的標準模組。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-141">The SDK includes standard modules that send telemetry without you having to write any code.</span></span> <span data-ttu-id="fe7b6-142">若要更詳細追蹤使用者動作或診斷問題，請[使用 API][api] 來傳送您自己的遙測。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-142">To track user actions or diagnose issues in more detail, [use the API][api] to send your own telemetry.</span></span>

## <span data-ttu-id="fe7b6-143"><a name="monitor"></a>查看遙測資料</span><span class="sxs-lookup"><span data-stu-id="fe7b6-143"><a name="monitor"></a>See telemetry data</span></span>
<span data-ttu-id="fe7b6-144">關閉 [快速入門] 刀鋒視窗，返回 Azure 入口網站中的應用程式刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-144">Close the quick start blade to return to your application blade in the Azure portal.</span></span>

<span data-ttu-id="fe7b6-145">按一下 [搜尋] 圖格以查看[診斷搜尋][diagnostic]，其中會顯示前幾個事件。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-145">Click the Search tile to see [Diagnostic Search][diagnostic], where the first events appear.</span></span> 

<span data-ttu-id="fe7b6-146">如果您預期有更多資料，請在幾秒之後按一下 [重新整理]。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-146">If you're expecting more data, click **Refresh** after a few seconds  .</span></span>

## <a name="creating-a-resource-automatically"></a><span data-ttu-id="fe7b6-147">自動建立資源</span><span class="sxs-lookup"><span data-stu-id="fe7b6-147">Creating a resource automatically</span></span>
<span data-ttu-id="fe7b6-148">您可以撰寫 [PowerShell 指令碼](app-insights-powershell.md) 來自動建立資源。</span><span class="sxs-lookup"><span data-stu-id="fe7b6-148">You can write a [PowerShell script](app-insights-powershell.md) to create a resource automatically.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe7b6-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fe7b6-149">Next steps</span></span>
* [<span data-ttu-id="fe7b6-150">建立儀表板</span><span class="sxs-lookup"><span data-stu-id="fe7b6-150">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="fe7b6-151">診斷搜尋</span><span class="sxs-lookup"><span data-stu-id="fe7b6-151">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="fe7b6-152">探索度量</span><span class="sxs-lookup"><span data-stu-id="fe7b6-152">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="fe7b6-153">撰寫分析查詢</span><span class="sxs-lookup"><span data-stu-id="fe7b6-153">Write Analytics queries</span></span>](app-insights-analytics.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[diagnostic]: app-insights-diagnostic-search.md
[metrics]: app-insights-metrics-explorer.md
[start]: app-insights-overview.md

