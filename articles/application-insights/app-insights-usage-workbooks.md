---
title: "調查使用方式資料並且與 Azure Application Insights 中的互動式活頁簿共用 | Microsoft docs"
description: "您 Web 應用程式的使用者人口統計分析。"
services: application-insights
documentationcenter: 
author: numberbycolors
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 06/12/2017
ms.author: bwren
ms.openlocfilehash: 75028b4fbda43d90f56690a33c7eb624fce049c8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="investigate-and-share-usage-data-with-interactive-workbooks-in-application-insights"></a><span data-ttu-id="6f09c-103">調查使用方式資料並且與 Application Insights 中的互動式活頁簿共用</span><span class="sxs-lookup"><span data-stu-id="6f09c-103">Investigate and share usage data with interactive workbooks in Application Insights</span></span>

<span data-ttu-id="6f09c-104">活頁簿將 [Azure Application Insights](app-insights-overview.md) 資料視覺效果、[分析查詢](app-insights-analytics.md) 及文字合併為互動式文件。</span><span class="sxs-lookup"><span data-stu-id="6f09c-104">Workbooks combine [Azure Application Insights](app-insights-overview.md) data visualizations, [Analytics queries](app-insights-analytics.md), and text into interactive documents.</span></span> <span data-ttu-id="6f09c-105">活頁簿可以由具有相同 Azure 資源存取權的其他小組成員編輯。</span><span class="sxs-lookup"><span data-stu-id="6f09c-105">Workbooks are editable by other team members with access to the same Azure resource.</span></span> <span data-ttu-id="6f09c-106">這表示用來建立活頁簿的查詢和控制項都可供讀取活頁簿的其他人使用，使其易於探索、擴充和檢查錯誤。</span><span class="sxs-lookup"><span data-stu-id="6f09c-106">This means the queries and controls used to create a workbook are available to other people reading the workbook, making them easy to explore, extend, and check for mistakes.</span></span>

<span data-ttu-id="6f09c-107">活頁簿對於下列案例很有用：</span><span class="sxs-lookup"><span data-stu-id="6f09c-107">Workbooks are helpful for scenarios like:</span></span>

* <span data-ttu-id="6f09c-108">當您事先不知道下列感興趣的計量時，探索應用程式的使用方式：使用者數目、保留率、轉換率等等。不同於 Application Insights 中的其他使用方式分析工具，活頁簿可讓您合併多種類型的視覺效果與分析，使其更適合這種自由形式探索。</span><span class="sxs-lookup"><span data-stu-id="6f09c-108">Exploring the usage of your app when you don't know the metrics of interest in advance: numbers of users, retention rates, conversion rates, etc. Unlike other usage analytics tools in Application Insights, workbooks let you combine multiple kinds of visualizations and analyses, making them great for this kind of free-form exploration.</span></span>
* <span data-ttu-id="6f09c-109">向小組說明新發行的功能如何執行，方法是顯示關鍵互動和其他計量的使用者計數。</span><span class="sxs-lookup"><span data-stu-id="6f09c-109">Explaining to your team how a newly released feature is performing, by showing user counts for key interactions and other metrics.</span></span>
* <span data-ttu-id="6f09c-110">與小組的其他成員分享應用程式中 A/B 實驗的結果。</span><span class="sxs-lookup"><span data-stu-id="6f09c-110">Sharing the results of an A/B experiment in your app with other members of your team.</span></span> <span data-ttu-id="6f09c-111">您可以使用文字說明實驗的目標，然後顯示用來評估實驗的每個使用方式計量和分析查詢，以及每個計量是高於或低於目標的清楚圖說文字。</span><span class="sxs-lookup"><span data-stu-id="6f09c-111">You can explain the goals for the experiment with text, then show each usage metric and Analytics query used to evaluate the experiment, along with clear call-outs for whether each metric was above- or below-target.</span></span>
* <span data-ttu-id="6f09c-112">報告應用程式使用方式中斷的影響，合併資料、文字說明和下一步的討論，以防止未來的中斷。</span><span class="sxs-lookup"><span data-stu-id="6f09c-112">Reporting the impact of an outage on the usage of your app, combining data, text explanation, and a discussion of next steps to prevent outages in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="6f09c-113">您的 Application Insights 資源必須包含分頁檢視或自訂事件，以便使用活頁簿。</span><span class="sxs-lookup"><span data-stu-id="6f09c-113">Your Application Insights resource must contain page views or custom events to use workbooks.</span></span> <span data-ttu-id="6f09c-114">[了解如何設定應用程式以使用 Application Insights JavaScript SDK 自動收集分頁檢視](app-insights-javascript.md)。</span><span class="sxs-lookup"><span data-stu-id="6f09c-114">[Learn how to set up your app to collect page views automatically with the Application Insights JavaScript SDK](app-insights-javascript.md).</span></span>
> 
> 

