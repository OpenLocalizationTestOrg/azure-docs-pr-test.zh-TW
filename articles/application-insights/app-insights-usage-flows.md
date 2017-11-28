---
title: "使用 Azure Application Insights 中的使用者傳送 aaaAnalyze 使用者瀏覽模式 |Microsoft 文件"
description: "分析使用者 hello 網頁和 web 應用程式的功能之間的瀏覽。"
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
ms.openlocfilehash: d3f35dc78e9874e4b7974604bf91c40a5e5b78eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-user-navigation-patterns-with-user-flows-in-application-insights"></a><span data-ttu-id="55829-103">在 Application Insights 中使用使用者流程分析使用者瀏覽模式</span><span class="sxs-lookup"><span data-stu-id="55829-103">Analyze user navigation patterns with User Flows in Application Insights</span></span>

![Application Insights 使用者流程工具](./media/app-insights-usage-flows/flows.png)

<span data-ttu-id="55829-105">hello 使用者流動工具以視覺化方式檢視使用者 hello 網頁和您的站台的功能之間的瀏覽。</span><span class="sxs-lookup"><span data-stu-id="55829-105">hello User Flows tool visualizes how users navigate between hello pages and features of your site.</span></span> <span data-ttu-id="55829-106">適合用來回答問題，例如：</span><span class="sxs-lookup"><span data-stu-id="55829-106">It's great for answering questions like:</span></span>
* <span data-ttu-id="55829-107">使用者如何離開網站上的分頁？</span><span class="sxs-lookup"><span data-stu-id="55829-107">How do users navigate away from a page on your site?</span></span>
* <span data-ttu-id="55829-108">使用者在網站上的分頁按了什麼？</span><span class="sxs-lookup"><span data-stu-id="55829-108">What do users click on a page on your site?</span></span>
* <span data-ttu-id="55829-109">Hello 會將使用者變換從您的網站的大部分？</span><span class="sxs-lookup"><span data-stu-id="55829-109">Where are hello places that users churn most from your site?</span></span>
* <span data-ttu-id="55829-110">有其中使用者重複 hello 相同的動作重複的位置嗎？</span><span class="sxs-lookup"><span data-stu-id="55829-110">Are there places where users repeat hello same action over and over?</span></span>

<span data-ttu-id="55829-111">hello 使用者流動工具將會啟動從初始頁面檢視或您指定的事件。</span><span class="sxs-lookup"><span data-stu-id="55829-111">hello User Flows tool starts from an initial page view or event that you specify.</span></span> <span data-ttu-id="55829-112">顯示指定此頁面檢視或自訂的事件，請使用者傳送 hello 頁面檢視和自訂之後在工作階段中，兩個步驟之後，依此類推，立即傳送使用者的事件。</span><span class="sxs-lookup"><span data-stu-id="55829-112">Given this page view or custom event, User Flows shows hello page views and custom events that users sent immediately afterwards during a session, two steps afterwards, and so forth.</span></span> <span data-ttu-id="55829-113">不同粗細的線條顯示每個路徑被使用者追蹤的次數。</span><span class="sxs-lookup"><span data-stu-id="55829-113">Lines of varying thickness show how many times each path was followed by users.</span></span> <span data-ttu-id="55829-114">特殊的 「 結束工作階段 」 節點顯示的使用者人數任何頁面檢視或自訂的事件之後傳送 hello 前面節點中，反白顯示的使用者可能保留您的網站。</span><span class="sxs-lookup"><span data-stu-id="55829-114">Special "Session Ended" nodes show how many users sent no page views or custom events after hello preceding node, highlighting where users probably left your site.</span></span>



> [!NOTE]
> <span data-ttu-id="55829-115">Application Insights 資源必須包含頁面檢視或自訂事件 toouse hello 使用者流動工具。</span><span class="sxs-lookup"><span data-stu-id="55829-115">Your Application Insights resource must contain page views or custom events toouse hello User Flows tool.</span></span> <span data-ttu-id="55829-116">[了解如何註冊您的應用程式 toocollect 頁面 tooset 檢視自動以 hello Application Insights JavaScript SDK](app-insights-javascript.md)。</span><span class="sxs-lookup"><span data-stu-id="55829-116">[Learn how tooset up your app toocollect page views automatically with hello Application Insights JavaScript SDK](app-insights-javascript.md).</span></span>
> 
> 

