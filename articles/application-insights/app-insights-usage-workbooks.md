---
title: "aaaInvestigate 和共用的使用量資料與 Azure Application Insights 中的互動式活頁簿 |Microsoft 文件"
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
ms.openlocfilehash: bdcebe0f97fdad0a0b301df5950dc09698f5a4dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="investigate-and-share-usage-data-with-interactive-workbooks-in-application-insights"></a><span data-ttu-id="0968b-103">調查使用方式資料並且與 Application Insights 中的互動式活頁簿共用</span><span class="sxs-lookup"><span data-stu-id="0968b-103">Investigate and share usage data with interactive workbooks in Application Insights</span></span>

<span data-ttu-id="0968b-104">活頁簿將 [Azure Application Insights](app-insights-overview.md) 資料視覺效果、[分析查詢](app-insights-analytics.md) 及文字合併為互動式文件。</span><span class="sxs-lookup"><span data-stu-id="0968b-104">Workbooks combine [Azure Application Insights](app-insights-overview.md) data visualizations, [Analytics queries](app-insights-analytics.md), and text into interactive documents.</span></span> <span data-ttu-id="0968b-105">活頁簿可以編輯存取 toohello 與其他小組成員相同的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="0968b-105">Workbooks are editable by other team members with access toohello same Azure resource.</span></span> <span data-ttu-id="0968b-106">這表示 hello 查詢和控制項使用的 toocreate 活頁簿可用 tooother 人讀取 hello 活頁簿，讓您輕鬆 tooexplore、 擴充和檢查錯誤。</span><span class="sxs-lookup"><span data-stu-id="0968b-106">This means hello queries and controls used toocreate a workbook are available tooother people reading hello workbook, making them easy tooexplore, extend, and check for mistakes.</span></span>

<span data-ttu-id="0968b-107">活頁簿對於下列案例很有用：</span><span class="sxs-lookup"><span data-stu-id="0968b-107">Workbooks are helpful for scenarios like:</span></span>

* <span data-ttu-id="0968b-108">瀏覽 hello 應用程式的使用方式，在不事先知道感興趣的 hello 度量： 使用者、 保留率、 轉換比率和其他內容的數字。不同於 Application Insights 中的其他使用方式分析工具，活頁簿可讓您合併多種類型的視覺效果與分析，使其更適合這種自由形式探索。</span><span class="sxs-lookup"><span data-stu-id="0968b-108">Exploring hello usage of your app when you don't know hello metrics of interest in advance: numbers of users, retention rates, conversion rates, etc. Unlike other usage analytics tools in Application Insights, workbooks let you combine multiple kinds of visualizations and analyses, making them great for this kind of free-form exploration.</span></span>
* <span data-ttu-id="0968b-109">說明 tooyour 小組如何執行新發行的功能，顯示使用者計數索引鍵的互動和其他度量資訊。</span><span class="sxs-lookup"><span data-stu-id="0968b-109">Explaining tooyour team how a newly released feature is performing, by showing user counts for key interactions and other metrics.</span></span>
* <span data-ttu-id="0968b-110">共用 hello 結果的 A / B 實驗中應用程式與其他小組成員。</span><span class="sxs-lookup"><span data-stu-id="0968b-110">Sharing hello results of an A/B experiment in your app with other members of your team.</span></span> <span data-ttu-id="0968b-111">您可以解釋 hello 的 hello 目標試驗的文字，則會顯示每個使用量度量及分析查詢使用 tooevaluate hello 試驗，以及清除圖說的每個度量是否上方或下方的目標。</span><span class="sxs-lookup"><span data-stu-id="0968b-111">You can explain hello goals for hello experiment with text, then show each usage metric and Analytics query used tooevaluate hello experiment, along with clear call-outs for whether each metric was above- or below-target.</span></span>
* <span data-ttu-id="0968b-112">報告中斷的 hello 影響 hello 使用方式的結合資料、 文字說明，以及下一個步驟 tooprevent 中斷 hello 未來的討論在您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0968b-112">Reporting hello impact of an outage on hello usage of your app, combining data, text explanation, and a discussion of next steps tooprevent outages in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="0968b-113">Application Insights 資源必須包含頁面檢視或自訂事件 toouse 活頁簿。</span><span class="sxs-lookup"><span data-stu-id="0968b-113">Your Application Insights resource must contain page views or custom events toouse workbooks.</span></span> <span data-ttu-id="0968b-114">[了解如何註冊您的應用程式 toocollect 頁面 tooset 檢視自動以 hello Application Insights JavaScript SDK](app-insights-javascript.md)。</span><span class="sxs-lookup"><span data-stu-id="0968b-114">[Learn how tooset up your app toocollect page views automatically with hello Application Insights JavaScript SDK](app-insights-javascript.md).</span></span>
> 
> 

