---
title: "在 Azure Application Insights 中使用使用者流程分析使用者瀏覽模式 | Microsoft docs"
description: "分析使用者如何在 Web 應用程式的分頁和功能之間進行瀏覽。"
services: application-insights
documentationcenter: 
author: numberbycolors
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 08/02/2017
ms.author: cfreeman
ms.openlocfilehash: d17ed3dff08f00a1d6a2108608e42b29f95fbd84
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="analyze-user-navigation-patterns-with-user-flows-in-application-insights"></a><span data-ttu-id="9ffa6-103">在 Application Insights 中使用使用者流程分析使用者瀏覽模式</span><span class="sxs-lookup"><span data-stu-id="9ffa6-103">Analyze user navigation patterns with User Flows in Application Insights</span></span>

![Application Insights 使用者流程工具](./media/app-insights-usage-flows/flows.png)

<span data-ttu-id="9ffa6-105">「使用者流程」工具會視覺化使用者如何在網站的分頁和功能之間進行瀏覽。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-105">The User Flows tool visualizes how users navigate between the pages and features of your site.</span></span> <span data-ttu-id="9ffa6-106">適合用來回答問題，例如：</span><span class="sxs-lookup"><span data-stu-id="9ffa6-106">It's great for answering questions like:</span></span>
* <span data-ttu-id="9ffa6-107">使用者如何離開網站上的分頁？</span><span class="sxs-lookup"><span data-stu-id="9ffa6-107">How do users navigate away from a page on your site?</span></span>
* <span data-ttu-id="9ffa6-108">使用者在網站上的分頁按了什麼？</span><span class="sxs-lookup"><span data-stu-id="9ffa6-108">What do users click on a page on your site?</span></span>
* <span data-ttu-id="9ffa6-109">使用者最常從您的網站變換的位置是哪裡？</span><span class="sxs-lookup"><span data-stu-id="9ffa6-109">Where are the places that users churn most from your site?</span></span>
* <span data-ttu-id="9ffa6-110">有使用者一再重複相同動作的位置嗎？</span><span class="sxs-lookup"><span data-stu-id="9ffa6-110">Are there places where users repeat the same action over and over?</span></span>

<span data-ttu-id="9ffa6-111">「使用者流程」工具會從初始分頁檢視或您指定的事件啟動。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-111">The User Flows tool starts from an initial page view or event that you specify.</span></span> <span data-ttu-id="9ffa6-112">指定此分頁檢視或自訂事件，「使用者流程」會顯示在工作階段期間使用者隨後立即傳送、兩個步驟之後傳送，依此類推的分頁檢視和自訂事件。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-112">Given this page view or custom event, User Flows shows the page views and custom events that users sent immediately afterwards during a session, two steps afterwards, and so forth.</span></span> <span data-ttu-id="9ffa6-113">不同粗細的線條顯示每個路徑被使用者追蹤的次數。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-113">Lines of varying thickness show how many times each path was followed by users.</span></span> <span data-ttu-id="9ffa6-114">特殊「工作階段已結束」節點顯示在上一個節點之後有多少使用者未傳送任何分頁檢視或自訂事件，醒目提示使用者可能離開網站的位置。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-114">Special "Session Ended" nodes show how many users sent no page views or custom events after the preceding node, highlighting where users probably left your site.</span></span>



> [!NOTE]
> <span data-ttu-id="9ffa6-115">您的 Application Insights 資源必須包含分頁檢視或自訂事件，以便使用「使用者流程」工具。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-115">Your Application Insights resource must contain page views or custom events to use the User Flows tool.</span></span> <span data-ttu-id="9ffa6-116">[了解如何設定應用程式以使用 Application Insights JavaScript SDK 自動收集分頁檢視](app-insights-javascript.md)。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-116">[Learn how to set up your app to collect page views automatically with the Application Insights JavaScript SDK](app-insights-javascript.md).</span></span>
> 
> 

## <a name="start-by-choosing-an-initial-page-view-or-custom-event"></a><span data-ttu-id="9ffa6-117">從選擇初始分頁檢視或自訂事件開始</span><span class="sxs-lookup"><span data-stu-id="9ffa6-117">Start by choosing an initial page view or custom event</span></span>

![為使用者流程選擇初始事件](./media/app-insights-usage-flows/flows-initial-event.png)