## <a name="start-by-choosing-an-initial-page-view-or-custom-event"></a><span data-ttu-id="55829-117">從選擇初始分頁檢視或自訂事件開始</span><span class="sxs-lookup"><span data-stu-id="55829-117">Start by choosing an initial page view or custom event</span></span>

![為使用者流程選擇初始事件](./media/app-insights-usage-flows/flows-initial-event.png)

<span data-ttu-id="55829-119">tooget 啟動回答問題與 hello 使用者流動工具選擇的初始頁面檢視或自訂事件 tooserve 做為起點 hello 視覺效果的 hello:</span><span class="sxs-lookup"><span data-stu-id="55829-119">tooget started answering questions with hello User Flows tool, choose an initial page view or custom event tooserve as hello starting point for hello visualization:</span></span>
1. <span data-ttu-id="55829-120">按一下 hello 中的 hello 連結 」 使用者要怎麼做後...？ 」</span><span class="sxs-lookup"><span data-stu-id="55829-120">Click hello link in hello "What do users do after...?"</span></span> <span data-ttu-id="55829-121">標題，或按一下 hello [編輯] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="55829-121">title, or click hello Edit button.</span></span> 
2. <span data-ttu-id="55829-122">從 hello 「 初始事件 」 的下拉式清單中選取的頁面檢視或自訂的事件。</span><span class="sxs-lookup"><span data-stu-id="55829-122">Select a page view or custom event from hello "Initial event" dropdown.</span></span>
3. <span data-ttu-id="55829-123">按一下 [建立圖形]。</span><span class="sxs-lookup"><span data-stu-id="55829-123">Click "Create graph".</span></span>

<span data-ttu-id="55829-124">hello hello 視覺效果的 「 步驟 1 」 欄會顯示哪些使用者未最常後方 hello 初始事件，排序上到下從最 tooleast 常。</span><span class="sxs-lookup"><span data-stu-id="55829-124">hello "Step 1" column of hello visualization shows what users did most frequently just after hello initial event, ordered top-to-bottom from most- tooleast-frequent.</span></span> <span data-ttu-id="55829-125">「 步驟 2 「 hello 和後續的資料行顯示哪些使用者之後，未建立 hello 方法的所有使用者的瀏覽您的網站。</span><span class="sxs-lookup"><span data-stu-id="55829-125">hello "Step 2" and subsequent columns show what users did thereafter, creating a picture of all hello ways users have navigated through your site.</span></span>

<span data-ttu-id="55829-126">根據預設，hello 使用者流動工具會隨機取樣只 hello 過去的 24 小時內的頁面檢視和自訂的事件，從您的網站。</span><span class="sxs-lookup"><span data-stu-id="55829-126">By default, hello User Flows tool randomly samples only hello last 24 hours of page views and custom event from your site.</span></span> <span data-ttu-id="55829-127">您可以增加 hello 時間範圍，並變更 hello hello [編輯] 功能表中的隨機取樣的效能和精確度達成平衡。</span><span class="sxs-lookup"><span data-stu-id="55829-127">You can increase hello time range and change hello balance of performance and accuracy for random sampling in hello Edit menu.</span></span>

<span data-ttu-id="55829-128">如果某些 hello 頁面檢視和自訂事件不相關的 tooyou，請按一下 hello"X"想 toohide hello 節點上。</span><span class="sxs-lookup"><span data-stu-id="55829-128">If some of hello page views and custom events aren't relevant tooyou, click hello "X" on hello nodes you want toohide.</span></span> <span data-ttu-id="55829-129">一旦您已選取您想要 toohide hello 節點，按一下下方 hello 視覺效果的 hello"建立圖形 」 按鈕。</span><span class="sxs-lookup"><span data-stu-id="55829-129">Once you've selected hello nodes you want toohide, click hello "Create graph" button below hello visualization.</span></span> <span data-ttu-id="55829-130">toosee 所有 hello 節點已經隱藏，請按一下 hello [編輯] 按鈕，然後查看 hello"排除事件 」 一節。</span><span class="sxs-lookup"><span data-stu-id="55829-130">toosee all of hello nodes you've hidden, click hello Edit button, then look at hello "Excluded events" section.</span></span>

