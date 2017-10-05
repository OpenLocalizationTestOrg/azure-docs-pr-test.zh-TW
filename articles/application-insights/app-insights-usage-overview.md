---
title: "使用 Azure Application Insights 進行 Web 應用程式的使用量分析 | Microsoft Docs"
description: "了解您的使用者，以及他們如何運用您的 web 應用程式。"
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
ms.openlocfilehash: 63b74399790b718e14a5b6e09bc009a336caf928
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="usage-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="3bf0a-103">使用 Application Insights 進行 Web 應用程式的使用量分析</span><span class="sxs-lookup"><span data-stu-id="3bf0a-103">Usage analysis for web applications with Application Insights</span></span>

<span data-ttu-id="3bf0a-104">您 Web 應用程式的哪些功能最受歡迎？</span><span class="sxs-lookup"><span data-stu-id="3bf0a-104">Which features of your web app are most popular?</span></span> <span data-ttu-id="3bf0a-105">您的使用者是否利用您的應用程式達到其目標呢？</span><span class="sxs-lookup"><span data-stu-id="3bf0a-105">Do your users achieve their goals with your app?</span></span> <span data-ttu-id="3bf0a-106">他們會在特定點退出，並在稍後返回嗎？</span><span class="sxs-lookup"><span data-stu-id="3bf0a-106">Do they drop out at particular points, and do they return later?</span></span>  <span data-ttu-id="3bf0a-107">[Azure Application Insights](app-insights-overview.md) 可協助您深入了解使用者如何使用 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-107">[Azure Application Insights](app-insights-overview.md) helps you gain powerful insights into how people use your web app.</span></span> <span data-ttu-id="3bf0a-108">每次您更新應用程式時，都可以評估它適用於使用者的程度。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-108">Every time you update your app, you can assess how well it works for users.</span></span> <span data-ttu-id="3bf0a-109">您可以透過了解這些來制定下一個開發週期的相關資料導向決策。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-109">With this knowledge, you can make data driven decisions about your next development cycles.</span></span>

## <a name="send-telemetry-from-your-app"></a><span data-ttu-id="3bf0a-110">傳送來自您應用程式的遙測</span><span class="sxs-lookup"><span data-stu-id="3bf0a-110">Send telemetry from your app</span></span>

<span data-ttu-id="3bf0a-111">若要獲得最佳體驗，請同時在您的應用程式伺服器程式碼和網頁中安裝 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-111">The best experience is obtained by installing Application Insights both in your app server code, and in your web pages.</span></span> <span data-ttu-id="3bf0a-112">您應用程式的用戶端和伺服器元件會將遙測資料傳送回 Azure 入口網站以供分析。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-112">The client and server components of your app send telemetry back to the Azure portal for analysis.</span></span>

1. <span data-ttu-id="3bf0a-113">**伺服器程式碼：**為您的 [ASP.NET](app-insights-asp-net.md)、[Azure](app-insights-azure.md)、[Java](app-insights-java-get-started.md)、[Node.js](app-insights-nodejs.md) 或[其他](app-insights-platforms.md)應用程式安裝適當的模組。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-113">**Server code:** Install the appropriate module for your [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), or [other](app-insights-platforms.md) app.</span></span>

    * <span data-ttu-id="3bf0a-114">*不想安裝伺服器程式碼嗎？請直接[建立 Azure Application Insights 資源](app-insights-create-new-resource.md)。*</span><span class="sxs-lookup"><span data-stu-id="3bf0a-114">*Don't want to install server code? Just [create an Azure Application Insights resource](app-insights-create-new-resource.md).*</span></span>