## <a name="editing-rearranging-cloning-and-deleting-workbook-sections"></a><span data-ttu-id="6f09c-115">編輯、重新排列、複製和刪除活頁簿區段</span><span class="sxs-lookup"><span data-stu-id="6f09c-115">Editing, rearranging, cloning, and deleting workbook sections</span></span>

<span data-ttu-id="6f09c-116">活頁簿是由下列區段組成：獨立的可編輯使用方式視覺效果、圖表、資料表、文字或分析查詢結果。</span><span class="sxs-lookup"><span data-stu-id="6f09c-116">A workbook is a made of sections: independently editable usage visualizations, charts, tables, text, or Analytics query results.</span></span>

<span data-ttu-id="6f09c-117">若要編輯活頁簿區段的內容，請按一下活頁簿區段右下方的 [編輯] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6f09c-117">To edit the contents of a workbook section, click the **Edit** button below and to the right of the workbook section.</span></span>

![Application Insights 活頁簿區段編輯控制項](./media/app-insights-usage-workbooks/editing-controls.png)

1. <span data-ttu-id="6f09c-119">當您完成編輯區段時，按一下區段左下角的 [完成編輯]。</span><span class="sxs-lookup"><span data-stu-id="6f09c-119">When you're done editing a section, click **Done Editing** in the bottom left corner of the section.</span></span>

2. <span data-ttu-id="6f09c-120">若要建立區段的複本，按一下 [複製此區段] 圖示。</span><span class="sxs-lookup"><span data-stu-id="6f09c-120">To create a duplicate of a section, click the **Clone this section** icon.</span></span> <span data-ttu-id="6f09c-121">建立重複的區段是逐一查看查詢而不會遺失先前反覆項目的絕佳方式。</span><span class="sxs-lookup"><span data-stu-id="6f09c-121">Creating duplicate sections is a great to way to iterate on a query without losing previous iterations.</span></span>

3. <span data-ttu-id="6f09c-122">若要在活頁簿中將區段上移，按一下 [上移] 或 [下移] 圖示。</span><span class="sxs-lookup"><span data-stu-id="6f09c-122">To move up a section in a workbook, click the **Move up** or **Move down** icon.</span></span>

4. <span data-ttu-id="6f09c-123">若要永久移除區段，按一下 [移除] 圖示。</span><span class="sxs-lookup"><span data-stu-id="6f09c-123">To remove a section permanently, click the **Remove** icon.</span></span>

## <a name="adding-usage-data-visualization-sections"></a><span data-ttu-id="6f09c-124">新增使用方式資料視覺效果區段</span><span class="sxs-lookup"><span data-stu-id="6f09c-124">Adding usage data visualization sections</span></span>

<span data-ttu-id="6f09c-125">活頁簿提供四種類型的內建使用方式分析視覺效果。</span><span class="sxs-lookup"><span data-stu-id="6f09c-125">Workbooks offer four types of built-in usage analytics visualizations.</span></span> <span data-ttu-id="6f09c-126">每個種類會回答應用程式使用方式的一般問題。</span><span class="sxs-lookup"><span data-stu-id="6f09c-126">Each answers a common question about the usage of your app.</span></span> <span data-ttu-id="6f09c-127">若要新增這四個區段以外的資料表和圖表，請新增分析查詢區段 (如下所示)。</span><span class="sxs-lookup"><span data-stu-id="6f09c-127">To add tables and charts other than these four sections, add Analytics query sections (see below).</span></span>

