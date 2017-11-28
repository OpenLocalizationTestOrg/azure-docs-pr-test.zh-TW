---
title: "使用 Azure Application Insights web 應用程式的 aaaUsage 分析 |Microsoft 文件"
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
ms.openlocfilehash: f7f9173cf411fa0d2dfb3b5ba99134a02bbc0e89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="usage-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="0ca5a-103">使用 Application Insights 進行 Web 應用程式的使用量分析</span><span class="sxs-lookup"><span data-stu-id="0ca5a-103">Usage analysis for web applications with Application Insights</span></span>

<span data-ttu-id="0ca5a-104">您 Web 應用程式的哪些功能最受歡迎？</span><span class="sxs-lookup"><span data-stu-id="0ca5a-104">Which features of your web app are most popular?</span></span> <span data-ttu-id="0ca5a-105">您的使用者是否利用您的應用程式達到其目標呢？</span><span class="sxs-lookup"><span data-stu-id="0ca5a-105">Do your users achieve their goals with your app?</span></span> <span data-ttu-id="0ca5a-106">他們會在特定點退出，並在稍後返回嗎？</span><span class="sxs-lookup"><span data-stu-id="0ca5a-106">Do they drop out at particular points, and do they return later?</span></span>  <span data-ttu-id="0ca5a-107">[Azure Application Insights](app-insights-overview.md) 可協助您深入了解使用者如何使用 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-107">[Azure Application Insights](app-insights-overview.md) helps you gain powerful insights into how people use your web app.</span></span> <span data-ttu-id="0ca5a-108">每次您更新應用程式時，都可以評估它適用於使用者的程度。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-108">Every time you update your app, you can assess how well it works for users.</span></span> <span data-ttu-id="0ca5a-109">您可以透過了解這些來制定下一個開發週期的相關資料導向決策。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-109">With this knowledge, you can make data driven decisions about your next development cycles.</span></span>

## <a name="send-telemetry-from-your-app"></a><span data-ttu-id="0ca5a-110">傳送來自您應用程式的遙測</span><span class="sxs-lookup"><span data-stu-id="0ca5a-110">Send telemetry from your app</span></span>

<span data-ttu-id="0ca5a-111">藉由在應用程式伺服器程式碼，和您的網頁中安裝 Application Insights 取得 hello 最佳體驗。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-111">hello best experience is obtained by installing Application Insights both in your app server code, and in your web pages.</span></span> <span data-ttu-id="0ca5a-112">hello 用戶端和伺服器元件，您的應用程式傳送遙測後 toohello Azure 入口網站進行分析。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-112">hello client and server components of your app send telemetry back toohello Azure portal for analysis.</span></span>

1. <span data-ttu-id="0ca5a-113">**伺服端程式碼：**安裝 hello 適當模組您[ASP.NET](app-insights-asp-net.md)， [Azure](app-insights-azure.md)， [Java](app-insights-java-get-started.md)， [Node.js](app-insights-nodejs.md)，或[其他](app-insights-platforms.md)應用程式。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-113">**Server code:** Install hello appropriate module for your [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), or [other](app-insights-platforms.md) app.</span></span>

    * <span data-ttu-id="0ca5a-114">*不想 tooinstall 伺服端程式碼嗎？請直接[建立 Azure Application Insights 資源](app-insights-create-new-resource.md)。*</span><span class="sxs-lookup"><span data-stu-id="0ca5a-114">*Don't want tooinstall server code? Just [create an Azure Application Insights resource](app-insights-create-new-resource.md).*</span></span>