2. <span data-ttu-id="3bf0a-115">**網頁程式碼：**開啟 [Azure 入口網站](https://portal.azure.com)、開啟您應用程式的 Application Insights 資源，然後開啟 [快速入門] > [監視及診斷用戶端應用程式]。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-115">**Web page code:** Open the [Azure portal](https://portal.azure.com), open the Application Insights resource for your app, and then open **Getting Started > Monitor and Diagnose Client-Side**.</span></span> 

    ![將指令碼複製到您主版頁面的標頭。](./media/app-insights-usage-overview/02-monitor-web-page.png)


3. <span data-ttu-id="3bf0a-117">**取得遙測資料：**以偵錯模式執行您的專案幾分鐘，然後在 Application Insights 的 [概觀] 刀鋒視窗中尋找結果。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-117">**Get telemetry:** Run your project in debug mode for a few minutes, and then look for results in the Overview blade in Application Insights.</span></span>

    <span data-ttu-id="3bf0a-118">發佈您的應用程式以監視應用程式的效能，並了解使用者如何利用您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-118">Publish your app to monitor your app's performance and find out what your users are doing with your app.</span></span>

## <a name="include-user-and-session-id-in-your-telemetry"></a><span data-ttu-id="3bf0a-119">將使用者與工作階段識別碼加入您的遙測</span><span class="sxs-lookup"><span data-stu-id="3bf0a-119">Include user and session ID in your telemetry</span></span>
<span data-ttu-id="3bf0a-120">若要追蹤使用者一段時間，Application Insights 需要識別他們的方式。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-120">To track users over time, Application Insights requires a way to identify them.</span></span> <span data-ttu-id="3bf0a-121">「事件工具」是唯一不需要使用者識別碼或工作階段識別碼的「使用量工具」。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-121">The Events tool is the only Usage tool that does not require a user ID or a session ID.</span></span>

<span data-ttu-id="3bf0a-122">在[此處](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context)開始傳送這些識別碼。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-122">Start sending these IDs [here](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span></span>

## <a name="explore-usage-demographics-and-statistics"></a><span data-ttu-id="3bf0a-123">探索使用量人口統計和統計資料</span><span class="sxs-lookup"><span data-stu-id="3bf0a-123">Explore usage demographics and statistics</span></span>
<span data-ttu-id="3bf0a-124">了解人們在使用您的應用程式時，他們最感興趣的網頁、使用者的所在位置，以及他們使用何種瀏覽器與作業系統。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-124">Find out when people use your app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> 

<span data-ttu-id="3bf0a-125">使用者與工作階段報告會依頁面或自訂事件來篩選資料，並透過諸如位置、環境及頁面等屬性，將這些頁面或自訂事件進行區隔。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-125">The Users and Sessions reports filter your data by pages or custom events, and segment them by properties such as location, environment, and page.</span></span> <span data-ttu-id="3bf0a-126">您也可以新增自己的篩選條件。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-126">You can also add your own filters.</span></span>

![使用者](./media/app-insights-usage-overview/users.png)  

<span data-ttu-id="3bf0a-128">右方情資指出資料集內的有趣模式。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-128">Insights on the right point out interesting patterns in the set of data.</span></span>  

* <span data-ttu-id="3bf0a-129">**使用者**報告會在您所選擇的時間週期內，計算存取您網頁的唯一使用者數目。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-129">The **Users** report counts the numbers of unique users that access your pages within your chosen time periods.</span></span> <span data-ttu-id="3bf0a-130">(會使用 Cookie 來計算使用者。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-130">(Users are counted by using cookies.</span></span> <span data-ttu-id="3bf0a-131">如果有人使用不同的瀏覽器或用戶端電腦來存取您的網站，或清除其 Cookie，系統就會將他們計算為多次。)</span><span class="sxs-lookup"><span data-stu-id="3bf0a-131">If someone accesses your site with different browsers or client machines, or clears their cookies, then they will be counted more than once.)</span></span>
* <span data-ttu-id="3bf0a-132">**工作階段**報告會計算存取您網站之使用者工作階段的數目。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-132">The **Sessions** report counts the number of user sessions that access your site.</span></span> <span data-ttu-id="3bf0a-133">工作階段是使用者活動的一段時間，在閒置時間超過半小時後就會加以終止。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-133">A session is a period of activity by a user, terminated by a period of inactivity of more than half an hour.</span></span>

