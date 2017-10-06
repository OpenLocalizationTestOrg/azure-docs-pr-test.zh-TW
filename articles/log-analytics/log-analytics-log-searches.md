---
title: "在 Azure 記錄分析記錄搜尋 aaaFind 資料 |Microsoft 文件"
description: "Toocombine 可讓您記錄搜尋，並相互關聯您環境內多個來源的任何電腦資料。"
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: 0d7b6712-1722-423b-a60f-05389cde3625
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: 1161857a0027f05726492417362cb24a8fe21ef8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="find-data-using-log-searches-in-log-analytics"></a><span data-ttu-id="14a7a-103">在 Log Analytics 中使用記錄搜尋以尋找資料</span><span class="sxs-lookup"><span data-stu-id="14a7a-103">Find data using log searches in Log Analytics</span></span>

>[!NOTE]
> <span data-ttu-id="14a7a-104">本文說明的記錄搜尋記錄分析中使用 hello 目前的查詢語言。</span><span class="sxs-lookup"><span data-stu-id="14a7a-104">This article describes log searches using hello current query language in Log Analytics.</span></span>  <span data-ttu-id="14a7a-105">如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，再過，您應該參閱[了解記錄搜尋中記錄分析 （新）](log-analytics-log-search-new.md)。</span><span class="sxs-lookup"><span data-stu-id="14a7a-105">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should refer too[Understanding log searches in Log Analytics (new)](log-analytics-log-search-new.md).</span></span>


<span data-ttu-id="14a7a-106">記錄分析的 hello 核心是 hello 記錄搜尋功能，可讓您 toocombine 和相互關聯您環境內多個來源的任何電腦資料。</span><span class="sxs-lookup"><span data-stu-id="14a7a-106">At hello core of Log Analytics is hello log search feature which allows you toocombine and correlate any machine data from multiple sources within your environment.</span></span> <span data-ttu-id="14a7a-107">解決方案也被 powered by 記錄搜尋 toobring 您度量特定問題領域的核心中。</span><span class="sxs-lookup"><span data-stu-id="14a7a-107">Solutions are also powered by log search toobring you metrics pivoted around a particular problem area.</span></span>

<span data-ttu-id="14a7a-108">在 hello 搜尋頁面上，您可以建立查詢，，然後在搜尋時，您可以篩選 hello 結果使用 facet 控制。</span><span class="sxs-lookup"><span data-stu-id="14a7a-108">On hello Search page, you can create a query, and then when you search, you can filter hello results by using facet controls.</span></span> <span data-ttu-id="14a7a-109">您也可以建立進階的查詢 tootransform、 篩選和報告結果。</span><span class="sxs-lookup"><span data-stu-id="14a7a-109">You can also create advanced queries tootransform, filter, and report on your results.</span></span>

<span data-ttu-id="14a7a-110">常見的記錄搜尋查詢會出現在大部分解決方案頁面中。</span><span class="sxs-lookup"><span data-stu-id="14a7a-110">Common log search queries appear on most solution pages.</span></span> <span data-ttu-id="14a7a-111">在整個 hello OMS 主控台中，您可以按一下磚或切入 tooother 項目中 tooview hello 項目詳細資料，使用 記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="14a7a-111">Throughout hello OMS console, you can click tiles or drill in tooother items tooview details about hello item by using log search.</span></span>

<span data-ttu-id="14a7a-112">在本教學課程中，我們將逐步範例 toocover 所有 hello 基本概念當您使用記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="14a7a-112">In this tutorial, we'll walk through examples toocover all hello basics when you use log search.</span></span>

<span data-ttu-id="14a7a-113">我們會以簡單、 實用的範例開頭，然後根據這些如此就可以了解實際的使用案例 toouse hello 語法 tooextract hello insights 您要如何從 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="14a7a-113">We'll start with simple, practical examples and then build on them so that you can get an understanding of practical use cases about how toouse hello syntax tooextract hello insights you want from hello data.</span></span>

