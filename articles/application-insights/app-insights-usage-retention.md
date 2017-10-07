---
title: "使用 Azure Application Insights web 應用程式的 aaaUser 保留分析 |Microsoft 文件"
description: "多少個使用者傳回 tooyour 應用程式？"
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
ms.openlocfilehash: 8bcee5f1611afbd69016ec3eef27832c304762a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="user-retention-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="6f2c8-103">使用 Application Insights 進行 Web 應用程式的使用者保留期分析</span><span class="sxs-lookup"><span data-stu-id="6f2c8-103">User retention analysis for web applications with Application Insights</span></span>

<span data-ttu-id="6f2c8-104">中的 hello 保留功能[Azure Application Insights](app-insights-overview.md)可協助您分析的使用者人數傳回 tooyour 應用程式和頻率執行特定工作或達成目標。</span><span class="sxs-lookup"><span data-stu-id="6f2c8-104">hello retention feature in [Azure Application Insights](app-insights-overview.md) helps you analyze how many users return tooyour app, and how often they perform particular tasks or achieve goals.</span></span> <span data-ttu-id="6f2c8-105">例如，如果您執行遊戲的站台時，無法比較 hello 的使用者之後遺失 hello 數目的遊戲會傳回 toohello 站台成功後，傳回使用者的數字。</span><span class="sxs-lookup"><span data-stu-id="6f2c8-105">For example, if you run a game site, you could compare hello numbers of users who return toohello site after losing a game with hello number who return after winning.</span></span> <span data-ttu-id="6f2c8-106">這項知識可以協助您改善使用者體驗和商務策略。</span><span class="sxs-lookup"><span data-stu-id="6f2c8-106">This knowledge can help you improve both your user experience and your business strategy.</span></span>

## <a name="get-started"></a><span data-ttu-id="6f2c8-107">開始使用</span><span class="sxs-lookup"><span data-stu-id="6f2c8-107">Get started</span></span>