[<span data-ttu-id="3bf0a-134">進一步了解「使用者」、「工作階段」和「事件」工具</span><span class="sxs-lookup"><span data-stu-id="3bf0a-134">More about the Users, Sessions, and Events tools</span></span>](app-insights-usage-segmentation.md)  

## <a name="page-views"></a><span data-ttu-id="3bf0a-135">頁面檢視</span><span class="sxs-lookup"><span data-stu-id="3bf0a-135">Page views</span></span>

<span data-ttu-id="3bf0a-136">在 [使用量] 刀鋒視窗中，按一下 [頁面檢視] 圖格可取得最常用頁面的明細：</span><span class="sxs-lookup"><span data-stu-id="3bf0a-136">From the Usage blade, click through the Page Views tile to get a breakdown of your most popular pages:</span></span>

![從 [概觀] 刀鋒視窗，按一下 [頁面檢視] 圖表](./media/app-insights-usage-overview/05-games.png)

<span data-ttu-id="3bf0a-138">上述範例來自遊戲網站。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-138">The example above is from a games web site.</span></span> <span data-ttu-id="3bf0a-139">從這些圖表，我們可以立即看到：</span><span class="sxs-lookup"><span data-stu-id="3bf0a-139">From the charts, we can instantly see:</span></span>

* <span data-ttu-id="3bf0a-140">在上一週使用量未改善。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-140">Usage hasn't improved in the past week.</span></span> <span data-ttu-id="3bf0a-141">也許我們應該考慮搜尋引擎最佳化？</span><span class="sxs-lookup"><span data-stu-id="3bf0a-141">Maybe we should think about search engine optimization?</span></span>
* <span data-ttu-id="3bf0a-142">網球是最受歡迎的遊戲頁面。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-142">Tennis is the most popular game page.</span></span> <span data-ttu-id="3bf0a-143">讓我們將焦點放在此頁面的進一步改善上。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-143">Let's focus on further improvements to this page.</span></span>
* <span data-ttu-id="3bf0a-144">平均而言，使用者大約每週瀏覽網球頁面三次。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-144">On average, users visit the Tennis page about three times per week.</span></span> <span data-ttu-id="3bf0a-145">(與使用者相比，工作階段數大約多出三倍)。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-145">(There are about three times more sessions than users.)</span></span>
* <span data-ttu-id="3bf0a-146">大多數使用者都是在美國工作週且在工作時間瀏覽此網站。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-146">Most users visit the site during the U.S. working week, and in working hours.</span></span> <span data-ttu-id="3bf0a-147">也許我們應該在網頁上提供一個 [快速隱藏] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-147">Perhaps we should provide a "quick hide" button on the web page.</span></span>
* <span data-ttu-id="3bf0a-148">圖表上的[註解](app-insights-annotations.md)會顯示新版網站的部署時間。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-148">The [annotations](app-insights-annotations.md) on the chart show when new versions of the website were deployed.</span></span> <span data-ttu-id="3bf0a-149">沒有任何一個最近的部署對使用量有明顯的影響。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-149">None of the recent deployments had a noticeable effect on usage.</span></span>

<span data-ttu-id="3bf0a-150">如果您要更詳細調查網站的流量，像是依您的網站在其頁面檢視遙測中所傳送之自訂屬性進行分割，該怎麼做？</span><span class="sxs-lookup"><span data-stu-id="3bf0a-150">What if you want to investigate the traffic to your site in more detail, like splitting by a custom property your site sends in its page view telemetry?</span></span>

1. <span data-ttu-id="3bf0a-151">在 [Application Insights 資源] 功能表中，開啟「事件」工具。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-151">Open the **Events** tool in the Application Insights resource menu.</span></span> <span data-ttu-id="3bf0a-152">此工具可讓您根據各種的篩選、同群使用者及區隔等選項，將應用程式所傳送出的頁面檢視和自訂事件數目進行分析。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-152">This tool lets you analyze how many page views and custom events were sent from your app, based on a variety of filtering, cohorting, and segmentation options.</span></span>
2. <span data-ttu-id="3bf0a-153">在 [已使用人員] 下拉式清單中，選取 [任何頁面檢視]。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-153">In the "Who used" dropdown, select "Any Page View".</span></span>
3. <span data-ttu-id="3bf0a-154">在 [分割者] 下拉式清單中，選取要用來分割您頁面檢視遙測的屬性。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-154">In the "Split by" dropdown, select a property by which to split your page view telemetry.</span></span>