<span data-ttu-id="14a7a-114">熟悉搜尋技術之後，您可以檢閱 hello[記錄分析記錄搜尋參考](log-analytics-search-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="14a7a-114">After you've familiar with search techniques, you can review hello [Log Analytics log search reference](log-analytics-search-reference.md).</span></span>

## <a name="use-basic-filters"></a><span data-ttu-id="14a7a-115">使用基本篩選器</span><span class="sxs-lookup"><span data-stu-id="14a7a-115">Use basic filters</span></span>
<span data-ttu-id="14a7a-116">hello 首先 tooknow 是該 hello 第一個部分的搜尋查詢，才能進行任何"|"直立線符號字元永遠是*篩選*。</span><span class="sxs-lookup"><span data-stu-id="14a7a-116">hello first thing tooknow is that hello first part of a search query, before any "|" vertical pipe character, is always a *filter*.</span></span> <span data-ttu-id="14a7a-117">您可以將其視為 TSQL 中的 WHERE 子句，以此判斷*什麼*資料 toopull 從 hello OMS 資料存放區的子集。</span><span class="sxs-lookup"><span data-stu-id="14a7a-117">You can think of it as a WHERE clause in TSQL--it determines *what* subset of data toopull out of hello OMS data store.</span></span> <span data-ttu-id="14a7a-118">Hello 資料存放區中搜尋主要是有關指定您想 tooextract，因此很自然地查詢會以 hello WHERE 子句開頭的 hello 資料 hello 特性。</span><span class="sxs-lookup"><span data-stu-id="14a7a-118">Searching in hello data store is largely about specifying hello characteristics of hello data that you want tooextract, so it is natural that a query would start with hello WHERE clause.</span></span>

<span data-ttu-id="14a7a-119">hello 最基本的篩選，您可以使用會*關鍵字*，例如 'error' 或 'timeout' 或電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="14a7a-119">hello most basic filters you can use are *keywords*, such as ‘error’ or ‘timeout’, or a computer name.</span></span> <span data-ttu-id="14a7a-120">這些簡單的查詢類型通常會傳回不同的圖形資料以 hello 相同結果集。</span><span class="sxs-lookup"><span data-stu-id="14a7a-120">These types of simple queries generally return diverse shapes of data within hello same result set.</span></span> <span data-ttu-id="14a7a-121">這是因為有不同的記錄分析*類型*hello 系統中的資料。</span><span class="sxs-lookup"><span data-stu-id="14a7a-121">This is because Log Analytics has different *types* of data in hello system.</span></span>

### <a name="tooconduct-a-simple-search"></a><span data-ttu-id="14a7a-122">tooconduct 簡單搜尋</span><span class="sxs-lookup"><span data-stu-id="14a7a-122">tooconduct a simple search</span></span>
1. <span data-ttu-id="14a7a-123">在 hello OMS 入口網站中，按一下 **記錄搜尋**。</span><span class="sxs-lookup"><span data-stu-id="14a7a-123">In hello OMS portal, click **Log Search**.</span></span>  
    <span data-ttu-id="14a7a-124">![搜尋圖格](./media/log-analytics-log-searches/oms-overview-log-search.png)</span><span class="sxs-lookup"><span data-stu-id="14a7a-124">![search tile](./media/log-analytics-log-searches/oms-overview-log-search.png)</span></span>
2. <span data-ttu-id="14a7a-125">在 hello 查詢欄位中，輸入`error`，然後按一下**搜尋**。</span><span class="sxs-lookup"><span data-stu-id="14a7a-125">In hello query field, type `error` and then click **Search**.</span></span>  
    <span data-ttu-id="14a7a-126">![搜尋錯誤](./media/log-analytics-log-searches/oms-search-error.png)</span><span class="sxs-lookup"><span data-stu-id="14a7a-126">![search error](./media/log-analytics-log-searches/oms-search-error.png)</span></span>  
    <span data-ttu-id="14a7a-127">例如，hello 查詢`error`hello 在下圖中傳回 100,000 個**事件**記錄 （由記錄管理所收集）、 18 **ConfigurationAlert** （由組態所產生的記錄評估） 到 12 **ConfigurationChange**記錄 （由 hello 變更追蹤所擷取）。</span><span class="sxs-lookup"><span data-stu-id="14a7a-127">For example, hello query for `error` in hello following image returned 100,000 **Event** records (collected by Log Management), 18 **ConfigurationAlert** records (generated by Configuration Assessment) and 12 **ConfigurationChange** records (captured by hello Change Tracking).</span></span>   
    <span data-ttu-id="14a7a-128">![搜尋結果](./media/log-analytics-log-searches/oms-search-results01.png)</span><span class="sxs-lookup"><span data-stu-id="14a7a-128">![search results](./media/log-analytics-log-searches/oms-search-results01.png)</span></span>  

<span data-ttu-id="14a7a-129">這些篩選器不一定是物件類型/類別。</span><span class="sxs-lookup"><span data-stu-id="14a7a-129">These filters are not really object types/classes.</span></span> <span data-ttu-id="14a7a-130">*型別*只標記或屬性，或字串/名稱/類別，所附加 tooa 一段資料。</span><span class="sxs-lookup"><span data-stu-id="14a7a-130">*Type* is just a tag, or a property, or a string/name/category, that is attached tooa piece of data.</span></span> <span data-ttu-id="14a7a-131">Hello 系統中的某些文件會標記為**Type: ConfigurationAlert**和某些會標記為**類型： 效能**，或**Type: Event**，依此類推。</span><span class="sxs-lookup"><span data-stu-id="14a7a-131">Some documents in hello system are tagged as **Type:ConfigurationAlert** and some are tagged as **Type:Perf**, or **Type:Event**, and so on.</span></span> <span data-ttu-id="14a7a-132">每個搜尋結果、 文件、 記錄或項目會顯示所有 hello 未經處理的屬性及其值的每個這些片段的資料，而且您可以使用那些欄位名稱 toospecify hello 篩選中想 tooretrieve 僅 hello 記錄時其中 hello 欄位具有指定值。</span><span class="sxs-lookup"><span data-stu-id="14a7a-132">Each search result, document, record, or entry displays all hello raw properties and their values for each of those pieces of data, and you can use those field names toospecify in hello filter when you want tooretrieve only hello records where hello field has that given value.</span></span>

<span data-ttu-id="14a7a-133">「類型」其實只是所有記錄都有的欄位，與任何其他欄位並沒有不同。</span><span class="sxs-lookup"><span data-stu-id="14a7a-133">*Type* is really just a field that all records have, it is not different from any other field.</span></span> <span data-ttu-id="14a7a-134">這被建立根據 hello hello 類型欄位的值。</span><span class="sxs-lookup"><span data-stu-id="14a7a-134">This was established based on hello value of hello Type field.</span></span> <span data-ttu-id="14a7a-135">該記錄會有不同的圖形或形式。</span><span class="sxs-lookup"><span data-stu-id="14a7a-135">That record will have a different shape or form.</span></span> <span data-ttu-id="14a7a-136">順帶一提，**類型 = Perf**，或**類型 = 事件**也是您的效能資料或事件需要 toolearn tooquery hello 語法。</span><span class="sxs-lookup"><span data-stu-id="14a7a-136">Incidentally, **Type=Perf**, or **Type=Event** is also hello syntax that you need toolearn tooquery for performance data or events.</span></span>

<span data-ttu-id="14a7a-137">Hello 欄位名稱之後和 hello 值之前，您可以使用冒號 （:） 或等號 （=）。</span><span class="sxs-lookup"><span data-stu-id="14a7a-137">You can use either a colon (:) or an equal sign (=) after hello field name and before hello value.</span></span> <span data-ttu-id="14a7a-138">**Type: Event**和**類型 = 事件**是相同的意義，您可以選擇 hello 您偏好的樣式。</span><span class="sxs-lookup"><span data-stu-id="14a7a-138">**Type:Event** and **Type=Event** are equivalent in meaning, you can choose hello style you prefer.</span></span>

<span data-ttu-id="14a7a-139">因此，如果 hello 輸入 = 效能記錄具有名為 'CounterName' 的欄位，然後您可以撰寫類似如下`Type=Perf CounterName="% Processor Time"`。</span><span class="sxs-lookup"><span data-stu-id="14a7a-139">So, if hello Type=Perf records have a field called 'CounterName', then you can write a query resembling `Type=Perf CounterName="% Processor Time"`.</span></span>

<span data-ttu-id="14a7a-140">這可以提供您唯一 hello 效能資料，其中 hello 效能計數器名稱是"%Processor Time"。</span><span class="sxs-lookup"><span data-stu-id="14a7a-140">This will give you only hello performance data where hello performance counter name is "% Processor Time".</span></span>

### <a name="toosearch-for-processor-time-performance-data"></a><span data-ttu-id="14a7a-141">toosearch 處理器時間效能資料</span><span class="sxs-lookup"><span data-stu-id="14a7a-141">toosearch for processor time performance data</span></span>
* <span data-ttu-id="14a7a-142">在 hello 搜尋查詢欄位中，輸入`Type=Perf CounterName="% Processor Time"`</span><span class="sxs-lookup"><span data-stu-id="14a7a-142">In hello search query field, type `Type=Perf CounterName="% Processor Time"`</span></span>

<span data-ttu-id="14a7a-143">您也可以更明確，並使用**InstanceName = _'total '** hello 查詢中，此為 Windows 效能計數器。</span><span class="sxs-lookup"><span data-stu-id="14a7a-143">You can also be more specific and use **InstanceName=_'Total'** in hello query, which is a Windows performance counter.</span></span> <span data-ttu-id="14a7a-144">您也可以選取 facet 和另一個 **field:value**。</span><span class="sxs-lookup"><span data-stu-id="14a7a-144">You can also select a facet and another **field:value**.</span></span> <span data-ttu-id="14a7a-145">hello 篩選器會自動加入 tooyour 篩選 hello 查詢列中。</span><span class="sxs-lookup"><span data-stu-id="14a7a-145">hello filter is automatically added tooyour filter in hello query bar.</span></span> <span data-ttu-id="14a7a-146">您可以在下列映像的 hello 看到。</span><span class="sxs-lookup"><span data-stu-id="14a7a-146">You can see this in hello following image.</span></span> <span data-ttu-id="14a7a-147">它會示範其中 tooclick tooadd **InstanceName: '_Total'** toohello 查詢，而不需要輸入任何項目。</span><span class="sxs-lookup"><span data-stu-id="14a7a-147">It shows you where tooclick tooadd **InstanceName:’_Total’** toohello query without typing anything.</span></span>

![搜尋 facet](./media/log-analytics-log-searches/oms-search-facet.png)

<span data-ttu-id="14a7a-149">您的查詢現在已成為 `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`</span><span class="sxs-lookup"><span data-stu-id="14a7a-149">Your query now becomes `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`</span></span>

<span data-ttu-id="14a7a-150">在此範例中，您不需要 toospecify**類型 = Perf** tooget toothis 結果。</span><span class="sxs-lookup"><span data-stu-id="14a7a-150">In this example, you don't have toospecify **Type=Perf** tooget toothis result.</span></span> <span data-ttu-id="14a7a-151">因為 CounterName 和 InstanceName hello 欄位只存在於類型的記錄 = 效能，hello 查詢 hello 先前較長的相同的結果是不夠具體 tooreturn hello:</span><span class="sxs-lookup"><span data-stu-id="14a7a-151">Because hello fields CounterName and InstanceName only exist for records of Type=Perf, hello query is specific enough tooreturn hello same results as hello longer, previous one:</span></span>

```
CounterName="% Processor Time" InstanceName="_Total"
```

<span data-ttu-id="14a7a-152">這是因為 hello 查詢中的所有 hello 篩選條件會都評估為*AND*彼此。</span><span class="sxs-lookup"><span data-stu-id="14a7a-152">This is because all hello filters in hello query are evaluated as being in *AND* with each other.</span></span> <span data-ttu-id="14a7a-153">實際上，hello 新增 toohello 準則的多個欄位，您取得小於，更特定且精緻的結果。</span><span class="sxs-lookup"><span data-stu-id="14a7a-153">Effectively, hello more fields you add toohello criteria, you get less, more specific and refined results.</span></span>

<span data-ttu-id="14a7a-154">例如，hello 查詢`Type=Event EventLog="Windows PowerShell"`太相同`Type=Event AND EventLog="Windows PowerShell"`。</span><span class="sxs-lookup"><span data-stu-id="14a7a-154">For example, hello query `Type=Event EventLog="Windows PowerShell"` is identical too`Type=Event AND EventLog="Windows PowerShell"`.</span></span> <span data-ttu-id="14a7a-155">它會傳回登入以及從 hello Windows PowerShell 事件記錄檔收集到的所有事件。</span><span class="sxs-lookup"><span data-stu-id="14a7a-155">It returns all events that were logged in and collected from hello Windows PowerShell event log.</span></span> <span data-ttu-id="14a7a-156">如果您加入篩選多次藉由重複選取相同的 facet，然後 hello 問題會相當明確-它可能會干擾 hello 搜尋列中，但它仍會傳回 hello 相同的結果因為 hello 隱含 AND 運算子一律都會有 hello。</span><span class="sxs-lookup"><span data-stu-id="14a7a-156">If you add a filter multiple times by repeatedly selecting hello same facet, then hello issue is purely cosmetic--it might clutter hello Search bar, but it still returns hello same results because hello implicit AND operator is always there.</span></span>

<span data-ttu-id="14a7a-157">您可以藉由明確使用 NOT 運算子，輕鬆地反轉隱含 AND 運算子 hello。</span><span class="sxs-lookup"><span data-stu-id="14a7a-157">You can easily reverse hello implicit AND operator by using a NOT operator explicitly.</span></span> <span data-ttu-id="14a7a-158">例如：</span><span class="sxs-lookup"><span data-stu-id="14a7a-158">For example:</span></span>

<span data-ttu-id="14a7a-159">`Type:Event NOT(EventLog:"Windows PowerShell")`或它的對等`Type=Event EventLog!="Windows PowerShell"`從所有其他不 hello 的 Windows PowerShell 記錄檔的記錄檔傳回所有事件。</span><span class="sxs-lookup"><span data-stu-id="14a7a-159">`Type:Event NOT(EventLog:"Windows PowerShell")` or its equivalent `Type=Event EventLog!="Windows PowerShell"` return all events from all other logs that are NOT hello Windows PowerShell log.</span></span>

<span data-ttu-id="14a7a-160">或者，您可以使用其他布林運算子，例如 'OR'。</span><span class="sxs-lookup"><span data-stu-id="14a7a-160">Or, you can use other Boolean operator such as ‘OR’.</span></span> <span data-ttu-id="14a7a-161">hello 下列查詢會傳回記錄的 hello EventLog 為應用程式或系統。</span><span class="sxs-lookup"><span data-stu-id="14a7a-161">hello following query returns records for which hello EventLog is either Application OR System.</span></span>

```
EventLog=Application OR EventLog=System
```

<span data-ttu-id="14a7a-162">使用上述查詢的 hello，您會取得項目兩個記錄中 hello 相同結果集。</span><span class="sxs-lookup"><span data-stu-id="14a7a-162">Using hello above query, you’ll get entries for both logs in hello same result set.</span></span>

<span data-ttu-id="14a7a-163">不過，如果您 hello 或藉由保留 hello 隱含 AND 以移除，然後 hello 下列查詢將不產生任何結果，因為沒有所屬 tooBOTH 記錄的事件記錄檔項目。</span><span class="sxs-lookup"><span data-stu-id="14a7a-163">However, if you remove hello OR by leaving hello implicit AND in place, then hello following query will not produce any results because there isn’t an event log entry that belongs tooBOTH logs.</span></span> <span data-ttu-id="14a7a-164">每個事件記錄檔項目會寫入 tooonly hello 兩個記錄檔的其中一個。</span><span class="sxs-lookup"><span data-stu-id="14a7a-164">Each event log entry was written tooonly one of hello two logs.</span></span>

```
EventLog=Application EventLog=System
```


## <a name="use-additional-filters"></a><span data-ttu-id="14a7a-165">使用其他篩選器</span><span class="sxs-lookup"><span data-stu-id="14a7a-165">Use additional filters</span></span>
<span data-ttu-id="14a7a-166">hello 下列查詢會傳回所有已傳送資料的 hello 電腦 2 的事件記錄檔項目。</span><span class="sxs-lookup"><span data-stu-id="14a7a-166">hello following query returns entries for 2 event logs for all hello computers that have sent data.</span></span>

```
EventLog=Application OR EventLog=System
```

![搜尋結果](./media/log-analytics-log-searches/oms-search-results03.png)

<span data-ttu-id="14a7a-168">選取其中一個 hello 欄位或篩選器會縮小 hello 查詢 tooa 特定電腦，並排除所有其他電腦。</span><span class="sxs-lookup"><span data-stu-id="14a7a-168">Selecting one of hello fields or filters will narrow hello query tooa specific computer, excluding all other ones.</span></span> <span data-ttu-id="14a7a-169">hello 產生的查詢就會類似下列 hello。</span><span class="sxs-lookup"><span data-stu-id="14a7a-169">hello resulting query would resemble hello following.</span></span>

```
EventLog=Application OR EventLog=System Computer=SERVER1.contoso.com
```

<span data-ttu-id="14a7a-170">這是對等 toohello 下列項目，因為 hello 隱含 and。</span><span class="sxs-lookup"><span data-stu-id="14a7a-170">Which is equivalent toohello following, because of hello implicit AND.</span></span>

```
EventLog=Application OR EventLog=System AND Computer=SERVER1.contoso.com
```

<span data-ttu-id="14a7a-171">每個查詢都會進行評估 hello 下列明確的順序。</span><span class="sxs-lookup"><span data-stu-id="14a7a-171">Each query is evaluated in hello following explicit order.</span></span> <span data-ttu-id="14a7a-172">請注意 hello 括號。</span><span class="sxs-lookup"><span data-stu-id="14a7a-172">Note hello parenthesis.</span></span>

```
(EventLog=Application OR EventLog=System) AND Computer=SERVER1.contoso.com
```

<span data-ttu-id="14a7a-173">如同 hello 事件記錄檔 欄位中，您可以擷取一組特定電腦的資料，藉由新增或者。</span><span class="sxs-lookup"><span data-stu-id="14a7a-173">Just like hello event log field, you can retrieve data only for a set of specific computers by adding OR.</span></span> <span data-ttu-id="14a7a-174">例如：</span><span class="sxs-lookup"><span data-stu-id="14a7a-174">For example:</span></span>

```
(EventLog=Application OR EventLog=System) AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com OR Computer=SERVER3.contoso.com)
```

<span data-ttu-id="14a7a-175">同樣地，下列查詢傳回這個 hello **%cpu 時間**hello 所選的兩部電腦。</span><span class="sxs-lookup"><span data-stu-id="14a7a-175">Similarly, this hello following query return **% CPU Time** for hello selected two computers only.</span></span>

```
CounterName="% Processor Time"  AND InstanceName="_Total" AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com)
```

### <a name="field-types"></a><span data-ttu-id="14a7a-176">欄位類型</span><span class="sxs-lookup"><span data-stu-id="14a7a-176">Field types</span></span>
<span data-ttu-id="14a7a-177">在建立篩選器時，您應該了解 hello 差異，在使用不同類型的記錄搜尋所傳回的欄位。</span><span class="sxs-lookup"><span data-stu-id="14a7a-177">When creating filters, you should understand hello differences in working with different types of fields returned by log searches.</span></span>

<span data-ttu-id="14a7a-178">**可搜尋的欄位**會在搜尋結果中以藍色顯示。</span><span class="sxs-lookup"><span data-stu-id="14a7a-178">**Searchable fields** show in blue in search results.</span></span>  <span data-ttu-id="14a7a-179">您可以使用可搜尋的欄位中搜尋條件特定 toohello 欄位 hello 如下：</span><span class="sxs-lookup"><span data-stu-id="14a7a-179">You can use searchable fields in search conditions specific toohello field such as hello following:</span></span>

```
Type: Event EventLevelName: "Error"
Type: SecurityEvent Computer:Contains("contoso.com")
Type: Event EventLevelName IN {"Error","Warning"}
```

<span data-ttu-id="14a7a-180">**自然語言檢索搜尋旗標欄位**會在搜尋結果中以灰色顯示。</span><span class="sxs-lookup"><span data-stu-id="14a7a-180">**Free text searchable fields** are shown in grey in search results.</span></span>  <span data-ttu-id="14a7a-181">它們不能與搜尋條件特定 toohello 欄位，例如可搜尋的欄位。</span><span class="sxs-lookup"><span data-stu-id="14a7a-181">They cannot be used with search conditions specific toohello field like searchable fields.</span></span>  <span data-ttu-id="14a7a-182">它們只會搜尋所有的欄位，例如 hello 下列跨越執行查詢時。</span><span class="sxs-lookup"><span data-stu-id="14a7a-182">They are only searched when performing a query across all fields such as hello following.</span></span>

```
"Error"
Type: Event "Exception"
```


### <a name="boolean-operators"></a><span data-ttu-id="14a7a-183">布林運算子</span><span class="sxs-lookup"><span data-stu-id="14a7a-183">Boolean operators</span></span>
<span data-ttu-id="14a7a-184">在日期時間和數字欄位中，您可以使用「大於」、「小於」和「小於或等於」來搜尋值。</span><span class="sxs-lookup"><span data-stu-id="14a7a-184">With datetime and numeric fields, you can search for values using *greater than*, *lesser than*, and *lesser than or equal*.</span></span> <span data-ttu-id="14a7a-185">您可以使用簡單的運算子，例如 >，<>、 =、 < =、 ！ = hello 查詢搜尋列中。</span><span class="sxs-lookup"><span data-stu-id="14a7a-185">You can use simple operators such as >, < , >=, <= , != in hello query search bar.</span></span>

<span data-ttu-id="14a7a-186">您可以查詢特定一段時間的特定事件記錄。</span><span class="sxs-lookup"><span data-stu-id="14a7a-186">You can query a specific event log for a specific period of time.</span></span> <span data-ttu-id="14a7a-187">例如，hello 過去 24 小時表示以 hello 下列助憶鍵運算式。</span><span class="sxs-lookup"><span data-stu-id="14a7a-187">For example, hello last 24 hours is expressed with hello following mnemonic expression.</span></span>

```
EventLog=System TimeGenerated>NOW-24HOURS
```


#### <a name="toosearch-using-a-boolean-operator"></a><span data-ttu-id="14a7a-188">toosearch 使用布林運算子</span><span class="sxs-lookup"><span data-stu-id="14a7a-188">toosearch using a boolean operator</span></span>
* <span data-ttu-id="14a7a-189">在 hello 搜尋查詢欄位中，輸入`EventLog=System TimeGenerated>NOW-24HOURS`</span><span class="sxs-lookup"><span data-stu-id="14a7a-189">In hello search query field, type `EventLog=System TimeGenerated>NOW-24HOURS`</span></span>  
    <span data-ttu-id="14a7a-190">![使用布林值來搜尋](./media/log-analytics-log-searches/oms-search-boolean.png)</span><span class="sxs-lookup"><span data-stu-id="14a7a-190">![search with boolean](./media/log-analytics-log-searches/oms-search-boolean.png)</span></span>

<span data-ttu-id="14a7a-191">雖然您可以控制 hello 時間間隔，以圖形方式，而且大多數時候您可能會想 toodo，有優點 tooincluding 直接在 hello 查詢時間篩選器。</span><span class="sxs-lookup"><span data-stu-id="14a7a-191">Although you can control hello time interval graphically, and most times you might want toodo that, there are advantages tooincluding a time filter directly into hello query.</span></span> <span data-ttu-id="14a7a-192">比方說，這非常適合儀表板，您可以覆寫每個圖格，不論 hello hello 時間*全域*hello 儀表板頁面上的時間選取器。</span><span class="sxs-lookup"><span data-stu-id="14a7a-192">For example, this works great with dashboards where you can override hello time for each tile, regardless of hello *global* time selector on hello dashboard page.</span></span> <span data-ttu-id="14a7a-193">如需詳細資訊，請參閱 [時間對儀表板很重要](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/)。</span><span class="sxs-lookup"><span data-stu-id="14a7a-193">For more information, see [Time Matters in Dashboard](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).</span></span>

<span data-ttu-id="14a7a-194">時藉由時間篩選，請記住，您會得到的結果 hello*交集*hello 的兩個時間週期： hello hello OMS 入口網站 (S1) 中指定的其中一個與 hello hello 查詢 (S2) 中指定的其中一個。</span><span class="sxs-lookup"><span data-stu-id="14a7a-194">When filtering by time, keep in mind that you get results for hello *intersection* of hello two time periods: hello one specified in hello OMS portal (S1) and hello one specified in hello query (S2).</span></span>

![交集](./media/log-analytics-log-searches/oms-search-intersection.png)

<span data-ttu-id="14a7a-196">這表示，如果 hello 時間週期不交集，例如您在其中選擇 hello OMS 入口網站中**本週**hello 查詢中定義在**過去一週**沒有交集，您將不會收到任何結果。</span><span class="sxs-lookup"><span data-stu-id="14a7a-196">This means, if hello time periods don’t intersect, for example in hello OMS portal where you choose **This week** and in hello query where you define **last week**, then there is no intersection and you won't receive any results.</span></span>

<span data-ttu-id="14a7a-197">用於 hello TimeGenerated 欄位的比較運算子也會在其他情況下很有用。</span><span class="sxs-lookup"><span data-stu-id="14a7a-197">Comparison operators used for hello TimeGenerated field are also useful in other situations.</span></span> <span data-ttu-id="14a7a-198">例如，用於數值欄位。</span><span class="sxs-lookup"><span data-stu-id="14a7a-198">For example, with numeric fields.</span></span>

<span data-ttu-id="14a7a-199">例如，假設組態評估警示有下列嚴重性值 hello:</span><span class="sxs-lookup"><span data-stu-id="14a7a-199">For example, given that Configuration Assessment’s alerts have hello following severity values:</span></span>

* <span data-ttu-id="14a7a-200">0 = 資訊</span><span class="sxs-lookup"><span data-stu-id="14a7a-200">0 = Information</span></span>
* <span data-ttu-id="14a7a-201">1 = 警告</span><span class="sxs-lookup"><span data-stu-id="14a7a-201">1 = Warning</span></span>
* <span data-ttu-id="14a7a-202">2 = 重大</span><span class="sxs-lookup"><span data-stu-id="14a7a-202">2 = Critical</span></span>

<span data-ttu-id="14a7a-203">您可以查詢警告和重大警示，並也排除的資訊以 hello 下列查詢：</span><span class="sxs-lookup"><span data-stu-id="14a7a-203">You can query for both warning and critical alerts and also exclude informational ones with hello following query:</span></span>

```
Type=ConfigurationAlert  Severity>=1
```


<span data-ttu-id="14a7a-204">您也可以使用範圍查詢。</span><span class="sxs-lookup"><span data-stu-id="14a7a-204">You can also use range queries.</span></span> <span data-ttu-id="14a7a-205">這表示您可以提供的值序列中的 hello 開頭和結尾範圍。</span><span class="sxs-lookup"><span data-stu-id="14a7a-205">This means that you can provide hello beginning and end range of values in a sequence.</span></span> <span data-ttu-id="14a7a-206">例如，如果您想從 hello Operations Manager 事件記錄檔的事件，其中 hello EventID 是大於或等於 too2100 但小於 2199，然後 hello 下列查詢就會傳回它們。</span><span class="sxs-lookup"><span data-stu-id="14a7a-206">For example, if you want events from hello Operations Manager event log where hello EventID is greater than or equal too2100 but not greater than 2199, then hello following query would return them.</span></span>

```
Type=Event EventLog="Operations Manager" EventID:[2100..2199]
```


> [!NOTE]
> <span data-ttu-id="14a7a-207">您必須使用 hello 範圍語法是 hello 冒號 （:） field: value 分隔符號和*不*hello 等號 （=）。</span><span class="sxs-lookup"><span data-stu-id="14a7a-207">hello range syntax you must use is hello colon (:) field:value separator and *not* hello equal sign (=).</span></span> <span data-ttu-id="14a7a-208">方括號括住 hello hello 範圍的下限和上限結尾，並使用兩個句點 （..） 隔開它們。</span><span class="sxs-lookup"><span data-stu-id="14a7a-208">Enclose hello lower and upper end of hello range in square brackets and separate them with two periods (..).</span></span>
>
>

## <a name="manipulate-search-results"></a><span data-ttu-id="14a7a-209">操控搜尋結果</span><span class="sxs-lookup"><span data-stu-id="14a7a-209">Manipulate search results</span></span>
<span data-ttu-id="14a7a-210">當您在搜尋資料時，您會想 toorefine 您的搜尋查詢，且有相當程度的控制權 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="14a7a-210">When you're searching for data, you'll want toorefine your search query and have a good level of control over hello results.</span></span> <span data-ttu-id="14a7a-211">當擷取結果時，您可以套用命令 tootransform 它們。</span><span class="sxs-lookup"><span data-stu-id="14a7a-211">When results are retrieved, you can apply commands tootransform them.</span></span>

<span data-ttu-id="14a7a-212">記錄分析搜尋中的命令*必須*hello 直立線符號字元 (|) 之後。</span><span class="sxs-lookup"><span data-stu-id="14a7a-212">Commands in Log Analytics searches *must* follow after hello vertical pipe character (|).</span></span> <span data-ttu-id="14a7a-213">篩選條件必須永遠是 hello 的查詢字串的第一個部分。</span><span class="sxs-lookup"><span data-stu-id="14a7a-213">A filter must always be hello first part of a query string.</span></span> <span data-ttu-id="14a7a-214">它會定義 hello 您正在使用的資料集，並再"那些結果 「 輸送到命令。</span><span class="sxs-lookup"><span data-stu-id="14a7a-214">It defines hello data set you're working with and then "pipes" those results into a command.</span></span> <span data-ttu-id="14a7a-215">然後，您可以使用 hello 管道 tooadd 其他命令。</span><span class="sxs-lookup"><span data-stu-id="14a7a-215">You can then use hello pipe tooadd additional commands.</span></span> <span data-ttu-id="14a7a-216">這是有點類似 toohello Windows PowerShell 管線。</span><span class="sxs-lookup"><span data-stu-id="14a7a-216">This is loosely similar toohello Windows PowerShell pipeline.</span></span>

<span data-ttu-id="14a7a-217">一般情況下，hello 記錄分析搜尋語言會嘗試 toofollow PowerShell 樣式和指導方針 toomake it 類似 toohello IT 專業人員和 tooease hello 學習曲線。</span><span class="sxs-lookup"><span data-stu-id="14a7a-217">In general, hello Log Analytics search language tries toofollow PowerShell style and guidelines toomake it similar toohello IT pros, and tooease hello learning curve.</span></span>

<span data-ttu-id="14a7a-218">命令具有動詞的名稱，因此您可以輕易地分辨它們執行的動作。</span><span class="sxs-lookup"><span data-stu-id="14a7a-218">Commands have names of verbs so you can easily tell what they do.</span></span>  

### <a name="sort"></a><span data-ttu-id="14a7a-219">排序</span><span class="sxs-lookup"><span data-stu-id="14a7a-219">Sort</span></span>
<span data-ttu-id="14a7a-220">hello sort 命令可讓您利用一或多個欄位排序 toodefine hello。</span><span class="sxs-lookup"><span data-stu-id="14a7a-220">hello sort command allows you toodefine hello sorting order by one or multiple fields.</span></span> <span data-ttu-id="14a7a-221">即使您不使用它，根據預設，會強制執行時間遞減順序。</span><span class="sxs-lookup"><span data-stu-id="14a7a-221">Even if you don’t use it, by default, a time descending order is enforced.</span></span> <span data-ttu-id="14a7a-222">hello 最新的結果一律會在搜尋結果的 hello 最上方。</span><span class="sxs-lookup"><span data-stu-id="14a7a-222">hello most recent results are always at hello top of search results.</span></span> <span data-ttu-id="14a7a-223">這表示當您執行搜尋時，真正利用 `Type=Event EventID=1234` 執行的內容如下：</span><span class="sxs-lookup"><span data-stu-id="14a7a-223">This means that when you run a search, with `Type=Event EventID=1234` what really is executed for you is:</span></span>

```
Type=Event EventID=1234 **| Sort TimeGenerated desc**
```

<span data-ttu-id="14a7a-224">這是經驗的因為它是經驗的您已在記錄中熟悉的 hello 型別。</span><span class="sxs-lookup"><span data-stu-id="14a7a-224">That's because it is hello type of experience you are familiar with in logs.</span></span> <span data-ttu-id="14a7a-225">例如，在 hello Windows 事件檢視器。</span><span class="sxs-lookup"><span data-stu-id="14a7a-225">For example, in hello Windows Event Viewer.</span></span>

<span data-ttu-id="14a7a-226">您可以使用 toochange hello 方法結果的排序。</span><span class="sxs-lookup"><span data-stu-id="14a7a-226">You can use Sort toochange hello way results are returned.</span></span> <span data-ttu-id="14a7a-227">hello 下列範例顯示此運作方式。</span><span class="sxs-lookup"><span data-stu-id="14a7a-227">hello following examples show how this works.</span></span>

```
Type=Event EventID=1234 | Sort TimeGenerated asc
```

```
Type=Event EventID=1234 | Sort Computer asc
```

```
Type=Event EventID=1234 | Sort Computer asc,TimeGenerated desc
```


<span data-ttu-id="14a7a-228">hello 簡單上述範例顯示命令的運作方式--它們會變更 hello 圖形的 hello hello 篩選傳回的結果。</span><span class="sxs-lookup"><span data-stu-id="14a7a-228">hello simple examples above show you how commands work--they change hello shape of hello results that hello filter returned.</span></span>

### <a name="limit-and-top"></a><span data-ttu-id="14a7a-229">Limit 和 top</span><span class="sxs-lookup"><span data-stu-id="14a7a-229">Limit and top</span></span>
<span data-ttu-id="14a7a-230">另一個較少人知道的命令是 LIMIT。</span><span class="sxs-lookup"><span data-stu-id="14a7a-230">Another less known command is LIMIT.</span></span> <span data-ttu-id="14a7a-231">Limit 為類似 PowerShell 的動詞。</span><span class="sxs-lookup"><span data-stu-id="14a7a-231">Limit is a PowerShell-like verb.</span></span> <span data-ttu-id="14a7a-232">限制為功能上與 toohello TOP 命令。</span><span class="sxs-lookup"><span data-stu-id="14a7a-232">Limit is functionally identical toohello TOP command.</span></span> <span data-ttu-id="14a7a-233">hello 下列查詢會傳回 hello 相同的結果。</span><span class="sxs-lookup"><span data-stu-id="14a7a-233">hello following queries return hello same results.</span></span>

```
Type=Event EventID=600 | Limit 1
```

```
Type=Event EventID=600 | Top 1
```


#### <a name="toosearch-using-top"></a><span data-ttu-id="14a7a-234">使用 top toosearch</span><span class="sxs-lookup"><span data-stu-id="14a7a-234">toosearch using top</span></span>
* <span data-ttu-id="14a7a-235">在 hello 搜尋查詢欄位中，輸入`Type=Event EventID=600 | Top 1` </span><span class="sxs-lookup"><span data-stu-id="14a7a-235">In hello search query field, type `Type=Event EventID=600 | Top 1` </span></span>  
    <span data-ttu-id="14a7a-236">![搜尋 top](./media/log-analytics-log-searches/oms-search-top.png)</span><span class="sxs-lookup"><span data-stu-id="14a7a-236">![search top](./media/log-analytics-log-searches/oms-search-top.png)</span></span>

<span data-ttu-id="14a7a-237">Hello 在圖中，有個 358 一千個記錄，附帶 EventID = 600。</span><span class="sxs-lookup"><span data-stu-id="14a7a-237">In hello image above, there are 358 thousand records with EventID=600.</span></span> <span data-ttu-id="14a7a-238">hello 欄位、 facet 和 hello 一律保留傳回的 hello 結果的顯示資訊的篩選器*hello 篩選部分*hello 查詢，這是任何縱線字元之前的 hello 一部分。</span><span class="sxs-lookup"><span data-stu-id="14a7a-238">hello fields, facets, and filters on hello left always show information about hello results returned *by hello filter portion* of hello query, which is hello part before any pipe character.</span></span> <span data-ttu-id="14a7a-239">hello**結果**窗格只會傳回最新的 1 hello 結果，因為 hello 範例命令會圖形化和轉換 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="14a7a-239">hello **Results** pane only returns hello most recent 1 result, because hello example command shaped and transformed hello results.</span></span>

### <a name="select"></a><span data-ttu-id="14a7a-240">選取</span><span class="sxs-lookup"><span data-stu-id="14a7a-240">Select</span></span>
<span data-ttu-id="14a7a-241">hello SELECT 命令的行為類似 PowerShell 中的 Select-object。</span><span class="sxs-lookup"><span data-stu-id="14a7a-241">hello SELECT command behaves like Select-Object in PowerShell.</span></span> <span data-ttu-id="14a7a-242">它會傳回不包含所有原始屬性的篩選結果。</span><span class="sxs-lookup"><span data-stu-id="14a7a-242">It returns filtered results that do not have all of their original properties.</span></span> <span data-ttu-id="14a7a-243">相反地，它會選取您所指定 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="14a7a-243">Instead, it selects only hello properties that you specify.</span></span>

#### <a name="toorun-a-search-using-hello-select-command"></a><span data-ttu-id="14a7a-244">搜尋使用 hello select 命令的 toorun</span><span class="sxs-lookup"><span data-stu-id="14a7a-244">toorun a search using hello select command</span></span>
1. <span data-ttu-id="14a7a-245">在 搜尋 中，輸入 `Type=Event`，然後按一下搜尋。</span><span class="sxs-lookup"><span data-stu-id="14a7a-245">In Search, type `Type=Event` and then click **Search**.</span></span>
2. <span data-ttu-id="14a7a-246">按一下**+ 顯示更多**其中一種 hello 結果 tooview hello 結果的所有 hello 屬性都有。</span><span class="sxs-lookup"><span data-stu-id="14a7a-246">Click **+ show more** in one of hello results tooview all hello properties that hello results have.</span></span>
3. <span data-ttu-id="14a7a-247">選取部分會明確地與 hello 查詢變更太`Type=Event | Select Computer,EventID,RenderedDescription`。</span><span class="sxs-lookup"><span data-stu-id="14a7a-247">Select some of those explicitly, and hello query changes too`Type=Event | Select Computer,EventID,RenderedDescription`.</span></span>  
    <span data-ttu-id="14a7a-248">![搜尋 select](./media/log-analytics-log-searches/oms-search-select.png)</span><span class="sxs-lookup"><span data-stu-id="14a7a-248">![search select](./media/log-analytics-log-searches/oms-search-select.png)</span></span>

<span data-ttu-id="14a7a-249">當您想 toocontrol 搜尋輸出，並選擇對探索，這通常不 hello 完整記錄的 hello 部分真的很重要的資料時，此命令會特別有用。</span><span class="sxs-lookup"><span data-stu-id="14a7a-249">This command is particularly useful when you want toocontrol search output and choose only hello portions of data that really matter for your exploration, which often isn’t hello full record.</span></span> <span data-ttu-id="14a7a-250">當不同類型的記錄有「部分」通用屬性，但不是「所有」屬性都共用時，這也非常有用。</span><span class="sxs-lookup"><span data-stu-id="14a7a-250">This is also useful when records of different types have *some* common properties, but not *all* of their properties are common.</span></span> <span data-ttu-id="14a7a-251">，您可以產生資料表，看起來更自然的輸出，或匯出 tooa CSV 檔案，然後必須在 Excel 中時正常運作。</span><span class="sxs-lookup"><span data-stu-id="14a7a-251">The, you can generate output that looks more naturally like a table, or work well when exported tooa CSV file and then massaged in Excel.</span></span>

## <a name="use-hello-measure-command"></a><span data-ttu-id="14a7a-252">使用 hello measure 命令</span><span class="sxs-lookup"><span data-stu-id="14a7a-252">Use hello measure command</span></span>
<span data-ttu-id="14a7a-253">量值是其中一個 hello 記錄分析搜尋中最具彈性的命令。</span><span class="sxs-lookup"><span data-stu-id="14a7a-253">MEASURE is one of hello most versatile commands in Log Analytics searches.</span></span> <span data-ttu-id="14a7a-254">它可讓您 tooapply 統計*函式*tooyour 資料和彙總的結果依指定的欄位分組。</span><span class="sxs-lookup"><span data-stu-id="14a7a-254">It allows you tooapply statistical *functions* tooyour data and aggregate results grouped by a given field.</span></span> <span data-ttu-id="14a7a-255">Measure 支援多個統計函數。</span><span class="sxs-lookup"><span data-stu-id="14a7a-255">There are multiple statistical functions that Measure supports.</span></span>

### <a name="measure-count"></a><span data-ttu-id="14a7a-256">Measure count()</span><span class="sxs-lookup"><span data-stu-id="14a7a-256">Measure count()</span></span>
<span data-ttu-id="14a7a-257">hello，第一次統計函數 toowork，且其中 hello 簡單 toounderstand hello *count （)*函式。</span><span class="sxs-lookup"><span data-stu-id="14a7a-257">hello first statistical function toowork with, and one of hello simplest toounderstand is hello *count()* function.</span></span>