<span data-ttu-id="6f09c-128">若要將 [使用者]、[工作階段]、[事件] 或 [保留期] 區段新增至活頁簿，請使用活頁簿底端或任何區段底端的 [新增使用者] 或其他對應按鈕。</span><span class="sxs-lookup"><span data-stu-id="6f09c-128">To add a Users, Sessions, Events, or Retention section to your workbook, use the **Add Users** or other corresponding button at the bottom of the workbook, or at the bottom of any section.</span></span>

![活頁簿中的使用者區段](./media/app-insights-usage-workbooks/users-section.png)

<span data-ttu-id="6f09c-130">[使用者] 區段會回答「有多少使用者檢視我的網站的某些分頁或使用某些功能？」</span><span class="sxs-lookup"><span data-stu-id="6f09c-130">**Users** sections answer "How many users viewed some page or used some feature of my site?"</span></span>

<span data-ttu-id="6f09c-131">[工作階段] 區段會回答「使用者耗費多少工作階段來檢視我的網站的某些分頁或使用某些功能？」</span><span class="sxs-lookup"><span data-stu-id="6f09c-131">**Sessions** sections answer "How many sessions did users spend viewing some page or using some feature of my site?"</span></span>

<span data-ttu-id="6f09c-132">[事件] 區段會回答「使用者檢視我的網站的某些分頁或使用某些功能多少次？」</span><span class="sxs-lookup"><span data-stu-id="6f09c-132">**Events** sections answer "How many times did users view some page or use some feature of my site?"</span></span>

<span data-ttu-id="6f09c-133">這三個區段類型會提供相同的控制項和視覺效果集合：</span><span class="sxs-lookup"><span data-stu-id="6f09c-133">Each of these three section types offers the same sets of controls and visualizations:</span></span>

* [<span data-ttu-id="6f09c-134">深入了解編輯使用者、工作階段和事件區段</span><span class="sxs-lookup"><span data-stu-id="6f09c-134">Learn more about editing Users, Sessions, and Events sections</span></span>](app-insights-usage-segmentation.md)
* <span data-ttu-id="6f09c-135">切換主要圖表、長條圖格線、自動深入解析及範例使用者視覺效果，方法是使用每個區段頂端的 [顯示圖表]、[顯示格線]、[顯示深入解析] 和 [這些使用者的範例] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="6f09c-135">Toggle the main chart, histogram grids, automatic insights, and sample users visualizations using the **Show Chart**, **Show Grid**, **Show Insights**, and **Sample of These Users** checkboxes at the top of each section.</span></span>

![活頁簿中的保留期區段](./media/app-insights-usage-workbooks/retention-section.png)

<span data-ttu-id="6f09c-137">[保留期] 區段會回答「在某天或某週檢視某些分頁或使用某些功能的人員中，有多少人員在後續一天或一週回來？」</span><span class="sxs-lookup"><span data-stu-id="6f09c-137">**Retention** sections answer "Of people who viewed some page or used some feature on one day or week, how many came back in a subsequent day or week?"</span></span>

* [<span data-ttu-id="6f09c-138">深入了解編輯保留期區段</span><span class="sxs-lookup"><span data-stu-id="6f09c-138">Learn more about editing Retention sections</span></span>](app-insights-usage-retention.md)
* <span data-ttu-id="6f09c-139">切換選擇性整體保留期圖表，方法是使用區段頂端的 [顯示整體保留期圖表] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="6f09c-139">Toggle the optional Overall Retention chart using the **Show overall retention chart** checkbox at the top of the section.</span></span>

## <a name="adding-application-insights-analytics-sections"></a><span data-ttu-id="6f09c-140">新增 Application Insights 分析區段</span><span class="sxs-lookup"><span data-stu-id="6f09c-140">Adding Application Insights Analytics sections</span></span>

![活頁簿中的分析區段](./media/app-insights-usage-workbooks/analytics-section.png)

<span data-ttu-id="6f09c-142">若要將 Application Insights 分析查詢區段新增至您的活頁簿，請使用活頁部底端或任何區段底端的 [新增分析查詢] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6f09c-142">To add an Application Insights Analytics query section to your workbook, use the **Add Analytics query** button at the bottom of the workbook, or at the bottom of any section.</span></span>