## <a name="retention---how-many-users-come-back"></a><span data-ttu-id="3bf0a-155">保留期 - 回來使用的使用者人數？</span><span class="sxs-lookup"><span data-stu-id="3bf0a-155">Retention - how many users come back?</span></span>

<span data-ttu-id="3bf0a-156">保留期可根據同群使用者在特定時間貯體期間執行的某些商務動作，協助您了解使用者返回使用其應用程式的頻率。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-156">Retention helps you understand how often your users return to use their app, based on cohorts of users that performed some business action during a certain time bucket.</span></span> 

- <span data-ttu-id="3bf0a-157">了解相較於其他功能，哪些特定功能會讓使用者回來使用</span><span class="sxs-lookup"><span data-stu-id="3bf0a-157">Understand what specific features cause users to come back more than others</span></span> 
- <span data-ttu-id="3bf0a-158">根據實際使用者資料的表單假設</span><span class="sxs-lookup"><span data-stu-id="3bf0a-158">Form hypotheses based on real user data</span></span> 
- <span data-ttu-id="3bf0a-159">判斷保留期是否為您產品的問題</span><span class="sxs-lookup"><span data-stu-id="3bf0a-159">Determine whether retention is a problem in your product</span></span> 

![保留](./media/app-insights-usage-overview/retention.png) 

<span data-ttu-id="3bf0a-161">在最上層的保留期控制項可讓您定義用來計算保留期的特定事件和時間範圍。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-161">The retention controls on top allow you to define specific events and time range to calculate retention.</span></span> <span data-ttu-id="3bf0a-162">中間的圖表會依指定的時間範圍提供整體保留期百分比的視覺表示法。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-162">The graph in the middle gives a visual representation of the overall retention percentage by the time range specified.</span></span> <span data-ttu-id="3bf0a-163">底部圖表代表指定時間內的個別保留期。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-163">The graph on the bottom represents individual retention in a given time period.</span></span> <span data-ttu-id="3bf0a-164">此詳細資料等級會使用更詳細的資料粒度，讓您了解使用者在做什麼，以及可能會影響舊有使用者的因素。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-164">This level of detail allows you to understand what your users are doing and what might affect returning users on a more detailed granularity.</span></span>  

[<span data-ttu-id="3bf0a-165">深入了解保留期工具</span><span class="sxs-lookup"><span data-stu-id="3bf0a-165">More about the Retention tool</span></span>](app-insights-usage-retention.md)

## <a name="custom-business-events"></a><span data-ttu-id="3bf0a-166">自訂商務事件</span><span class="sxs-lookup"><span data-stu-id="3bf0a-166">Custom business events</span></span>

<span data-ttu-id="3bf0a-167">若要清楚了解使用者會使用您的 Web 應用程式來做什麼，插入程式碼行來記錄自訂事件會很有用。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-167">To get a clear understanding of what users do with your web app, it's useful to insert lines of code to log custom events.</span></span> <span data-ttu-id="3bf0a-168">這些事件可以追蹤任何項目，從詳細的使用者動作 (例如按一下特定按鈕)，到更重要的商務事件 (例如購物或遊戲獲勝)。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-168">These events can track anything from detailed user actions such as clicking specific buttons, to more significant business events such as making a purchase or winning a game.</span></span> 

<span data-ttu-id="3bf0a-169">雖然在某些情況下，頁面檢視可以代表有用的事件，但一般而言它並不正確。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-169">Although in some cases, page views can represent useful events, it isn't true in general.</span></span> <span data-ttu-id="3bf0a-170">使用者可以開啟產品網頁而無需購買產品。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-170">A user can open a product page without buying the product.</span></span> 