## <a name="editing-rearranging-cloning-and-deleting-workbook-sections"></a><span data-ttu-id="0968b-115">編輯、重新排列、複製和刪除活頁簿區段</span><span class="sxs-lookup"><span data-stu-id="0968b-115">Editing, rearranging, cloning, and deleting workbook sections</span></span>

<span data-ttu-id="0968b-116">活頁簿是由下列區段組成：獨立的可編輯使用方式視覺效果、圖表、資料表、文字或分析查詢結果。</span><span class="sxs-lookup"><span data-stu-id="0968b-116">A workbook is a made of sections: independently editable usage visualizations, charts, tables, text, or Analytics query results.</span></span>

<span data-ttu-id="0968b-117">tooedit hello 內容的活頁簿 區段中，按一下 hello**編輯**下面的按鈕和 toohello hello 活頁簿區段的權限。</span><span class="sxs-lookup"><span data-stu-id="0968b-117">tooedit hello contents of a workbook section, click hello **Edit** button below and toohello right of hello workbook section.</span></span>

![Application Insights 活頁簿區段編輯控制項](./media/app-insights-usage-workbooks/editing-controls.png)

1. <span data-ttu-id="0968b-119">當您完成編輯區段，按一下**完成編輯**hello 的左下角 hello > 一節中。</span><span class="sxs-lookup"><span data-stu-id="0968b-119">When you're done editing a section, click **Done Editing** in hello bottom left corner of hello section.</span></span>

2. <span data-ttu-id="0968b-120">toocreate 重複的區段中，按一下 hello**複製本節**圖示。</span><span class="sxs-lookup"><span data-stu-id="0968b-120">toocreate a duplicate of a section, click hello **Clone this section** icon.</span></span> <span data-ttu-id="0968b-121">建立重複的區段是絕佳的 tooway tooiterate 查詢，而不會遺失先前反覆項目。</span><span class="sxs-lookup"><span data-stu-id="0968b-121">Creating duplicate sections is a great tooway tooiterate on a query without losing previous iterations.</span></span>

3. <span data-ttu-id="0968b-122">活頁簿中的區段組成 toomove 按一下 hello**向上移動**或**下移**圖示。</span><span class="sxs-lookup"><span data-stu-id="0968b-122">toomove up a section in a workbook, click hello **Move up** or **Move down** icon.</span></span>

4. <span data-ttu-id="0968b-123">tooremove 區段永久，按一下 hello**移除**圖示。</span><span class="sxs-lookup"><span data-stu-id="0968b-123">tooremove a section permanently, click hello **Remove** icon.</span></span>

## <a name="adding-usage-data-visualization-sections"></a><span data-ttu-id="0968b-124">新增使用方式資料視覺效果區段</span><span class="sxs-lookup"><span data-stu-id="0968b-124">Adding usage data visualization sections</span></span>

<span data-ttu-id="0968b-125">活頁簿提供四種類型的內建使用方式分析視覺效果。</span><span class="sxs-lookup"><span data-stu-id="0968b-125">Workbooks offer four types of built-in usage analytics visualizations.</span></span> <span data-ttu-id="0968b-126">每個回應 hello 使用量的相關應用程式的常見的問題。</span><span class="sxs-lookup"><span data-stu-id="0968b-126">Each answers a common question about hello usage of your app.</span></span> <span data-ttu-id="0968b-127">tooadd 資料表和圖表以外這些四個區段中，加入分析查詢區段 （如下所示）。</span><span class="sxs-lookup"><span data-stu-id="0968b-127">tooadd tables and charts other than these four sections, add Analytics query sections (see below).</span></span>

<span data-ttu-id="0968b-128">tooadd 使用者、 工作階段、 事件或保留區段 tooyour 活頁簿中，使用 hello**新增使用者**或其他對應按鈕在 hello 底部 hello 活頁簿，或在任何區段的 hello 底部。</span><span class="sxs-lookup"><span data-stu-id="0968b-128">tooadd a Users, Sessions, Events, or Retention section tooyour workbook, use hello **Add Users** or other corresponding button at hello bottom of hello workbook, or at hello bottom of any section.</span></span>