2. <span data-ttu-id="0ca5a-115">**網頁程式碼：**開啟 hello [Azure 入口網站](https://portal.azure.com)，開啟您的應用程式的 hello Application Insights 資源，並開啟**入門 > 監視和診斷用戶端**。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-115">**Web page code:** Open hello [Azure portal](https://portal.azure.com), open hello Application Insights resource for your app, and then open **Getting Started > Monitor and Diagnose Client-Side**.</span></span> 

    ![Hello 指令碼複製到的主版網頁的 hello 開頭。](./media/app-insights-usage-overview/02-monitor-web-page.png)


3. <span data-ttu-id="0ca5a-117">**取得遙測：**幾分鐘，偵錯模式執行您的專案，然後尋找 Application Insights 中的 hello 概觀刀鋒視窗中的結果。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-117">**Get telemetry:** Run your project in debug mode for a few minutes, and then look for results in hello Overview blade in Application Insights.</span></span>

    <span data-ttu-id="0ca5a-118">發行應用程式 toomonitor 應用程式效能，並找出您的使用者與您的應用程式的行為。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-118">Publish your app toomonitor your app's performance and find out what your users are doing with your app.</span></span>

## <a name="include-user-and-session-id-in-your-telemetry"></a><span data-ttu-id="0ca5a-119">將使用者與工作階段識別碼加入您的遙測</span><span class="sxs-lookup"><span data-stu-id="0ca5a-119">Include user and session ID in your telemetry</span></span>
<span data-ttu-id="0ca5a-120">tootrack 使用者一段時間，Application Insights 需要方式 tooidentify 它們。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-120">tootrack users over time, Application Insights requires a way tooidentify them.</span></span> <span data-ttu-id="0ca5a-121">hello 事件工具是 hello 唯一的 [使用量] 工具，不需要使用者識別碼或工作階段識別碼。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-121">hello Events tool is hello only Usage tool that does not require a user ID or a session ID.</span></span>

<span data-ttu-id="0ca5a-122">在[此處](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context)開始傳送這些識別碼。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-122">Start sending these IDs [here](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span></span>

## <a name="explore-usage-demographics-and-statistics"></a><span data-ttu-id="0ca5a-123">探索使用量人口統計和統計資料</span><span class="sxs-lookup"><span data-stu-id="0ca5a-123">Explore usage demographics and statistics</span></span>
<span data-ttu-id="0ca5a-124">了解人們在使用您的應用程式時，他們最感興趣的網頁、使用者的所在位置，以及他們使用何種瀏覽器與作業系統。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-124">Find out when people use your app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> 

<span data-ttu-id="0ca5a-125">hello 使用者和工作階段報表篩選網頁或自訂的事件資料，而且這些區段的屬性，例如位置、 環境及頁面。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-125">hello Users and Sessions reports filter your data by pages or custom events, and segment them by properties such as location, environment, and page.</span></span> <span data-ttu-id="0ca5a-126">您也可以新增自己的篩選條件。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-126">You can also add your own filters.</span></span>

![使用者](./media/app-insights-usage-overview/users.png)  

<span data-ttu-id="0ca5a-128">Hello 右邊的洞察能力點出 hello 資料集的有趣模式。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-128">Insights on hello right point out interesting patterns in hello set of data.</span></span>  

* <span data-ttu-id="0ca5a-129">hello**使用者**報告會算進 hello 存取您的網頁，您所選擇的時間週期內的唯一使用者數目。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-129">hello **Users** report counts hello numbers of unique users that access your pages within your chosen time periods.</span></span> <span data-ttu-id="0ca5a-130">(會使用 Cookie 來計算使用者。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-130">(Users are counted by using cookies.</span></span> <span data-ttu-id="0ca5a-131">如果有人使用不同的瀏覽器或用戶端電腦來存取您的網站，或清除其 Cookie，系統就會將他們計算為多次。)</span><span class="sxs-lookup"><span data-stu-id="0ca5a-131">If someone accesses your site with different browsers or client machines, or clears their cookies, then they will be counted more than once.)</span></span>
* <span data-ttu-id="0ca5a-132">hello**工作階段**報告會算進 hello 存取您的網站的使用者工作階段數目。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-132">hello **Sessions** report counts hello number of user sessions that access your site.</span></span> <span data-ttu-id="0ca5a-133">工作階段是使用者活動的一段時間，在閒置時間超過半小時後就會加以終止。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-133">A session is a period of activity by a user, terminated by a period of inactivity of more than half an hour.</span></span>