<span data-ttu-id="3bf0a-171">您可以使用特定商務事件，透過網站將使用者的進度製作成圖表。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-171">With specific business events, you can chart your users' progress through your site.</span></span> <span data-ttu-id="3bf0a-172">您可以找出他們對不同選項的偏好，以及它們退出或遇到困難之處。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-172">You can find out their preferences for different options, and where they drop out or have difficulties.</span></span> <span data-ttu-id="3bf0a-173">您可以透過了解這些對開發待處理項目的優先順序做出明智決策。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-173">With this knowledge, you can make informed decisions about the priorities in your development backlog.</span></span>

<span data-ttu-id="3bf0a-174">可以在網頁中記錄事件︰</span><span class="sxs-lookup"><span data-stu-id="3bf0a-174">Events can be logged in the web page:</span></span>

```JavaScript

    appInsights.trackEvent("ExpandDetailTab", {DetailTab: tabName});
```

<span data-ttu-id="3bf0a-175">或在 Web 應用程式的伺服器端︰</span><span class="sxs-lookup"><span data-stu-id="3bf0a-175">Or in the server side of the web app:</span></span>

```C#
    var tc = new Microsoft.ApplicationInsights.TelemetryClient();
    tc.TrackEvent("CreatedAccount", new Dictionary<string,string> {"AccountType":account.Type}, null);
    ...
    tc.TrackEvent("AddedItemToCart", new Dictionary<string,string> {"Item":item.Name}, null);
    ...
    tc.TrackEvent("CompletedPurchase");
```

<span data-ttu-id="3bf0a-176">您可以將屬性值附加至這些事件，當您在入口網站中檢查它們時，就可以將事件進行篩選或分割。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-176">You can attach property values to these events, so that you can filter or split the events when you inspect them in the portal.</span></span> <span data-ttu-id="3bf0a-177">此外，會將一組標準的屬性附加至每個事件，例如匿名使用者識別碼，這可讓您追蹤個別使用者的活動順序。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-177">In addition, a standard set of properties is attached to each event, such as anonymous user ID, which allows you to trace the sequence of activities of an individual user.</span></span>