<span data-ttu-id="14a7a-258">例如，來自任何搜尋查詢結果`Type=Event`，顯示篩選，又稱為 facet 上 hello 搜尋結果的左邊。</span><span class="sxs-lookup"><span data-stu-id="14a7a-258">Results from any search query such as `Type=Event`, show filters also called facets on hello left side of search results.</span></span> <span data-ttu-id="14a7a-259">hello 篩選器會顯示執行 hello 搜尋中所指定 hello 結果欄位值的分佈。</span><span class="sxs-lookup"><span data-stu-id="14a7a-259">hello filters show a distribution of values by a given field for hello results in hello search executed.</span></span>

![搜尋 measure count](./media/log-analytics-log-searches/oms-search-measure-count01.png)

<span data-ttu-id="14a7a-261">例如，在 hello 映像，您會看到 hello**電腦**欄位，它顯示 hello 結果中的 hello 幾乎 739 一千個事件，內有 68 唯一且不同的值為 hello**電腦**那些記錄中的欄位。</span><span class="sxs-lookup"><span data-stu-id="14a7a-261">For example, in hello image above you'll see hello **Computer** field and it shows that within hello almost 739 thousand events in hello results, there are 68 unique and distinct values for hello **Computer** field in those records.</span></span> <span data-ttu-id="14a7a-262">hello 磚只會顯示 hello hello 最常見 5 的值所撰寫的 hello 的前 5 個**電腦**欄位)，依據包含該欄位中的該特定値的文件的 hello 數目來排序。</span><span class="sxs-lookup"><span data-stu-id="14a7a-262">hello tile only shows hello top 5, which are hello most common 5 values that are written in hello **Computer** fields), sorted by hello number of documents that contain that specific value in that field.</span></span> <span data-ttu-id="14a7a-263">Hello 映像中，您可以看到 – 之間幾乎 369 一千個事件 – 90 千位來自 hello OpsInsights04.contoso.com 電腦，83 千從 hello DB03.contoso.com 電腦，依此類推。</span><span class="sxs-lookup"><span data-stu-id="14a7a-263">In hello image you can see that – among those almost 369 thousand events – 90 thousand come from hello OpsInsights04.contoso.com computer, 83 thousand from hello DB03.contoso.com computer, and so on.</span></span>

