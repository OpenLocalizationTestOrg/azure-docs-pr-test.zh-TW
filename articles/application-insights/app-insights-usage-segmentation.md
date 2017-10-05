---
title: "Azure Application Insights 中的使用者、工作階段和事件分析 | Microsoft Docs"
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
ms.openlocfilehash: b154a01d1690bff4950ebc1ff5a5b89894d4d111
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="users-sessions-and-events-analysis-in-application-insights"></a><span data-ttu-id="a26a9-103">Application Insights 中的使用者、工作階段和事件分析</span><span class="sxs-lookup"><span data-stu-id="a26a9-103">Users, sessions, and events analysis in Application Insights</span></span>

<span data-ttu-id="a26a9-104">了解人們在使用您的 Web 應用程式時，他們最感興趣的網頁、使用者的所在位置，以及他們使用何種瀏覽器與作業系統。</span><span class="sxs-lookup"><span data-stu-id="a26a9-104">Find out when people use your web app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> <span data-ttu-id="a26a9-105">使用 [Azure Application Insights](app-insights-overview.md) 來分析商務和使用量遙測。</span><span class="sxs-lookup"><span data-stu-id="a26a9-105">Analyze business and usage telemetry by using [Azure Application Insights](app-insights-overview.md).</span></span>

## <a name="get-started"></a><span data-ttu-id="a26a9-106">開始使用</span><span class="sxs-lookup"><span data-stu-id="a26a9-106">Get started</span></span>