![活頁簿中的使用者區段](./media/app-insights-usage-workbooks/users-section.png)

<span data-ttu-id="0968b-130">[使用者] 區段會回答「有多少使用者檢視我的網站的某些分頁或使用某些功能？」</span><span class="sxs-lookup"><span data-stu-id="0968b-130">**Users** sections answer "How many users viewed some page or used some feature of my site?"</span></span>

<span data-ttu-id="0968b-131">[工作階段] 區段會回答「使用者耗費多少工作階段來檢視我的網站的某些分頁或使用某些功能？」</span><span class="sxs-lookup"><span data-stu-id="0968b-131">**Sessions** sections answer "How many sessions did users spend viewing some page or using some feature of my site?"</span></span>

<span data-ttu-id="0968b-132">[事件] 區段會回答「使用者檢視我的網站的某些分頁或使用某些功能多少次？」</span><span class="sxs-lookup"><span data-stu-id="0968b-132">**Events** sections answer "How many times did users view some page or use some feature of my site?"</span></span>

<span data-ttu-id="0968b-133">每個三個區段類型的控制項和視覺效果的相同集合提供 hello:</span><span class="sxs-lookup"><span data-stu-id="0968b-133">Each of these three section types offers hello same sets of controls and visualizations:</span></span>

* [<span data-ttu-id="0968b-134">深入了解編輯使用者、工作階段和事件區段</span><span class="sxs-lookup"><span data-stu-id="0968b-134">Learn more about editing Users, Sessions, and Events sections</span></span>](app-insights-usage-segmentation.md)
* <span data-ttu-id="0968b-135">切換 hello 主要圖表、 長條圖方格、 自動的深入資訊和範例使用者視覺效果使用 hello**顯示圖表**，**顯示方格**，**顯示 Insights**，和**這些使用者的範例**在每個區段的 hello 最上方的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="0968b-135">Toggle hello main chart, histogram grids, automatic insights, and sample users visualizations using hello **Show Chart**, **Show Grid**, **Show Insights**, and **Sample of These Users** checkboxes at hello top of each section.</span></span>

![活頁簿中的保留期區段](./media/app-insights-usage-workbooks/retention-section.png)

<span data-ttu-id="0968b-137">[保留期] 區段會回答「在某天或某週檢視某些分頁或使用某些功能的人員中，有多少人員在後續一天或一週回來？」</span><span class="sxs-lookup"><span data-stu-id="0968b-137">**Retention** sections answer "Of people who viewed some page or used some feature on one day or week, how many came back in a subsequent day or week?"</span></span>

* [<span data-ttu-id="0968b-138">深入了解編輯保留期區段</span><span class="sxs-lookup"><span data-stu-id="0968b-138">Learn more about editing Retention sections</span></span>](app-insights-usage-retention.md)
* <span data-ttu-id="0968b-139">切換 hello 選擇性整體保留使用圖表 hello**顯示整體保留圖表**在 hello hello 區段頂端的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="0968b-139">Toggle hello optional Overall Retention chart using hello **Show overall retention chart** checkbox at hello top of hello section.</span></span>

## <a name="adding-application-insights-analytics-sections"></a><span data-ttu-id="0968b-140">新增 Application Insights 分析區段</span><span class="sxs-lookup"><span data-stu-id="0968b-140">Adding Application Insights Analytics sections</span></span>

![活頁簿中的分析區段](./media/app-insights-usage-workbooks/analytics-section.png)

<span data-ttu-id="0968b-142">tooadd 應用程式 Insights 分析查詢區段 tooyour 活頁簿中，使用 hello**加入分析查詢**底部 hello hello 活頁簿，或在任何區段的 hello 底部的按鈕。</span><span class="sxs-lookup"><span data-stu-id="0968b-142">tooadd an Application Insights Analytics query section tooyour workbook, use hello **Add Analytics query** button at hello bottom of hello workbook, or at hello bottom of any section.</span></span>

