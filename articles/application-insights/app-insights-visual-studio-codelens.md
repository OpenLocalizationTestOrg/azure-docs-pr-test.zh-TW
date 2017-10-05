---
title: "Visual Studio CodeLens 中的 Application Insights 遙測 | Microsoft Docs"
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
ms.openlocfilehash: 20933afab55043ccc5ce908c04c6e4a7a28e3538
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-telemetry-in-visual-studio-codelens"></a><span data-ttu-id="c6ece-103">Visual Studio CodeLens 中的 Application Insights 遙測</span><span class="sxs-lookup"><span data-stu-id="c6ece-103">Application Insights telemetry in Visual Studio CodeLens</span></span>
<span data-ttu-id="c6ece-104">Web 應用程式的程式碼方法可透過遙測資料來標註出執行階段及要求回應時間。</span><span class="sxs-lookup"><span data-stu-id="c6ece-104">Methods in the code of your web app can be annotated with telemetry about run-time exceptions and request response times.</span></span> <span data-ttu-id="c6ece-105">如果您在應用程式中安裝 [Azure Application Insights](app-insights-overview.md)，遙測會出現在 Visual Studio [CodeLens](https://msdn.microsoft.com/library/dn269218.aspx) - 各函式頂端的註解，也就是您慣於查看有否實用資訊之處，例如參考函式的位置數或上次編輯函式的人員。</span><span class="sxs-lookup"><span data-stu-id="c6ece-105">If you install [Azure Application Insights](app-insights-overview.md) in your application, the telemetry appears in Visual Studio [CodeLens](https://msdn.microsoft.com/library/dn269218.aspx) - the notes at the top of each function where you're used to seeing useful information such as the number of places the function is referenced or the last person who edited it.</span></span>

![CodeLens](./media/app-insights-visual-studio-codelens/codelens-overview.png)

> [!NOTE]
> <span data-ttu-id="c6ece-107">CodeLens 中的 Application Insights 可用於 Visual Studio 2015 Update 3 及更新版本，或適用於最新版的 [開發人員分析工具延伸模組](https://visualstudiogallery.msdn.microsoft.com/82367b81-3f97-4de1-bbf1-eaf52ddc635a)。</span><span class="sxs-lookup"><span data-stu-id="c6ece-107">Application Insights in CodeLens is available in Visual Studio 2015 Update 3 and later, or with the latest version of [Developer Analytics Tools extension](https://visualstudiogallery.msdn.microsoft.com/82367b81-3f97-4de1-bbf1-eaf52ddc635a).</span></span> <span data-ttu-id="c6ece-108">CodeLens 適用於 Visual Studio 的 Enterprise 和 Professional 版本。</span><span class="sxs-lookup"><span data-stu-id="c6ece-108">CodeLens is available in the Enterprise and Professional editions of Visual Studio.</span></span>
> 
> 

## <a name="where-to-find-application-insights-data"></a><span data-ttu-id="c6ece-109">何處尋找 Application Insights 資料</span><span class="sxs-lookup"><span data-stu-id="c6ece-109">Where to find Application Insights data</span></span>
<span data-ttu-id="c6ece-110">請前往 Web 應用程式的公用要求方法，Application Insights 遙測資料可在其 CodeLens 指標中找到。</span><span class="sxs-lookup"><span data-stu-id="c6ece-110">Look for Application Insights telemetry in the CodeLens indicators of the public request methods of your web application.</span></span> <span data-ttu-id="c6ece-111">CodeLens 指標會顯示於 C# 和 Visual Basic 程式碼中的方法和其他宣告上方。</span><span class="sxs-lookup"><span data-stu-id="c6ece-111">CodeLens indicators are shown above method and other declarations in C# and Visual Basic code.</span></span> <span data-ttu-id="c6ece-112">如果 Application Insights 資料可用於某個方法，您將會看到要求和例外狀況的指標，例如「100 個要求，%1 個失敗」或「10 個例外狀況」。</span><span class="sxs-lookup"><span data-stu-id="c6ece-112">If Application Insights data is available for a method, you'll see indicators for requests and exceptions such as "100 requests, 1% failed" or "10 exceptions."</span></span> <span data-ttu-id="c6ece-113">如需詳細資料，按一下 CodeLens 指標。</span><span class="sxs-lookup"><span data-stu-id="c6ece-113">Click a CodeLens indicator for more details.</span></span> 

> [!TIP]
> <span data-ttu-id="c6ece-114">在其他 CodeLens 指標出現後，Application Insights 要求和例外狀況指標可能需要額外幾秒鐘才能載入。</span><span class="sxs-lookup"><span data-stu-id="c6ece-114">Application Insights request and exception indicators may take a few extra seconds to load after other CodeLens indicators appear.</span></span>
> 
> 

## <a name="exceptions-in-codelens"></a><span data-ttu-id="c6ece-115">CodeLens 中的例外狀況</span><span class="sxs-lookup"><span data-stu-id="c6ece-115">Exceptions in CodeLens</span></span>
![TBD](./media/app-insights-visual-studio-codelens/codelens-exceptions.png)

<span data-ttu-id="c6ece-117">例外狀況 CodeLens 指標在透過方法處理要求時，也會一面顯示過去 24 小時內您應用程式中 15 個最頻繁發生的例外狀況數目。</span><span class="sxs-lookup"><span data-stu-id="c6ece-117">The exception CodeLens indicator shows the number of exceptions that have occurred in the past 24 hours from the 15 most frequently occurring exceptions in your application during that period, while processing the request served by the method.</span></span>

<span data-ttu-id="c6ece-118">若要查看更多詳細資料，請按一下例外狀況 CodeLens 指標︰</span><span class="sxs-lookup"><span data-stu-id="c6ece-118">To see more details, click the exceptions CodeLens indicator:</span></span>

* <span data-ttu-id="c6ece-119">最近 24 小時 (相對於前 24 小時) 內例外狀況數目的百分比變化</span><span class="sxs-lookup"><span data-stu-id="c6ece-119">The percentage change in number of exceptions from the most recent 24 hours relative to the prior 24 hours</span></span>
* <span data-ttu-id="c6ece-120">選擇 [移至程式碼]  可瀏覽至擲回例外狀況之函數的原始程式碼</span><span class="sxs-lookup"><span data-stu-id="c6ece-120">Choose **Go to code** to navigate to the source code for the function throwing the exception</span></span>
* <span data-ttu-id="c6ece-121">選擇 [搜尋]  可查詢過去 24 小時內發生此例外狀況的所有執行個體</span><span class="sxs-lookup"><span data-stu-id="c6ece-121">Choose **Search** to query all instances of this exception that have occurred in the past 24 hours</span></span>
* <span data-ttu-id="c6ece-122">選擇 [趨勢]  可檢視過去 24 小時內此例外狀況的發生次數的趨勢視覺效果</span><span class="sxs-lookup"><span data-stu-id="c6ece-122">Choose **Trend** to view a trend visualization for occurrences of this exception in the past 24 hours</span></span>
* <span data-ttu-id="c6ece-123">選擇 [檢視此應用程式中的所有例外狀況]  可查詢過去 24 小時內發生的所有例外狀況</span><span class="sxs-lookup"><span data-stu-id="c6ece-123">Choose **View all exceptions in this app** to query all exceptions that have occurred in the past 24 hours</span></span>
* <span data-ttu-id="c6ece-124">選擇 [探索例外狀況區域]  可檢視過去 24 小時內發生的所有例外狀況的趨勢視覺效果。</span><span class="sxs-lookup"><span data-stu-id="c6ece-124">Choose **Explore exception trends** to view a trend visualization for all exceptions that have occurred in the past 24 hours.</span></span> 

> [!TIP]
> <span data-ttu-id="c6ece-125">如果您在 CodeLens 中看到「0 個例外狀況」，但您知道應該有例外狀況，請檢查並確定已在 CodeLens 中選取正確的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="c6ece-125">If you see "0 exceptions" in CodeLens but you know there should be exceptions, check to make sure the right Application Insights resource is selected in CodeLens.</span></span> <span data-ttu-id="c6ece-126">若要選取其他資源，請在 [方案總管] 中以滑鼠右鍵按一下您的專案，然後選擇 [Application Insights] > [選擇遙測來源]。</span><span class="sxs-lookup"><span data-stu-id="c6ece-126">To select another resource, right-click on your project in the Solution Explorer and choose **Application Insights > Choose Telemetry Source**.</span></span> <span data-ttu-id="c6ece-127">CodeLens 只會顯示過去 24 小時內您的應用程式中 15 個最頻繁發生的例外狀況，所以如果某例外狀況的發生頻率是第 16 位或更不常發生，您將會看到「0 個例外狀況」。</span><span class="sxs-lookup"><span data-stu-id="c6ece-127">CodeLens is only shown for the 15 most frequently occurring exceptions in your application in the past 24 hours, so if an exception is the 16th most frequently or less, you'll see "0 exceptions."</span></span> <span data-ttu-id="c6ece-128">ASP.NET 檢視中的例外狀況可能不會出現在產生這些檢視的控制器方法上。</span><span class="sxs-lookup"><span data-stu-id="c6ece-128">Exceptions from ASP.NET views may not appear on the controller methods that generated those views.</span></span>
> 
> [!TIP]
> <span data-ttu-id="c6ece-129">如果您在 CodeLens 中看到「？</span><span class="sxs-lookup"><span data-stu-id="c6ece-129">If you see "?</span></span> <span data-ttu-id="c6ece-130">個例外狀況」，您需要建立您的 Azure 帳戶與 Visual Studio 的關聯，否則您的 Azure 帳戶認證可能會過期。</span><span class="sxs-lookup"><span data-stu-id="c6ece-130">exceptions" in CodeLens, you need to associate your Azure account with Visual Studio or your Azure account credential may have expired.</span></span> <span data-ttu-id="c6ece-131">在任一種情況下，按一下「？</span><span class="sxs-lookup"><span data-stu-id="c6ece-131">In either case, click "?</span></span> <span data-ttu-id="c6ece-132">個例外狀況」，然後選擇 [新增帳戶...]  以輸入認證。</span><span class="sxs-lookup"><span data-stu-id="c6ece-132">exceptions" and choose **Add an account...** to enter your credentials.</span></span>
> 
> 

## <a name="requests-in-codelens"></a><span data-ttu-id="c6ece-133">CodeLens 中的要求</span><span class="sxs-lookup"><span data-stu-id="c6ece-133">Requests in CodeLens</span></span>
![TBD](./media/app-insights-visual-studio-codelens/codelens-requests.png)

<span data-ttu-id="c6ece-135">要求 CodeLens 指標會顯示過去 24 小時內方法已提供服務的 HTTP 要求數目，加上這些要求失敗的百分比。</span><span class="sxs-lookup"><span data-stu-id="c6ece-135">The request CodeLens indicator shows the number of HTTP requests that been serviced by a method in the past 24 hours, plus the percentage of those requests that failed.</span></span>

<span data-ttu-id="c6ece-136">若要查看更多詳細資料，請按一下要求 CodeLens 指標︰</span><span class="sxs-lookup"><span data-stu-id="c6ece-136">To see more details, click the requests CodeLens indicator:</span></span>

* <span data-ttu-id="c6ece-137">過去 24 小時 (相較於前 24 小時) 內要求數目、失敗的要求或平均回應時間的絕對值和百分比變更</span><span class="sxs-lookup"><span data-stu-id="c6ece-137">The absolute and percentage changes in number of requests, failed requests, and average response times over the past 24 hours compared to the prior 24 hours</span></span>
* <span data-ttu-id="c6ece-138">方法的可靠性，該值的計算方式為過去 24 小時內未失敗的要求百分比</span><span class="sxs-lookup"><span data-stu-id="c6ece-138">The reliability of the method, calculated as the percentage of requests that did not fail in the past 24 hours</span></span>
* <span data-ttu-id="c6ece-139">選擇 [搜尋]  要求或失敗的要求，以查詢過去 24 小時內發生的所有 (失敗) 要求</span><span class="sxs-lookup"><span data-stu-id="c6ece-139">Choose **Search** for requests or failed requests to query all the (failed) requests that occurred in the past 24 hours</span></span>
* <span data-ttu-id="c6ece-140">選擇 [趨勢]  可檢視過去 24 小時內要求、失敗的要求或平均回應時間的趨勢視覺效果。</span><span class="sxs-lookup"><span data-stu-id="c6ece-140">Choose **Trend** to view a trend visualization for requests, failed requests, or average response times in the past 24 hours.</span></span>
* <span data-ttu-id="c6ece-141">選擇 CodeLens 詳細資料檢視左上角的 Application Insights 資源名稱，以變更哪個資源是 CodeLens 資料的來源。</span><span class="sxs-lookup"><span data-stu-id="c6ece-141">Choose the name of the Application Insights resource in the upper left corner of the CodeLens details view to change which resource is the source for CodeLens data.</span></span>

## <span data-ttu-id="c6ece-142"><a name="next"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="c6ece-142"><a name="next"></a>Next steps</span></span>
|  |  |
| --- | --- |
| <span data-ttu-id="c6ece-143">**[在 Visual Studio 中使用 Application Insights](app-insights-visual-studio.md)**</span><span class="sxs-lookup"><span data-stu-id="c6ece-143">**[Working with Application Insights in Visual Studio](app-insights-visual-studio.md)**</span></span><br/><span data-ttu-id="c6ece-144">搜尋遙測、查看 CodeLens 中的資料，以及設定 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="c6ece-144">Search telemetry, see data in CodeLens, and configure Application Insights.</span></span> <span data-ttu-id="c6ece-145">盡在 Visual Studio 中。</span><span class="sxs-lookup"><span data-stu-id="c6ece-145">All within Visual Studio.</span></span> |![以滑鼠右鍵按一下專案，然後選擇 [Application Insights]、[搜尋]](./media/app-insights-visual-studio-codelens/34.png) |
| <span data-ttu-id="c6ece-147">**[新增更多測試](app-insights-asp-net-more.md)**</span><span class="sxs-lookup"><span data-stu-id="c6ece-147">**[Add more data](app-insights-asp-net-more.md)**</span></span><br/><span data-ttu-id="c6ece-148">監視使用狀況、可用性、相依性、例外狀況。</span><span class="sxs-lookup"><span data-stu-id="c6ece-148">Monitor usage, availability, dependencies, exceptions.</span></span> <span data-ttu-id="c6ece-149">整合來自記錄架構的追蹤。</span><span class="sxs-lookup"><span data-stu-id="c6ece-149">Integrate traces from logging frameworks.</span></span> <span data-ttu-id="c6ece-150">撰寫自訂遙測。</span><span class="sxs-lookup"><span data-stu-id="c6ece-150">Write custom telemetry.</span></span> |![Visual Studio](./media/app-insights-visual-studio-codelens/64.png) |
| <span data-ttu-id="c6ece-152">**[使用 Application Insights 入口網站](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="c6ece-152">**[Working with the Application Insights portal](app-insights-dashboards.md)**</span></span><br/><span data-ttu-id="c6ece-153">儀表板、功能強大的診斷和分析工具、警示、即時的應用程式相依性對應，以及遙測匯出等功能。</span><span class="sxs-lookup"><span data-stu-id="c6ece-153">Dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and telemetry export.</span></span> |![Visual Studio](./media/app-insights-visual-studio-codelens/62.png) |