<span data-ttu-id="3bf0a-178">深入了解[自訂事件](app-insights-api-custom-events-metrics.md#trackevent)和[屬性](app-insights-api-custom-events-metrics.md#properties)。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-178">Learn more about [custom events](app-insights-api-custom-events-metrics.md#trackevent) and [properties](app-insights-api-custom-events-metrics.md#properties).</span></span>

### <a name="slice-and-dice-events"></a><span data-ttu-id="3bf0a-179">將事件進行交叉分析</span><span class="sxs-lookup"><span data-stu-id="3bf0a-179">Slice and dice events</span></span>

<span data-ttu-id="3bf0a-180">在「使用者」、「工作階段」和「事件」工具中，您可以依使用者、事件名稱和屬性將自訂事件進行交叉分析。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-180">In the Users, Sessions, and Events tools, you can slice and dice custom events by user, event name, and properties.</span></span>
<span data-ttu-id="3bf0a-181">![使用者](./media/app-insights-usage-overview/users.png)</span><span class="sxs-lookup"><span data-stu-id="3bf0a-181">![Users](./media/app-insights-usage-overview/users.png)</span></span>  
  
## <a name="design-the-telemetry-with-the-app"></a><span data-ttu-id="3bf0a-182">使用應用程式來設計遙測</span><span class="sxs-lookup"><span data-stu-id="3bf0a-182">Design the telemetry with the app</span></span>

<span data-ttu-id="3bf0a-183">當您在設計您應用程式的每項功能時，請考慮要如何利用使用者來測量它的成功。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-183">When you are designing each feature of your app, consider how you are going to measure its success with your users.</span></span> <span data-ttu-id="3bf0a-184">決定您需要記錄哪些商務事件，並從開頭將這些事件的追蹤呼叫編碼至應用程式。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-184">Decide what business events you need to record, and code the tracking calls for those events into your app from the start.</span></span>

## <a name="a--b-testing"></a><span data-ttu-id="3bf0a-185">A | B 測試</span><span class="sxs-lookup"><span data-stu-id="3bf0a-185">A | B Testing</span></span>
<span data-ttu-id="3bf0a-186">如果您不知道哪個功能的變數將更可能成功，請兩者都釋出，讓兩者都可供不同使用者存取。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-186">If you don't know which variant of a feature will be more successful, release both of them, making each accessible to different users.</span></span> <span data-ttu-id="3bf0a-187">測量每一個的成功，然後移至整合的版本。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-187">Measure the success of each, and then move to a unified version.</span></span>

<span data-ttu-id="3bf0a-188">針對此技術，您會將獨特的屬性值附加到每個應用程式版本所傳送的所有遙測。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-188">For this technique, you attach distinct property values to all the telemetry that is sent by each version of your app.</span></span> <span data-ttu-id="3bf0a-189">您可以在作用中 TelemetryContext 中定義屬性來執行該動作。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-189">You can do that by defining properties in the active TelemetryContext.</span></span> <span data-ttu-id="3bf0a-190">這些預設屬性會加入到應用程式傳送的每個遙測訊息 - 不只是您的自訂訊息，還有標準遙測。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-190">These default properties are added to every telemetry message that the application sends - not just your custom messages, but the standard telemetry as well.</span></span>

<span data-ttu-id="3bf0a-191">在 Application Insights 入口網站中，將資料依屬性值篩選並分割，以便比較不同版本。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-191">In the Application Insights portal, filter and split your data on the property values, so as to compare the different versions.</span></span>

<span data-ttu-id="3bf0a-192">若要這樣做，[請設定遙測初始設定式](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer)：</span><span class="sxs-lookup"><span data-stu-id="3bf0a-192">To do this, [set up a telemetry initializer](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span></span>

```C#


    // Telemetry initializer class
    public class MyTelemetryInitializer : ITelemetryInitializer
    {
        public void Initialize (ITelemetry telemetry)
        {
            telemetry.Properties["AppVersion"] = "v2.1";
        }
    }
```

<span data-ttu-id="3bf0a-193">在 Web 應用程式初始設定式例如 Global.asax.cs 中：</span><span class="sxs-lookup"><span data-stu-id="3bf0a-193">In the web app initializer such as Global.asax.cs:</span></span>

```C#

    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```

<span data-ttu-id="3bf0a-194">所有新的 TelemetryClients 都會自動新增您指定的屬性值。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-194">All new TelemetryClients automatically add the property value you specify.</span></span> <span data-ttu-id="3bf0a-195">個別的遙測事件可以覆寫預設值。</span><span class="sxs-lookup"><span data-stu-id="3bf0a-195">Individual telemetry events can override the default values.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3bf0a-196">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3bf0a-196">Next steps</span></span>
   - [<span data-ttu-id="3bf0a-197">使用者、工作階段、事件</span><span class="sxs-lookup"><span data-stu-id="3bf0a-197">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
   - [<span data-ttu-id="3bf0a-198">漏斗圖</span><span class="sxs-lookup"><span data-stu-id="3bf0a-198">Funnels</span></span>](usage-funnels.md)
   - [<span data-ttu-id="3bf0a-199">保留</span><span class="sxs-lookup"><span data-stu-id="3bf0a-199">Retention</span></span>](app-insights-usage-retention.md)
   - [<span data-ttu-id="3bf0a-200">使用者流程</span><span class="sxs-lookup"><span data-stu-id="3bf0a-200">User Flows</span></span>](app-insights-usage-flows.md)
   - [<span data-ttu-id="3bf0a-201">活頁簿</span><span class="sxs-lookup"><span data-stu-id="3bf0a-201">Workbooks</span></span>](app-insights-usage-workbooks.md)
   - [<span data-ttu-id="3bf0a-202">新增使用者內容</span><span class="sxs-lookup"><span data-stu-id="3bf0a-202">Add user context</span></span>](app-insights-usage-send-user-context.md)