<span data-ttu-id="9ffa6-119">若要開始使用「使用者流程」工具回答問題，請選擇初始分頁檢視或自訂事件作為視覺效果的起點：</span><span class="sxs-lookup"><span data-stu-id="9ffa6-119">To get started answering questions with the User Flows tool, choose an initial page view or custom event to serve as the starting point for the visualization:</span></span>
1. <span data-ttu-id="9ffa6-120">按一下「使用者之後要怎麼做...？」標題</span><span class="sxs-lookup"><span data-stu-id="9ffa6-120">Click the link in the "What do users do after...?"</span></span> <span data-ttu-id="9ffa6-121">中的連結，或者按一下 [編輯] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-121">title, or click the Edit button.</span></span> 
2. <span data-ttu-id="9ffa6-122">從 [初始事件] 下拉式清單中選取分頁檢視或自訂事件。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-122">Select a page view or custom event from the "Initial event" dropdown.</span></span>
3. <span data-ttu-id="9ffa6-123">按一下 [建立圖形]。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-123">Click "Create graph".</span></span>

<span data-ttu-id="9ffa6-124">視覺效果的 [步驟 1] 資料行會顯示使用者最常在初始事件之後做什麼，由上到下依序為最常至最少。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-124">The "Step 1" column of the visualization shows what users did most frequently just after the initial event, ordered top-to-bottom from most- to least-frequent.</span></span> <span data-ttu-id="9ffa6-125">[步驟 2] 和後續的資料行會顯示使用者之後的動作，建立使用者瀏覽您的網站一路下來的圖片。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-125">The "Step 2" and subsequent columns show what users did thereafter, creating a picture of all the ways users have navigated through your site.</span></span>

<span data-ttu-id="9ffa6-126">根據預設，「使用者流程」工具會從您的網站隨機取樣僅過去 24 小時的分頁檢視和自訂事件。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-126">By default, the User Flows tool randomly samples only the last 24 hours of page views and custom event from your site.</span></span> <span data-ttu-id="9ffa6-127">您可以增加時間範圍，並變更在 [編輯] 功能表中隨機取樣的效能和精確度平衡。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-127">You can increase the time range and change the balance of performance and accuracy for random sampling in the Edit menu.</span></span>

<span data-ttu-id="9ffa6-128">如果某些分頁檢視和自訂事件與您不相關，在您想要隱藏的節點上按一下 [X]。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-128">If some of the page views and custom events aren't relevant to you, click the "X" on the nodes you want to hide.</span></span> <span data-ttu-id="9ffa6-129">一旦您已選取想要隱藏的節點，按一下視覺效果下方的 [建立圖形] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-129">Once you've selected the nodes you want to hide, click the "Create graph" button below the visualization.</span></span> <span data-ttu-id="9ffa6-130">若要查看隱藏的所有節點，請按一下 [編輯] 按鈕，然後查看 [排除事件] 區段。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-130">To see all of the nodes you've hidden, click the Edit button, then look at the "Excluded events" section.</span></span>

<span data-ttu-id="9ffa6-131">如果分頁檢視或自訂事件遺失，您預期會在視覺效果上看到：</span><span class="sxs-lookup"><span data-stu-id="9ffa6-131">If page views or custom events are missing that you expect to see on the visualization:</span></span>
* <span data-ttu-id="9ffa6-132">在 [編輯] 功能表中檢查 [排除事件] 區段。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-132">Check the "Excluded events" section in the Edit menu.</span></span>
* <span data-ttu-id="9ffa6-133">使用 [編輯] 功能表中的 [詳細資料層級] 控制項，在視覺效果中包含較不常見的事件。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-133">Use the "Detail level" control in the Edit menu to include less-frequent events in the visualization.</span></span>
* <span data-ttu-id="9ffa6-134">如果使用者不常傳送您預期的分頁檢視或自訂事件，請嘗試增加 [編輯] 功能表中視覺效果的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-134">If the page view or custom event you expect is sent infrequently by users, try increasing the time range of the visualization in the Edit menu.</span></span>
* <span data-ttu-id="9ffa6-135">請確定您預期的分頁檢視或自訂事件設定為由網站原始程式碼中的 Application Insights SDK 收集。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-135">Make sure the page view or custom event you expect is set up to be collected by the Application Insights SDK in the source code of your site.</span></span> [<span data-ttu-id="9ffa6-136">深入了解收集自訂事件。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-136">Learn more about collecting custom events.</span></span>](app-insights-api-custom-events-metrics.md)

<span data-ttu-id="9ffa6-137">如果您想要在視覺效果中看到更多步驟，請使用 [編輯] 功能表中的 [步驟數目] 滑桿。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-137">If you want to see more steps in the visualization, use the "Number of steps" slider in the Edit menu.</span></span>