<span data-ttu-id="55829-131">如果頁面檢視或自訂事件遺失，您會預期 toosee hello 視覺效果：</span><span class="sxs-lookup"><span data-stu-id="55829-131">If page views or custom events are missing that you expect toosee on hello visualization:</span></span>
* <span data-ttu-id="55829-132">請檢查 hello [編輯] 功能表中的 hello"排除事件 」 一節。</span><span class="sxs-lookup"><span data-stu-id="55829-132">Check hello "Excluded events" section in hello Edit menu.</span></span>
* <span data-ttu-id="55829-133">Hello 「 詳細資料層級 」 中使用控制項 hello 編輯功能表 tooinclude 較不頻繁事件 hello 視覺效果中。</span><span class="sxs-lookup"><span data-stu-id="55829-133">Use hello "Detail level" control in hello Edit menu tooinclude less-frequent events in hello visualization.</span></span>
* <span data-ttu-id="55829-134">如果 hello 頁面檢視或自訂您預期的事件，則由使用者不常傳送，請嘗試增加 hello 時間範圍 hello [編輯] 功能表中的 hello 視覺效果。</span><span class="sxs-lookup"><span data-stu-id="55829-134">If hello page view or custom event you expect is sent infrequently by users, try increasing hello time range of hello visualization in hello Edit menu.</span></span>
* <span data-ttu-id="55829-135">請確定 hello 頁面檢視或自訂您預期設定 toobe hello 原始程式碼，您的網站中的 hello Application Insights SDK 所收集的事件。</span><span class="sxs-lookup"><span data-stu-id="55829-135">Make sure hello page view or custom event you expect is set up toobe collected by hello Application Insights SDK in hello source code of your site.</span></span> [<span data-ttu-id="55829-136">深入了解收集自訂事件。</span><span class="sxs-lookup"><span data-stu-id="55829-136">Learn more about collecting custom events.</span></span>](app-insights-api-custom-events-metrics.md)

<span data-ttu-id="55829-137">如果您想的 toosee hello 視覺效果中，使用在 hello hello 」 的步驟的數目 滑桿中的多個步驟 編輯 功能表。</span><span class="sxs-lookup"><span data-stu-id="55829-137">If you want toosee more steps in hello visualization, use hello "Number of steps" slider in hello Edit menu.</span></span>

## <a name="after-visiting-a-page-or-feature-where-do-users-go-and-what-do-they-click"></a><span data-ttu-id="55829-138">造訪分頁或功能之後，使用者的去向以及他們按了什麼？</span><span class="sxs-lookup"><span data-stu-id="55829-138">After visiting a page or feature, where do users go and what do they click?</span></span>

![使用使用者流動 toounderstand，使用者按一下](./media/app-insights-usage-flows/flows-one-step.png)

<span data-ttu-id="55829-140">如果頁面檢視您初始的事件，hello 第一個資料行 (「 步驟 1 」) 的 hello 視覺效果是哪些使用者沒有瀏覽 hello 頁面之後，立即快速 toounderstand。</span><span class="sxs-lookup"><span data-stu-id="55829-140">If your initial event is a page view, hello first column ("Step 1") of hello visualization is a quick way toounderstand what users did immediately after visiting hello page.</span></span> <span data-ttu-id="55829-141">請嘗試在視窗下一步 toohello 使用者流動的視覺效果中開啟您的網站。</span><span class="sxs-lookup"><span data-stu-id="55829-141">Try opening your site in a window next toohello User Flows visualization.</span></span> <span data-ttu-id="55829-142">比較您的預期使用者與 hello 頁面 toohello 清單 hello 」 步驟 1 」 資料行中的事件之間的互動方式。</span><span class="sxs-lookup"><span data-stu-id="55829-142">Compare your expectations of how users interact with hello page toohello list of events in hello "Step 1" column.</span></span> <span data-ttu-id="55829-143">通常，看起來不顯著 tooyour 小組的 hello 頁面上的 UI 項目可以是之間 hello hello 頁面上最常使用。</span><span class="sxs-lookup"><span data-stu-id="55829-143">Often, a UI element on hello page that seems insignificant tooyour team can be among hello most-used on hello page.</span></span> <span data-ttu-id="55829-144">它可以是設計改良 tooyour 站台的最佳起始點。</span><span class="sxs-lookup"><span data-stu-id="55829-144">It can be a great starting point for design improvements tooyour site.</span></span>