[<span data-ttu-id="0ca5a-134">進一步了解 hello 使用者、 工作階段和事件工具</span><span class="sxs-lookup"><span data-stu-id="0ca5a-134">More about hello Users, Sessions, and Events tools</span></span>](app-insights-usage-segmentation.md)  

## <a name="page-views"></a><span data-ttu-id="0ca5a-135">頁面檢視</span><span class="sxs-lookup"><span data-stu-id="0ca5a-135">Page views</span></span>

<span data-ttu-id="0ca5a-136">在 hello 使用量刀鋒視窗中，按一下 透過 hello 頁面檢視磚 tooget 最受歡迎頁面的分析：</span><span class="sxs-lookup"><span data-stu-id="0ca5a-136">From hello Usage blade, click through hello Page Views tile tooget a breakdown of your most popular pages:</span></span>

![從 hello 概觀刀鋒視窗中，按一下 hello 頁面檢視圖表](./media/app-insights-usage-overview/05-games.png)

<span data-ttu-id="0ca5a-138">hello 上述範例中取自遊戲的網站。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-138">hello example above is from a games web site.</span></span> <span data-ttu-id="0ca5a-139">從 hello 圖表，我們可以立即看到：</span><span class="sxs-lookup"><span data-stu-id="0ca5a-139">From hello charts, we can instantly see:</span></span>

* <span data-ttu-id="0ca5a-140">過去一週時，未在 hello 改進使用方式。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-140">Usage hasn't improved in hello past week.</span></span> <span data-ttu-id="0ca5a-141">也許我們應該考慮搜尋引擎最佳化？</span><span class="sxs-lookup"><span data-stu-id="0ca5a-141">Maybe we should think about search engine optimization?</span></span>
* <span data-ttu-id="0ca5a-142">鱣是 hello 最受歡迎的遊戲頁面。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-142">Tennis is hello most popular game page.</span></span> <span data-ttu-id="0ca5a-143">讓我們重點討論進一步改進 toothis 頁面。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-143">Let's focus on further improvements toothis page.</span></span>
* <span data-ttu-id="0ca5a-144">平均而言，使用者瀏覽 hello 鱣頁面三倍每週。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-144">On average, users visit hello Tennis page about three times per week.</span></span> <span data-ttu-id="0ca5a-145">(與使用者相比，工作階段數大約多出三倍)。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-145">(There are about three times more sessions than users.)</span></span>
* <span data-ttu-id="0ca5a-146">Hello 美國工作週、 期間以及在工作時間，大部分的使用者瀏覽 hello 站台。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-146">Most users visit hello site during hello U.S. working week, and in working hours.</span></span> <span data-ttu-id="0ca5a-147">可能是我們應該 hello 網頁上提供的 [快速隱藏] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-147">Perhaps we should provide a "quick hide" button on hello web page.</span></span>
* <span data-ttu-id="0ca5a-148">hello[註解](app-insights-annotations.md)hello 圖表上顯示 當已部署的 hello 網站的新版本。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-148">hello [annotations](app-insights-annotations.md) on hello chart show when new versions of hello website were deployed.</span></span> <span data-ttu-id="0ca5a-149">無 hello 新的部署有明顯的影響，在使用方式。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-149">None of hello recent deployments had a noticeable effect on usage.</span></span>

<span data-ttu-id="0ca5a-150">如果您想 tooinvestigate hello 流量 tooyour 站台的詳細資料，例如分割您的站台傳送它的網頁檢視遙測中的自訂屬性的嗎？</span><span class="sxs-lookup"><span data-stu-id="0ca5a-150">What if you want tooinvestigate hello traffic tooyour site in more detail, like splitting by a custom property your site sends in its page view telemetry?</span></span>

