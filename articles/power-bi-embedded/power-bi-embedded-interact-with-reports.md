---
title: "搭配報表使用 hello JavaScript API 的 aaaInteract |Microsoft 文件"
description: "Power BI Embedded，與使用 hello JavaScript API 的報表互動"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: bdd885d3-1b00-4dcf-bdff-531eb1f97bfb
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: 657e4d5cee031bdda173ab3f451cc19b93ddb17b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="interact-with-power-bi-reports-using-hello-javascript-api"></a><span data-ttu-id="79e5f-103">使用 hello JavaScript API 的 Power BI 報表與互動</span><span class="sxs-lookup"><span data-stu-id="79e5f-103">Interact with Power BI reports using hello JavaScript API</span></span>
<span data-ttu-id="79e5f-104">hello Power BI JavaScript API 可讓您 tooeasily Power BI 報表內嵌到應用程式。</span><span class="sxs-lookup"><span data-stu-id="79e5f-104">hello Power BI JavaScript API enables you tooeasily embed Power BI reports into your applications.</span></span> <span data-ttu-id="79e5f-105">以 hello API，您的應用程式以程式設計的方式可以與不同的報表元素，例如分頁和篩選互動。</span><span class="sxs-lookup"><span data-stu-id="79e5f-105">With hello API, your applications can programmatically interact with different report elements like pages and filters.</span></span> <span data-ttu-id="79e5f-106">此互動功能可讓 Power BI 報告更能夠融合到您的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="79e5f-106">This interactivity makes Power BI reports a more integrated part of your application.</span></span>

<span data-ttu-id="79e5f-107">應用程式中內嵌 Power BI 報表時，您使用 iframe 裝載 hello 應用的一部分。</span><span class="sxs-lookup"><span data-stu-id="79e5f-107">You embed a Power BI report in your application by using an iframe that is hosted as part of hello application.</span></span> <span data-ttu-id="79e5f-108">hello iframe 做為您的應用程式與 hello 報表之間的界限，為您可以在下列映像的 hello 中看到。</span><span class="sxs-lookup"><span data-stu-id="79e5f-108">hello iframe acts as a boundary between your application and hello report, as you can see in hello following image.</span></span> 

![不具 JavaScript API 的 Power BI Embedded iframe](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-1.png)

<span data-ttu-id="79e5f-110">hello iframe hello 內嵌程序中來得簡單許多，但是沒有 hello JavaScript API hello 報表和應用程式無法彼此互動。</span><span class="sxs-lookup"><span data-stu-id="79e5f-110">hello iframe makes hello embedding process a lot easier, but without hello JavaScript API hello report and your application can't interact with each other.</span></span> <span data-ttu-id="79e5f-111">這種欠缺的互動功能，可讓覺得 hello 報表不全然 hello 應用程式的一部分。</span><span class="sxs-lookup"><span data-stu-id="79e5f-111">This lack of interaction can make it feel like hello report is not really part of hello application.</span></span> <span data-ttu-id="79e5f-112">hello 報表和應用程式真的需要 toocommunicate 來回，如 hello 下列影像所示。</span><span class="sxs-lookup"><span data-stu-id="79e5f-112">hello report and application really need toocommunicate back and forth, as in hello following image.</span></span>

![具有 JavaScript API 的 Power BI Embedded iframe](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-2.png)

<span data-ttu-id="79e5f-114">hello Power BI JavaScript API，可讓您可以安全地通過 hello iframe 界限 toowrite 程式碼。</span><span class="sxs-lookup"><span data-stu-id="79e5f-114">hello Power BI JavaScript API enables you toowrite code that can securely pass through hello iframe boundary.</span></span> <span data-ttu-id="79e5f-115">這樣做可讓您的應用程式 tooprogrammatically 報表和來自使用者 hello 報表內進行的動作事件 toolisten 中執行的動作。</span><span class="sxs-lookup"><span data-stu-id="79e5f-115">This enables your application tooprogrammatically perform an action in a report, and toolisten for events from actions that users make within hello report.</span></span>