<span data-ttu-id="14a7a-264">如果您想 toosee 所有值，因為 hello 磚只會顯示只有 hello 前 5 個？</span><span class="sxs-lookup"><span data-stu-id="14a7a-264">What if you want toosee all values, since hello tile only shows only hello top 5?</span></span>

<span data-ttu-id="14a7a-265">這是什麼 hello 量值與 hello count （） 函式可以執行的命令。</span><span class="sxs-lookup"><span data-stu-id="14a7a-265">That’s what hello measure command can do with hello count() function.</span></span> <span data-ttu-id="14a7a-266">此函數不會使用任何參數。</span><span class="sxs-lookup"><span data-stu-id="14a7a-266">This function doesn't use any parameters.</span></span> <span data-ttu-id="14a7a-267">您只需要指定您要 toogroup 由 hello hello 欄位**電腦**欄位在此情況下：</span><span class="sxs-lookup"><span data-stu-id="14a7a-267">You just specify hello field by which you want toogroup by – hello **Computer** field in this case:</span></span>

`Type=Event | Measure count() by Computer`

![搜尋 measure count](./media/log-analytics-log-searches/oms-search-measure-count-computer.png)

<span data-ttu-id="14a7a-269">不過，**Computer** 只是每個資料片段「中」使用的欄位 - 不涉及關聯式資料庫，其他地方也都沒有別的 **Computer** 物件。</span><span class="sxs-lookup"><span data-stu-id="14a7a-269">However, **Computer** is just a field used *in* each piece of data – there are no relational databases involved and there is no separate **Computer** object anywhere.</span></span> <span data-ttu-id="14a7a-270">只要 hello 值*中*hello 可以描述哪個實體產生它們，以及其他一些特性和層面 hello 資料，因此 hello 詞彙*facet*。</span><span class="sxs-lookup"><span data-stu-id="14a7a-270">Just hello values *in* hello data can describe which entity generated them, and a number of other characteristics and aspects of hello data – hence hello term *facet*.</span></span> <span data-ttu-id="14a7a-271">不過，您也可以根據其他欄位分組。</span><span class="sxs-lookup"><span data-stu-id="14a7a-271">However, you can just as well group by other fields.</span></span> <span data-ttu-id="14a7a-272">因為 hello 的輸送到 hello measure 命令的幾乎 739 一千個事件的原始結果也具有名為欄位**EventID**，您可以套用 hello 依據該欄位的相同技巧 toogroup 並取得 by EventID 事件計數：</span><span class="sxs-lookup"><span data-stu-id="14a7a-272">Because hello original results of almost 739 thousand events that are piped into hello measure command also have a field called **EventID**, you can apply hello same technique toogroup by that field and get a count of events by EventID:</span></span>