<span data-ttu-id="6f2c8-108">如果您還沒有看到 hello 保留工具在 hello Application Insights 入口網站中的資料[學習 tooget hello 使用量工具的啟動方式](app-insights-usage-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="6f2c8-108">If you don't yet see data in hello retention tool in hello Application Insights portal, [learn how tooget started with hello usage tools](app-insights-usage-overview.md).</span></span>

## <a name="hello-retention-tool"></a><span data-ttu-id="6f2c8-109">hello 保留工具</span><span class="sxs-lookup"><span data-stu-id="6f2c8-109">hello Retention tool</span></span>

![保留期工具](./media/app-insights-usage-retention/retention.png)

1. <span data-ttu-id="6f2c8-111">hello 工具列可讓使用者 toocreate 新保留報表、 開啟現有的保留報表、 儲存目前保留報表或將儲存為、 還原所做的變更 toosaved 報表、 重新整理 hello 在報表上，透過電子郵件或直接連結，並存取 hello 共用報表的資料文件頁面。</span><span class="sxs-lookup"><span data-stu-id="6f2c8-111">hello toolbar allows users toocreate new retention reports, open existing retention reports, save current retention report or save as, revert changes made toosaved reports, refresh data on hello report, share report via email or direct link, and access hello documentation page.</span></span> 
2. <span data-ttu-id="6f2c8-112">根據預設，保留期會顯示執行任何動作然後回來，並且在一段期間內未執行任何其他動作的所有使用者。</span><span class="sxs-lookup"><span data-stu-id="6f2c8-112">By default, retention shows all users who did anything then came back and did anything else over a period.</span></span> <span data-ttu-id="6f2c8-113">您可以選取事件 toonarrow hello 專注於特定的使用者活動的不同的組合。</span><span class="sxs-lookup"><span data-stu-id="6f2c8-113">You can select different combination of events toonarrow hello focus on specific user activities.</span></span>
3. <span data-ttu-id="6f2c8-114">在屬性新增一或多個篩選條件。</span><span class="sxs-lookup"><span data-stu-id="6f2c8-114">Add one or more filters on properties.</span></span> <span data-ttu-id="6f2c8-115">例如，您可以將重點放在特定國家或區域中的使用者。</span><span class="sxs-lookup"><span data-stu-id="6f2c8-115">For example, you can focus on users in a particular country or region.</span></span> <span data-ttu-id="6f2c8-116">按一下**更新**設定 hello 篩選器之後。</span><span class="sxs-lookup"><span data-stu-id="6f2c8-116">Click **Update** after setting hello filters.</span></span> 
4. <span data-ttu-id="6f2c8-117">hello 整體保留圖表可顯示使用者保留的摘要跨 hello 選取的時間週期。</span><span class="sxs-lookup"><span data-stu-id="6f2c8-117">hello overall retention chart shows a summary of user retention across hello selected time period.</span></span> 
5. <span data-ttu-id="6f2c8-118">hello 方格會顯示 hello 人數保留 #2 中的相應 toohello 查詢產生器。</span><span class="sxs-lookup"><span data-stu-id="6f2c8-118">hello grid shows hello number of users retained according toohello query builder in #2.</span></span> <span data-ttu-id="6f2c8-119">每個資料列都代表使用者的 cohort 期間顯示 hello 時間執行的任何事件。</span><span class="sxs-lookup"><span data-stu-id="6f2c8-119">Each row represents a cohort of users who performed any event in hello time period shown.</span></span> <span data-ttu-id="6f2c8-120">Hello 資料列中的每個資料格會顯示多少個該 cohort 傳回在更新期間至少一次。</span><span class="sxs-lookup"><span data-stu-id="6f2c8-120">Each cell in hello row shows how many of that cohort returned at least once in a later period.</span></span> <span data-ttu-id="6f2c8-121">有些使用者可能會在不只一個期間內回來使用。</span><span class="sxs-lookup"><span data-stu-id="6f2c8-121">Some users may return in more than one period.</span></span> 
6. <span data-ttu-id="6f2c8-122">hello insights 卡顯示前五個起始事件，並前五個傳回事件 toogive 使用者更深入了解其保留報表。</span><span class="sxs-lookup"><span data-stu-id="6f2c8-122">hello insights cards show top five initiating events, and top five returned events toogive users a better understanding of their retention report.</span></span> 

![保留滑鼠暫留](./media/app-insights-usage-retention/hover.png)

<span data-ttu-id="6f2c8-124">使用者可以將滑鼠停留在 hello 保留工具 tooaccess hello 分析按鈕上的資料格，以及說明哪些 hello 儲存格的工具提示的方法。</span><span class="sxs-lookup"><span data-stu-id="6f2c8-124">Users can hover over cells on hello retention tool tooaccess hello analytics button and tool tips explaining what hello cell means.</span></span> <span data-ttu-id="6f2c8-125">hello 分析按鈕會預先填入的查詢 toogenerate 使用者與使用者 toohello 分析工具從 hello 儲存格。</span><span class="sxs-lookup"><span data-stu-id="6f2c8-125">hello Analytics button takes users toohello Analytics tool with a pre-populated query toogenerate users from hello cell.</span></span> 

## <a name="use-business-events-tootrack-retention"></a><span data-ttu-id="6f2c8-126">使用商務事件 tootrack 保留</span><span class="sxs-lookup"><span data-stu-id="6f2c8-126">Use business events tootrack retention</span></span>

<span data-ttu-id="6f2c8-127">tooget hello 最有用保留分析，將量值的事件，代表重要的商務活動。</span><span class="sxs-lookup"><span data-stu-id="6f2c8-127">tooget hello most useful retention analysis, measure events that represent significant business activities.</span></span> 

<span data-ttu-id="6f2c8-128">比方說，許多使用者可能會開啟網頁應用程式中而不播放，它會顯示 hello 遊戲。</span><span class="sxs-lookup"><span data-stu-id="6f2c8-128">For example, many users might open a page in your app without playing hello game that it displays.</span></span> <span data-ttu-id="6f2c8-129">追蹤只 hello 頁面檢視因此會提供不正確的方式有許多人 tooplay hello 遊戲後返回先前享受它估計。</span><span class="sxs-lookup"><span data-stu-id="6f2c8-129">Tracking just hello page views would therefore provide an inaccurate estimate of how many people return tooplay hello game after enjoying it previously.</span></span> <span data-ttu-id="6f2c8-130">tooget 清楚地了解傳回播放程式，您的應用程式應該傳送自訂事件時使用者實際播放。</span><span class="sxs-lookup"><span data-stu-id="6f2c8-130">tooget a clear picture of returning players, your app should send a custom event when a user actually plays.</span></span>  

<span data-ttu-id="6f2c8-131">它是很好的作法 toocode 自訂事件，代表關鍵商務動作，並使用這些保留分析。</span><span class="sxs-lookup"><span data-stu-id="6f2c8-131">It's good practice toocode custom events that represent key business actions, and use these for your retention analysis.</span></span> <span data-ttu-id="6f2c8-132">toocapture hello 遊戲結果，您需要 toowrite 一行程式碼 toosend 自訂事件 tooApplication 深入資訊。</span><span class="sxs-lookup"><span data-stu-id="6f2c8-132">toocapture hello game outcome, you need toowrite a line of code toosend a custom event tooApplication Insights.</span></span> <span data-ttu-id="6f2c8-133">如果您將資料寫入或 Node.JS hello 網頁程式碼中，它看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="6f2c8-133">If you write it in hello web page code or in Node.JS, it looks like this:</span></span>

```JavaScript
    appinsights.trackEvent("won game");
```

<span data-ttu-id="6f2c8-134">或是以 ASP.NET 伺服器程式碼撰寫：</span><span class="sxs-lookup"><span data-stu-id="6f2c8-134">Or in ASP.NET server code:</span></span>

```C#
   telemetry.TrackEvent("won game");
```

<span data-ttu-id="6f2c8-135">[深入了解撰寫自訂事件](app-insights-api-custom-events-metrics.md#trackevent)。</span><span class="sxs-lookup"><span data-stu-id="6f2c8-135">[Learn more about writing custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>


## <a name="next-steps"></a><span data-ttu-id="6f2c8-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6f2c8-136">Next steps</span></span>
- <span data-ttu-id="6f2c8-137">tooenable 使用狀況發生時，開始傳送[自訂事件](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent)或[頁面檢視](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views)。</span><span class="sxs-lookup"><span data-stu-id="6f2c8-137">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="6f2c8-138">如果您已傳送自訂事件或網頁 檢視中瀏覽 hello 使用量工具 toolearn 如何使用者使用您的服務。</span><span class="sxs-lookup"><span data-stu-id="6f2c8-138">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    - [<span data-ttu-id="6f2c8-139">使用者、工作階段、事件</span><span class="sxs-lookup"><span data-stu-id="6f2c8-139">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="6f2c8-140">漏斗圖</span><span class="sxs-lookup"><span data-stu-id="6f2c8-140">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="6f2c8-141">使用者流程</span><span class="sxs-lookup"><span data-stu-id="6f2c8-141">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="6f2c8-142">活頁簿</span><span class="sxs-lookup"><span data-stu-id="6f2c8-142">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="6f2c8-143">新增使用者內容</span><span class="sxs-lookup"><span data-stu-id="6f2c8-143">Add user context</span></span>](app-insights-usage-send-user-context.md)


