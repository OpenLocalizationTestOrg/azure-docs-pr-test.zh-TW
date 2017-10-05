---
title: "使用 Azure Application Insights 進行 Web 應用程式的使用者保留期分析 | Microsoft Docs"
description: "有多少使用者會回來使用您的應用程式？"
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: 7f7ca19ab171278bbd82f68e3822bc650b25373d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="user-retention-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="759ac-103">使用 Application Insights 進行 Web 應用程式的使用者保留期分析</span><span class="sxs-lookup"><span data-stu-id="759ac-103">User retention analysis for web applications with Application Insights</span></span>

<span data-ttu-id="759ac-104">[Azure Application Insights](app-insights-overview.md) 中的保留功能可協助您分析回來使用您應用程式的使用者人數，以及他們執行特定工作或達成目標的頻率。</span><span class="sxs-lookup"><span data-stu-id="759ac-104">The retention feature in [Azure Application Insights](app-insights-overview.md) helps you analyze how many users return to your app, and how often they perform particular tasks or achieve goals.</span></span> <span data-ttu-id="759ac-105">例如，如果您執行遊戲網站，您可以比較使用者在遊戲落敗與遊戲獲勝後，回到網站的數目。</span><span class="sxs-lookup"><span data-stu-id="759ac-105">For example, if you run a game site, you could compare the numbers of users who return to the site after losing a game with the number who return after winning.</span></span> <span data-ttu-id="759ac-106">這項知識可以協助您改善使用者體驗和商務策略。</span><span class="sxs-lookup"><span data-stu-id="759ac-106">This knowledge can help you improve both your user experience and your business strategy.</span></span>

## <a name="get-started"></a><span data-ttu-id="759ac-107">開始使用</span><span class="sxs-lookup"><span data-stu-id="759ac-107">Get started</span></span>