```
Type=Event | Measure count() by EventID
```

<span data-ttu-id="14a7a-273">如果您不感興趣 hello 實際記錄計數包含特定值，但會改為您只想要的清單 hello 值本身，您可以加入*選取*命令結尾 hello 它，只要選取 hello 第一個資料行：</span><span class="sxs-lookup"><span data-stu-id="14a7a-273">If you're not interested in hello actual record count that contain a specific value, but instead if you only want a list of hello values themselves, you can add a *Select* command at hello end of it and just select hello first column:</span></span>

```
Type=Event | Measure count() by EventID | Select EventID
```

<span data-ttu-id="14a7a-274">然後您可以取得更複雜和預先排序 hello 查詢中的 hello 結果或也您可以只按一下 hello hello 方格中的資料行。</span><span class="sxs-lookup"><span data-stu-id="14a7a-274">Then you can get more intricate and pre-sort hello results in hello query, or you can just click hello columns in hello grid, too.</span></span>

```
Type=Event | Measure count() by EventID | Select EventID | Sort EventID asc
```

#### <a name="toosearch-using-measure-count"></a><span data-ttu-id="14a7a-275">使用 measure count toosearch</span><span class="sxs-lookup"><span data-stu-id="14a7a-275">toosearch using measure count</span></span>
* <span data-ttu-id="14a7a-276">在 hello 搜尋查詢欄位中，輸入`Type=Event | Measure count() by EventID`</span><span class="sxs-lookup"><span data-stu-id="14a7a-276">In hello search query field, type `Type=Event | Measure count() by EventID`</span></span>
* <span data-ttu-id="14a7a-277">附加`| Select EventID`toohello hello 查詢的結尾。</span><span class="sxs-lookup"><span data-stu-id="14a7a-277">Append `| Select EventID` toohello end of hello query.</span></span>
* <span data-ttu-id="14a7a-278">最後，將附加`| Sort EventID asc`toohello hello 查詢的結尾。</span><span class="sxs-lookup"><span data-stu-id="14a7a-278">Finally, append `| Sort EventID asc` toohello end of hello query.</span></span>

<span data-ttu-id="14a7a-279">有幾個要點 toonotice 與強調：</span><span class="sxs-lookup"><span data-stu-id="14a7a-279">There are a couple important points toonotice and emphasize:</span></span>

<span data-ttu-id="14a7a-280">首先，您所看到的 hello 結果不再 hello 未經處理的結果。</span><span class="sxs-lookup"><span data-stu-id="14a7a-280">First, hello results you see are not hello original raw results anymore.</span></span> <span data-ttu-id="14a7a-281">相反地，它們是彙總的結果 – 基本上是結果的群組。</span><span class="sxs-lookup"><span data-stu-id="14a7a-281">Instead, they are aggregated results – essentially groups of results.</span></span> <span data-ttu-id="14a7a-282">這不是問題，但您應該了解您正與非常不同的資料不同的圖形 hello 未經處理的圖形，便會建立 hello 彙總/統計函數結果的 hello 立即進行互動。</span><span class="sxs-lookup"><span data-stu-id="14a7a-282">This isn't a problem, but you should understand that you're interacting with a very different shape of data that differs from hello original raw shape that gets created on hello fly as a result of hello aggregation/statistical function.</span></span>

<span data-ttu-id="14a7a-283">第二個，**測量計數**傳回目前只有 hello 前 100 個不同結果。</span><span class="sxs-lookup"><span data-stu-id="14a7a-283">Second, **Measure count** currently returns only hello top 100 distinct results.</span></span> <span data-ttu-id="14a7a-284">這項限制不適用 toohello 其他統計函數。</span><span class="sxs-lookup"><span data-stu-id="14a7a-284">This limit does not apply toohello other statistical functions.</span></span> <span data-ttu-id="14a7a-285">因此，您通常必須 toouse 更精確的篩選器第一個 toosearch 特定項目然後再套用 measure count （）。</span><span class="sxs-lookup"><span data-stu-id="14a7a-285">So, you'll usually need toouse a more precise filter first toosearch for specific items before you apply measure count().</span></span>

## <a name="use-hello-max-and-min-functions-with-hello-measure-command"></a><span data-ttu-id="14a7a-286">透過 hello measure 命令使用 hello max 和 min 函數</span><span class="sxs-lookup"><span data-stu-id="14a7a-286">Use hello max and min functions with hello measure command</span></span>
<span data-ttu-id="14a7a-287">有 **Measure Max()** 和 **Measure Min()** 在其中很有用的各種案例。</span><span class="sxs-lookup"><span data-stu-id="14a7a-287">There are various scenarios where **Measure Max()** and **Measure Min()** are useful.</span></span> <span data-ttu-id="14a7a-288">不過，由於每個函數彼此相反，我們將說明 Max ()，而您可以自己實驗 Min ()。</span><span class="sxs-lookup"><span data-stu-id="14a7a-288">However, since each function is opposite of each other, we'll illustrate Max() and you can experiment with Min() on your own.</span></span>

<span data-ttu-id="14a7a-289">如果您查詢安全性事件，它們會有不同的**層級**屬性。</span><span class="sxs-lookup"><span data-stu-id="14a7a-289">If you query for security events, they have a **Level** property that can vary.</span></span> <span data-ttu-id="14a7a-290">例如：</span><span class="sxs-lookup"><span data-stu-id="14a7a-290">For example:</span></span>

```
Type=SecurityEvent
```

![搜尋 measure count 開始](./media/log-analytics-log-searches/oms-search-measure-max01.png)

<span data-ttu-id="14a7a-292">如果您要 tooview hello 最大值為 hello 安全性的所有事件指定共用 「 電腦，hello 群組依據 欄位中，您可以使用</span><span class="sxs-lookup"><span data-stu-id="14a7a-292">If you want tooview hello highest value for all of hello security events given a common Computer, hello group by field, you can use</span></span>

```
Type=ConfigurationAlert | Measure Max(Level) by Computer
```

![搜尋 measure max 電腦](./media/log-analytics-log-searches/oms-search-measure-max02.png)

<span data-ttu-id="14a7a-294">它會顯示有 hello 電腦**層級**記錄，其中大部分都有至少層級 8，許多具有 16 個層級。</span><span class="sxs-lookup"><span data-stu-id="14a7a-294">It will display that for hello computers that had **Level** records, most of them have at least level 8, many had a level of 16.</span></span>

```
Type=ConfigurationAlert | Measure Max(Severity) by Computer
```

![搜尋 measure max 時間產生電腦](./media/log-analytics-log-searches/oms-search-measure-max03.png)

<span data-ttu-id="14a7a-296">此函數適用於數字，但它也可以使用日期時間欄位。</span><span class="sxs-lookup"><span data-stu-id="14a7a-296">This function works well with numbers, but it also works with DateTime fields.</span></span> <span data-ttu-id="14a7a-297">它是最後一個元素的 hello 有用 toocheck 或任何資料片段的最新時間戳記編製索引的每台電腦。</span><span class="sxs-lookup"><span data-stu-id="14a7a-297">It is useful toocheck for hello last or most recent time stamp for any piece of data indexed for each computer.</span></span> <span data-ttu-id="14a7a-298">例如： 當 hello 最新的安全性事件報告的每部機器？</span><span class="sxs-lookup"><span data-stu-id="14a7a-298">For example: When was hello most recent security event reported for each machine?</span></span>

```
Type=ConfigurationChange | Measure Max(TimeGenerated) by Computer
```

## <a name="use-hello-avg-function-with-hello-measure-command"></a><span data-ttu-id="14a7a-299">使用 hello measure 命令使用 hello avg 函數</span><span class="sxs-lookup"><span data-stu-id="14a7a-299">Use hello avg function with hello measure command</span></span>
<span data-ttu-id="14a7a-300">hello measure 搭配使用 avg （） 統計函數可讓您 toocalculate hello 平均值某些欄位，以及群組結果 hello 相同或其他欄位。</span><span class="sxs-lookup"><span data-stu-id="14a7a-300">hello Avg() statistical function used with measure allows you toocalculate hello average value for some field, and group results by hello same or other field.</span></span> <span data-ttu-id="14a7a-301">這適用於各種情況，例如效能資料。</span><span class="sxs-lookup"><span data-stu-id="14a7a-301">This is useful in a variety of cases, such as performance data.</span></span>

<span data-ttu-id="14a7a-302">我們將從效能等級開始介紹。</span><span class="sxs-lookup"><span data-stu-id="14a7a-302">We'll start with performance data.</span></span> <span data-ttu-id="14a7a-303">請注意，OMS 目前會收集 Windows 和 Linux 機器的效能計數器。</span><span class="sxs-lookup"><span data-stu-id="14a7a-303">Note that OMS currently collects performance counters for both Windows and Linux machines.</span></span>

<span data-ttu-id="14a7a-304">如 toosearch*所有*效能資料，hello 最基本的查詢如下：</span><span class="sxs-lookup"><span data-stu-id="14a7a-304">toosearch for *all* performance data, hello most basic query is:</span></span>

```
Type=Perf
```

![搜尋 avg 開始](./media/log-analytics-log-searches/oms-search-avg01.png)