<span data-ttu-id="0968b-143">分析查詢區段可讓您將 Application Insights 資料的任意查詢新增至活頁簿。</span><span class="sxs-lookup"><span data-stu-id="0968b-143">Analytics query sections let you add arbitrary queries over your Application Insights data into workbooks.</span></span> <span data-ttu-id="0968b-144">這種彈性表示分析查詢區段應該是您移至 toofor 回答關於以外 hello 四個以上所列的使用者、 工作階段、 事件和保留，像是您網站的任何問題：</span><span class="sxs-lookup"><span data-stu-id="0968b-144">This flexibility means Analytics query sections should be your go-toofor answering any questions about your site other than hello four listed above for Users, Sessions, Events, and Retention, like:</span></span>

* <span data-ttu-id="0968b-145">例外狀況數量未 hello 期間您站台的擲回相同時間週期內的使用方式下降？</span><span class="sxs-lookup"><span data-stu-id="0968b-145">How many exceptions did your site throw during hello same time period as a decline in usage?</span></span>
* <span data-ttu-id="0968b-146">Hello 散發的使用者檢視某些頁面的頁面載入時間是什麼？</span><span class="sxs-lookup"><span data-stu-id="0968b-146">What was hello distribution of page load times for users viewing some page?</span></span>
* <span data-ttu-id="0968b-147">有多少使用者檢視您的網站上的某些分頁集合，但是未檢視其他分頁集合？</span><span class="sxs-lookup"><span data-stu-id="0968b-147">How many users viewed some set of pages on your site, but not some other set of pages?</span></span> <span data-ttu-id="0968b-148">如果您有使用者使用不同的站台的功能子集的叢集，這可能會很有用的 toounderstand (使用 hello`join`運算子以 hello `kind=leftanti` hello 記錄分析查詢語言中的修飾詞)。</span><span class="sxs-lookup"><span data-stu-id="0968b-148">This can be useful toounderstand if you have clusters of users who use different subsets of your site's functionality (use hello `join` operator with hello `kind=leftanti` modifier in hello Log Analytics query language).</span></span>