<span data-ttu-id="55829-145">如果您的初始事件的自訂事件，hello 第一欄會顯示使用者未執行該動作之後，只要。</span><span class="sxs-lookup"><span data-stu-id="55829-145">If your initial event is a custom event, hello first column shows what users did just after performing that action.</span></span> <span data-ttu-id="55829-146">如同網頁檢視，請考慮是否 hello 觀察到的使用者行為符合您的小組目標和期望。</span><span class="sxs-lookup"><span data-stu-id="55829-146">As with page views, consider if hello observed behavior of your users matches your team's goals and expectations.</span></span> <span data-ttu-id="55829-147">如果您選取的初始事件 「 加入項目 tooShopping 購物車 」，例如，請查看 toosee 如果"Go tooCheckout 」 和 「 已完成採購 」 會出現在不久之後 hello 視覺效果。</span><span class="sxs-lookup"><span data-stu-id="55829-147">If your selected initial event is "Added Item tooShopping Cart", for example, look toosee if "Go tooCheckout" and "Completed Purchase" appear in hello visualization shortly thereafter.</span></span> <span data-ttu-id="55829-148">如果使用者行為與您的預期不同，請使用 hello 視覺效果 toounderstand 如何使用者會取得 「 受困於連結 」 您的站台目前的設計。</span><span class="sxs-lookup"><span data-stu-id="55829-148">If user behavior is much different from your expectations, use hello visualization toounderstand how users are getting "trapped" by your site's current design.</span></span>

## <a name="where-are-hello-places-that-users-churn-most-from-your-site"></a><span data-ttu-id="55829-149">Hello 會將使用者變換從您的網站的大部分？</span><span class="sxs-lookup"><span data-stu-id="55829-149">Where are hello places that users churn most from your site?</span></span>

<span data-ttu-id="55829-150">監看式 」 工作階段結束 」 節點中出現高總 hello 視覺效果，特別是早期流程中的資料行中。</span><span class="sxs-lookup"><span data-stu-id="55829-150">Watch for "Session Ended" nodes that appear high-up in a column in hello visualization, especially early in a flow.</span></span> <span data-ttu-id="55829-151">也就是說，許多使用者下列 hello 上述路徑的網頁和 UI 互動之後，可能變換從您的網站。</span><span class="sxs-lookup"><span data-stu-id="55829-151">This means many users probably churned from your site after following hello preceding path of pages and UI interactions.</span></span> <span data-ttu-id="55829-152">有時候變換是預期的 - 例如，在電子商務網站上完成購買之後 - 但是變換通常是設計問題、效能不佳，或您的網站可以改善之其他問題的徵兆。</span><span class="sxs-lookup"><span data-stu-id="55829-152">Sometimes churn is expected - after completing a purchase on an eCommerce site, for example - but usually churn is a sign of design problems, poor performance, or other issues with your site that can be improved.</span></span>

<span data-ttu-id="55829-153">請注意，「工作階段已結束」節點只會根據這個 Application Insights 資源所收集的遙測。</span><span class="sxs-lookup"><span data-stu-id="55829-153">Keep in mind that "Session Ended" nodes are based only on telemetry collected by this Application Insights resource.</span></span> <span data-ttu-id="55829-154">如果 Application Insights 未收到某些使用者互動的遙測，使用者可能仍然有互動網站在這些方法中 hello 使用者流動工具顯示 hello 工作階段結束之後。</span><span class="sxs-lookup"><span data-stu-id="55829-154">If Application Insights doesn't receive telemetry for certain user interactions, users could still have interacted with your site in those ways after hello User Flows tool says hello session ended.</span></span>

## <a name="are-there-places-where-users-repeat-hello-same-action-over-and-over"></a><span data-ttu-id="55829-155">有其中使用者重複 hello 相同的動作重複的位置嗎？</span><span class="sxs-lookup"><span data-stu-id="55829-155">Are there places where users repeat hello same action over and over?</span></span>