<span data-ttu-id="14a7a-306">hello 您會注意到的第一件事是記錄分析會顯示三個檢視方塊： 清單中，它會顯示 hello 圖表; 後面顯示 hello 實際的記錄顯示效能計數器資料; 表格式檢視的資料表並顯示 hello 圖表效能計數器的度量。</span><span class="sxs-lookup"><span data-stu-id="14a7a-306">hello first thing you'll notice is that Log Analytics shows you three perspectives: List, which shows you which shows hello actual records behind hello charts; Table, which shows a tabular view of performance counter data; and Metrics, which shows charts for hello performance counters.</span></span>

<span data-ttu-id="14a7a-307">Hello 在圖中，有兩組標示的欄位，以指出 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="14a7a-307">In hello image above, there are two sets of fields marked that indicate hello following:</span></span>

* <span data-ttu-id="14a7a-308">hello 第一組會識別 Windows 效能計數器名稱、 物件名稱和執行個體名稱中 hello 查詢篩選器。</span><span class="sxs-lookup"><span data-stu-id="14a7a-308">hello first set identifies Windows Performance Counter Name, Object Name, and Instance Name in hello query filter.</span></span> <span data-ttu-id="14a7a-309">這些是您可能會最常用來做為 facet/篩選 hello 欄位</span><span class="sxs-lookup"><span data-stu-id="14a7a-309">These are hello fields you probably will most commonly use as facets/filters</span></span>
* <span data-ttu-id="14a7a-310">**CounterValue**是 hello 的 hello 計數器的實際值。</span><span class="sxs-lookup"><span data-stu-id="14a7a-310">**CounterValue** is hello actual value of hello counter.</span></span> <span data-ttu-id="14a7a-311">在此範例中，hello 值是*75*。</span><span class="sxs-lookup"><span data-stu-id="14a7a-311">In this example, hello value is *75*.</span></span>
* <span data-ttu-id="14a7a-312">**TimeGenerated** 為 12:51，採用 24 小時制的時間格式。</span><span class="sxs-lookup"><span data-stu-id="14a7a-312">**TimeGenerated** is 12:51, in 24-hour time format.</span></span>

<span data-ttu-id="14a7a-313">以下是在圖形中的 hello 度量的檢視。</span><span class="sxs-lookup"><span data-stu-id="14a7a-313">Here's a view of hello metrics in a graph.</span></span>

![搜尋 avg 開始](./media/log-analytics-log-searches/oms-search-avg02.png)

<span data-ttu-id="14a7a-315">了解 hello 效能記錄圖形，並閱讀其他搜尋技術之後, 您可以使用 measure avg （) tooaggregate 這種類型的數值資料。</span><span class="sxs-lookup"><span data-stu-id="14a7a-315">After reading about hello Perf record shape, and having read about other search techniques, you can use measure Avg() tooaggregate this type of numerical data.</span></span>

<span data-ttu-id="14a7a-316">以下是簡單的範例：</span><span class="sxs-lookup"><span data-stu-id="14a7a-316">Here's a simple example:</span></span>

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" | Measure Avg(CounterValue) by Computer
```

![搜尋 avg samplevalue](./media/log-analytics-log-searches/oms-search-avg03.png)

<span data-ttu-id="14a7a-318">在此範例中，您可以選取 hello CPU 時間總計效能計數器和電腦的平均。</span><span class="sxs-lookup"><span data-stu-id="14a7a-318">In this example, you select hello CPU Total Time performance counter and average by Computer.</span></span> <span data-ttu-id="14a7a-319">如果您想 toonarrow 向您的結果 tooonly hello 6 小時，您可以使用 hello 時間篩選控制項，或指定查詢中，如下所示：</span><span class="sxs-lookup"><span data-stu-id="14a7a-319">If you want toonarrow down your results tooonly hello last 6 hours, you can either use hello time filter control or specify in your query as follows:</span></span>

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer
```

### <a name="toosearch-using-hello-avg-function-with-hello-measure-command"></a><span data-ttu-id="14a7a-320">toosearch hello measure 命令使用 hello avg 函數</span><span class="sxs-lookup"><span data-stu-id="14a7a-320">toosearch using hello avg function with hello measure command</span></span>
* <span data-ttu-id="14a7a-321">在 hello 搜尋查詢方塊中，輸入`Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`。</span><span class="sxs-lookup"><span data-stu-id="14a7a-321">In hello Search query box, type `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.</span></span>

<span data-ttu-id="14a7a-322">您可以「跨」  電腦彙總資料，並將其相互關聯。</span><span class="sxs-lookup"><span data-stu-id="14a7a-322">You can aggregate and correlate data *across* computers.</span></span> <span data-ttu-id="14a7a-323">例如，假設您有一組某種伺服器陣列，其中每個節點都是相等的 tooany 中主機的另一個它們剛剛做所有 hello 相同類型的工作和負載也應該大致平衡。</span><span class="sxs-lookup"><span data-stu-id="14a7a-323">For example, imagine that you have a set of hosts in some sort of farm where each node is equal tooany other one and they just do all hello same type of work and load should be roughly balanced.</span></span> <span data-ttu-id="14a7a-324">您可以取得所有在其中一個都將以下列查詢，並取得 hello 整個伺服器陣列的平均 hello 計數器。</span><span class="sxs-lookup"><span data-stu-id="14a7a-324">You could get their counters all in one go with hello following query and get averages for hello entire farm.</span></span> <span data-ttu-id="14a7a-325">您可以選擇以下列範例中的 hello hello 電腦啟動：</span><span class="sxs-lookup"><span data-stu-id="14a7a-325">You can start by choosing hello computers with hello following example:</span></span>

```
Type=Perf AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

<span data-ttu-id="14a7a-326">現在您擁有 hello 電腦，您也只想 tooselect 兩個關鍵效能指標 (Kpi): %cpu 使用量和 %可用磁碟空間。</span><span class="sxs-lookup"><span data-stu-id="14a7a-326">Now that you have hello computers, you also only want tooselect two key performance indicators (KPIs): % CPU Usage and % Free Disk Space.</span></span> <span data-ttu-id="14a7a-327">因此，hello 查詢的該部分會變成：</span><span class="sxs-lookup"><span data-stu-id="14a7a-327">So, that part of hello query becomes:</span></span>

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS
```

<span data-ttu-id="14a7a-328">現在您可以將電腦和計數器加入與下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="14a7a-328">Now you can add computers and counters with hello following example:</span></span>

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

<span data-ttu-id="14a7a-329">因為您有非常明確的選取範圍，hello**測量 avg （）**命令可以傳回 hello 平均不是依電腦，而是跨 hello 伺服陣列中，只要群組依據 CounterName。</span><span class="sxs-lookup"><span data-stu-id="14a7a-329">Because you have a very specific selection, hello **measure Avg()** command can return hello average not by computer, but across hello farm, simply by grouping by CounterName.</span></span> <span data-ttu-id="14a7a-330">例如：</span><span class="sxs-lookup"><span data-stu-id="14a7a-330">For example:</span></span>

```
Type=Perf  InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03") | Measure Avg(CounterValue) by CounterName
```

<span data-ttu-id="14a7a-331">這可提供您數個環境 KPI 的實用精簡檢視。</span><span class="sxs-lookup"><span data-stu-id="14a7a-331">This gives you a useful compact view of a couple of your environment's KPIs.</span></span>

![搜尋 avg grouping](./media/log-analytics-log-searches/oms-search-avg04.png)

<span data-ttu-id="14a7a-333">您可以在儀表板中輕鬆使用 hello 搜尋查詢。</span><span class="sxs-lookup"><span data-stu-id="14a7a-333">You can easily use hello search query in a dashboard.</span></span> <span data-ttu-id="14a7a-334">例如，您無法儲存 hello 搜尋查詢，並從名為它建立儀表板*Web 伺服陣列 Kpi*。</span><span class="sxs-lookup"><span data-stu-id="14a7a-334">For example, you could save hello search query and create a dashboard from it named *Web Farm KPIs*.</span></span> <span data-ttu-id="14a7a-335">toolearn 進一步了解使用儀表板，請參閱[記錄分析中建立自訂的儀表板](log-analytics-dashboards.md)。</span><span class="sxs-lookup"><span data-stu-id="14a7a-335">toolearn more about using dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span></span>

![搜尋 avg 儀表板](./media/log-analytics-log-searches/oms-search-avg05.png)

### <a name="use-hello-sum-function-with-hello-measure-command"></a><span data-ttu-id="14a7a-337">使用 hello measure 命令使用 hello sum 函數</span><span class="sxs-lookup"><span data-stu-id="14a7a-337">Use hello sum function with hello measure command</span></span>
<span data-ttu-id="14a7a-338">hello sum 函式是 hello measure 命令的類似 tooother 函式。</span><span class="sxs-lookup"><span data-stu-id="14a7a-338">hello sum function is similar tooother functions of hello measure command.</span></span> <span data-ttu-id="14a7a-339">您可以看到有關如何 toouse hello sum 函數，在範例[Microsoft Azure Operational Insights 中的 W3C IIS 記錄搜尋](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx)。</span><span class="sxs-lookup"><span data-stu-id="14a7a-339">You can see an example about how toouse hello sum function at [W3C IIS Logs Search in Microsoft Azure Operational Insights](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).</span></span>

<span data-ttu-id="14a7a-340">您可以搭配使用 Max() 和 Min() 與數字、日期時間和文字字串。</span><span class="sxs-lookup"><span data-stu-id="14a7a-340">You can use Max() and Min() with numbers, date times and text strings.</span></span> <span data-ttu-id="14a7a-341">透過文字字串，它們會依字母順序排序，而您會取得第一個和最後一個。</span><span class="sxs-lookup"><span data-stu-id="14a7a-341">With text strings, they are sorted alphabetically and you get first and last.</span></span>

<span data-ttu-id="14a7a-342">不過，您無法搭配使用 Sum() 與數值欄位以外的任何項目。</span><span class="sxs-lookup"><span data-stu-id="14a7a-342">However, you cannot use Sum() with anything other than numerical fields.</span></span> <span data-ttu-id="14a7a-343">這也適用於 tooAvg()。</span><span class="sxs-lookup"><span data-stu-id="14a7a-343">This also applies tooAvg().</span></span>

### <a name="use-hello-percentile-function-with-hello-measure-command"></a><span data-ttu-id="14a7a-344">透過 hello measure 命令使用 hello 百分位數函數</span><span class="sxs-lookup"><span data-stu-id="14a7a-344">Use hello percentile function with hello measure command</span></span>
<span data-ttu-id="14a7a-345">hello 百分位數函式是類似 tooAvg() 和 sum （），您只可以將它用於數值欄位。</span><span class="sxs-lookup"><span data-stu-id="14a7a-345">hello percentile function is similar tooAvg() and Sum() in that you can only use it for numerical fields.</span></span> <span data-ttu-id="14a7a-346">您可以使用任何百分位數的數值欄位 1 too99 之間。</span><span class="sxs-lookup"><span data-stu-id="14a7a-346">You can use any percentile between 1 too99 on a numeric field.</span></span> <span data-ttu-id="14a7a-347">您也可以同時使用 **percentile** 和 **pct** 命令。</span><span class="sxs-lookup"><span data-stu-id="14a7a-347">You can also use both **percentile** and **pct** commands.</span></span> <span data-ttu-id="14a7a-348">以下提供一些範例：</span><span class="sxs-lookup"><span data-stu-id="14a7a-348">Here are few examples:</span></span>  

```
Type:Perf CounterName:"DiskTransers/sec" |measure percentile95(CurrentValue) by Computer
```
```
Type:Perf ObjectName=LogicalDisk CounterName="Current Disk Queue Length" Computer="MyComputerName" | measure pct65(CurrentValue) by InstanceName
```

## <a name="use-hello-where-command"></a><span data-ttu-id="14a7a-349">在命令時使用 hello</span><span class="sxs-lookup"><span data-stu-id="14a7a-349">Use hello where command</span></span>
<span data-ttu-id="14a7a-350">hello 命令的運作方式類似篩選條件，但它可以套用在 hello 管線 toofurther 篩選彙總在 hello 查詢開頭篩選過的相對於的 tooraw 結果由 measure-command-產生的結果。</span><span class="sxs-lookup"><span data-stu-id="14a7a-350">hello where command works like a filter, but it can be applied in hello pipeline toofurther filter aggregated results that have been produced by a Measure command – as opposed tooraw results that are filtered at hello beginning of a query.</span></span>

<span data-ttu-id="14a7a-351">例如：</span><span class="sxs-lookup"><span data-stu-id="14a7a-351">For example:</span></span>

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer
```