## <a name="after-visiting-a-page-or-feature-where-do-users-go-and-what-do-they-click"></a><span data-ttu-id="9ffa6-138">造訪分頁或功能之後，使用者的去向以及他們按了什麼？</span><span class="sxs-lookup"><span data-stu-id="9ffa6-138">After visiting a page or feature, where do users go and what do they click?</span></span>

![使用「使用者流程」以了解使用者點擊的位置](./media/app-insights-usage-flows/flows-one-step.png)

<span data-ttu-id="9ffa6-140">如果您的初始事件是分頁檢視，視覺效果的第一個資料行 ([步驟 1]) 是了解使用者造訪分頁之後隨即做了什麼的快速方法。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-140">If your initial event is a page view, the first column ("Step 1") of the visualization is a quick way to understand what users did immediately after visiting the page.</span></span> <span data-ttu-id="9ffa6-141">請嘗試在「使用者流程」視覺效果旁邊的視窗中開啟您的網站。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-141">Try opening your site in a window next to the User Flows visualization.</span></span> <span data-ttu-id="9ffa6-142">比較您預期使用者與分頁的互動方式與 [步驟 1] 資料行中的事件清單。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-142">Compare your expectations of how users interact with the page to the list of events in the "Step 1" column.</span></span> <span data-ttu-id="9ffa6-143">通常，看起來對於小組微不足道之分頁的 UI 元素，會是分頁上的最常用元素之一。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-143">Often, a UI element on the page that seems insignificant to your team can be among the most-used on the page.</span></span> <span data-ttu-id="9ffa6-144">它是為網站設計增強功能的絕佳起點。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-144">It can be a great starting point for design improvements to your site.</span></span>

<span data-ttu-id="9ffa6-145">如果您的初始事件是自訂事件，第一個資料行會顯示使用者在執行該動作之後做了什麼。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-145">If your initial event is a custom event, the first column shows what users did just after performing that action.</span></span> <span data-ttu-id="9ffa6-146">如同分頁檢視，請考慮觀察到的使用者行為是否符合您的小組目標和期望。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-146">As with page views, consider if the observed behavior of your users matches your team's goals and expectations.</span></span> <span data-ttu-id="9ffa6-147">舉例來說，如果您的選取初始事件是「將項目新增至購物車」，則查看「前往結帳」和「已完成採購」是否隨即出現在視覺效果中。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-147">If your selected initial event is "Added Item to Shopping Cart", for example, look to see if "Go to Checkout" and "Completed Purchase" appear in the visualization shortly thereafter.</span></span> <span data-ttu-id="9ffa6-148">如果使用者行為與您的預期大不相同，請使用視覺效果以了解使用者如何「受困」於網站的目前設計。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-148">If user behavior is much different from your expectations, use the visualization to understand how users are getting "trapped" by your site's current design.</span></span>

## <a name="where-are-the-places-that-users-churn-most-from-your-site"></a><span data-ttu-id="9ffa6-149">使用者最常從您的網站變換的位置是哪裡？</span><span class="sxs-lookup"><span data-stu-id="9ffa6-149">Where are the places that users churn most from your site?</span></span>

<span data-ttu-id="9ffa6-150">查看出現在視覺效果上層資料行中的「工作階段已結束」節點，特別是流程的早期。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-150">Watch for "Session Ended" nodes that appear high-up in a column in the visualization, especially early in a flow.</span></span> <span data-ttu-id="9ffa6-151">這表示許多使用者可能在遵循分頁和 UI 互動的前面路徑之後，從您的網站變換。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-151">This means many users probably churned from your site after following the preceding path of pages and UI interactions.</span></span> <span data-ttu-id="9ffa6-152">有時候變換是預期的 - 例如，在電子商務網站上完成購買之後 - 但是變換通常是設計問題、效能不佳，或您的網站可以改善之其他問題的徵兆。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-152">Sometimes churn is expected - after completing a purchase on an eCommerce site, for example - but usually churn is a sign of design problems, poor performance, or other issues with your site that can be improved.</span></span>

<span data-ttu-id="9ffa6-153">請注意，「工作階段已結束」節點只會根據這個 Application Insights 資源所收集的遙測。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-153">Keep in mind that "Session Ended" nodes are based only on telemetry collected by this Application Insights resource.</span></span> <span data-ttu-id="9ffa6-154">如果 Application Insights 未收到特定使用者互動的遙測，使用者仍然可以在「使用者流程」工具指出工作階段已結束之後，使用那些方式與網站互動。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-154">If Application Insights doesn't receive telemetry for certain user interactions, users could still have interacted with your site in those ways after the User Flows tool says the session ended.</span></span>