<span data-ttu-id="759ac-108">如果您在 Application Insights 入口網站中尚未看到保留工具中的資料，請[了解如何開始使用使用量工具](app-insights-usage-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="759ac-108">If you don't yet see data in the retention tool in the Application Insights portal, [learn how to get started with the usage tools](app-insights-usage-overview.md).</span></span>

## <a name="the-retention-tool"></a><span data-ttu-id="759ac-109">保留期工具</span><span class="sxs-lookup"><span data-stu-id="759ac-109">The Retention tool</span></span>

![保留期工具](./media/app-insights-usage-retention/retention.png)

1. <span data-ttu-id="759ac-111">工具列可讓使用者建立新的保留報告、開啟現有的保留報告、儲存目前保留報告或另存新檔、還原對已儲存之報表所做的變更、重新整理報表上的資料、透過電子郵件或直接連結共用報表，以及存取文件頁面。</span><span class="sxs-lookup"><span data-stu-id="759ac-111">The toolbar allows users to create new retention reports, open existing retention reports, save current retention report or save as, revert changes made to saved reports, refresh data on the report, share report via email or direct link, and access the documentation page.</span></span> 
2. <span data-ttu-id="759ac-112">根據預設，保留期會顯示執行任何動作然後回來，並且在一段期間內未執行任何其他動作的所有使用者。</span><span class="sxs-lookup"><span data-stu-id="759ac-112">By default, retention shows all users who did anything then came back and did anything else over a period.</span></span> <span data-ttu-id="759ac-113">您可以選取不同組合的事件，以縮小特定使用者活動的關注範圍。</span><span class="sxs-lookup"><span data-stu-id="759ac-113">You can select different combination of events to narrow the focus on specific user activities.</span></span>
3. <span data-ttu-id="759ac-114">在屬性新增一或多個篩選條件。</span><span class="sxs-lookup"><span data-stu-id="759ac-114">Add one or more filters on properties.</span></span> <span data-ttu-id="759ac-115">例如，您可以將重點放在特定國家或區域中的使用者。</span><span class="sxs-lookup"><span data-stu-id="759ac-115">For example, you can focus on users in a particular country or region.</span></span> <span data-ttu-id="759ac-116">設定篩選條件後，按一下 [更新]。</span><span class="sxs-lookup"><span data-stu-id="759ac-116">Click **Update** after setting the filters.</span></span> 
4. <span data-ttu-id="759ac-117">整體保留圖表顯示所選期間內的使用者保留摘要。</span><span class="sxs-lookup"><span data-stu-id="759ac-117">The overall retention chart shows a summary of user retention across the selected time period.</span></span> 
5. <span data-ttu-id="759ac-118">此格線根據 #2 中的查詢產生器顯示保留的使用者數目。</span><span class="sxs-lookup"><span data-stu-id="759ac-118">The grid shows the number of users retained according to the query builder in #2.</span></span> <span data-ttu-id="759ac-119">每個資料列代表在所顯示的時間週期內執行任何事件的同群使用者。</span><span class="sxs-lookup"><span data-stu-id="759ac-119">Each row represents a cohort of users who performed any event in the time period shown.</span></span> <span data-ttu-id="759ac-120">資料列中的每個資料格會顯示該同群使用者中在稍後期間內至少回來使用一次的數目。</span><span class="sxs-lookup"><span data-stu-id="759ac-120">Each cell in the row shows how many of that cohort returned at least once in a later period.</span></span> <span data-ttu-id="759ac-121">有些使用者可能會在不只一個期間內回來使用。</span><span class="sxs-lookup"><span data-stu-id="759ac-121">Some users may return in more than one period.</span></span> 
6. <span data-ttu-id="759ac-122">Insights 卡顯示前五個起始事件，以及前五個傳回的事件，讓使用者深入了解其保留報表。</span><span class="sxs-lookup"><span data-stu-id="759ac-122">The insights cards show top five initiating events, and top five returned events to give users a better understanding of their retention report.</span></span> 

![保留滑鼠暫留](./media/app-insights-usage-retention/hover.png)

<span data-ttu-id="759ac-124">使用者可以將滑鼠停留在保留工具上的資料格，來存取會說明資料格所代表之意義的分析按鈕和工具提示。</span><span class="sxs-lookup"><span data-stu-id="759ac-124">Users can hover over cells on the retention tool to access the analytics button and tool tips explaining what the cell means.</span></span> <span data-ttu-id="759ac-125">[分析] 按鈕會帶領使用者前往具有預先填入查詢的分析工具，以從儲存格產生使用者。</span><span class="sxs-lookup"><span data-stu-id="759ac-125">The Analytics button takes users to the Analytics tool with a pre-populated query to generate users from the cell.</span></span> 

## <a name="use-business-events-to-track-retention"></a><span data-ttu-id="759ac-126">使用商務事件來追蹤保留期</span><span class="sxs-lookup"><span data-stu-id="759ac-126">Use business events to track retention</span></span>

<span data-ttu-id="759ac-127">若要取得最有用的保留期分析，請測量代表重要商務活動的事件。</span><span class="sxs-lookup"><span data-stu-id="759ac-127">To get the most useful retention analysis, measure events that represent significant business activities.</span></span> 

<span data-ttu-id="759ac-128">例如，許多在應用程式中開啟頁面的使用者可能不會玩它所顯示的遊戲。</span><span class="sxs-lookup"><span data-stu-id="759ac-128">For example, many users might open a page in your app without playing the game that it displays.</span></span> <span data-ttu-id="759ac-129">因此，僅追蹤頁面檢視所提供的先前玩過遊戲後再回來玩的人數估計可能會有誤。</span><span class="sxs-lookup"><span data-stu-id="759ac-129">Tracking just the page views would therefore provide an inaccurate estimate of how many people return to play the game after enjoying it previously.</span></span> <span data-ttu-id="759ac-130">若要取得舊玩家的明確內容，您的應用程式應該在使用者實際玩過遊戲時才傳送自訂事件。</span><span class="sxs-lookup"><span data-stu-id="759ac-130">To get a clear picture of returning players, your app should send a custom event when a user actually plays.</span></span>  

<span data-ttu-id="759ac-131">最佳做法是將代表重要商務動作的自訂事件編碼，並使用這些來進行保留期分析。</span><span class="sxs-lookup"><span data-stu-id="759ac-131">It's good practice to code custom events that represent key business actions, and use these for your retention analysis.</span></span> <span data-ttu-id="759ac-132">若要擷取遊戲的結果，您需要撰寫一行程式碼，將自訂事件傳送至 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="759ac-132">To capture the game outcome, you need to write a line of code to send a custom event to Application Insights.</span></span> <span data-ttu-id="759ac-133">如果您是以網頁程式碼或 Node.JS 來撰寫，它看起來會像這樣︰</span><span class="sxs-lookup"><span data-stu-id="759ac-133">If you write it in the web page code or in Node.JS, it looks like this:</span></span>

```JavaScript
    appinsights.trackEvent("won game");
```

<span data-ttu-id="759ac-134">或是以 ASP.NET 伺服器程式碼撰寫：</span><span class="sxs-lookup"><span data-stu-id="759ac-134">Or in ASP.NET server code:</span></span>

```C#
   telemetry.TrackEvent("won game");
```

<span data-ttu-id="759ac-135">[深入了解撰寫自訂事件](app-insights-api-custom-events-metrics.md#trackevent)。</span><span class="sxs-lookup"><span data-stu-id="759ac-135">[Learn more about writing custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>


## <a name="next-steps"></a><span data-ttu-id="759ac-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="759ac-136">Next steps</span></span>
- <span data-ttu-id="759ac-137">若要啟用使用體驗，請開始傳送「自訂事件」[](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent)或「頁面檢視」[](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views)。</span><span class="sxs-lookup"><span data-stu-id="759ac-137">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="759ac-138">如果您已傳送自訂事件或頁面檢視，請探索「使用量工具」，以了解使用者如何使用您的服務。</span><span class="sxs-lookup"><span data-stu-id="759ac-138">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    - [<span data-ttu-id="759ac-139">使用者、工作階段、事件</span><span class="sxs-lookup"><span data-stu-id="759ac-139">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="759ac-140">漏斗圖</span><span class="sxs-lookup"><span data-stu-id="759ac-140">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="759ac-141">使用者流程</span><span class="sxs-lookup"><span data-stu-id="759ac-141">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="759ac-142">活頁簿</span><span class="sxs-lookup"><span data-stu-id="759ac-142">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="759ac-143">新增使用者內容</span><span class="sxs-lookup"><span data-stu-id="759ac-143">Add user context</span></span>](app-insights-usage-send-user-context.md)