## <a name="what-can-you-do-with-hello-power-bi-javascript-api"></a><span data-ttu-id="79e5f-116">您可以使用 Power BI JavaScript API hello 做什麼？</span><span class="sxs-lookup"><span data-stu-id="79e5f-116">What can you do with hello Power BI JavaScript API?</span></span>
<span data-ttu-id="79e5f-117">以 hello JavaScript API 可以管理報表、 瀏覽報表中的 toopages、 篩選報表，和處理內嵌事件。</span><span class="sxs-lookup"><span data-stu-id="79e5f-117">With hello JavaScript API you can manage reports, navigate toopages in a report, filter a report, and handle embedding events.</span></span> <span data-ttu-id="79e5f-118">hello 下列圖表顯示 hello API hello 結構。</span><span class="sxs-lookup"><span data-stu-id="79e5f-118">hello following diagram shows hello structure of hello API.</span></span>

![Power BI JavaScript API 圖表](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-3.png)

### <a name="manage-reports"></a><span data-ttu-id="79e5f-120">管理報告</span><span class="sxs-lookup"><span data-stu-id="79e5f-120">Manage reports</span></span>
<span data-ttu-id="79e5f-121">hello Javascript 應用程式開發介面可讓您在 hello 報表和頁面層級 toomanage 行為：</span><span class="sxs-lookup"><span data-stu-id="79e5f-121">hello Javascript API enables you toomanage behavior at hello report and page level:</span></span>

* <span data-ttu-id="79e5f-122">安全地將特定的 Power BI 報表內嵌在您的應用程式-請嘗試 hello[內嵌示範應用程式](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)</span><span class="sxs-lookup"><span data-stu-id="79e5f-122">Embed a specific Power BI Report securely in your application - try hello [embed demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)</span></span>
  * <span data-ttu-id="79e5f-123">設定存取權杖</span><span class="sxs-lookup"><span data-stu-id="79e5f-123">Set access token</span></span>
* <span data-ttu-id="79e5f-124">Hello 報表設定</span><span class="sxs-lookup"><span data-stu-id="79e5f-124">Configure hello report</span></span>
  * <span data-ttu-id="79e5f-125">啟用和停用 hello 篩選 窗格和頁面導覽窗格-重試 hello[更新示範應用程式中設定](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)</span><span class="sxs-lookup"><span data-stu-id="79e5f-125">Enable and disable hello filter pane and page navigation pane - try hello [update settings demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)</span></span>
  * <span data-ttu-id="79e5f-126">設定網頁及篩選器的預設值-重試 hello[組預設值示範](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)</span><span class="sxs-lookup"><span data-stu-id="79e5f-126">Set defaults for pages and filters - try hello [set defaults demo](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)</span></span>
* <span data-ttu-id="79e5f-127">進入或離開全螢幕模式</span><span class="sxs-lookup"><span data-stu-id="79e5f-127">Enter and exit full screen mode</span></span>

[<span data-ttu-id="79e5f-128">深入了解內嵌報告</span><span class="sxs-lookup"><span data-stu-id="79e5f-128">Learn more about embedding a report</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embedding-Basics)