<span data-ttu-id="0968b-149">使用 hello[記錄分析查詢語言參考](https://docs.loganalytics.io/)toolearn 深入了解撰寫查詢。</span><span class="sxs-lookup"><span data-stu-id="0968b-149">Use hello [Log Analytics query language reference](https://docs.loganalytics.io/) toolearn more about writing queries.</span></span>

## <a name="adding-text-and-markdown-sections"></a><span data-ttu-id="0968b-150">新增文字和 Markdown 區段</span><span class="sxs-lookup"><span data-stu-id="0968b-150">Adding text and Markdown sections</span></span>

<span data-ttu-id="0968b-151">新增標題、 說明、 和實況報導 tooyour 活頁簿，可協助變成旁白的一組資料表和圖表。</span><span class="sxs-lookup"><span data-stu-id="0968b-151">Adding headings, explanations, and commentary tooyour workbooks helps turn a set of tables and charts into a narrative.</span></span> <span data-ttu-id="0968b-152">活頁簿中的文字區段支援 hello [Markdown 語法](https://daringfireball.net/projects/markdown/)文字格式設定，例如標題、 粗體、 斜體和項目符號清單。</span><span class="sxs-lookup"><span data-stu-id="0968b-152">Text sections in workbooks support hello [Markdown syntax](https://daringfireball.net/projects/markdown/) for text formatting, like headings, bold, italics, and bulleted lists.</span></span>

<span data-ttu-id="0968b-153">tooadd 文字區段 tooyour 活頁簿使用 hello**加入文字**底部 hello hello 活頁簿，或在任何區段的 hello 底部的按鈕。</span><span class="sxs-lookup"><span data-stu-id="0968b-153">tooadd a text section tooyour workbook, use hello **Add text** button at hello bottom of hello workbook, or at hello bottom of any section.</span></span>

## <a name="saving-and-sharing-workbooks-with-your-team"></a><span data-ttu-id="0968b-154">儲存活頁簿並且與小組共用</span><span class="sxs-lookup"><span data-stu-id="0968b-154">Saving and sharing workbooks with your team</span></span>

<span data-ttu-id="0968b-155">活頁簿都儲存在 Application Insights 資源，有兩種 hello**我的報表**私人 tooyou 區段或 hello**共用報表**具有存取權可存取 tooeveryone 區段toohello Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="0968b-155">Workbooks are saved within an Application Insights resource, either in hello **My Reports** section that's private tooyou or in hello **Shared Reports** section that's accessible tooeveryone with access toohello Application Insights resource.</span></span> <span data-ttu-id="0968b-156">tooview hello 資源中的所有 hello 活頁簿都按一下 hello**開啟**hello 動作列中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="0968b-156">tooview all hello workbooks in hello resource, click hello **Open** button in hello action bar.</span></span>

<span data-ttu-id="0968b-157">為目前的活頁簿 tooshare**我的報表**:</span><span class="sxs-lookup"><span data-stu-id="0968b-157">tooshare a workbook that's currently in **My Reports**:</span></span>

1. <span data-ttu-id="0968b-158">按一下**開啟**hello 動作列中</span><span class="sxs-lookup"><span data-stu-id="0968b-158">Click **Open** in hello action bar</span></span>
2. <span data-ttu-id="0968b-159">按一下 hello"..."按鈕旁邊 hello 活頁簿中，您想 tooshare</span><span class="sxs-lookup"><span data-stu-id="0968b-159">Click hello "..." button beside hello workbook you want tooshare</span></span>
3. <span data-ttu-id="0968b-160">按一下**移動 tooShared 報表**。</span><span class="sxs-lookup"><span data-stu-id="0968b-160">Click **Move tooShared Reports**.</span></span>

<span data-ttu-id="0968b-161">tooshare 活頁簿的連結，或透過電子郵件，按一下**共用**hello 動作列中。</span><span class="sxs-lookup"><span data-stu-id="0968b-161">tooshare a workbook with a link or via email, click **Share** in hello action bar.</span></span> <span data-ttu-id="0968b-162">請記住 hello 連結的收件者需要存取 toothis hello Azure 入口網站 tooview hello 活頁簿中的資源。</span><span class="sxs-lookup"><span data-stu-id="0968b-162">Keep in mind that recipients of hello link need access toothis resource in hello Azure portal tooview hello workbook.</span></span> <span data-ttu-id="0968b-163">toomake 編輯收件者需要至少 hello 資源的參與者權限。</span><span class="sxs-lookup"><span data-stu-id="0968b-163">toomake edits, recipients need at least Contributor permissions for hello resource.</span></span>

<span data-ttu-id="0968b-164">toopin 連結 tooa 活頁簿 tooan Azure 儀表板：</span><span class="sxs-lookup"><span data-stu-id="0968b-164">toopin a link tooa workbook tooan Azure Dashboard:</span></span>

1. <span data-ttu-id="0968b-165">按一下**開啟**hello 動作列中</span><span class="sxs-lookup"><span data-stu-id="0968b-165">Click **Open** in hello action bar</span></span>
2. <span data-ttu-id="0968b-166">按一下 hello"..."按鈕旁邊 hello 活頁簿中，您想 toopin</span><span class="sxs-lookup"><span data-stu-id="0968b-166">Click hello "..." button beside hello workbook you want toopin</span></span>
3. <span data-ttu-id="0968b-167">按一下**Pin toodashboard**。</span><span class="sxs-lookup"><span data-stu-id="0968b-167">Click **Pin toodashboard**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0968b-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0968b-168">Next steps</span></span>

## <a name="next-steps"></a><span data-ttu-id="0968b-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0968b-169">Next steps</span></span>
- <span data-ttu-id="0968b-170">tooenable 使用狀況發生時，開始傳送[自訂事件](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent)或[頁面檢視](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views)。</span><span class="sxs-lookup"><span data-stu-id="0968b-170">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="0968b-171">如果您已傳送自訂事件或網頁 檢視中瀏覽 hello 使用量工具 toolearn 如何使用者使用您的服務。</span><span class="sxs-lookup"><span data-stu-id="0968b-171">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    - [<span data-ttu-id="0968b-172">使用者、工作階段、事件</span><span class="sxs-lookup"><span data-stu-id="0968b-172">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="0968b-173">漏斗圖</span><span class="sxs-lookup"><span data-stu-id="0968b-173">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="0968b-174">保留</span><span class="sxs-lookup"><span data-stu-id="0968b-174">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="0968b-175">使用者流程</span><span class="sxs-lookup"><span data-stu-id="0968b-175">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="0968b-176">新增使用者內容</span><span class="sxs-lookup"><span data-stu-id="0968b-176">Add user context</span></span>](app-insights-usage-send-user-context.md)
    