1. <span data-ttu-id="0ca5a-151">開啟 hello**事件**hello Application Insights 資源功能表中的工具。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-151">Open hello **Events** tool in hello Application Insights resource menu.</span></span> <span data-ttu-id="0ca5a-152">此工具可讓您根據各種的篩選、同群使用者及區隔等選項，將應用程式所傳送出的頁面檢視和自訂事件數目進行分析。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-152">This tool lets you analyze how many page views and custom events were sent from your app, based on a variety of filtering, cohorting, and segmentation options.</span></span>
2. <span data-ttu-id="0ca5a-153">在 hello 「 誰使用 」 的下拉式清單中，選取"Any 頁面檢視 」。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-153">In hello "Who used" dropdown, select "Any Page View".</span></span>
3. <span data-ttu-id="0ca5a-154">在 hello 「 分割 」 的下拉式清單中選取哪個 toosplit 網頁檢視遙測的屬性。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-154">In hello "Split by" dropdown, select a property by which toosplit your page view telemetry.</span></span>

## <a name="retention---how-many-users-come-back"></a><span data-ttu-id="0ca5a-155">保留期 - 回來使用的使用者人數？</span><span class="sxs-lookup"><span data-stu-id="0ca5a-155">Retention - how many users come back?</span></span>

<span data-ttu-id="0ca5a-156">保留可協助您了解頻率您的使用者會傳回 toouse 應用程式中，根據 cohorts 的執行期間特定時間貯體某些商務動作的使用者。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-156">Retention helps you understand how often your users return toouse their app, based on cohorts of users that performed some business action during a certain time bucket.</span></span> 

- <span data-ttu-id="0ca5a-157">了解哪些特定的功能會導致使用者 toocome 後比其他更多</span><span class="sxs-lookup"><span data-stu-id="0ca5a-157">Understand what specific features cause users toocome back more than others</span></span> 
- <span data-ttu-id="0ca5a-158">根據實際使用者資料的表單假設</span><span class="sxs-lookup"><span data-stu-id="0ca5a-158">Form hypotheses based on real user data</span></span> 
- <span data-ttu-id="0ca5a-159">判斷保留期是否為您產品的問題</span><span class="sxs-lookup"><span data-stu-id="0ca5a-159">Determine whether retention is a problem in your product</span></span> 

![保留](./media/app-insights-usage-overview/retention.png) 

<span data-ttu-id="0ca5a-161">在最上層的 hello 保留控制項可讓您 toodefine 特定事件和時間範圍 toocalculate 保留。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-161">hello retention controls on top allow you toodefine specific events and time range toocalculate retention.</span></span> <span data-ttu-id="0ca5a-162">hello 圖 hello 中間讓 hello 的視覺表示法所指定的時間範圍 hello 整體保留百分比。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-162">hello graph in hello middle gives a visual representation of hello overall retention percentage by hello time range specified.</span></span> <span data-ttu-id="0ca5a-163">hello 下方 hello 圖形代表個別的保留在指定的時段內。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-163">hello graph on hello bottom represents individual retention in a given time period.</span></span> <span data-ttu-id="0ca5a-164">此詳細層級可讓您 toounderstand 哪些使用者執行的工作和功能可能會影響傳回的使用者，更詳細的資料粒度。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-164">This level of detail allows you toounderstand what your users are doing and what might affect returning users on a more detailed granularity.</span></span>  

[<span data-ttu-id="0ca5a-165">Hello 保留工具有關的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="0ca5a-165">More about hello Retention tool</span></span>](app-insights-usage-retention.md)

## <a name="custom-business-events"></a><span data-ttu-id="0ca5a-166">自訂商務事件</span><span class="sxs-lookup"><span data-stu-id="0ca5a-166">Custom business events</span></span>

<span data-ttu-id="0ca5a-167">tooget 哪些使用者清楚了解如何處理您的 web 應用程式，就很有用的 tooinsert toolog 自訂事件時，程式碼行。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-167">tooget a clear understanding of what users do with your web app, it's useful tooinsert lines of code toolog custom events.</span></span> <span data-ttu-id="0ca5a-168">這些事件可以從詳細的使用者動作，例如按一下特定的按鈕，toomore 重要的商務事件，例如在購買或獲勝追蹤任何項目。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-168">These events can track anything from detailed user actions such as clicking specific buttons, toomore significant business events such as making a purchase or winning a game.</span></span> 