### <a name="navigate-toopages-in-a-report"></a><span data-ttu-id="79e5f-129">瀏覽報表中的 toopages</span><span class="sxs-lookup"><span data-stu-id="79e5f-129">Navigate toopages in a report</span></span>
<span data-ttu-id="79e5f-130">hello JavaScript API enbales 所有的您 toodiscover 報表和 tooset hello 目前頁面中的分頁。</span><span class="sxs-lookup"><span data-stu-id="79e5f-130">hello JavaScript API enbales you toodiscover all pages in a report and tooset hello current page.</span></span> <span data-ttu-id="79e5f-131">再試一次 hello[示範應用程式中瀏覽](http://azure-samples.github.io/powerbi-angular-client/#/scenario3)。</span><span class="sxs-lookup"><span data-stu-id="79e5f-131">Try hello [navigation demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).</span></span>

[<span data-ttu-id="79e5f-132">深入了解頁面瀏覽</span><span class="sxs-lookup"><span data-stu-id="79e5f-132">Learn more about page navigation</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Page-Navigation)

### <a name="filter-a-report"></a><span data-ttu-id="79e5f-133">篩選報告</span><span class="sxs-lookup"><span data-stu-id="79e5f-133">Filter a report</span></span>
<span data-ttu-id="79e5f-134">hello JavaScript 應用程式開發介面會提供基本和進階篩選的內嵌的報表和報表頁面的功能。</span><span class="sxs-lookup"><span data-stu-id="79e5f-134">hello JavaScript API provides basic and advanced filtering capabilities for embedded reports and report pages.</span></span> <span data-ttu-id="79e5f-135">再試一次 hello[篩選示範應用程式](http://azure-samples.github.io/powerbi-angular-client/#/scenario4)，並檢閱一些基本的程式碼。</span><span class="sxs-lookup"><span data-stu-id="79e5f-135">Try hello [filtering demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario4), and review some introductory code here.</span></span>  

#### <a name="basic-filters"></a><span data-ttu-id="79e5f-136">基本篩選器</span><span class="sxs-lookup"><span data-stu-id="79e5f-136">Basic filters</span></span>
<span data-ttu-id="79e5f-137">基本篩選放置在資料行或階層層級，並包含的值 tooinclude 」 或 「 排除清單。</span><span class="sxs-lookup"><span data-stu-id="79e5f-137">A basic filter is placed on a column or hierarchy level and contains a list of values tooinclude or exclude.</span></span>

```
const basicFilter: pbi.models.IBasicFilter = {
  $schema: "http://powerbi.com/product/schema#basic",
  target: {
    table: "Store",
    column: "Count"
  },
  operator: "In",
  values: [1,2,3,4]
}
```


#### <a name="advanced-filters"></a><span data-ttu-id="79e5f-138">進階篩選器</span><span class="sxs-lookup"><span data-stu-id="79e5f-138">Advanced filters</span></span>
<span data-ttu-id="79e5f-139">進階篩選器使用 hello 邏輯運算子或 OR，而且接受一個或兩個條件，每個都有自己的運算子和值。</span><span class="sxs-lookup"><span data-stu-id="79e5f-139">Advanced filters use hello logical operator AND or OR, and accept one or two conditions, each with their own operator and value.</span></span> <span data-ttu-id="79e5f-140">支援的條件如下︰</span><span class="sxs-lookup"><span data-stu-id="79e5f-140">Supported conditions are:</span></span>

* <span data-ttu-id="79e5f-141">None</span><span class="sxs-lookup"><span data-stu-id="79e5f-141">None</span></span>
* <span data-ttu-id="79e5f-142">LessThan</span><span class="sxs-lookup"><span data-stu-id="79e5f-142">LessThan</span></span>
* <span data-ttu-id="79e5f-143">LessThanOrEqual</span><span class="sxs-lookup"><span data-stu-id="79e5f-143">LessThanOrEqual</span></span>
* <span data-ttu-id="79e5f-144">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="79e5f-144">GreaterThan</span></span>
* <span data-ttu-id="79e5f-145">GreaterThanOrEqual</span><span class="sxs-lookup"><span data-stu-id="79e5f-145">GreaterThanOrEqual</span></span>
* <span data-ttu-id="79e5f-146">Contains</span><span class="sxs-lookup"><span data-stu-id="79e5f-146">Contains</span></span>
* <span data-ttu-id="79e5f-147">DoesNotContain</span><span class="sxs-lookup"><span data-stu-id="79e5f-147">DoesNotContain</span></span>
* <span data-ttu-id="79e5f-148">StartsWith</span><span class="sxs-lookup"><span data-stu-id="79e5f-148">StartsWith</span></span>
* <span data-ttu-id="79e5f-149">DoesNotStartWith</span><span class="sxs-lookup"><span data-stu-id="79e5f-149">DoesNotStartWith</span></span>
* <span data-ttu-id="79e5f-150">Is</span><span class="sxs-lookup"><span data-stu-id="79e5f-150">Is</span></span>
* <span data-ttu-id="79e5f-151">IsNot</span><span class="sxs-lookup"><span data-stu-id="79e5f-151">IsNot</span></span>
* <span data-ttu-id="79e5f-152">IsBlank</span><span class="sxs-lookup"><span data-stu-id="79e5f-152">IsBlank</span></span>
* <span data-ttu-id="79e5f-153">IsNotBlank</span><span class="sxs-lookup"><span data-stu-id="79e5f-153">IsNotBlank</span></span>

```
const advancedFilter: pbi.models.IAdvancedFilter = {
  $schema: "http://powerbi.com/product/schema#advanced",
  target: {
    table: "Store",
    column: "Name"
  },
  logicalOperator: "Or",
  conditions: [
    {
      operator: "Contains",
      value: "Wash"
    },
    {
      operator: "Contains",
      value: "Park"
    }
  ]
}
```
[<span data-ttu-id="79e5f-154">深入了解篩選</span><span class="sxs-lookup"><span data-stu-id="79e5f-154">Learn more about filtering</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Filters)

### <a name="handling-events"></a><span data-ttu-id="79e5f-155">錯誤事件</span><span class="sxs-lookup"><span data-stu-id="79e5f-155">Handling events</span></span>
<span data-ttu-id="79e5f-156">此外 hello iframe toosending 資訊，您的應用程式也可以接收 hello 下列來自 hello iframe 的事件的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="79e5f-156">In addition toosending information into hello iframe, your application can also receive information on hello following events coming from hello iframe:</span></span>

* <span data-ttu-id="79e5f-157">內嵌</span><span class="sxs-lookup"><span data-stu-id="79e5f-157">Embed</span></span>
  * <span data-ttu-id="79e5f-158">已載入</span><span class="sxs-lookup"><span data-stu-id="79e5f-158">loaded</span></span>
  * <span data-ttu-id="79e5f-159">錯誤</span><span class="sxs-lookup"><span data-stu-id="79e5f-159">error</span></span>
* <span data-ttu-id="79e5f-160">報告</span><span class="sxs-lookup"><span data-stu-id="79e5f-160">Reports</span></span>
  * <span data-ttu-id="79e5f-161">pageChanged</span><span class="sxs-lookup"><span data-stu-id="79e5f-161">pageChanged</span></span>
  * <span data-ttu-id="79e5f-162">dataSelected (敬請期待)</span><span class="sxs-lookup"><span data-stu-id="79e5f-162">dataSelected (coming soon)</span></span>

[<span data-ttu-id="79e5f-163">深入了解處理事件</span><span class="sxs-lookup"><span data-stu-id="79e5f-163">Learn more about handling events</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Handling-Events)

## <a name="next-steps"></a><span data-ttu-id="79e5f-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="79e5f-164">Next steps</span></span>
<span data-ttu-id="79e5f-165">如需 hello Power BI JavaScript API 的詳細資訊，請參閱下列連結查看 hello:</span><span class="sxs-lookup"><span data-stu-id="79e5f-165">For more information about hello Power BI JavaScript API, check out hello following links:</span></span>

* [<span data-ttu-id="79e5f-166">JavaScript API Wiki</span><span class="sxs-lookup"><span data-stu-id="79e5f-166">JavaScript API Wiki</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki)
* [<span data-ttu-id="79e5f-167">物件模型參考</span><span class="sxs-lookup"><span data-stu-id="79e5f-167">Object model reference</span></span>](https://microsoft.github.io/powerbi-models/modules/_models_.html)
* <span data-ttu-id="79e5f-168">範例</span><span class="sxs-lookup"><span data-stu-id="79e5f-168">Samples</span></span>
  * [<span data-ttu-id="79e5f-169">Angular</span><span class="sxs-lookup"><span data-stu-id="79e5f-169">Angular</span></span>](http://azure-samples.github.io/powerbi-angular-client)
  * [<span data-ttu-id="79e5f-170">Ember</span><span class="sxs-lookup"><span data-stu-id="79e5f-170">Ember</span></span>](https://github.com/Microsoft/powerbi-ember)
* [<span data-ttu-id="79e5f-171">實況示範</span><span class="sxs-lookup"><span data-stu-id="79e5f-171">Live demo</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)