<span data-ttu-id="14a7a-352">您可以加入另一個縱線"|"字元和 hello 命令 tooonly 從何處取得的電腦的平均 CPU 高於 80%，與下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="14a7a-352">You can add another pipe "|" character and hello Where command tooonly get computers whose average CPU is above 80%, with hello following example:</span></span>

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer | Where AVGCPU>80
```

<span data-ttu-id="14a7a-353">如果您已熟悉 Microsoft System Center Operations Manager，您可以將 hello 的管理組件詞彙中的命令。</span><span class="sxs-lookup"><span data-stu-id="14a7a-353">If you're familiar with Microsoft System Center - Operations Manager, you can think of hello where command in management pack terms.</span></span> <span data-ttu-id="14a7a-354">如果 hello 範例是一項規則，hello 的 hello 查詢的第一個部分是 hello 資料來源和 hello，命令看起來會 hello 條件偵測。</span><span class="sxs-lookup"><span data-stu-id="14a7a-354">If hello example were a rule, hello first part of hello query would be hello data source and hello where command would be hello condition detection.</span></span>

<span data-ttu-id="14a7a-355">您可以使用 hello 查詢當做一個磚中**我的儀表板**，作為監視器，toosee 時電腦 Cpu 是否過度使用。</span><span class="sxs-lookup"><span data-stu-id="14a7a-355">You can use hello query as a tile in **My Dashboard**, as a monitor of sorts, toosee when computer CPUs are over-utilized.</span></span> <span data-ttu-id="14a7a-356">toolearn 深入了解儀表板，請參閱[記錄分析中建立自訂的儀表板](log-analytics-dashboards.md)。</span><span class="sxs-lookup"><span data-stu-id="14a7a-356">toolearn more about dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span></span> <span data-ttu-id="14a7a-357">您也可以建立和使用儀表板使用 hello 行動裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="14a7a-357">You can also create and use dashboards using hello mobile app.</span></span> <span data-ttu-id="14a7a-358">如需詳細資訊，請參閱 [OMS 行動應用程式 ](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)。</span><span class="sxs-lookup"><span data-stu-id="14a7a-358">For more information, see [OMS Mobile App ](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865).</span></span> <span data-ttu-id="14a7a-359">在 hello 底部兩個磚的 hello 下列映像，您可以看到 hello 監視器顯示清單，表示為數字。</span><span class="sxs-lookup"><span data-stu-id="14a7a-359">In hello bottom two tiles of hello following image, you can see hello monitor displayed a list and as a number.</span></span> <span data-ttu-id="14a7a-360">基本上，您一定想 hello 數字 toobe 零，並且 hello 清單 toobe 空白。</span><span class="sxs-lookup"><span data-stu-id="14a7a-360">Essentially, you always want hello number toobe zero and hello list toobe empty.</span></span> <span data-ttu-id="14a7a-361">否則，它會指出警示條件。</span><span class="sxs-lookup"><span data-stu-id="14a7a-361">Otherwise, it indicates an alert condition.</span></span> <span data-ttu-id="14a7a-362">如有需要您可以使用它 tootake 看看那些電腦不足的壓力。</span><span class="sxs-lookup"><span data-stu-id="14a7a-362">If needed, you can use it tootake a look at which machines are under pressure.</span></span>

![行動儀表板](./media/log-analytics-log-searches/oms-search-mobile.png)

## <a name="use-hello-in-operator"></a><span data-ttu-id="14a7a-364">使用運算子中的 hello</span><span class="sxs-lookup"><span data-stu-id="14a7a-364">Use hello in operator</span></span>
<span data-ttu-id="14a7a-365">hello *IN*運算子，連同*NOT IN*可讓您 toouse 子搜尋，也就是包含另一個搜尋作為引數的搜尋。</span><span class="sxs-lookup"><span data-stu-id="14a7a-365">hello *IN* operator, along with *NOT IN* allows you toouse subsearches, which are searches that include another search as an argument.</span></span> <span data-ttu-id="14a7a-366">它們會以大括號 {} 包含在另一個「主要」或「外部」搜尋內。</span><span class="sxs-lookup"><span data-stu-id="14a7a-366">They are contained in braces {} within another *primary* or *outer* search.</span></span> <span data-ttu-id="14a7a-367">hello 子搜尋的結果，通常是不同結果的清單將做為引數用於其主要搜尋中。</span><span class="sxs-lookup"><span data-stu-id="14a7a-367">hello result of a subsearch, often a list of distinct results, is then used as an argument in its primary search.</span></span>

<span data-ttu-id="14a7a-368">您可以使用子搜尋 toomatch 子集您無法直接在搜尋運算式中，但可從搜尋產生描述您的資料。</span><span class="sxs-lookup"><span data-stu-id="14a7a-368">You can use subsearches toomatch subsets of your data that you cannot describe directly in a search expression, but which can be generated from a search.</span></span> <span data-ttu-id="14a7a-369">例如，如果您想要使用的所有事件的一個搜尋 toofind*缺少安全性更新的電腦*，則您需要 toodesign 子搜尋，先識別*缺少安全性更新的電腦*再尋找事件隸屬 toothose 主機。</span><span class="sxs-lookup"><span data-stu-id="14a7a-369">For example, if you’re interested in using one search toofind all events from *computers missing security updates*, then you need toodesign a subsearch that first identifies that *computers missing security updates* before it finds events belonging toothose hosts.</span></span>

<span data-ttu-id="14a7a-370">因此，您無法表示*電腦目前遺失必要的安全性更新*以 hello 下列查詢：</span><span class="sxs-lookup"><span data-stu-id="14a7a-370">So, you could express *computers currently missing required security updates* with hello following query:</span></span>

```
Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer
```    

![IN 搜尋範例](./media/log-analytics-log-searches/oms-search-in01-revised.png)

<span data-ttu-id="14a7a-372">Hello 清單之後，您可以使用 hello 搜尋作為內部搜尋 toofeed hello 清單中的電腦到外部 （主要） 搜尋會尋找這些電腦的事件。</span><span class="sxs-lookup"><span data-stu-id="14a7a-372">Once you have hello list, you can use hello search as an inner search toofeed hello list of computers into an outer (primary) search that will look for events for those computers.</span></span> <span data-ttu-id="14a7a-373">您以大括號括住 hello 內部搜尋，再饋送其結果作為篩選/欄位使用 hello IN 運算子的 hello 外部搜尋中的可能值。</span><span class="sxs-lookup"><span data-stu-id="14a7a-373">You do this by enclosing hello inner search in braces and feeding its results as possible values for a filter/field in hello outer search using hello IN operator.</span></span> <span data-ttu-id="14a7a-374">hello 查詢會類似如下：</span><span class="sxs-lookup"><span data-stu-id="14a7a-374">hello query would resemble:</span></span>

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer}
```
![IN 搜尋範例](./media/log-analytics-log-searches/oms-search-in02-revised.png)