<span data-ttu-id="0ca5a-169">雖然在某些情況下，頁面檢視可以代表有用的事件，但一般而言它並不正確。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-169">Although in some cases, page views can represent useful events, it isn't true in general.</span></span> <span data-ttu-id="0ca5a-170">使用者可以開啟 [產品] 頁面上，而不購買 hello 產品。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-170">A user can open a product page without buying hello product.</span></span> 

<span data-ttu-id="0ca5a-171">您可以使用特定商務事件，透過網站將使用者的進度製作成圖表。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-171">With specific business events, you can chart your users' progress through your site.</span></span> <span data-ttu-id="0ca5a-172">您可以找出他們對不同選項的偏好，以及它們退出或遇到困難之處。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-172">You can find out their preferences for different options, and where they drop out or have difficulties.</span></span> <span data-ttu-id="0ca5a-173">使用這項知識，您可以做出有關明智 hello 優先順序開發待辦項目中。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-173">With this knowledge, you can make informed decisions about hello priorities in your development backlog.</span></span>

<span data-ttu-id="0ca5a-174">可以在 hello web 網頁中記錄事件：</span><span class="sxs-lookup"><span data-stu-id="0ca5a-174">Events can be logged in hello web page:</span></span>

```JavaScript

    appInsights.trackEvent("ExpandDetailTab", {DetailTab: tabName});
```

<span data-ttu-id="0ca5a-175">或 hello 伺服器端的 hello web 應用程式：</span><span class="sxs-lookup"><span data-stu-id="0ca5a-175">Or in hello server side of hello web app:</span></span>

```C#
    var tc = new Microsoft.ApplicationInsights.TelemetryClient();
    tc.TrackEvent("CreatedAccount", new Dictionary<string,string> {"AccountType":account.Type}, null);
    ...
    tc.TrackEvent("AddedItemToCart", new Dictionary<string,string> {"Item":item.Name}, null);
    ...
    tc.TrackEvent("CompletedPurchase");
```

<span data-ttu-id="0ca5a-176">讓您可以篩選或分割 hello 事件，當您檢查這些 hello 入口網站中，您可以附加屬性值 toothese 事件。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-176">You can attach property values toothese events, so that you can filter or split hello events when you inspect them in hello portal.</span></span> <span data-ttu-id="0ca5a-177">此外，一組標準的屬性是使用者的附加的 tooeach 事件，例如匿名使用者識別碼，可讓您 tootrace hello 一連串個別的活動。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-177">In addition, a standard set of properties is attached tooeach event, such as anonymous user ID, which allows you tootrace hello sequence of activities of an individual user.</span></span>

