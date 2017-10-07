---
title: "在 Visual Studio CodeLens Insights 遙測 aaaApplication |Microsoft 文件"
description: "使用 Visual Studio 中的 CodeLens 快速存取 Application Insights 要求和例外狀況遙測。"
services: application-insights
documentationcenter: .net
author: numberbycolors
manager: carmonm
ms.assetid: 93559e44-23cb-4b9d-8425-60f7f0d0a82c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: e812aa48f2a67eea860e7ecde341855763bb8a8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-telemetry-in-visual-studio-codelens"></a><span data-ttu-id="44d58-103">Visual Studio CodeLens 中的 Application Insights 遙測</span><span class="sxs-lookup"><span data-stu-id="44d58-103">Application Insights telemetry in Visual Studio CodeLens</span></span>
<span data-ttu-id="44d58-104">Hello web 應用程式的程式碼中的方法可以標註具有執行階段例外狀況的遙測，並要求回應時間。</span><span class="sxs-lookup"><span data-stu-id="44d58-104">Methods in hello code of your web app can be annotated with telemetry about run-time exceptions and request response times.</span></span> <span data-ttu-id="44d58-105">如果您安裝[Azure Application Insights](app-insights-overview.md)應用程式中 hello 遙測會出現在 Visual Studio [CodeLens](https://msdn.microsoft.com/library/dn269218.aspx) -hello hello 頂端，您的使用位置的每個函式的備忘稿 tooseeing 有用資訊，例如 hello 數目上的芳鄰 hello 函式參考，或 hello 上次編輯它的人員。</span><span class="sxs-lookup"><span data-stu-id="44d58-105">If you install [Azure Application Insights](app-insights-overview.md) in your application, hello telemetry appears in Visual Studio [CodeLens](https://msdn.microsoft.com/library/dn269218.aspx) - hello notes at hello top of each function where you're used tooseeing useful information such as hello number of places hello function is referenced or hello last person who edited it.</span></span>

![CodeLens](./media/app-insights-visual-studio-codelens/codelens-overview.png)

> [!NOTE]
> <span data-ttu-id="44d58-107">CodeLens 中的 application Insights 是用於 Visual Studio 2015 Update 3 及更新版本，或是與 hello 最新版本[開發人員分析工具延伸模組](https://visualstudiogallery.msdn.microsoft.com/82367b81-3f97-4de1-bbf1-eaf52ddc635a)。</span><span class="sxs-lookup"><span data-stu-id="44d58-107">Application Insights in CodeLens is available in Visual Studio 2015 Update 3 and later, or with hello latest version of [Developer Analytics Tools extension](https://visualstudiogallery.msdn.microsoft.com/82367b81-3f97-4de1-bbf1-eaf52ddc635a).</span></span> <span data-ttu-id="44d58-108">CodeLens 提供了 hello 企業版和專業版的 Visual Studio 版本。</span><span class="sxs-lookup"><span data-stu-id="44d58-108">CodeLens is available in hello Enterprise and Professional editions of Visual Studio.</span></span>
> 
> 

## <a name="where-toofind-application-insights-data"></a><span data-ttu-id="44d58-109">其中 toofind Application Insights 資料</span><span class="sxs-lookup"><span data-stu-id="44d58-109">Where toofind Application Insights data</span></span>
<span data-ttu-id="44d58-110">尋找在 hello CodeLens 指標 hello 公用要求方法的 web 應用程式中的 Application Insights 遙測。</span><span class="sxs-lookup"><span data-stu-id="44d58-110">Look for Application Insights telemetry in hello CodeLens indicators of hello public request methods of your web application.</span></span> <span data-ttu-id="44d58-111">CodeLens 指標會顯示於 C# 和 Visual Basic 程式碼中的方法和其他宣告上方。</span><span class="sxs-lookup"><span data-stu-id="44d58-111">CodeLens indicators are shown above method and other declarations in C# and Visual Basic code.</span></span> <span data-ttu-id="44d58-112">如果 Application Insights 資料可用於某個方法，您將會看到要求和例外狀況的指標，例如「100 個要求，%1 個失敗」或「10 個例外狀況」。</span><span class="sxs-lookup"><span data-stu-id="44d58-112">If Application Insights data is available for a method, you'll see indicators for requests and exceptions such as "100 requests, 1% failed" or "10 exceptions."</span></span> <span data-ttu-id="44d58-113">如需詳細資料，按一下 CodeLens 指標。</span><span class="sxs-lookup"><span data-stu-id="44d58-113">Click a CodeLens indicator for more details.</span></span> 

> [!TIP]
> <span data-ttu-id="44d58-114">Application Insights 要求和例外狀況指標可能需要一些額外的秒鐘 tooload 之後會出現其他 CodeLens 的指標。</span><span class="sxs-lookup"><span data-stu-id="44d58-114">Application Insights request and exception indicators may take a few extra seconds tooload after other CodeLens indicators appear.</span></span>
> 
> 

## <a name="exceptions-in-codelens"></a><span data-ttu-id="44d58-115">CodeLens 中的例外狀況</span><span class="sxs-lookup"><span data-stu-id="44d58-115">Exceptions in CodeLens</span></span>
![TBD](./media/app-insights-visual-studio-codelens/codelens-exceptions.png)

<span data-ttu-id="44d58-117">hello 例外狀況的 CodeLens 指標會顯示 hello hello 15 多數經常發生例外狀況，您的應用程式，在該期間內，處理 hello 要求時由 hello 方法從 hello 在過去 24 小時內發生的例外狀況數目。</span><span class="sxs-lookup"><span data-stu-id="44d58-117">hello exception CodeLens indicator shows hello number of exceptions that have occurred in hello past 24 hours from hello 15 most frequently occurring exceptions in your application during that period, while processing hello request served by hello method.</span></span>

<span data-ttu-id="44d58-118">toosee 更多詳細資訊，按一下 hello 例外狀況的 CodeLens 指標：</span><span class="sxs-lookup"><span data-stu-id="44d58-118">toosee more details, click hello exceptions CodeLens indicator:</span></span>

* <span data-ttu-id="44d58-119">例外狀況的 hello 最近 24 小時相對 toohello 先前從次數 24 小時 hello 百分比變更</span><span class="sxs-lookup"><span data-stu-id="44d58-119">hello percentage change in number of exceptions from hello most recent 24 hours relative toohello prior 24 hours</span></span>
* <span data-ttu-id="44d58-120">選擇**移 toocode** toonavigate toohello 原始程式碼 hello 函式擲回 hello 例外狀況</span><span class="sxs-lookup"><span data-stu-id="44d58-120">Choose **Go toocode** toonavigate toohello source code for hello function throwing hello exception</span></span>
* <span data-ttu-id="44d58-121">選擇**搜尋**tooquery 中發生此例外狀況的所有執行個體 hello 過去 24 小時</span><span class="sxs-lookup"><span data-stu-id="44d58-121">Choose **Search** tooquery all instances of this exception that have occurred in hello past 24 hours</span></span>
* <span data-ttu-id="44d58-122">選擇**趨勢**tooview 這個例外狀況在 hello 過去 24 小時內的項目趨勢視覺效果</span><span class="sxs-lookup"><span data-stu-id="44d58-122">Choose **Trend** tooview a trend visualization for occurrences of this exception in hello past 24 hours</span></span>
* <span data-ttu-id="44d58-123">選擇**檢視此應用程式中的所有例外狀況**tooquery 中所發生的所有例外狀況 hello 過去 24 小時</span><span class="sxs-lookup"><span data-stu-id="44d58-123">Choose **View all exceptions in this app** tooquery all exceptions that have occurred in hello past 24 hours</span></span>
* <span data-ttu-id="44d58-124">選擇**探索例外狀況的趨勢**tooview 趨勢視覺效果中發生的 hello 過去 24 小時內的所有例外狀況。</span><span class="sxs-lookup"><span data-stu-id="44d58-124">Choose **Explore exception trends** tooview a trend visualization for all exceptions that have occurred in hello past 24 hours.</span></span> 

> [!TIP]
> <span data-ttu-id="44d58-125">如果您看到 [0 例外狀況] CodeLens 中，但您知道應該例外狀況，請檢查 toomake 確定 CodeLens 已選取 hello 右 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="44d58-125">If you see "0 exceptions" in CodeLens but you know there should be exceptions, check toomake sure hello right Application Insights resource is selected in CodeLens.</span></span> <span data-ttu-id="44d58-126">tooselect 另一個資源，hello 方案總管] 中的專案上按一下滑鼠右鍵，然後選擇 [ **Application Insights > 選擇遙測來源**。</span><span class="sxs-lookup"><span data-stu-id="44d58-126">tooselect another resource, right-click on your project in hello Solution Explorer and choose **Application Insights > Choose Telemetry Source**.</span></span> <span data-ttu-id="44d58-127">CodeLens 僅會顯示 hello 15 多數經常發生例外狀況，應用程式中 hello 過去 24 小時，因此，如果例外狀況經常 hello 大部分 16 或更少，您會看到 [0 例外狀況]。</span><span class="sxs-lookup"><span data-stu-id="44d58-127">CodeLens is only shown for hello 15 most frequently occurring exceptions in your application in hello past 24 hours, so if an exception is hello 16th most frequently or less, you'll see "0 exceptions."</span></span> <span data-ttu-id="44d58-128">例外狀況，從 ASP.NET 檢視可能不會出現在產生這些檢視表的 hello 控制器方法。</span><span class="sxs-lookup"><span data-stu-id="44d58-128">Exceptions from ASP.NET views may not appear on hello controller methods that generated those views.</span></span>
> 
> [!TIP]
> <span data-ttu-id="44d58-129">如果您在 CodeLens 中看到「？</span><span class="sxs-lookup"><span data-stu-id="44d58-129">If you see "?</span></span> <span data-ttu-id="44d58-130">例外狀況 > CodeLens，您需要的 tooassociate Visual Studio 或您的 Azure 帳戶的認證與您的 Azure 帳戶可能已過期。</span><span class="sxs-lookup"><span data-stu-id="44d58-130">exceptions" in CodeLens, you need tooassociate your Azure account with Visual Studio or your Azure account credential may have expired.</span></span> <span data-ttu-id="44d58-131">在任一種情況下，按一下「？</span><span class="sxs-lookup"><span data-stu-id="44d58-131">In either case, click "?</span></span> <span data-ttu-id="44d58-132">例外狀況]，然後選擇 [**新增帳戶...** tooenter 您的認證。</span><span class="sxs-lookup"><span data-stu-id="44d58-132">exceptions" and choose **Add an account...** tooenter your credentials.</span></span>
> 
> 

## <a name="requests-in-codelens"></a><span data-ttu-id="44d58-133">CodeLens 中的要求</span><span class="sxs-lookup"><span data-stu-id="44d58-133">Requests in CodeLens</span></span>
![TBD](./media/app-insights-visual-studio-codelens/codelens-requests.png)

<span data-ttu-id="44d58-135">hello CodeLens 指標顯示 hello 數目的 HTTP 要求會要求已由 hello 過去 24 小時，再加上 hello 百分比，這些失敗的要求中的方法提供服務。</span><span class="sxs-lookup"><span data-stu-id="44d58-135">hello request CodeLens indicator shows hello number of HTTP requests that been serviced by a method in hello past 24 hours, plus hello percentage of those requests that failed.</span></span>

<span data-ttu-id="44d58-136">詳細資訊，請按一下 toosee hello 要求 CodeLens 指標：</span><span class="sxs-lookup"><span data-stu-id="44d58-136">toosee more details, click hello requests CodeLens indicator:</span></span>

* <span data-ttu-id="44d58-137">過去 24 小時比較 toohello 先前 hello 透過 24 小時 hello 中要求、 失敗的要求和平均回應時間的數字的絕對值和百分比變更</span><span class="sxs-lookup"><span data-stu-id="44d58-137">hello absolute and percentage changes in number of requests, failed requests, and average response times over hello past 24 hours compared toohello prior 24 hours</span></span>
* <span data-ttu-id="44d58-138">hello 方法，計算為未通過 hello 在過去 24 小時內的要求 hello 百分比的 hello 可靠性</span><span class="sxs-lookup"><span data-stu-id="44d58-138">hello reliability of hello method, calculated as hello percentage of requests that did not fail in hello past 24 hours</span></span>
* <span data-ttu-id="44d58-139">選擇**搜尋**個要求或所有 hello （失敗） 的要求中所發生 hello 過去 24 小時內失敗的要求 tooquery</span><span class="sxs-lookup"><span data-stu-id="44d58-139">Choose **Search** for requests or failed requests tooquery all hello (failed) requests that occurred in hello past 24 hours</span></span>
* <span data-ttu-id="44d58-140">選擇**趨勢**tooview 趨勢視覺效果的要求、 失敗的要求或平均回應時間在 hello 過去 24 小時。</span><span class="sxs-lookup"><span data-stu-id="44d58-140">Choose **Trend** tooview a trend visualization for requests, failed requests, or average response times in hello past 24 hours.</span></span>
* <span data-ttu-id="44d58-141">Hello 左上角的 hello CodeLens 詳細資料檢視 toochange 哪些資源是 hello CodeLens 資料來源選擇 hello hello Application Insights 資源名稱。</span><span class="sxs-lookup"><span data-stu-id="44d58-141">Choose hello name of hello Application Insights resource in hello upper left corner of hello CodeLens details view toochange which resource is hello source for CodeLens data.</span></span>

## <span data-ttu-id="44d58-142"><a name="next"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="44d58-142"><a name="next"></a>Next steps</span></span>
|  |  |
| --- | --- |
| <span data-ttu-id="44d58-143">**[在 Visual Studio 中使用 Application Insights](app-insights-visual-studio.md)**</span><span class="sxs-lookup"><span data-stu-id="44d58-143">**[Working with Application Insights in Visual Studio](app-insights-visual-studio.md)**</span></span><br/><span data-ttu-id="44d58-144">搜尋遙測、查看 CodeLens 中的資料，以及設定 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="44d58-144">Search telemetry, see data in CodeLens, and configure Application Insights.</span></span> <span data-ttu-id="44d58-145">盡在 Visual Studio 中。</span><span class="sxs-lookup"><span data-stu-id="44d58-145">All within Visual Studio.</span></span> |![Hello 專案上按一下滑鼠右鍵，然後選擇 Application Insights 搜尋](./media/app-insights-visual-studio-codelens/34.png) |
| <span data-ttu-id="44d58-147">**[新增更多測試](app-insights-asp-net-more.md)**</span><span class="sxs-lookup"><span data-stu-id="44d58-147">**[Add more data](app-insights-asp-net-more.md)**</span></span><br/><span data-ttu-id="44d58-148">監視使用狀況、可用性、相依性、例外狀況。</span><span class="sxs-lookup"><span data-stu-id="44d58-148">Monitor usage, availability, dependencies, exceptions.</span></span> <span data-ttu-id="44d58-149">整合來自記錄架構的追蹤。</span><span class="sxs-lookup"><span data-stu-id="44d58-149">Integrate traces from logging frameworks.</span></span> <span data-ttu-id="44d58-150">撰寫自訂遙測。</span><span class="sxs-lookup"><span data-stu-id="44d58-150">Write custom telemetry.</span></span> |![Visual Studio](./media/app-insights-visual-studio-codelens/64.png) |
| <span data-ttu-id="44d58-152">**[使用 hello Application Insights 入口網站](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="44d58-152">**[Working with hello Application Insights portal](app-insights-dashboards.md)**</span></span><br/><span data-ttu-id="44d58-153">儀表板、功能強大的診斷和分析工具、警示、即時的應用程式相依性對應，以及遙測匯出等功能。</span><span class="sxs-lookup"><span data-stu-id="44d58-153">Dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and telemetry export.</span></span> |![Visual Studio](./media/app-insights-visual-studio-codelens/62.png) |