<span data-ttu-id="55829-156">尋找頁面檢視或自訂的事件是由許多使用者重複跨 hello 視覺效果中的後續步驟。</span><span class="sxs-lookup"><span data-stu-id="55829-156">Look for a page view or custom event that is repeated by many users across subsequent steps in hello visualization.</span></span> <span data-ttu-id="55829-157">這通常表示使用者會在您的網站上執行重複的動作。</span><span class="sxs-lookup"><span data-stu-id="55829-157">This usually means that users are performing repetitive actions on your site.</span></span> <span data-ttu-id="55829-158">如果您發現重複，請思考變更 hello 設計您的網站，或加入新的功能 tooreduce 重複。</span><span class="sxs-lookup"><span data-stu-id="55829-158">If you find repetition, think about changing hello design of your site or adding new functionality tooreduce repetition.</span></span> <span data-ttu-id="55829-159">例如，如果您發現使用者在資料表元素的每個資料列上執行重複動作，則新增大量編輯功能。</span><span class="sxs-lookup"><span data-stu-id="55829-159">For example, adding bulk edit functionality if you find users performing repetitive actions on each row of a table element.</span></span>

## <a name="common-questions"></a><span data-ttu-id="55829-160">常見問題</span><span class="sxs-lookup"><span data-stu-id="55829-160">Common Questions</span></span>

### <a name="why-do-steps-appear-disconnected"></a><span data-ttu-id="55829-161">為什麼步驟顯示中斷連線？</span><span class="sxs-lookup"><span data-stu-id="55829-161">Why do steps appear disconnected?</span></span>

![具有已中斷連線步驟的使用者流程](./media/app-insights-usage-flows/flows-disconnected.png)

<span data-ttu-id="55829-163">如果已中斷連線的使用者傳送的視覺效果中的步驟 （資料行），則表示 hello hello 步驟之間的使用者所採取的路徑沒有夠頻繁且足以 toobe 所示。</span><span class="sxs-lookup"><span data-stu-id="55829-163">If steps (columns) in a User Flows visualization are disconnected, it means none of hello paths taken by users between hello steps were frequent enough toobe shown.</span></span> <span data-ttu-id="55829-164">因此 hello 步驟會顯示已連線，調整 hello [編輯] 功能表中的 hello 「 詳細資料層級 」 滑桿，tooshow 小於 hello 視覺效果上常見的事件。</span><span class="sxs-lookup"><span data-stu-id="55829-164">tooshow less frequent events on hello visualization so hello steps appear connected, adjust hello "Detail level" slider in hello Edit menu.</span></span>

### <a name="does-hello-initial-event-represent-hello-first-time-hello-event-appears-in-a-session-or-any-time-it-appears-in-a-session"></a><span data-ttu-id="55829-165">沒有 hello 初始事件代表 hello 第一個時間 hello 事件出現在工作階段，或出現在工作階段中任何時間？</span><span class="sxs-lookup"><span data-stu-id="55829-165">Does hello initial event represent hello first time hello event appears in a session, or any time it appears in a session?</span></span>

<span data-ttu-id="55829-166">hello 初始事件 hello 視覺效果只代表 hello 使用者傳送該頁面檢視或自訂的事件工作階段期間的第一次。</span><span class="sxs-lookup"><span data-stu-id="55829-166">hello initial event on hello visualization only represents hello first time a user sent that page view or custom event during a session.</span></span> <span data-ttu-id="55829-167">如果使用者可以在工作階段中，多次傳送 hello 初始事件則 hello 」 步驟 1 」 資料行只會顯示使用者 hello 之後的行為方式*第一個*初始事件的執行個體，並非所有的執行個體。</span><span class="sxs-lookup"><span data-stu-id="55829-167">If users can send hello initial event multiple times in a session, then hello "Step 1" column only shows how users behave after hello *first* instance of initial event, not all instances.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55829-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="55829-168">Next steps</span></span>

* [<span data-ttu-id="55829-169">使用量概觀</span><span class="sxs-lookup"><span data-stu-id="55829-169">Usage overview</span></span>](app-insights-usage-overview.md)
* [<span data-ttu-id="55829-170">使用者、工作階段和事件</span><span class="sxs-lookup"><span data-stu-id="55829-170">Users, Sessions, and Events</span></span>](app-insights-usage-segmentation.md)
* [<span data-ttu-id="55829-171">保留</span><span class="sxs-lookup"><span data-stu-id="55829-171">Retention</span></span>](app-insights-usage-retention.md)
* [<span data-ttu-id="55829-172">加入自訂事件 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="55829-172">Adding custom events tooyour app</span></span>](app-insights-api-custom-events-metrics.md)