<span data-ttu-id="0ca5a-178">深入了解[自訂事件](app-insights-api-custom-events-metrics.md#trackevent)和[屬性](app-insights-api-custom-events-metrics.md#properties)。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-178">Learn more about [custom events](app-insights-api-custom-events-metrics.md#trackevent) and [properties](app-insights-api-custom-events-metrics.md#properties).</span></span>

### <a name="slice-and-dice-events"></a><span data-ttu-id="0ca5a-179">將事件進行交叉分析</span><span class="sxs-lookup"><span data-stu-id="0ca5a-179">Slice and dice events</span></span>

<span data-ttu-id="0ca5a-180">Hello 使用者、 工作階段和事件工具 中，您可以配量，並分析依使用者、 事件名稱和屬性的自訂事件。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-180">In hello Users, Sessions, and Events tools, you can slice and dice custom events by user, event name, and properties.</span></span>
<span data-ttu-id="0ca5a-181">![使用者](./media/app-insights-usage-overview/users.png)</span><span class="sxs-lookup"><span data-stu-id="0ca5a-181">![Users](./media/app-insights-usage-overview/users.png)</span></span>  
  
## <a name="design-hello-telemetry-with-hello-app"></a><span data-ttu-id="0ca5a-182">設計 hello 與 hello 應用程式的遙測</span><span class="sxs-lookup"><span data-stu-id="0ca5a-182">Design hello telemetry with hello app</span></span>

<span data-ttu-id="0ca5a-183">當您在設計您的應用程式的每項功能時，請考慮要如何 toomeasure 成功與您的使用者。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-183">When you are designing each feature of your app, consider how you are going toomeasure its success with your users.</span></span> <span data-ttu-id="0ca5a-184">決定您需要 toorecord，和程式碼到您的應用程式追蹤的事件會呼叫從 hello hello 的商務事件的開始。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-184">Decide what business events you need toorecord, and code hello tracking calls for those events into your app from hello start.</span></span>

## <a name="a--b-testing"></a><span data-ttu-id="0ca5a-185">A | B 測試</span><span class="sxs-lookup"><span data-stu-id="0ca5a-185">A | B Testing</span></span>
<span data-ttu-id="0ca5a-186">如果您不知道哪些 variant 某項功能將會更成功，請將它釋放這兩種，讓每個可存取 toodifferent 使用者。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-186">If you don't know which variant of a feature will be more successful, release both of them, making each accessible toodifferent users.</span></span> <span data-ttu-id="0ca5a-187">測量各自的 hello 成功，然後將 tooa 統一的版本。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-187">Measure hello success of each, and then move tooa unified version.</span></span>

<span data-ttu-id="0ca5a-188">這項技巧，您附加相異的屬性值 tooall hello 遙測傳送的每個版本的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-188">For this technique, you attach distinct property values tooall hello telemetry that is sent by each version of your app.</span></span> <span data-ttu-id="0ca5a-189">您可以執行，藉由定義屬性在 hello active TelemetryContext。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-189">You can do that by defining properties in hello active TelemetryContext.</span></span> <span data-ttu-id="0ca5a-190">這些預設屬性會加入 tooevery hello 應用程式的遙測訊息傳送的不只是您自訂的訊息，但也 hello 標準遙測。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-190">These default properties are added tooevery telemetry message that hello application sends - not just your custom messages, but hello standard telemetry as well.</span></span>

<span data-ttu-id="0ca5a-191">在 hello Application Insights 入口網站篩選，並在 hello 屬性值，將資料分割，以 toocompare hello 不同版本。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-191">In hello Application Insights portal, filter and split your data on hello property values, so as toocompare hello different versions.</span></span>

<span data-ttu-id="0ca5a-192">toodo，[設定遙測的初始設定式](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span><span class="sxs-lookup"><span data-stu-id="0ca5a-192">toodo this, [set up a telemetry initializer](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span></span>

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

<span data-ttu-id="0ca5a-193">Hello web 應用程式初始設定式中 Global.asax.cs 例如：</span><span class="sxs-lookup"><span data-stu-id="0ca5a-193">In hello web app initializer such as Global.asax.cs:</span></span>

```C#

    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```

<span data-ttu-id="0ca5a-194">所有新 TelemetryClients 自動加入您所指定的 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-194">All new TelemetryClients automatically add hello property value you specify.</span></span> <span data-ttu-id="0ca5a-195">個別的遙測事件可以覆寫 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="0ca5a-195">Individual telemetry events can override hello default values.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ca5a-196">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0ca5a-196">Next steps</span></span>
   - [<span data-ttu-id="0ca5a-197">使用者、工作階段、事件</span><span class="sxs-lookup"><span data-stu-id="0ca5a-197">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
   - [<span data-ttu-id="0ca5a-198">漏斗圖</span><span class="sxs-lookup"><span data-stu-id="0ca5a-198">Funnels</span></span>](usage-funnels.md)
   - [<span data-ttu-id="0ca5a-199">保留</span><span class="sxs-lookup"><span data-stu-id="0ca5a-199">Retention</span></span>](app-insights-usage-retention.md)
   - [<span data-ttu-id="0ca5a-200">使用者流程</span><span class="sxs-lookup"><span data-stu-id="0ca5a-200">User Flows</span></span>](app-insights-usage-flows.md)
   - [<span data-ttu-id="0ca5a-201">活頁簿</span><span class="sxs-lookup"><span data-stu-id="0ca5a-201">Workbooks</span></span>](app-insights-usage-workbooks.md)
   - [<span data-ttu-id="0ca5a-202">新增使用者內容</span><span class="sxs-lookup"><span data-stu-id="0ca5a-202">Add user context</span></span>](app-insights-usage-send-user-context.md)
