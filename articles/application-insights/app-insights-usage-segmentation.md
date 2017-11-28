---
title: "在 Azure Application Insights aaaUser、 session 和事件分析 |Microsoft 文件"
description: "您 Web 應用程式的使用者人口統計分析。"
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
ms.openlocfilehash: 152ab90e9a25c03087d3ebbde1263ec72acb227e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="users-sessions-and-events-analysis-in-application-insights"></a><span data-ttu-id="70a4d-103">Application Insights 中的使用者、工作階段和事件分析</span><span class="sxs-lookup"><span data-stu-id="70a4d-103">Users, sessions, and events analysis in Application Insights</span></span>

<span data-ttu-id="70a4d-104">了解人們在使用您的 Web 應用程式時，他們最感興趣的網頁、使用者的所在位置，以及他們使用何種瀏覽器與作業系統。</span><span class="sxs-lookup"><span data-stu-id="70a4d-104">Find out when people use your web app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> <span data-ttu-id="70a4d-105">使用 [Azure Application Insights](app-insights-overview.md) 來分析商務和使用量遙測。</span><span class="sxs-lookup"><span data-stu-id="70a4d-105">Analyze business and usage telemetry by using [Azure Application Insights](app-insights-overview.md).</span></span>

## <a name="get-started"></a><span data-ttu-id="70a4d-106">開始使用</span><span class="sxs-lookup"><span data-stu-id="70a4d-106">Get started</span></span>