<span data-ttu-id="a26a9-107">如果您在 Application Insights 入口網站中尚未看到 [使用者]、[工作階段] 或 [事件] 刀鋒視窗中的資料，[請了解如何開始使用使用量工具](app-insights-usage-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a26a9-107">If you don't yet see data in the users, sessions, or events blades in the Application Insights portal, [learn how to get started with the usage tools](app-insights-usage-overview.md).</span></span>

## <a name="the-users-sessions-and-events-segmentation-tool"></a><span data-ttu-id="a26a9-108">「使用者」、「工作階段」和「事件」分割工具</span><span class="sxs-lookup"><span data-stu-id="a26a9-108">The Users, Sessions, and Events segmentation tool</span></span>

<span data-ttu-id="a26a9-109">三個 [使用量] 刀鋒視窗會使用相同的工具，從三個方面將您 Web 應用程式的遙測進行交叉分析。</span><span class="sxs-lookup"><span data-stu-id="a26a9-109">Three of the usage blades use the same tool to slice and dice telemetry from your web app from three perspectives.</span></span> <span data-ttu-id="a26a9-110">透過將資料進行篩選及分割，您會發現關於不同頁面和功能之相對使用方式的深入解析。</span><span class="sxs-lookup"><span data-stu-id="a26a9-110">By filtering and splitting the data, you can uncover insights about the relative usage of different pages and features.</span></span>

* <span data-ttu-id="a26a9-111">**使用者工具**︰使用您應用程式的使用者數目和應用程式的功能。</span><span class="sxs-lookup"><span data-stu-id="a26a9-111">**Users tool**: How many people used your app and its features.</span></span>  <span data-ttu-id="a26a9-112">會使用儲存在瀏覽器 Cookie 中的匿名識別碼來計算使用者。</span><span class="sxs-lookup"><span data-stu-id="a26a9-112">Users are counted by using anonymous IDs stored in browser cookies.</span></span> <span data-ttu-id="a26a9-113">使用不同瀏覽器或電腦的單一使用者將會計算為多個使用者。</span><span class="sxs-lookup"><span data-stu-id="a26a9-113">A single person using different browsers or machines will be counted as more than one user.</span></span>
* <span data-ttu-id="a26a9-114">**工作階段工具**︰已包含應用程式的特定頁面和功能之使用者活動的工作階段數目。</span><span class="sxs-lookup"><span data-stu-id="a26a9-114">**Sessions tool**: How many sessions of user activity have included certain pages and features of your app.</span></span> <span data-ttu-id="a26a9-115">在使用者閒置半小時或連續使用 24 小時之後，就會計算工作階段。</span><span class="sxs-lookup"><span data-stu-id="a26a9-115">A session is counted after half an hour of user inactivity, or after continuous 24h of use.</span></span>
* <span data-ttu-id="a26a9-116">**事件工具**︰您應用程式的特定頁面與功能之使用頻率。</span><span class="sxs-lookup"><span data-stu-id="a26a9-116">**Events tool**: How often certain pages and features of your app are used.</span></span> <span data-ttu-id="a26a9-117">當瀏覽器從您的應用程式載入頁面時 (假如您已[將它進行檢測](app-insights-javascript.md)) 就會計算頁面檢視。</span><span class="sxs-lookup"><span data-stu-id="a26a9-117">A page view is counted when a browser loads a page from your app, provided you have [instrumented it](app-insights-javascript.md).</span></span> 

    <span data-ttu-id="a26a9-118">自訂事件代表您應用程式中的事情發生一次，通常是諸如按一下按鈕或完成某些工作等使用者互動。</span><span class="sxs-lookup"><span data-stu-id="a26a9-118">A custom event represents one occurrence of something happening in your app, often a user interaction like a button click or the completion of some task.</span></span> <span data-ttu-id="a26a9-119">將程式碼插入您的應用程式可[產生自訂事件](app-insights-api-custom-events-metrics.md#trackevent)。</span><span class="sxs-lookup"><span data-stu-id="a26a9-119">You insert code in your app to [generate custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>

![使用量工具](./media/app-insights-usage-segmentation/users.png)

## <a name="querying-for-certain-users"></a><span data-ttu-id="a26a9-121">查詢特定使用者</span><span class="sxs-lookup"><span data-stu-id="a26a9-121">Querying for Certain Users</span></span> 

<span data-ttu-id="a26a9-122">瀏覽不同群組的使用者，方法是調整 [使用者] 工具頂端的查詢選項︰</span><span class="sxs-lookup"><span data-stu-id="a26a9-122">Explore different groups of users by adjusting the query options at the top of the Users tool:</span></span> 

* <span data-ttu-id="a26a9-123">已使用者︰選擇自訂事件和頁面檢視。</span><span class="sxs-lookup"><span data-stu-id="a26a9-123">Who used: Choose custom events and page views.</span></span> 
* <span data-ttu-id="a26a9-124">期間︰選擇時間範圍。</span><span class="sxs-lookup"><span data-stu-id="a26a9-124">During: Choose a time range.</span></span> 
* <span data-ttu-id="a26a9-125">方法︰選擇將資料貯體的方式，可依一段時間或依另一個屬性 (例如瀏覽器或城市)。</span><span class="sxs-lookup"><span data-stu-id="a26a9-125">By: Choose how to bucket the data, either by a period of time or by another property such as browser or city.</span></span> 
* <span data-ttu-id="a26a9-126">分割方法︰選擇要用來分割或區隔資料的屬性。</span><span class="sxs-lookup"><span data-stu-id="a26a9-126">Split By: Choose a property by which to split or segment the data.</span></span> 
* <span data-ttu-id="a26a9-127">新增篩選條件︰將查詢根據其屬性 (例如瀏覽器或城市) 限制為特定使用者、工作階段或事件。</span><span class="sxs-lookup"><span data-stu-id="a26a9-127">Add Filters: Limit the query to certain users, sessions, or events based on their properties, such as browser or city.</span></span> 
 
## <a name="saving-and-sharing-reports"></a><span data-ttu-id="a26a9-128">儲存和共用報告</span><span class="sxs-lookup"><span data-stu-id="a26a9-128">Saving and sharing reports</span></span> 
<span data-ttu-id="a26a9-129">您可以透過下列方式來儲存使用者報告：儲存在 [我的報告] 區段中，僅供您自己私人使用；或儲存在 [共用的報告] 區段中，與擁有 Application Insights 資源存取權的其他所有人共用。</span><span class="sxs-lookup"><span data-stu-id="a26a9-129">You can save Users reports, either private just to you in the My Reports section, or shared with everyone else with access to this Application Insights resource in the Shared Reports section.</span></span>  
 
<span data-ttu-id="a26a9-130">當儲存報告或編輯其屬性時，選擇「目前相對時間範圍」將報告儲存，就會持續將資料重新整理，返回某個固定的時間量。</span><span class="sxs-lookup"><span data-stu-id="a26a9-130">While saving a report or editing its properties, choose "Current Relative Time Range" to save a report will continuously refreshed data, going back some fixed amount of time.</span></span>  
 
<span data-ttu-id="a26a9-131">選擇「目前絕對時間範圍」可儲存一組固定資料的報告。</span><span class="sxs-lookup"><span data-stu-id="a26a9-131">Choose "Current Absolute Time Range" to save a report with a fixed set of data.</span></span> <span data-ttu-id="a26a9-132">請記住，Application Insights 中的資料只會儲存 90 天，因此，如果將絕對時間範圍的報告儲存超過 90 天後，報告就會顯示為空白。</span><span class="sxs-lookup"><span data-stu-id="a26a9-132">Keep in mind that data in Application Insights is only stored for 90 days, so if more than 90 days have passed since a report with an absolute time range was saved, the report will appear empty.</span></span> 
 
## <a name="example-instances"></a><span data-ttu-id="a26a9-133">範例執行個體</span><span class="sxs-lookup"><span data-stu-id="a26a9-133">Example instances</span></span>

<span data-ttu-id="a26a9-134">範例執行個體一節說明一些符合目前查詢之個別使用者、工作階段或事件的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a26a9-134">The Example instances section shows information about a handful of individual users, sessions, or events that are matched by the current query.</span></span> <span data-ttu-id="a26a9-135">除了彙總之外，考量並瀏覽個人行為可深入解析使用者實際使用您應用程式的方式。</span><span class="sxs-lookup"><span data-stu-id="a26a9-135">Considering and exploring the behaviors of individuals, in addition to aggregates, can provide insights about how people actually use your app.</span></span> 
 
## <a name="insights"></a><span data-ttu-id="a26a9-136">深入解析</span><span class="sxs-lookup"><span data-stu-id="a26a9-136">Insights</span></span> 

<span data-ttu-id="a26a9-137">[深入解析] 資訊看板會顯示具有共同屬性的大型叢集使用者。</span><span class="sxs-lookup"><span data-stu-id="a26a9-137">The Insights sidebar shows large clusters of users that share common properties.</span></span> <span data-ttu-id="a26a9-138">這些叢集中會發現一些您應用程式使用方式的意外趨勢。</span><span class="sxs-lookup"><span data-stu-id="a26a9-138">These clusters can uncover surprising trends in how people use your app.</span></span> <span data-ttu-id="a26a9-139">例如，如果您應用程式所有的使用量中有 40% 是來自使用單一功能的使用者。</span><span class="sxs-lookup"><span data-stu-id="a26a9-139">For example, if 40% of all of the usage of your app comes from people using a single feature.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="a26a9-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a26a9-140">Next steps</span></span>
- <span data-ttu-id="a26a9-141">若要啟用使用體驗，請開始傳送「自訂事件」[](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent)或「頁面檢視」[](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views)。</span><span class="sxs-lookup"><span data-stu-id="a26a9-141">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="a26a9-142">如果您已傳送自訂事件或頁面檢視，請探索「使用量工具」，以了解使用者如何使用您的服務。</span><span class="sxs-lookup"><span data-stu-id="a26a9-142">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    - [<span data-ttu-id="a26a9-143">漏斗圖</span><span class="sxs-lookup"><span data-stu-id="a26a9-143">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="a26a9-144">保留</span><span class="sxs-lookup"><span data-stu-id="a26a9-144">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="a26a9-145">使用者流程</span><span class="sxs-lookup"><span data-stu-id="a26a9-145">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="a26a9-146">活頁簿</span><span class="sxs-lookup"><span data-stu-id="a26a9-146">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="a26a9-147">新增使用者內容</span><span class="sxs-lookup"><span data-stu-id="a26a9-147">Add user context</span></span>](app-insights-usage-send-user-context.md)