## <a name="are-there-places-where-users-repeat-the-same-action-over-and-over"></a><span data-ttu-id="9ffa6-155">有使用者一再重複相同動作的位置嗎？</span><span class="sxs-lookup"><span data-stu-id="9ffa6-155">Are there places where users repeat the same action over and over?</span></span>

<span data-ttu-id="9ffa6-156">尋找許多使用者跨視覺效果的後續步驟重複的分頁檢視或自訂事件。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-156">Look for a page view or custom event that is repeated by many users across subsequent steps in the visualization.</span></span> <span data-ttu-id="9ffa6-157">這通常表示使用者會在您的網站上執行重複的動作。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-157">This usually means that users are performing repetitive actions on your site.</span></span> <span data-ttu-id="9ffa6-158">如果您發現重複，請考慮變更網站的設計或新增功能以減少重複。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-158">If you find repetition, think about changing the design of your site or adding new functionality to reduce repetition.</span></span> <span data-ttu-id="9ffa6-159">例如，如果您發現使用者在資料表元素的每個資料列上執行重複動作，則新增大量編輯功能。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-159">For example, adding bulk edit functionality if you find users performing repetitive actions on each row of a table element.</span></span>

## <a name="common-questions"></a><span data-ttu-id="9ffa6-160">常見問題</span><span class="sxs-lookup"><span data-stu-id="9ffa6-160">Common Questions</span></span>

### <a name="why-do-steps-appear-disconnected"></a><span data-ttu-id="9ffa6-161">為什麼步驟顯示中斷連線？</span><span class="sxs-lookup"><span data-stu-id="9ffa6-161">Why do steps appear disconnected?</span></span>

![具有已中斷連線步驟的使用者流程](./media/app-insights-usage-flows/flows-disconnected.png)

<span data-ttu-id="9ffa6-163">如果「使用者流程」視覺效果中的步驟 (資料行) 已中斷連線，則表示使用者在步驟之間所採取的路徑都不夠頻繁而無法顯示。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-163">If steps (columns) in a User Flows visualization are disconnected, it means none of the paths taken by users between the steps were frequent enough to be shown.</span></span> <span data-ttu-id="9ffa6-164">若要在視覺效果上顯示較不頻繁的事件，讓步驟顯示連線，請調整 [編輯] 功能表中的 [詳細資料層級] 滑桿。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-164">To show less frequent events on the visualization so the steps appear connected, adjust the "Detail level" slider in the Edit menu.</span></span>

### <a name="does-the-initial-event-represent-the-first-time-the-event-appears-in-a-session-or-any-time-it-appears-in-a-session"></a><span data-ttu-id="9ffa6-165">初始事件代表事件第一次出現在工作階段中，或是出現在工作階段中的任一次？</span><span class="sxs-lookup"><span data-stu-id="9ffa6-165">Does the initial event represent the first time the event appears in a session, or any time it appears in a session?</span></span>

<span data-ttu-id="9ffa6-166">視覺效果的初始事件只代表使用者第一次在工作期間傳送該分頁檢視或自訂事件。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-166">The initial event on the visualization only represents the first time a user sent that page view or custom event during a session.</span></span> <span data-ttu-id="9ffa6-167">如果使用者可以在工作階段中傳送初始事件多次，則 [步驟 1] 資料行只會顯示使用者在初始事件  第一個執行個體 (而非所有執行個體) 之後的行為方式。</span><span class="sxs-lookup"><span data-stu-id="9ffa6-167">If users can send the initial event multiple times in a session, then the "Step 1" column only shows how users behave after the *first* instance of initial event, not all instances.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ffa6-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9ffa6-168">Next steps</span></span>

* [<span data-ttu-id="9ffa6-169">使用量概觀</span><span class="sxs-lookup"><span data-stu-id="9ffa6-169">Usage overview</span></span>](app-insights-usage-overview.md)
* [<span data-ttu-id="9ffa6-170">使用者、工作階段和事件</span><span class="sxs-lookup"><span data-stu-id="9ffa6-170">Users, Sessions, and Events</span></span>](app-insights-usage-segmentation.md)
* [<span data-ttu-id="9ffa6-171">保留</span><span class="sxs-lookup"><span data-stu-id="9ffa6-171">Retention</span></span>](app-insights-usage-retention.md)
* [<span data-ttu-id="9ffa6-172">將自訂事件新增至您的應用程式</span><span class="sxs-lookup"><span data-stu-id="9ffa6-172">Adding custom events to your app</span></span>](app-insights-api-custom-events-metrics.md)