<span data-ttu-id="70a4d-107">如果您還沒有看到 hello 使用者、 工作階段或在 hello Application Insights 入口網站事件刀鋒視窗中的資料[學習 tooget hello 使用量工具的啟動方式](app-insights-usage-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="70a4d-107">If you don't yet see data in hello users, sessions, or events blades in hello Application Insights portal, [learn how tooget started with hello usage tools](app-insights-usage-overview.md).</span></span>

## <a name="hello-users-sessions-and-events-segmentation-tool"></a><span data-ttu-id="70a4d-108">hello 使用者、 工作階段和事件分割工具</span><span class="sxs-lookup"><span data-stu-id="70a4d-108">hello Users, Sessions, and Events segmentation tool</span></span>

<span data-ttu-id="70a4d-109">Hello 使用量使用刀鋒視窗中的三種 hello 相同工具 tooslice 和擲骰遙測從您的 web 應用程式，從三個檢視方塊。</span><span class="sxs-lookup"><span data-stu-id="70a4d-109">Three of hello usage blades use hello same tool tooslice and dice telemetry from your web app from three perspectives.</span></span> <span data-ttu-id="70a4d-110">藉由篩選，並將 hello 資料分割，您能夠發現深入了解不同的頁面和功能的 hello 相對的使用方式。</span><span class="sxs-lookup"><span data-stu-id="70a4d-110">By filtering and splitting hello data, you can uncover insights about hello relative usage of different pages and features.</span></span>

* <span data-ttu-id="70a4d-111">**使用者工具**︰使用您應用程式的使用者數目和應用程式的功能。</span><span class="sxs-lookup"><span data-stu-id="70a4d-111">**Users tool**: How many people used your app and its features.</span></span>  <span data-ttu-id="70a4d-112">會使用儲存在瀏覽器 Cookie 中的匿名識別碼來計算使用者。</span><span class="sxs-lookup"><span data-stu-id="70a4d-112">Users are counted by using anonymous IDs stored in browser cookies.</span></span> <span data-ttu-id="70a4d-113">使用不同瀏覽器或電腦的單一使用者將會計算為多個使用者。</span><span class="sxs-lookup"><span data-stu-id="70a4d-113">A single person using different browsers or machines will be counted as more than one user.</span></span>
* <span data-ttu-id="70a4d-114">**工作階段工具**︰已包含應用程式的特定頁面和功能之使用者活動的工作階段數目。</span><span class="sxs-lookup"><span data-stu-id="70a4d-114">**Sessions tool**: How many sessions of user activity have included certain pages and features of your app.</span></span> <span data-ttu-id="70a4d-115">在使用者閒置半小時或連續使用 24 小時之後，就會計算工作階段。</span><span class="sxs-lookup"><span data-stu-id="70a4d-115">A session is counted after half an hour of user inactivity, or after continuous 24h of use.</span></span>
* <span data-ttu-id="70a4d-116">**事件工具**︰您應用程式的特定頁面與功能之使用頻率。</span><span class="sxs-lookup"><span data-stu-id="70a4d-116">**Events tool**: How often certain pages and features of your app are used.</span></span> <span data-ttu-id="70a4d-117">當瀏覽器從您的應用程式載入頁面時 (假如您已[將它進行檢測](app-insights-javascript.md)) 就會計算頁面檢視。</span><span class="sxs-lookup"><span data-stu-id="70a4d-117">A page view is counted when a browser loads a page from your app, provided you have [instrumented it](app-insights-javascript.md).</span></span> 

    <span data-ttu-id="70a4d-118">自訂事件表示一個出現項目內容中您的應用程式，通常使用者互動例如按一下按鈕，或 hello 的部分工作完成的情況。</span><span class="sxs-lookup"><span data-stu-id="70a4d-118">A custom event represents one occurrence of something happening in your app, often a user interaction like a button click or hello completion of some task.</span></span> <span data-ttu-id="70a4d-119">您將程式碼插入您的應用程式太[產生自訂的事件](app-insights-api-custom-events-metrics.md#trackevent)。</span><span class="sxs-lookup"><span data-stu-id="70a4d-119">You insert code in your app too[generate custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>

![使用量工具](./media/app-insights-usage-segmentation/users.png)

## <a name="querying-for-certain-users"></a><span data-ttu-id="70a4d-121">查詢特定使用者</span><span class="sxs-lookup"><span data-stu-id="70a4d-121">Querying for Certain Users</span></span> 

<span data-ttu-id="70a4d-122">瀏覽不同的使用者群組，藉由調整 hello 頂端 hello hello 使用者工具的查詢選項：</span><span class="sxs-lookup"><span data-stu-id="70a4d-122">Explore different groups of users by adjusting hello query options at hello top of hello Users tool:</span></span> 

* <span data-ttu-id="70a4d-123">已使用者︰選擇自訂事件和頁面檢視。</span><span class="sxs-lookup"><span data-stu-id="70a4d-123">Who used: Choose custom events and page views.</span></span> 
* <span data-ttu-id="70a4d-124">期間︰選擇時間範圍。</span><span class="sxs-lookup"><span data-stu-id="70a4d-124">During: Choose a time range.</span></span> 
* <span data-ttu-id="70a4d-125">藉由： 選擇如何 toobucket hello 資料一段時間或另一個屬性，例如瀏覽器或縣 （市）。</span><span class="sxs-lookup"><span data-stu-id="70a4d-125">By: Choose how toobucket hello data, either by a period of time or by another property such as browser or city.</span></span> 
* <span data-ttu-id="70a4d-126">依分割： Toosplit 或區段 hello 資料所選擇的屬性。</span><span class="sxs-lookup"><span data-stu-id="70a4d-126">Split By: Choose a property by which toosplit or segment hello data.</span></span> 
* <span data-ttu-id="70a4d-127">加入篩選： 限制 hello 查詢 toocertain 使用者、 工作階段或其屬性，例如瀏覽器或縣 （市） 為基礎的事件。</span><span class="sxs-lookup"><span data-stu-id="70a4d-127">Add Filters: Limit hello query toocertain users, sessions, or events based on their properties, such as browser or city.</span></span> 
 
## <a name="saving-and-sharing-reports"></a><span data-ttu-id="70a4d-128">儲存和共用報告</span><span class="sxs-lookup"><span data-stu-id="70a4d-128">Saving and sharing reports</span></span> 
<span data-ttu-id="70a4d-129">您可以儲存的報表使用者，可能是私用的只是 tooyou hello 我的報表區段中，或與存取 toothis Application Insights 資源與其他人共用在 hello 共用的報表 區段中。</span><span class="sxs-lookup"><span data-stu-id="70a4d-129">You can save Users reports, either private just tooyou in hello My Reports section, or shared with everyone else with access toothis Application Insights resource in hello Shared Reports section.</span></span>  
 
<span data-ttu-id="70a4d-130">當儲存報表，或編輯其屬性，請選擇 「 目前相對時間範圍 」 toosave 報表將會持續重新整理資料，返回固定一段時間。</span><span class="sxs-lookup"><span data-stu-id="70a4d-130">While saving a report or editing its properties, choose "Current Relative Time Range" toosave a report will continuously refreshed data, going back some fixed amount of time.</span></span>  
 
<span data-ttu-id="70a4d-131">選擇 「 目前絕對時間範圍 」 toosave 報表以一組固定的資料。</span><span class="sxs-lookup"><span data-stu-id="70a4d-131">Choose "Current Absolute Time Range" toosave a report with a fixed set of data.</span></span> <span data-ttu-id="70a4d-132">請記住 90 天，因此如果超過 90 天內有過具有絕對時間範圍的報表已儲存只會儲存在 Application Insights 中的資料，hello 報表將會顯示為空白。</span><span class="sxs-lookup"><span data-stu-id="70a4d-132">Keep in mind that data in Application Insights is only stored for 90 days, so if more than 90 days have passed since a report with an absolute time range was saved, hello report will appear empty.</span></span> 
 
## <a name="example-instances"></a><span data-ttu-id="70a4d-133">範例執行個體</span><span class="sxs-lookup"><span data-stu-id="70a4d-133">Example instances</span></span>

<span data-ttu-id="70a4d-134">hello 範例執行個體 > 一節顯示少數幾個個別的使用者、 工作階段或 hello 目前的查詢會比對事件的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="70a4d-134">hello Example instances section shows information about a handful of individual users, sessions, or events that are matched by hello current query.</span></span> <span data-ttu-id="70a4d-135">考量和瀏覽的個人，在加法 tooaggregates hello 行為可深入了解如何實際使用您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="70a4d-135">Considering and exploring hello behaviors of individuals, in addition tooaggregates, can provide insights about how people actually use your app.</span></span> 
 
## <a name="insights"></a><span data-ttu-id="70a4d-136">深入解析</span><span class="sxs-lookup"><span data-stu-id="70a4d-136">Insights</span></span> 

<span data-ttu-id="70a4d-137">hello Insights [資訊看板] 會顯示大型叢集的共用通用屬性的使用者。</span><span class="sxs-lookup"><span data-stu-id="70a4d-137">hello Insights sidebar shows large clusters of users that share common properties.</span></span> <span data-ttu-id="70a4d-138">這些叢集中會發現一些您應用程式使用方式的意外趨勢。</span><span class="sxs-lookup"><span data-stu-id="70a4d-138">These clusters can uncover surprising trends in how people use your app.</span></span> <span data-ttu-id="70a4d-139">例如，如果 40%的所有應用程式的 hello 使用量來自人使用單一的功能。</span><span class="sxs-lookup"><span data-stu-id="70a4d-139">For example, if 40% of all of hello usage of your app comes from people using a single feature.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="70a4d-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="70a4d-140">Next steps</span></span>
- <span data-ttu-id="70a4d-141">tooenable 使用狀況發生時，開始傳送[自訂事件](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent)或[頁面檢視](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views)。</span><span class="sxs-lookup"><span data-stu-id="70a4d-141">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="70a4d-142">如果您已傳送自訂事件或網頁 檢視中瀏覽 hello 使用量工具 toolearn 如何使用者使用您的服務。</span><span class="sxs-lookup"><span data-stu-id="70a4d-142">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    - [<span data-ttu-id="70a4d-143">漏斗圖</span><span class="sxs-lookup"><span data-stu-id="70a4d-143">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="70a4d-144">保留</span><span class="sxs-lookup"><span data-stu-id="70a4d-144">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="70a4d-145">使用者流程</span><span class="sxs-lookup"><span data-stu-id="70a4d-145">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="70a4d-146">活頁簿</span><span class="sxs-lookup"><span data-stu-id="70a4d-146">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="70a4d-147">新增使用者內容</span><span class="sxs-lookup"><span data-stu-id="70a4d-147">Add user context</span></span>](app-insights-usage-send-user-context.md)