<span data-ttu-id="6f09c-143">分析查詢區段可讓您將 Application Insights 資料的任意查詢新增至活頁簿。</span><span class="sxs-lookup"><span data-stu-id="6f09c-143">Analytics query sections let you add arbitrary queries over your Application Insights data into workbooks.</span></span> <span data-ttu-id="6f09c-144">這種彈性表示分析查詢區段應該是您在回答上述四個區段 (使用者、工作階段、事件和保留期) 以外的任何網站相關問題時的一時之選，例如：</span><span class="sxs-lookup"><span data-stu-id="6f09c-144">This flexibility means Analytics query sections should be your go-to for answering any questions about your site other than the four listed above for Users, Sessions, Events, and Retention, like:</span></span>

* <span data-ttu-id="6f09c-145">在與拒絕使用方式相同的時間週期期間，您的網站擲回多少例外狀況？</span><span class="sxs-lookup"><span data-stu-id="6f09c-145">How many exceptions did your site throw during the same time period as a decline in usage?</span></span>
* <span data-ttu-id="6f09c-146">檢視某些分頁之使用者的分頁載入時間散發是多久？</span><span class="sxs-lookup"><span data-stu-id="6f09c-146">What was the distribution of page load times for users viewing some page?</span></span>
* <span data-ttu-id="6f09c-147">有多少使用者檢視您的網站上的某些分頁集合，但是未檢視其他分頁集合？</span><span class="sxs-lookup"><span data-stu-id="6f09c-147">How many users viewed some set of pages on your site, but not some other set of pages?</span></span> <span data-ttu-id="6f09c-148">如果您有叢集使用者使用網站功能的不同子集 (使用 `join` 運算子搭配 Log Analytics 查詢語言的 `kind=leftanti` 修飾詞)，這項功能相當有用。</span><span class="sxs-lookup"><span data-stu-id="6f09c-148">This can be useful to understand if you have clusters of users who use different subsets of your site's functionality (use the `join` operator with the `kind=leftanti` modifier in the Log Analytics query language).</span></span>