<span data-ttu-id="14a7a-376">也請注意 hello hello 內部搜尋中使用，因為篩選 hello 系統更新評估所需的時間的所有電腦的快照集每隔 24 小時。</span><span class="sxs-lookup"><span data-stu-id="14a7a-376">Also notice hello time filter used in hello inner search because hello System Update Assessment takes a snapshot of all computers every 24 hours.</span></span> <span data-ttu-id="14a7a-377">您可以藉由只搜尋一天，更輕鬆且精確地進行 hello 內部查詢。</span><span class="sxs-lookup"><span data-stu-id="14a7a-377">You can make hello inner query more lightweight and precise by only searching for a day.</span></span> <span data-ttu-id="14a7a-378">hello 外部搜尋則是透過 hello 時間選取範圍在 hello 使用者介面中，擷取事件 hello 過去 7 天。</span><span class="sxs-lookup"><span data-stu-id="14a7a-378">hello outer search instead uses hello time selection in hello user interface, retrieving events from hello last 7 days.</span></span> <span data-ttu-id="14a7a-379">如需時間運算子的詳細資訊，請參閱 [布林運算子](#boolean-operators) 。</span><span class="sxs-lookup"><span data-stu-id="14a7a-379">See [Boolean operators](#boolean-operators) for more information about time operators.</span></span>

<span data-ttu-id="14a7a-380">因為您實際上只使用 hello hello 做為篩選值的內部搜尋的結果 hello 外部，您仍然可以套用 hello 外部搜尋中的命令。</span><span class="sxs-lookup"><span data-stu-id="14a7a-380">Because you really only use hello results of hello inner search as a filter value for hello outer one, you can still apply commands in hello outer search.</span></span> <span data-ttu-id="14a7a-381">例如，您仍然可以上述事件的另一個 measure 命令的群組 hello:</span><span class="sxs-lookup"><span data-stu-id="14a7a-381">For example, you can still group hello above events with another measure command:</span></span>

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer} | measure count() by Source
```

![IN 搜尋範例](./media/log-analytics-log-searches/oms-search-in03-revised.png)

<span data-ttu-id="14a7a-383">通常，您希望您的內部查詢 tooexecute 快速因為記錄分析服務端逾時，它也 tooreturn 更少結果。</span><span class="sxs-lookup"><span data-stu-id="14a7a-383">Generally, you want your inner query tooexecute quickly because Log Analytics has service-side timeouts for it and also tooreturn a small amount of results.</span></span> <span data-ttu-id="14a7a-384">如果 hello 內部查詢傳回更多結果，hello 結果清單會遭到截斷，而可能導致 hello 外部搜尋 tooreturn 不正確的結果。</span><span class="sxs-lookup"><span data-stu-id="14a7a-384">If hello inner query returns more results, hello result list gets truncated, which could potentially cause hello outer search tooreturn incorrect results.</span></span>

<span data-ttu-id="14a7a-385">另一個規則是該 hello 內部搜尋目前必須 tooprovide*彙總*結果。</span><span class="sxs-lookup"><span data-stu-id="14a7a-385">Another rule is that hello inner search currently needs tooprovide *aggregated* results.</span></span> <span data-ttu-id="14a7a-386">換句話說，它必須包含「measure」  命令；您目前無法將未經處理的結果送到外部搜尋。</span><span class="sxs-lookup"><span data-stu-id="14a7a-386">In other words, it must contain a *measure* command; you cannot currently feed raw results into an outer search.</span></span>

<span data-ttu-id="14a7a-387">此外，可以有只有一個 IN 運算子，而且它必須是 hello hello 查詢中的最後一個篩選條件。</span><span class="sxs-lookup"><span data-stu-id="14a7a-387">Also, there can be only one IN operator and it must be hello last filter in hello query.</span></span> <span data-ttu-id="14a7a-388">多個 IN 運算子不可以是或者，這基本上可防止執行多個子搜尋： hello 重要點是該只有一個子/內部搜尋可能會有每個外部搜尋。</span><span class="sxs-lookup"><span data-stu-id="14a7a-388">Multiple IN operators cannot be OR’d – this essentially prevents running multiple subsearches: hello important point is that only one sub/inner search is possible for each outer search.</span></span>

<span data-ttu-id="14a7a-389">即使有這些限制，IN 可讓許多種類的相互關聯的搜尋和可讓您 toodefine 類似 toogroups，例如電腦、 使用者或檔案-不論 hello 欄位資料中的包含。</span><span class="sxs-lookup"><span data-stu-id="14a7a-389">Even with these limits, IN enables many kinds of correlated searches, and allows you toodefine something similar toogroups such as computers, users, or files – whatever hello fields in your data contain.</span></span> <span data-ttu-id="14a7a-390">以下還有其他範例：</span><span class="sxs-lookup"><span data-stu-id="14a7a-390">Here are more examples:</span></span>

<span data-ttu-id="14a7a-391">**已停用自動更新設定的電腦中遺失的所有更新**</span><span class="sxs-lookup"><span data-stu-id="14a7a-391">**All updates missing from computers where Automatic Update setting is disabled**</span></span>

```
Type=Update UpdateState=Needed Optional=false Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual | measure count() by Computer} | measure count() by KBID
```

<span data-ttu-id="14a7a-392">**執行 SQL Server (即 SQL 評估執行所在) 的電腦中的所有錯誤事件**</span><span class="sxs-lookup"><span data-stu-id="14a7a-392">**All error events from computers running SQL Server (=where SQL Assessment has run)**</span></span>

```
Type=Event EventLevelName=error Computer IN {Type=SQLAssessmentRecommendation | measure count() by Computer}
```

<span data-ttu-id="14a7a-393">**屬於網域控制站 (即 AD 評估執行所在) 的電腦中的所有安全性事件**</span><span class="sxs-lookup"><span data-stu-id="14a7a-393">**All security events from computers that are Domain Controllers (=where AD Assessment has run)**</span></span>

```
Type=SecurityEvent Computer IN { Type=ADAssessmentRecommendation | measure count() by Computer }
```

<span data-ttu-id="14a7a-394">**哪些其他帳戶已登入 toohello 其中與 baconland\jochan 所登入相同的電腦嗎？**</span><span class="sxs-lookup"><span data-stu-id="14a7a-394">**Which other accounts have logged on toohello same computers where account BACONLAND\jochan has logged on?**</span></span>

```
Type=SecurityEvent EventID=4624   Account!="BACONLAND\\jochan" Computer IN { Type=SecurityEvent EventID=4624   Account="BACONLAND\\jochan" | measure count() by Computer } | measure count() by Account
```

## <a name="use-hello-distinct-command"></a><span data-ttu-id="14a7a-395">使用 hello distinct 命令</span><span class="sxs-lookup"><span data-stu-id="14a7a-395">Use hello distinct command</span></span>
<span data-ttu-id="14a7a-396">如 hello 名稱所示，此命令會提供欄位的相異值清單。</span><span class="sxs-lookup"><span data-stu-id="14a7a-396">As hello name suggests, this command provides a list of distinct values for a field.</span></span> <span data-ttu-id="14a7a-397">它出乎意料地簡單，但卻相當實用。</span><span class="sxs-lookup"><span data-stu-id="14a7a-397">It's surprisingly simple but quite useful.</span></span> <span data-ttu-id="14a7a-398">hello 達成相同使用 measure count （） 命令也，如下所示。</span><span class="sxs-lookup"><span data-stu-id="14a7a-398">hello same could be achieved with measure count() command as well, as shown below.</span></span>

```
Type=Event | Measure count() by Computer
```

![DISTINCT 搜尋命令範例](./media/log-analytics-log-searches/oms-search-distinct01-revised.png)

<span data-ttu-id="14a7a-400">不過，如果您感興趣的只是只有相異值，且不 hello 計數為具有之值的文件的清單，然後 DISTINCT 可以提供較為簡潔且更容易 tooread 輸出，以及較短的語法，如下所示。</span><span class="sxs-lookup"><span data-stu-id="14a7a-400">However, if all you're interested in is just a list of distinct values and not hello count of documents that have that values, then DISTINCT can provide cleaner and easier tooread output, and shorter syntax, as shown below.</span></span>

```
Type=Event | Distinct Computer
```
![DISTINCT 搜尋命令範例](./media/log-analytics-log-searches/oms-search-distinct02-revised.png)

## <a name="use-hello-countdistinct-function-with-hello-measure-command"></a><span data-ttu-id="14a7a-402">透過 hello measure 命令使用 hello countdistinct 函數</span><span class="sxs-lookup"><span data-stu-id="14a7a-402">Use hello countdistinct function with hello measure command</span></span>
<span data-ttu-id="14a7a-403">hello countdistinct 函數會計算每個群組內的相異值的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="14a7a-403">hello countdistinct function counts hello number of distinct values within each group.</span></span> <span data-ttu-id="14a7a-404">例如，它可能是使用 toocount hello 唯一回報的電腦數目每一種類型：</span><span class="sxs-lookup"><span data-stu-id="14a7a-404">For example, it could be used toocount hello number of unique computers reporting for each Type:</span></span>

```
* | measure countdistinct(Computer) by Type
```

![OMS-countdistinct](./media/log-analytics-log-searches/oms-countdistinct.png)

## <a name="use-hello-measure-interval-command"></a><span data-ttu-id="14a7a-406">使用 hello measure 間隔命令</span><span class="sxs-lookup"><span data-stu-id="14a7a-406">Use hello measure interval command</span></span>
<span data-ttu-id="14a7a-407">透過接近即時的效能資料收集，您可以在 Log Analytics 中收集和視覺化任何效能計數器。</span><span class="sxs-lookup"><span data-stu-id="14a7a-407">With near real-time performance data collection, you can collect and visualize any performance counter in Log Analytics.</span></span> <span data-ttu-id="14a7a-408">只要輸入 hello 查詢**類型： 效能**會傳回數千個度量 hello 計數器和記錄分析環境中的伺服器數目為基礎的圖形。</span><span class="sxs-lookup"><span data-stu-id="14a7a-408">Simply entering hello query **Type:Perf** will return thousands of metric graphs based on hello number of counters and servers in your Log Analytics environment.</span></span> <span data-ttu-id="14a7a-409">視度量彙總，您可以查看 hello 高的層級，以及深入探討更精細的資料，因為您需要在環境中整體度量。</span><span class="sxs-lookup"><span data-stu-id="14a7a-409">With on-demand metric aggregation, you can look at hello overall metrics in your environment at a high level, and deep dive into more granular data as you need to.</span></span>

<span data-ttu-id="14a7a-410">我們假設您想 tooknow 何謂 hello 平均 CPU 跨所有電腦。</span><span class="sxs-lookup"><span data-stu-id="14a7a-410">Let’s say that you want tooknow what is hello average CPU across all your computers.</span></span> <span data-ttu-id="14a7a-411">查看 hello 的每部電腦的平均 CPU 不可能很有幫助因為結果取得平滑化。toolook 到更多詳細資料，您可以彙總結果中較小的時間視窗區塊，並尋找時間序列跨不同的維度。</span><span class="sxs-lookup"><span data-stu-id="14a7a-411">Looking at hello average CPU for every computer might not be helpful because results may get smoothed out. toolook into more details, you can aggregate your result in a smaller time window chunks, and look into a time series across different dimensions.</span></span> <span data-ttu-id="14a7a-412">例如，您可以執行 hello 每小時的平均 CPU 使用量的所有電腦，如下所示：</span><span class="sxs-lookup"><span data-stu-id="14a7a-412">For example, you can perform hello hourly average of CPU usage across all your computers as follows:</span></span>

```
Type:Perf CounterName="% Processor Time" InstanceName="_Total" | measure avg(CounterValue) by Computer Interval 1HOUR
```

![測量平均間隔](./media/log-analytics-log-searches/oms-measure-avg-interval.png)

<span data-ttu-id="14a7a-414">根據預設，這些結果會顯示在多數列的互動式折線圖中。</span><span class="sxs-lookup"><span data-stu-id="14a7a-414">By default these results will be displayed in a multi-series interactive line chart.</span></span>  <span data-ttu-id="14a7a-415">這個圖表支援數列切換 (透過 y 軸重新調整)、縮放和暫留。</span><span class="sxs-lookup"><span data-stu-id="14a7a-415">This chart supports series toggling (with y-axis rescaling), zooming, and hovering.</span></span>  <span data-ttu-id="14a7a-416">hello 資料表顯示選項是仍然可供檢視 hello 未經處理資料，如有必要的。</span><span class="sxs-lookup"><span data-stu-id="14a7a-416">hello table display option is still available for viewing hello raw data if necessary.</span></span>

<span data-ttu-id="14a7a-417">您也可以根據其他欄位分組。</span><span class="sxs-lookup"><span data-stu-id="14a7a-417">You can also group by other fields.</span></span> <span data-ttu-id="14a7a-418">在此範例中，我要在一部特定電腦的所有 hello %計數器，我想 tooknow 何謂 hello 的每個計數器每小時 70 百分位數：</span><span class="sxs-lookup"><span data-stu-id="14a7a-418">In this example, I am looking at all hello % counters for one specific computer, and I want tooknow what is hello hourly 70 percentiles of every counter:</span></span>

```
Type:Perf Computer=beefpatty4 CounterName=%* InstanceName=_Total | measure percentile70(CounterValue) by CounterName Interval 1HOUR
```
<span data-ttu-id="14a7a-419">一件事 toonote 是，這些查詢不會限制的 tooperformance 計數器。</span><span class="sxs-lookup"><span data-stu-id="14a7a-419">One thing toonote is that these queries are not limited tooperformance counters.</span></span> <span data-ttu-id="14a7a-420">您可以套用它們 tooany 度量。</span><span class="sxs-lookup"><span data-stu-id="14a7a-420">You can apply them tooany metric.</span></span> <span data-ttu-id="14a7a-421">在此範例中，我要查看 W3C IIS 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="14a7a-421">In this example, I’m looking at W3C IIS logs.</span></span> <span data-ttu-id="14a7a-422">我想 tooknow 何謂 hello 處理每個要求的 5 分鐘間隔內所需的最大時間：</span><span class="sxs-lookup"><span data-stu-id="14a7a-422">I want tooknow what is hello maximum time it takes over a 5-minute interval for processing each request:</span></span>

```
Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES
```

### <a name="use-multiple-aggregates-in-one-query"></a><span data-ttu-id="14a7a-423">在單一查詢中使用多個彙總</span><span class="sxs-lookup"><span data-stu-id="14a7a-423">Use multiple aggregates in one query</span></span>
<span data-ttu-id="14a7a-424">您可以在 measure 命令中指定多個彙總子句。</span><span class="sxs-lookup"><span data-stu-id="14a7a-424">You can specify multiple aggregate clauses in a measure command.</span></span>  <span data-ttu-id="14a7a-425">每個子句皆可獨立給予別名。</span><span class="sxs-lookup"><span data-stu-id="14a7a-425">Each one can be aliased independently.</span></span>  <span data-ttu-id="14a7a-426">如果未指定別名 hello 產生欄位名稱就是所用的 hello 彙總函式 (也就是 「 avg(CounterValue)"avg(CounterValue)) 的。</span><span class="sxs-lookup"><span data-stu-id="14a7a-426">If it is not given an alias hello resulting field name will be hello aggregate function that was used (i.e. "avg(CounterValue)" for avg(CounterValue)).</span></span>

 ```
Type=WireData | measure avg(ReceivedBytes), avg(SentBytes) by Direction interval 1hour
```
![OMS-multiaggregates1](./media/log-analytics-log-searches/oms-multiaggregates1.png)

<span data-ttu-id="14a7a-428">以下是另一個範例︰</span><span class="sxs-lookup"><span data-stu-id="14a7a-428">Here is another example:</span></span>

 ```
* | measure countdistinct(Computer) as Computers, count() as TotalRecords by Type
```


## <a name="next-steps"></a><span data-ttu-id="14a7a-429">後續步驟</span><span class="sxs-lookup"><span data-stu-id="14a7a-429">Next steps</span></span>
<span data-ttu-id="14a7a-430">如需關於記錄檔搜尋的其他資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="14a7a-430">For additional information about log searches, see:</span></span>

* <span data-ttu-id="14a7a-431">使用[自訂欄位中記錄分析](log-analytics-custom-fields.md)tooextend 記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="14a7a-431">Use [Custom fields in Log Analytics](log-analytics-custom-fields.md) tooextend log searches.</span></span>
* <span data-ttu-id="14a7a-432">檢閱 hello[記錄分析記錄搜尋參考](log-analytics-search-reference.md)tooview hello 的所有搜尋欄位和 facet 用於記錄分析。</span><span class="sxs-lookup"><span data-stu-id="14a7a-432">Review hello [Log Analytics log search reference](log-analytics-search-reference.md) tooview all of hello search fields and facets available in Log Analytics.</span></span>