<span data-ttu-id="6f09c-149">使用 [Log Analytics 查詢語言參考](https://docs.loganalytics.io/)以深入了解撰寫查詢。</span><span class="sxs-lookup"><span data-stu-id="6f09c-149">Use the [Log Analytics query language reference](https://docs.loganalytics.io/) to learn more about writing queries.</span></span>

## <a name="adding-text-and-markdown-sections"></a><span data-ttu-id="6f09c-150">新增文字和 Markdown 區段</span><span class="sxs-lookup"><span data-stu-id="6f09c-150">Adding text and Markdown sections</span></span>

<span data-ttu-id="6f09c-151">將標題、說明及註解新增至您的活頁簿，可協助將一組資料表和圖表變成敘述。</span><span class="sxs-lookup"><span data-stu-id="6f09c-151">Adding headings, explanations, and commentary to your workbooks helps turn a set of tables and charts into a narrative.</span></span> <span data-ttu-id="6f09c-152">活頁簿中的文字區段支援 [Markdown 語法](https://daringfireball.net/projects/markdown/)以進行文字格式設定，例如標題、粗體、斜體和項目符號清單。</span><span class="sxs-lookup"><span data-stu-id="6f09c-152">Text sections in workbooks support the [Markdown syntax](https://daringfireball.net/projects/markdown/) for text formatting, like headings, bold, italics, and bulleted lists.</span></span>

<span data-ttu-id="6f09c-153">若要將文字區段新增至您的活頁簿，請使用活頁部底端或任何區段底端的 [新增文字] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6f09c-153">To add a text section to your workbook, use the **Add text** button at the bottom of the workbook, or at the bottom of any section.</span></span>

## <a name="saving-and-sharing-workbooks-with-your-team"></a><span data-ttu-id="6f09c-154">儲存活頁簿並且與小組共用</span><span class="sxs-lookup"><span data-stu-id="6f09c-154">Saving and sharing workbooks with your team</span></span>

<span data-ttu-id="6f09c-155">活頁簿會儲存在 Application Insights 資源中，儲存在您私人使用的 [我的報表] 區段中，或是可供具有 Application Insights 資源存取權的每個人存取的 [共用報表] 區段中。</span><span class="sxs-lookup"><span data-stu-id="6f09c-155">Workbooks are saved within an Application Insights resource, either in the **My Reports** section that's private to you or in the **Shared Reports** section that's accessible to everyone with access to the Application Insights resource.</span></span> <span data-ttu-id="6f09c-156">若要檢視資源中的所有活頁簿，請按一下動作列中的 [開啟] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6f09c-156">To view all the workbooks in the resource, click the **Open** button in the action bar.</span></span>

<span data-ttu-id="6f09c-157">若要共用目前在 [我的報表] 的活頁簿：</span><span class="sxs-lookup"><span data-stu-id="6f09c-157">To share a workbook that's currently in **My Reports**:</span></span>

1. <span data-ttu-id="6f09c-158">按一下動作列中的 [開啟]</span><span class="sxs-lookup"><span data-stu-id="6f09c-158">Click **Open** in the action bar</span></span>
2. <span data-ttu-id="6f09c-159">按一下您想要共用之活頁簿旁邊的 [...] 按鈕</span><span class="sxs-lookup"><span data-stu-id="6f09c-159">Click the "..." button beside the workbook you want to share</span></span>
3. <span data-ttu-id="6f09c-160">按一下 [移至共用報表]。</span><span class="sxs-lookup"><span data-stu-id="6f09c-160">Click **Move to Shared Reports**.</span></span>

<span data-ttu-id="6f09c-161">若要使用連結或透過電子郵件共用活頁簿，請按一下動作列中的 [共用]。</span><span class="sxs-lookup"><span data-stu-id="6f09c-161">To share a workbook with a link or via email, click **Share** in the action bar.</span></span> <span data-ttu-id="6f09c-162">請注意，連結的收件者需要在 Azure 入口網站中存取此資源的存取權，才能檢視活頁簿。</span><span class="sxs-lookup"><span data-stu-id="6f09c-162">Keep in mind that recipients of the link need access to this resource in the Azure portal to view the workbook.</span></span> <span data-ttu-id="6f09c-163">若要進行編輯，收件者至少需要資源的參與者權限。</span><span class="sxs-lookup"><span data-stu-id="6f09c-163">To make edits, recipients need at least Contributor permissions for the resource.</span></span>

<span data-ttu-id="6f09c-164">若要將活頁簿的連結釘選到 Azure 儀表板：</span><span class="sxs-lookup"><span data-stu-id="6f09c-164">To pin a link to a workbook to an Azure Dashboard:</span></span>

1. <span data-ttu-id="6f09c-165">按一下動作列中的 [開啟]</span><span class="sxs-lookup"><span data-stu-id="6f09c-165">Click **Open** in the action bar</span></span>
2. <span data-ttu-id="6f09c-166">按一下您想要釘選之活頁簿旁邊的 [...] 按鈕</span><span class="sxs-lookup"><span data-stu-id="6f09c-166">Click the "..." button beside the workbook you want to pin</span></span>
3. <span data-ttu-id="6f09c-167">按一下 [釘選到儀表板]。</span><span class="sxs-lookup"><span data-stu-id="6f09c-167">Click **Pin to dashboard**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f09c-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6f09c-168">Next steps</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f09c-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6f09c-169">Next steps</span></span>
- <span data-ttu-id="6f09c-170">若要啟用使用體驗，請開始傳送「自訂事件」[](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent)或「頁面檢視」[](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views)。</span><span class="sxs-lookup"><span data-stu-id="6f09c-170">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="6f09c-171">如果您已傳送自訂事件或頁面檢視，請探索「使用量工具」，以了解使用者如何使用您的服務。</span><span class="sxs-lookup"><span data-stu-id="6f09c-171">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    - [<span data-ttu-id="6f09c-172">使用者、工作階段、事件</span><span class="sxs-lookup"><span data-stu-id="6f09c-172">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="6f09c-173">漏斗圖</span><span class="sxs-lookup"><span data-stu-id="6f09c-173">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="6f09c-174">保留</span><span class="sxs-lookup"><span data-stu-id="6f09c-174">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="6f09c-175">使用者流程</span><span class="sxs-lookup"><span data-stu-id="6f09c-175">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="6f09c-176">新增使用者內容</span><span class="sxs-lookup"><span data-stu-id="6f09c-176">Add user context</span></span>](app-insights-usage-send-user-context.md)
    
