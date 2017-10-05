---
title: "使用 Azure Log Analytics 中的記錄檔搜尋來尋找資料 | Microsoft Docs"
description: "記錄檔搜尋可讓您結合和相互關聯您環境內多個來源的任何電腦資料。"
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
ms.openlocfilehash: bf237a837297cb8f1ab3a3340139133adcd2b244
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="find-data-using-log-searches-in-log-analytics"></a><span data-ttu-id="32ca6-103">在 Log Analytics 中使用記錄搜尋以尋找資料</span><span class="sxs-lookup"><span data-stu-id="32ca6-103">Find data using log searches in Log Analytics</span></span>

>[!NOTE]
> <span data-ttu-id="32ca6-104">本文說明在 Azure Log Analytics 中使用目前查詢語言的記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="32ca6-104">This article describes log searches using the current query language in Log Analytics.</span></span>  <span data-ttu-id="32ca6-105">如果您的工作區已升級為[新的 Log Analytics 查詢語言](log-analytics-log-search-upgrade.md)，則您應該參閱[了解 Log Analytics 中的記錄搜尋 (新)](log-analytics-log-search-new.md)。</span><span class="sxs-lookup"><span data-stu-id="32ca6-105">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should refer to [Understanding log searches in Log Analytics (new)](log-analytics-log-search-new.md).</span></span>


<span data-ttu-id="32ca6-106">Log Analytics 的核心是記錄檔搜尋功能，可讓您結合和相互關聯您環境內多個來源的任何電腦資料。</span><span class="sxs-lookup"><span data-stu-id="32ca6-106">At the core of Log Analytics is the log search feature which allows you to combine and correlate any machine data from multiple sources within your environment.</span></span> <span data-ttu-id="32ca6-107">解決方案也是由記錄搜尋發動，可讓您針對特定問題領域進行度量。</span><span class="sxs-lookup"><span data-stu-id="32ca6-107">Solutions are also powered by log search to bring you metrics pivoted around a particular problem area.</span></span>

<span data-ttu-id="32ca6-108">在 [搜尋] 頁面上，您可以建立查詢，然後在搜尋時，您可以使用 Facet 控制篩選結果。</span><span class="sxs-lookup"><span data-stu-id="32ca6-108">On the Search page, you can create a query, and then when you search, you can filter the results by using facet controls.</span></span> <span data-ttu-id="32ca6-109">您也可以建立進階查詢來轉換、篩選和報告結果。</span><span class="sxs-lookup"><span data-stu-id="32ca6-109">You can also create advanced queries to transform, filter, and report on your results.</span></span>

<span data-ttu-id="32ca6-110">常見的記錄搜尋查詢會出現在大部分解決方案頁面中。</span><span class="sxs-lookup"><span data-stu-id="32ca6-110">Common log search queries appear on most solution pages.</span></span> <span data-ttu-id="32ca6-111">在整個 OMS 主控台中，您可以按一下圖格或向內切入其他項目，使用 [記錄檔搜尋] 來檢視項目的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="32ca6-111">Throughout the OMS console, you can click tiles or drill in to other items to view details about the item by using log search.</span></span>

<span data-ttu-id="32ca6-112">在本教學課程中，我們將逐步解說範例，以涵蓋您使用記錄搜尋時的所有基本項目。</span><span class="sxs-lookup"><span data-stu-id="32ca6-112">In this tutorial, we'll walk through examples to cover all the basics when you use log search.</span></span>

<span data-ttu-id="32ca6-113">我們會以簡單、實用的範例開頭，然後根據這些範例進一步說明，讓您可以了解實際的使用案例，了解如何使用語法從資料擷取您想要的觀點。</span><span class="sxs-lookup"><span data-stu-id="32ca6-113">We'll start with simple, practical examples and then build on them so that you can get an understanding of practical use cases about how to use the syntax to extract the insights you want from the data.</span></span>

<span data-ttu-id="32ca6-114">在熟悉搜尋技術之後，您可以檢閱 [Log Analytics 記錄檔搜尋參考資料](log-analytics-search-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="32ca6-114">After you've familiar with search techniques, you can review the [Log Analytics log search reference](log-analytics-search-reference.md).</span></span>

## <a name="use-basic-filters"></a><span data-ttu-id="32ca6-115">使用基本篩選器</span><span class="sxs-lookup"><span data-stu-id="32ca6-115">Use basic filters</span></span>
<span data-ttu-id="32ca6-116">首先要知道的事情是搜尋查詢的第一個部分，在任何 "|" 分隔號字元之前，一律為「篩選器」 。</span><span class="sxs-lookup"><span data-stu-id="32ca6-116">The first thing to know is that the first part of a search query, before any "|" vertical pipe character, is always a *filter*.</span></span> <span data-ttu-id="32ca6-117">您可以將它當做 TSQL 中的 WHERE 子句--它會判斷要從 OMS 資料存放區提取「哪個」  資料子集。</span><span class="sxs-lookup"><span data-stu-id="32ca6-117">You can think of it as a WHERE clause in TSQL--it determines *what* subset of data to pull out of the OMS data store.</span></span> <span data-ttu-id="32ca6-118">在資料存放區中搜尋主要是有關指定您想要擷取的資料特性，因此查詢會很自然地以 WHERE 子句開頭。</span><span class="sxs-lookup"><span data-stu-id="32ca6-118">Searching in the data store is largely about specifying the characteristics of the data that you want to extract, so it is natural that a query would start with the WHERE clause.</span></span>

<span data-ttu-id="32ca6-119">您可以使用之最基本的篩選器為「關鍵字」 ，例如 'error' 或 'timeout' 或電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="32ca6-119">The most basic filters you can use are *keywords*, such as ‘error’ or ‘timeout’, or a computer name.</span></span> <span data-ttu-id="32ca6-120">這些簡單的查詢類型通常會在相同的結果集內傳回各種資料圖形。</span><span class="sxs-lookup"><span data-stu-id="32ca6-120">These types of simple queries generally return diverse shapes of data within the same result set.</span></span> <span data-ttu-id="32ca6-121">這是因為 Log Analytics 在系統中有不同「類型」  的資料。</span><span class="sxs-lookup"><span data-stu-id="32ca6-121">This is because Log Analytics has different *types* of data in the system.</span></span>

### <a name="to-conduct-a-simple-search"></a><span data-ttu-id="32ca6-122">進行簡單搜尋</span><span class="sxs-lookup"><span data-stu-id="32ca6-122">To conduct a simple search</span></span>
1. <span data-ttu-id="32ca6-123">在 OMS 入口網站中，按一下 [記錄檔搜尋] 。</span><span class="sxs-lookup"><span data-stu-id="32ca6-123">In the OMS portal, click **Log Search**.</span></span>  
    <span data-ttu-id="32ca6-124">![搜尋圖格](./media/log-analytics-log-searches/oms-overview-log-search.png)</span><span class="sxs-lookup"><span data-stu-id="32ca6-124">![search tile](./media/log-analytics-log-searches/oms-overview-log-search.png)</span></span>
2. <span data-ttu-id="32ca6-125">在查詢欄位中，輸入 `error`，然後按一下 [搜尋]。</span><span class="sxs-lookup"><span data-stu-id="32ca6-125">In the query field, type `error` and then click **Search**.</span></span>  
    <span data-ttu-id="32ca6-126">![搜尋錯誤](./media/log-analytics-log-searches/oms-search-error.png)</span><span class="sxs-lookup"><span data-stu-id="32ca6-126">![search error](./media/log-analytics-log-searches/oms-search-error.png)</span></span>  
    <span data-ttu-id="32ca6-127">例如，在下圖中，查詢 `error` 會傳回 100,000 個 **Event** 記錄 (由記錄檔管理所收集)、18 個 **ConfigurationAlert** 記錄 (由組態評估所產生)，以及 12 個 **ConfigurationChange** 記錄 (由變更追蹤所擷取)。</span><span class="sxs-lookup"><span data-stu-id="32ca6-127">For example, the query for `error` in the following image returned 100,000 **Event** records (collected by Log Management), 18 **ConfigurationAlert** records (generated by Configuration Assessment) and 12 **ConfigurationChange** records (captured by the Change Tracking).</span></span>   
    <span data-ttu-id="32ca6-128">![搜尋結果](./media/log-analytics-log-searches/oms-search-results01.png)</span><span class="sxs-lookup"><span data-stu-id="32ca6-128">![search results](./media/log-analytics-log-searches/oms-search-results01.png)</span></span>  

<span data-ttu-id="32ca6-129">這些篩選器不一定是物件類型/類別。</span><span class="sxs-lookup"><span data-stu-id="32ca6-129">These filters are not really object types/classes.</span></span> <span data-ttu-id="32ca6-130"> 只是附加到資料片段的標記或屬性，或字串/名稱/類別。</span><span class="sxs-lookup"><span data-stu-id="32ca6-130">*Type* is just a tag, or a property, or a string/name/category, that is attached to a piece of data.</span></span> <span data-ttu-id="32ca6-131">系統中的某些文件會標記為 **Type:ConfigurationAlert**，而某些會標記為 **Type:Perf** 或 **Type:Event** 等等。</span><span class="sxs-lookup"><span data-stu-id="32ca6-131">Some documents in the system are tagged as **Type:ConfigurationAlert** and some are tagged as **Type:Perf**, or **Type:Event**, and so on.</span></span> <span data-ttu-id="32ca6-132">每個搜尋結果、文件、記錄或項目都會顯示所有未經處理的屬性及它們針對每個資料片段的値，當您只想擷取欄位在其中具有指定値的記錄時，您可以在篩選器中使用那些欄位名稱來指定。</span><span class="sxs-lookup"><span data-stu-id="32ca6-132">Each search result, document, record, or entry displays all the raw properties and their values for each of those pieces of data, and you can use those field names to specify in the filter when you want to retrieve only the records where the field has that given value.</span></span>

<span data-ttu-id="32ca6-133">「類型」其實只是所有記錄都有的欄位，與任何其他欄位並沒有不同。</span><span class="sxs-lookup"><span data-stu-id="32ca6-133">*Type* is really just a field that all records have, it is not different from any other field.</span></span> <span data-ttu-id="32ca6-134">這是根據 [類型] 欄位的值所建立的。</span><span class="sxs-lookup"><span data-stu-id="32ca6-134">This was established based on the value of the Type field.</span></span> <span data-ttu-id="32ca6-135">該記錄會有不同的圖形或形式。</span><span class="sxs-lookup"><span data-stu-id="32ca6-135">That record will have a different shape or form.</span></span> <span data-ttu-id="32ca6-136">順帶一提，**Type=Perf** 或 **Type=Event** 也是您需要了解以查詢效能資料或事件的語法。</span><span class="sxs-lookup"><span data-stu-id="32ca6-136">Incidentally, **Type=Perf**, or **Type=Event** is also the syntax that you need to learn to query for performance data or events.</span></span>

<span data-ttu-id="32ca6-137">您可以在欄位名稱之後和值之前使用冒號 (:) 或等號 (=)。</span><span class="sxs-lookup"><span data-stu-id="32ca6-137">You can use either a colon (:) or an equal sign (=) after the field name and before the value.</span></span> <span data-ttu-id="32ca6-138">**Type:Event** and **Type=Event** 在意義上是相等的，您可以選擇您偏好的樣式。</span><span class="sxs-lookup"><span data-stu-id="32ca6-138">**Type:Event** and **Type=Event** are equivalent in meaning, you can choose the style you prefer.</span></span>

<span data-ttu-id="32ca6-139">因此，如果 Type=Perf 記錄具有名為 'CounterName' 的欄位，您就可以撰寫類似於 `Type=Perf CounterName="% Processor Time"`的查詢。</span><span class="sxs-lookup"><span data-stu-id="32ca6-139">So, if the Type=Perf records have a field called 'CounterName', then you can write a query resembling `Type=Perf CounterName="% Processor Time"`.</span></span>

<span data-ttu-id="32ca6-140">如此可以只提供您效能資料，其中的效能計數器名稱是"%Processor Time"。</span><span class="sxs-lookup"><span data-stu-id="32ca6-140">This will give you only the performance data where the performance counter name is "% Processor Time".</span></span>

### <a name="to-search-for-processor-time-performance-data"></a><span data-ttu-id="32ca6-141">搜尋處理器時間效能資料</span><span class="sxs-lookup"><span data-stu-id="32ca6-141">To search for processor time performance data</span></span>
* <span data-ttu-id="32ca6-142">在搜尋查詢欄位中，輸入 `Type=Perf CounterName="% Processor Time"`</span><span class="sxs-lookup"><span data-stu-id="32ca6-142">In the search query field, type `Type=Perf CounterName="% Processor Time"`</span></span>

<span data-ttu-id="32ca6-143">您也可以更明確地在查詢中使用 **InstanceName=_'Total'**，此為 Windows 效能計數器。</span><span class="sxs-lookup"><span data-stu-id="32ca6-143">You can also be more specific and use **InstanceName=_'Total'** in the query, which is a Windows performance counter.</span></span> <span data-ttu-id="32ca6-144">您也可以選取 facet 和另一個 **field:value**。</span><span class="sxs-lookup"><span data-stu-id="32ca6-144">You can also select a facet and another **field:value**.</span></span> <span data-ttu-id="32ca6-145">篩選器會自動加入至查詢列的篩選器中。</span><span class="sxs-lookup"><span data-stu-id="32ca6-145">The filter is automatically added to your filter in the query bar.</span></span> <span data-ttu-id="32ca6-146">您可以在下列映像中看到此情況。</span><span class="sxs-lookup"><span data-stu-id="32ca6-146">You can see this in the following image.</span></span> <span data-ttu-id="32ca6-147">其中向您顯示在哪裡按一下，以將 **InstanceName:’_Total’** 新增至查詢，而不需要輸入任何項目。</span><span class="sxs-lookup"><span data-stu-id="32ca6-147">It shows you where to click to add **InstanceName:’_Total’** to the query without typing anything.</span></span>

![搜尋 facet](./media/log-analytics-log-searches/oms-search-facet.png)

<span data-ttu-id="32ca6-149">您的查詢現在已成為 `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`</span><span class="sxs-lookup"><span data-stu-id="32ca6-149">Your query now becomes `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`</span></span>

<span data-ttu-id="32ca6-150">在此範例中，您不必指定 **Type=Perf** 來取得這個結果。</span><span class="sxs-lookup"><span data-stu-id="32ca6-150">In this example, you don't have to specify **Type=Perf** to get to this result.</span></span> <span data-ttu-id="32ca6-151">因為 CounterName 和 InstanceName 欄位只會為 Type=Perf 的記錄而存在，所以特定的查詢會傳回的結果和先前較長的結果相同：</span><span class="sxs-lookup"><span data-stu-id="32ca6-151">Because the fields CounterName and InstanceName only exist for records of Type=Perf, the query is specific enough to return the same results as the longer, previous one:</span></span>

```
CounterName="% Processor Time" InstanceName="_Total"
```

<span data-ttu-id="32ca6-152">這是因為查詢中的所有篩選器都會彼此評估為「AND」  。</span><span class="sxs-lookup"><span data-stu-id="32ca6-152">This is because all the filters in the query are evaluated as being in *AND* with each other.</span></span> <span data-ttu-id="32ca6-153">事實上，您將愈多欄位加入至準則，您得到的更特定且精緻的結果愈少。</span><span class="sxs-lookup"><span data-stu-id="32ca6-153">Effectively, the more fields you add to the criteria, you get less, more specific and refined results.</span></span>

<span data-ttu-id="32ca6-154">例如，查詢 `Type=Event EventLog="Windows PowerShell"` 等同於 `Type=Event AND EventLog="Windows PowerShell"`。</span><span class="sxs-lookup"><span data-stu-id="32ca6-154">For example, the query `Type=Event EventLog="Windows PowerShell"` is identical to `Type=Event AND EventLog="Windows PowerShell"`.</span></span> <span data-ttu-id="32ca6-155">它會傳回記錄於 Windows PowerShell 事件記錄檔中以及從該事件記錄檔收集到的所有事件。</span><span class="sxs-lookup"><span data-stu-id="32ca6-155">It returns all events that were logged in and collected from the Windows PowerShell event log.</span></span> <span data-ttu-id="32ca6-156">如果您藉由重複選取相同的 facet 以多次加入篩選器，此問題會相當明確--它可能會干擾 [搜尋] 列，但它仍會傳回相同的結果，因為隱含 AND 運算子一律都會在其中。</span><span class="sxs-lookup"><span data-stu-id="32ca6-156">If you add a filter multiple times by repeatedly selecting the same facet, then the issue is purely cosmetic--it might clutter the Search bar, but it still returns the same results because the implicit AND operator is always there.</span></span>

<span data-ttu-id="32ca6-157">您可以藉由明確使用 NOT 運算子，輕鬆地反轉隱含 AND 運算子。</span><span class="sxs-lookup"><span data-stu-id="32ca6-157">You can easily reverse the implicit AND operator by using a NOT operator explicitly.</span></span> <span data-ttu-id="32ca6-158">例如：</span><span class="sxs-lookup"><span data-stu-id="32ca6-158">For example:</span></span>

<span data-ttu-id="32ca6-159">`Type:Event NOT(EventLog:"Windows PowerShell")` 或其相等的 `Type=Event EventLog!="Windows PowerShell"` 會從「不是」Windows PowerShell 記錄檔的所有其他記錄檔傳回所有事件。</span><span class="sxs-lookup"><span data-stu-id="32ca6-159">`Type:Event NOT(EventLog:"Windows PowerShell")` or its equivalent `Type=Event EventLog!="Windows PowerShell"` return all events from all other logs that are NOT the Windows PowerShell log.</span></span>

<span data-ttu-id="32ca6-160">或者，您可以使用其他布林運算子，例如 'OR'。</span><span class="sxs-lookup"><span data-stu-id="32ca6-160">Or, you can use other Boolean operator such as ‘OR’.</span></span> <span data-ttu-id="32ca6-161">下列查詢會傳回 EventLog 為應用程式或系統的記錄。</span><span class="sxs-lookup"><span data-stu-id="32ca6-161">The following query returns records for which the EventLog is either Application OR System.</span></span>

```
EventLog=Application OR EventLog=System
```

<span data-ttu-id="32ca6-162">使用上述查詢，您會在相同的結果集中取得兩個記錄的項目。</span><span class="sxs-lookup"><span data-stu-id="32ca6-162">Using the above query, you’ll get entries for both logs in the same result set.</span></span>

<span data-ttu-id="32ca6-163">不過，如果您藉由保留隱含 AND 以移除 OR，下列查詢就不會產生任何結果，因為沒有屬於這兩個記錄的事件記錄項目。</span><span class="sxs-lookup"><span data-stu-id="32ca6-163">However, if you remove the OR by leaving the implicit AND in place, then the following query will not produce any results because there isn’t an event log entry that belongs to BOTH logs.</span></span> <span data-ttu-id="32ca6-164">每個事件記錄項目只會寫入至兩個記錄之一。</span><span class="sxs-lookup"><span data-stu-id="32ca6-164">Each event log entry was written to only one of the two logs.</span></span>

```
EventLog=Application EventLog=System
```


## <a name="use-additional-filters"></a><span data-ttu-id="32ca6-165">使用其他篩選器</span><span class="sxs-lookup"><span data-stu-id="32ca6-165">Use additional filters</span></span>
<span data-ttu-id="32ca6-166">下列查詢會傳回已傳送資料的所有電腦的 2 個事件記錄的項目。</span><span class="sxs-lookup"><span data-stu-id="32ca6-166">The following query returns entries for 2 event logs for all the computers that have sent data.</span></span>

```
EventLog=Application OR EventLog=System
```

![搜尋結果](./media/log-analytics-log-searches/oms-search-results03.png)

<span data-ttu-id="32ca6-168">選取其中一個欄位或篩選器會縮小查詢範圍到特定的電腦，並排除所有其他電腦。</span><span class="sxs-lookup"><span data-stu-id="32ca6-168">Selecting one of the fields or filters will narrow the query to a specific computer, excluding all other ones.</span></span> <span data-ttu-id="32ca6-169">產生的查詢如下所示。</span><span class="sxs-lookup"><span data-stu-id="32ca6-169">The resulting query would resemble the following.</span></span>

```
EventLog=Application OR EventLog=System Computer=SERVER1.contoso.com
```

<span data-ttu-id="32ca6-170">因為隱含 AND 的緣故，這相當於下列內容。</span><span class="sxs-lookup"><span data-stu-id="32ca6-170">Which is equivalent to the following, because of the implicit AND.</span></span>

```
EventLog=Application OR EventLog=System AND Computer=SERVER1.contoso.com
```

<span data-ttu-id="32ca6-171">每個查詢都會以下列明確的順序進行評估。</span><span class="sxs-lookup"><span data-stu-id="32ca6-171">Each query is evaluated in the following explicit order.</span></span> <span data-ttu-id="32ca6-172">請注意括號。</span><span class="sxs-lookup"><span data-stu-id="32ca6-172">Note the parenthesis.</span></span>

```
(EventLog=Application OR EventLog=System) AND Computer=SERVER1.contoso.com
```

<span data-ttu-id="32ca6-173">就像事件記錄欄位一般，您可以藉由新增 OR，即可只擷取一組特定電腦的資料。</span><span class="sxs-lookup"><span data-stu-id="32ca6-173">Just like the event log field, you can retrieve data only for a set of specific computers by adding OR.</span></span> <span data-ttu-id="32ca6-174">例如：</span><span class="sxs-lookup"><span data-stu-id="32ca6-174">For example:</span></span>

```
(EventLog=Application OR EventLog=System) AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com OR Computer=SERVER3.contoso.com)
```

<span data-ttu-id="32ca6-175">同樣地，下列查詢只會傳回已選取之兩部電腦的 **% CPU 時間** 。</span><span class="sxs-lookup"><span data-stu-id="32ca6-175">Similarly, this the following query return **% CPU Time** for the selected two computers only.</span></span>

```
CounterName="% Processor Time"  AND InstanceName="_Total" AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com)
```

### <a name="field-types"></a><span data-ttu-id="32ca6-176">欄位類型</span><span class="sxs-lookup"><span data-stu-id="32ca6-176">Field types</span></span>
<span data-ttu-id="32ca6-177">建立篩選時，您應該了解使用記錄搜尋所傳回之不同欄位類型的差異。</span><span class="sxs-lookup"><span data-stu-id="32ca6-177">When creating filters, you should understand the differences in working with different types of fields returned by log searches.</span></span>

<span data-ttu-id="32ca6-178">**可搜尋的欄位**會在搜尋結果中以藍色顯示。</span><span class="sxs-lookup"><span data-stu-id="32ca6-178">**Searchable fields** show in blue in search results.</span></span>  <span data-ttu-id="32ca6-179">您可以在欄位特定搜尋條件中使用可搜尋的欄位，如下所示：</span><span class="sxs-lookup"><span data-stu-id="32ca6-179">You can use searchable fields in search conditions specific to the field such as the following:</span></span>

```
Type: Event EventLevelName: "Error"
Type: SecurityEvent Computer:Contains("contoso.com")
Type: Event EventLevelName IN {"Error","Warning"}
```

<span data-ttu-id="32ca6-180">**自然語言檢索搜尋旗標欄位**會在搜尋結果中以灰色顯示。</span><span class="sxs-lookup"><span data-stu-id="32ca6-180">**Free text searchable fields** are shown in grey in search results.</span></span>  <span data-ttu-id="32ca6-181">這些欄位無法像是可搜尋的欄位一樣搭配欄位特定搜尋條件使用。</span><span class="sxs-lookup"><span data-stu-id="32ca6-181">They cannot be used with search conditions specific to the field like searchable fields.</span></span>  <span data-ttu-id="32ca6-182">只有在跨所有欄位執行查詢時才能進行搜尋，如下所示。</span><span class="sxs-lookup"><span data-stu-id="32ca6-182">They are only searched when performing a query across all fields such as the following.</span></span>

```
"Error"
Type: Event "Exception"
```


### <a name="boolean-operators"></a><span data-ttu-id="32ca6-183">布林運算子</span><span class="sxs-lookup"><span data-stu-id="32ca6-183">Boolean operators</span></span>
<span data-ttu-id="32ca6-184">在日期時間和數字欄位中，您可以使用「大於」、「小於」和「小於或等於」來搜尋值。</span><span class="sxs-lookup"><span data-stu-id="32ca6-184">With datetime and numeric fields, you can search for values using *greater than*, *lesser than*, and *lesser than or equal*.</span></span> <span data-ttu-id="32ca6-185">您可以使用簡單的運算子，例如查詢搜尋列中的 >、<、>=、<=、!=。</span><span class="sxs-lookup"><span data-stu-id="32ca6-185">You can use simple operators such as >, < , >=, <= , != in the query search bar.</span></span>

<span data-ttu-id="32ca6-186">您可以查詢特定一段時間的特定事件記錄。</span><span class="sxs-lookup"><span data-stu-id="32ca6-186">You can query a specific event log for a specific period of time.</span></span> <span data-ttu-id="32ca6-187">例如，過去 24 小時會使用下列助憶鍵運算式表示。</span><span class="sxs-lookup"><span data-stu-id="32ca6-187">For example, the last 24 hours is expressed with the following mnemonic expression.</span></span>

```
EventLog=System TimeGenerated>NOW-24HOURS
```


#### <a name="to-search-using-a-boolean-operator"></a><span data-ttu-id="32ca6-188">使用布林運算子來搜尋</span><span class="sxs-lookup"><span data-stu-id="32ca6-188">To search using a boolean operator</span></span>
* <span data-ttu-id="32ca6-189">在搜尋查詢欄位中，輸入 `EventLog=System TimeGenerated>NOW-24HOURS`</span><span class="sxs-lookup"><span data-stu-id="32ca6-189">In the search query field, type `EventLog=System TimeGenerated>NOW-24HOURS`</span></span>  
    <span data-ttu-id="32ca6-190">![使用布林值來搜尋](./media/log-analytics-log-searches/oms-search-boolean.png)</span><span class="sxs-lookup"><span data-stu-id="32ca6-190">![search with boolean](./media/log-analytics-log-searches/oms-search-boolean.png)</span></span>

<span data-ttu-id="32ca6-191">雖然您可以以圖形方式控制時間間隔，而且大多數時候您可能會想這麼做，但是將時間篩選器直接包含在查詢中還是有其優點。</span><span class="sxs-lookup"><span data-stu-id="32ca6-191">Although you can control the time interval graphically, and most times you might want to do that, there are advantages to including a time filter directly into the query.</span></span> <span data-ttu-id="32ca6-192">例如，這非常適合儀表板，無論儀表板頁面上的「全域」  時間選取器為何，您都可以在其中覆寫每個磚的時間。</span><span class="sxs-lookup"><span data-stu-id="32ca6-192">For example, this works great with dashboards where you can override the time for each tile, regardless of the *global* time selector on the dashboard page.</span></span> <span data-ttu-id="32ca6-193">如需詳細資訊，請參閱 [時間對儀表板很重要](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/)。</span><span class="sxs-lookup"><span data-stu-id="32ca6-193">For more information, see [Time Matters in Dashboard](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).</span></span>

<span data-ttu-id="32ca6-194">藉由時間篩選時，請記住，您會得到兩個時間週期的「交集」  結果：一個時間週期指定於 OMS 入口網站 (S1)，另一個時間週期指定於查詢 (S2) 中。</span><span class="sxs-lookup"><span data-stu-id="32ca6-194">When filtering by time, keep in mind that you get results for the *intersection* of the two time periods: the one specified in the OMS portal (S1) and the one specified in the query (S2).</span></span>

![交集](./media/log-analytics-log-searches/oms-search-intersection.png)

<span data-ttu-id="32ca6-196">這表示，如果時間週期沒有交集，例如，您在 OMS 入口網路中選擇**本週**，但在查詢中定義**上週**，則沒有交集，您將不會收到任何結果。</span><span class="sxs-lookup"><span data-stu-id="32ca6-196">This means, if the time periods don’t intersect, for example in the OMS portal where you choose **This week** and in the query where you define **last week**, then there is no intersection and you won't receive any results.</span></span>

<span data-ttu-id="32ca6-197">用於 TimeGenerated 欄位的比較運算子在其他情況下也很有用。</span><span class="sxs-lookup"><span data-stu-id="32ca6-197">Comparison operators used for the TimeGenerated field are also useful in other situations.</span></span> <span data-ttu-id="32ca6-198">例如，用於數值欄位。</span><span class="sxs-lookup"><span data-stu-id="32ca6-198">For example, with numeric fields.</span></span>

<span data-ttu-id="32ca6-199">例如，假設組態評估的警示有下列嚴重性值：</span><span class="sxs-lookup"><span data-stu-id="32ca6-199">For example, given that Configuration Assessment’s alerts have the following severity values:</span></span>

* <span data-ttu-id="32ca6-200">0 = 資訊</span><span class="sxs-lookup"><span data-stu-id="32ca6-200">0 = Information</span></span>
* <span data-ttu-id="32ca6-201">1 = 警告</span><span class="sxs-lookup"><span data-stu-id="32ca6-201">1 = Warning</span></span>
* <span data-ttu-id="32ca6-202">2 = 重大</span><span class="sxs-lookup"><span data-stu-id="32ca6-202">2 = Critical</span></span>

<span data-ttu-id="32ca6-203">您可以查詢警告和重大警示，並且排除具備下列查詢的資訊警示：</span><span class="sxs-lookup"><span data-stu-id="32ca6-203">You can query for both warning and critical alerts and also exclude informational ones with the following query:</span></span>

```
Type=ConfigurationAlert  Severity>=1
```


<span data-ttu-id="32ca6-204">您也可以使用範圍查詢。</span><span class="sxs-lookup"><span data-stu-id="32ca6-204">You can also use range queries.</span></span> <span data-ttu-id="32ca6-205">這表示您可以序列提供値的開始和結束範圍。</span><span class="sxs-lookup"><span data-stu-id="32ca6-205">This means that you can provide the beginning and end range of values in a sequence.</span></span> <span data-ttu-id="32ca6-206">例如，如果您想要來自 Operations Manager 事件記錄 (其中 EventID 大於或等於 2100，但小於 2199) 的事件，下列查詢就會傳回它們。</span><span class="sxs-lookup"><span data-stu-id="32ca6-206">For example, if you want events from the Operations Manager event log where the EventID is greater than or equal to 2100 but not greater than 2199, then the following query would return them.</span></span>

```
Type=Event EventLog="Operations Manager" EventID:[2100..2199]
```


> [!NOTE]
> <span data-ttu-id="32ca6-207">您必須使用的範圍語法是冒號 (:) field:value 分隔符號，「不」是等號 (=)。</span><span class="sxs-lookup"><span data-stu-id="32ca6-207">The range syntax you must use is the colon (:) field:value separator and *not* the equal sign (=).</span></span> <span data-ttu-id="32ca6-208">用方括號括住範圍的下限和上限結尾，並使用兩個句點 (..) 隔開它們。</span><span class="sxs-lookup"><span data-stu-id="32ca6-208">Enclose the lower and upper end of the range in square brackets and separate them with two periods (..).</span></span>
>
>

## <a name="manipulate-search-results"></a><span data-ttu-id="32ca6-209">操控搜尋結果</span><span class="sxs-lookup"><span data-stu-id="32ca6-209">Manipulate search results</span></span>
<span data-ttu-id="32ca6-210">當您在搜尋資料時，您會想要精簡搜尋查詢，並已經對結果有相當程度的控制。</span><span class="sxs-lookup"><span data-stu-id="32ca6-210">When you're searching for data, you'll want to refine your search query and have a good level of control over the results.</span></span> <span data-ttu-id="32ca6-211">擷取結果時，您可以套用命令以將其轉換。</span><span class="sxs-lookup"><span data-stu-id="32ca6-211">When results are retrieved, you can apply commands to transform them.</span></span>

<span data-ttu-id="32ca6-212">Log Analytics 搜尋中的命令「必須」  跟在分隔號字元 (|) 之後。</span><span class="sxs-lookup"><span data-stu-id="32ca6-212">Commands in Log Analytics searches *must* follow after the vertical pipe character (|).</span></span> <span data-ttu-id="32ca6-213">篩選器一律為查詢字串的第一個部分。</span><span class="sxs-lookup"><span data-stu-id="32ca6-213">A filter must always be the first part of a query string.</span></span> <span data-ttu-id="32ca6-214">它會定義您正在使用的資料集，然後將那些結果「輸送」入命令。</span><span class="sxs-lookup"><span data-stu-id="32ca6-214">It defines the data set you're working with and then "pipes" those results into a command.</span></span> <span data-ttu-id="32ca6-215">然後您可以使用管道來新增其他命令。</span><span class="sxs-lookup"><span data-stu-id="32ca6-215">You can then use the pipe to add additional commands.</span></span> <span data-ttu-id="32ca6-216">這樣有點類似 Windows PowerShell 管線。</span><span class="sxs-lookup"><span data-stu-id="32ca6-216">This is loosely similar to the Windows PowerShell pipeline.</span></span>

<span data-ttu-id="32ca6-217">一般而言，Log Analytics 搜尋語言會嘗試遵循 PowerShell 樣式和指導方針，使它類似於 IT 專業人員，並簡化學習曲線。</span><span class="sxs-lookup"><span data-stu-id="32ca6-217">In general, the Log Analytics search language tries to follow PowerShell style and guidelines to make it similar to the IT pros, and to ease the learning curve.</span></span>

<span data-ttu-id="32ca6-218">命令具有動詞的名稱，因此您可以輕易地分辨它們執行的動作。</span><span class="sxs-lookup"><span data-stu-id="32ca6-218">Commands have names of verbs so you can easily tell what they do.</span></span>  

### <a name="sort"></a><span data-ttu-id="32ca6-219">排序</span><span class="sxs-lookup"><span data-stu-id="32ca6-219">Sort</span></span>
<span data-ttu-id="32ca6-220">sort 命令可讓您利用一或多個欄位來定義排序順序。</span><span class="sxs-lookup"><span data-stu-id="32ca6-220">The sort command allows you to define the sorting order by one or multiple fields.</span></span> <span data-ttu-id="32ca6-221">即使您不使用它，根據預設，會強制執行時間遞減順序。</span><span class="sxs-lookup"><span data-stu-id="32ca6-221">Even if you don’t use it, by default, a time descending order is enforced.</span></span> <span data-ttu-id="32ca6-222">最新的結果永遠在搜尋結果的頂端。</span><span class="sxs-lookup"><span data-stu-id="32ca6-222">The most recent results are always at the top of search results.</span></span> <span data-ttu-id="32ca6-223">這表示當您執行搜尋時，真正利用 `Type=Event EventID=1234` 執行的內容如下：</span><span class="sxs-lookup"><span data-stu-id="32ca6-223">This means that when you run a search, with `Type=Event EventID=1234` what really is executed for you is:</span></span>

```
Type=Event EventID=1234 **| Sort TimeGenerated desc**
```

<span data-ttu-id="32ca6-224">這是因為它是您在記錄中熟悉的經驗類型。</span><span class="sxs-lookup"><span data-stu-id="32ca6-224">That's because it is the type of experience you are familiar with in logs.</span></span> <span data-ttu-id="32ca6-225">例如，在 Windows 事件檢視器中。</span><span class="sxs-lookup"><span data-stu-id="32ca6-225">For example, in the Windows Event Viewer.</span></span>

<span data-ttu-id="32ca6-226">您可以使用 Sort 來變更傳回結果的方式。</span><span class="sxs-lookup"><span data-stu-id="32ca6-226">You can use Sort to change the way results are returned.</span></span> <span data-ttu-id="32ca6-227">下列範例顯示此運作方式。</span><span class="sxs-lookup"><span data-stu-id="32ca6-227">The following examples show how this works.</span></span>

```
Type=Event EventID=1234 | Sort TimeGenerated asc
```

```
Type=Event EventID=1234 | Sort Computer asc
```

```
Type=Event EventID=1234 | Sort Computer asc,TimeGenerated desc
```


<span data-ttu-id="32ca6-228">上述的簡單範例顯示命令的運作方式--它們會變更篩選器傳回結果的圖形。</span><span class="sxs-lookup"><span data-stu-id="32ca6-228">The simple examples above show you how commands work--they change the shape of the results that the filter returned.</span></span>

### <a name="limit-and-top"></a><span data-ttu-id="32ca6-229">Limit 和 top</span><span class="sxs-lookup"><span data-stu-id="32ca6-229">Limit and top</span></span>
<span data-ttu-id="32ca6-230">另一個較少人知道的命令是 LIMIT。</span><span class="sxs-lookup"><span data-stu-id="32ca6-230">Another less known command is LIMIT.</span></span> <span data-ttu-id="32ca6-231">Limit 為類似 PowerShell 的動詞。</span><span class="sxs-lookup"><span data-stu-id="32ca6-231">Limit is a PowerShell-like verb.</span></span> <span data-ttu-id="32ca6-232">Limit 在功能上和 TOP 命令相同。</span><span class="sxs-lookup"><span data-stu-id="32ca6-232">Limit is functionally identical to the TOP command.</span></span> <span data-ttu-id="32ca6-233">下列查詢會傳回相同的結果。</span><span class="sxs-lookup"><span data-stu-id="32ca6-233">The following queries return the same results.</span></span>

```
Type=Event EventID=600 | Limit 1
```

```
Type=Event EventID=600 | Top 1
```


#### <a name="to-search-using-top"></a><span data-ttu-id="32ca6-234">使用 top 搜尋</span><span class="sxs-lookup"><span data-stu-id="32ca6-234">To search using top</span></span>
* <span data-ttu-id="32ca6-235">在搜尋查詢欄位中，輸入 `Type=Event EventID=600 | Top 1` </span><span class="sxs-lookup"><span data-stu-id="32ca6-235">In the search query field, type `Type=Event EventID=600 | Top 1` </span></span>  
    <span data-ttu-id="32ca6-236">![搜尋 top](./media/log-analytics-log-searches/oms-search-top.png)</span><span class="sxs-lookup"><span data-stu-id="32ca6-236">![search top](./media/log-analytics-log-searches/oms-search-top.png)</span></span>

<span data-ttu-id="32ca6-237">在上圖中，有 358 個記錄含有 EventID=600。</span><span class="sxs-lookup"><span data-stu-id="32ca6-237">In the image above, there are 358 thousand records with EventID=600.</span></span> <span data-ttu-id="32ca6-238">左邊的欄位、facet 和篩選器永遠會顯示查詢的「篩選器部分」  所傳回的結果資訊，也就是任何縱線字元之前的部分。</span><span class="sxs-lookup"><span data-stu-id="32ca6-238">The fields, facets, and filters on the left always show information about the results returned *by the filter portion* of the query, which is the part before any pipe character.</span></span> <span data-ttu-id="32ca6-239">[結果]  窗格只會傳回最新的 1 個結果，因為範例命令會圖形化和轉換結果。</span><span class="sxs-lookup"><span data-stu-id="32ca6-239">The **Results** pane only returns the most recent 1 result, because the example command shaped and transformed the results.</span></span>

### <a name="select"></a><span data-ttu-id="32ca6-240">選取</span><span class="sxs-lookup"><span data-stu-id="32ca6-240">Select</span></span>
<span data-ttu-id="32ca6-241">SELECT 命令的行為類似 PowerShell 中的 Select-Object。</span><span class="sxs-lookup"><span data-stu-id="32ca6-241">The SELECT command behaves like Select-Object in PowerShell.</span></span> <span data-ttu-id="32ca6-242">它會傳回不包含所有原始屬性的篩選結果。</span><span class="sxs-lookup"><span data-stu-id="32ca6-242">It returns filtered results that do not have all of their original properties.</span></span> <span data-ttu-id="32ca6-243">相反地，它只會選取您所指定的屬性。</span><span class="sxs-lookup"><span data-stu-id="32ca6-243">Instead, it selects only the properties that you specify.</span></span>

#### <a name="to-run-a-search-using-the-select-command"></a><span data-ttu-id="32ca6-244">使用 select 命令執行搜尋</span><span class="sxs-lookup"><span data-stu-id="32ca6-244">To run a search using the select command</span></span>
1. <span data-ttu-id="32ca6-245">在 [搜尋] 中，輸入 `Type=Event`，然後按一下 [搜尋]。</span><span class="sxs-lookup"><span data-stu-id="32ca6-245">In Search, type `Type=Event` and then click **Search**.</span></span>
2. <span data-ttu-id="32ca6-246">按一下其中一種結果中的 [+ 顯示更多]  ，以檢視結果具有的屬性。</span><span class="sxs-lookup"><span data-stu-id="32ca6-246">Click **+ show more** in one of the results to view all the properties that the results have.</span></span>
3. <span data-ttu-id="32ca6-247">明確地選取部分，查詢會變更為 `Type=Event | Select Computer,EventID,RenderedDescription`。</span><span class="sxs-lookup"><span data-stu-id="32ca6-247">Select some of those explicitly, and the query changes to `Type=Event | Select Computer,EventID,RenderedDescription`.</span></span>  
    <span data-ttu-id="32ca6-248">![搜尋 select](./media/log-analytics-log-searches/oms-search-select.png)</span><span class="sxs-lookup"><span data-stu-id="32ca6-248">![search select](./media/log-analytics-log-searches/oms-search-select.png)</span></span>

<span data-ttu-id="32ca6-249">當您想要控制搜尋輸出，並且只選擇對探索真的很重要的資料部分 (通常不是完整記錄) 時，這會是特別有用的命令。</span><span class="sxs-lookup"><span data-stu-id="32ca6-249">This command is particularly useful when you want to control search output and choose only the portions of data that really matter for your exploration, which often isn’t the full record.</span></span> <span data-ttu-id="32ca6-250">當不同類型的記錄有「部分」通用屬性，但不是「所有」屬性都共用時，這也非常有用。</span><span class="sxs-lookup"><span data-stu-id="32ca6-250">This is also useful when records of different types have *some* common properties, but not *all* of their properties are common.</span></span> <span data-ttu-id="32ca6-251">然後，您可以產生看起來就像資料表一般自然的輸出，或在匯出至 CSV 檔案，然後傳遞訊息至 Excel 中時正常運作。</span><span class="sxs-lookup"><span data-stu-id="32ca6-251">The, you can generate output that looks more naturally like a table, or work well when exported to a CSV file and then massaged in Excel.</span></span>

## <a name="use-the-measure-command"></a><span data-ttu-id="32ca6-252">使用 measure 命令</span><span class="sxs-lookup"><span data-stu-id="32ca6-252">Use the measure command</span></span>
<span data-ttu-id="32ca6-253">MEASURE 是 Log Analytics 搜尋中最具彈性的命令之一。</span><span class="sxs-lookup"><span data-stu-id="32ca6-253">MEASURE is one of the most versatile commands in Log Analytics searches.</span></span> <span data-ttu-id="32ca6-254">它可讓您將統計「函數」  套用至資料，並依照指定的欄位分組來彙總結果。</span><span class="sxs-lookup"><span data-stu-id="32ca6-254">It allows you to apply statistical *functions* to your data and aggregate results grouped by a given field.</span></span> <span data-ttu-id="32ca6-255">Measure 支援多個統計函數。</span><span class="sxs-lookup"><span data-stu-id="32ca6-255">There are multiple statistical functions that Measure supports.</span></span>

### <a name="measure-count"></a><span data-ttu-id="32ca6-256">Measure count()</span><span class="sxs-lookup"><span data-stu-id="32ca6-256">Measure count()</span></span>
<span data-ttu-id="32ca6-257">第一個要使用的統計函數，也是最容易了解的統計函數就是「count()」  函數。</span><span class="sxs-lookup"><span data-stu-id="32ca6-257">The first statistical function to work with, and one of the simplest to understand is the *count()* function.</span></span>

<span data-ttu-id="32ca6-258">來自任何搜尋查詢 (例如 `Type=Event`) 的結果會在搜尋結果的左邊顯示篩選，又稱為 Facet。</span><span class="sxs-lookup"><span data-stu-id="32ca6-258">Results from any search query such as `Type=Event`, show filters also called facets on the left side of search results.</span></span> <span data-ttu-id="32ca6-259">篩選器會在執行的搜尋中透過指定的結果欄位顯示值的分佈。</span><span class="sxs-lookup"><span data-stu-id="32ca6-259">The filters show a distribution of values by a given field for the results in the search executed.</span></span>

![搜尋 measure count](./media/log-analytics-log-searches/oms-search-measure-count01.png)

<span data-ttu-id="32ca6-261">例如，在上面的影像中，您會看到 **Computer** 欄位，它指出在結果中將近 739,000 個事件內，那些記錄中的 **Computer** 欄位有 68 個唯一且不同的值。</span><span class="sxs-lookup"><span data-stu-id="32ca6-261">For example, in the image above you'll see the **Computer** field and it shows that within the almost 739 thousand events in the results, there are 68 unique and distinct values for the **Computer** field in those records.</span></span> <span data-ttu-id="32ca6-262">磚只會顯示前 5 個値 (也就是最常寫入 **Computer** 欄位中的 5 個值)，依據在該欄位中含有該特定値的文件數目來排序。</span><span class="sxs-lookup"><span data-stu-id="32ca6-262">The tile only shows the top 5, which are the most common 5 values that are written in the **Computer** fields), sorted by the number of documents that contain that specific value in that field.</span></span> <span data-ttu-id="32ca6-263">在圖中，您可以看到 – 在將近 36 萬 9 千個事件之中 - 9 萬個事件來自 OpsInsights04.contoso.com 電腦，8 萬 3 千個事件來自 DB03.contoso.com 電腦，諸如此類。</span><span class="sxs-lookup"><span data-stu-id="32ca6-263">In the image you can see that – among those almost 369 thousand events – 90 thousand come from the OpsInsights04.contoso.com computer, 83 thousand from the DB03.contoso.com computer, and so on.</span></span>

<span data-ttu-id="32ca6-264">由於磚只會顯示前 5 個値，如果要查看所有的值怎麼辦？</span><span class="sxs-lookup"><span data-stu-id="32ca6-264">What if you want to see all values, since the tile only shows only the top 5?</span></span>

<span data-ttu-id="32ca6-265">measure 命令可以使用 count () 函數達成。</span><span class="sxs-lookup"><span data-stu-id="32ca6-265">That’s what the measure command can do with the count() function.</span></span> <span data-ttu-id="32ca6-266">此函數不會使用任何參數。</span><span class="sxs-lookup"><span data-stu-id="32ca6-266">This function doesn't use any parameters.</span></span> <span data-ttu-id="32ca6-267">您只需要指定想做為分組依據的欄位即可 – 在此案例中為 **Computer** 欄位：</span><span class="sxs-lookup"><span data-stu-id="32ca6-267">You just specify the field by which you want to group by – the **Computer** field in this case:</span></span>

`Type=Event | Measure count() by Computer`

![搜尋 measure count](./media/log-analytics-log-searches/oms-search-measure-count-computer.png)

<span data-ttu-id="32ca6-269">不過，**Computer** 只是每個資料片段「中」使用的欄位 - 不涉及關聯式資料庫，其他地方也都沒有別的 **Computer** 物件。</span><span class="sxs-lookup"><span data-stu-id="32ca6-269">However, **Computer** is just a field used *in* each piece of data – there are no relational databases involved and there is no separate **Computer** object anywhere.</span></span> <span data-ttu-id="32ca6-270">只有資料「中」的値可以描述哪個實體產生它們，以及資料的其他一些特性和面向 - 所以才稱為 *Facet*。</span><span class="sxs-lookup"><span data-stu-id="32ca6-270">Just the values *in* the data can describe which entity generated them, and a number of other characteristics and aspects of the data – hence the term *facet*.</span></span> <span data-ttu-id="32ca6-271">不過，您也可以根據其他欄位分組。</span><span class="sxs-lookup"><span data-stu-id="32ca6-271">However, you can just as well group by other fields.</span></span> <span data-ttu-id="32ca6-272">因為輸送到 measure 命令的將近 73 萬 9 千個事件的原始結果也有一個稱為 **EventID** 的欄位，所以您可以套用相同的技巧，依據該欄位分組，並根據 EventID 取得事件計數：</span><span class="sxs-lookup"><span data-stu-id="32ca6-272">Because the original results of almost 739 thousand events that are piped into the measure command also have a field called **EventID**, you can apply the same technique to group by that field and get a count of events by EventID:</span></span>

```
Type=Event | Measure count() by EventID
```

<span data-ttu-id="32ca6-273">如果您對包含特定値的實際記錄計數不感興趣，而只想要取得值本身的清單，您可以在尾端加上「Select」  命令，並只選取第一個資料行：</span><span class="sxs-lookup"><span data-stu-id="32ca6-273">If you're not interested in the actual record count that contain a specific value, but instead if you only want a list of the values themselves, you can add a *Select* command at the end of it and just select the first column:</span></span>

```
Type=Event | Measure count() by EventID | Select EventID
```

<span data-ttu-id="32ca6-274">然後您就可以在查詢中取得更複雜和預先排序的結果，或者您也可以只按一下方格中的資料行。</span><span class="sxs-lookup"><span data-stu-id="32ca6-274">Then you can get more intricate and pre-sort the results in the query, or you can just click the columns in the grid, too.</span></span>

```
Type=Event | Measure count() by EventID | Select EventID | Sort EventID asc
```

#### <a name="to-search-using-measure-count"></a><span data-ttu-id="32ca6-275">使用 measure count 搜尋</span><span class="sxs-lookup"><span data-stu-id="32ca6-275">To search using measure count</span></span>
* <span data-ttu-id="32ca6-276">在搜尋查詢欄位中，輸入 `Type=Event | Measure count() by EventID`</span><span class="sxs-lookup"><span data-stu-id="32ca6-276">In the search query field, type `Type=Event | Measure count() by EventID`</span></span>
* <span data-ttu-id="32ca6-277">將 `| Select EventID` 附加至查詢的結尾。</span><span class="sxs-lookup"><span data-stu-id="32ca6-277">Append `| Select EventID` to the end of the query.</span></span>
* <span data-ttu-id="32ca6-278">最後，將 `| Sort EventID asc` 附加至查詢的結尾。</span><span class="sxs-lookup"><span data-stu-id="32ca6-278">Finally, append `| Sort EventID asc` to the end of the query.</span></span>

<span data-ttu-id="32ca6-279">有一些要注意與強調的重點：</span><span class="sxs-lookup"><span data-stu-id="32ca6-279">There are a couple important points to notice and emphasize:</span></span>

<span data-ttu-id="32ca6-280">首先，您看到的結果不是未經處理的結果了。</span><span class="sxs-lookup"><span data-stu-id="32ca6-280">First, the results you see are not the original raw results anymore.</span></span> <span data-ttu-id="32ca6-281">相反地，它們是彙總的結果 – 基本上是結果的群組。</span><span class="sxs-lookup"><span data-stu-id="32ca6-281">Instead, they are aggregated results – essentially groups of results.</span></span> <span data-ttu-id="32ca6-282">這不是問題，但您應該了解您正與非常不同的資料圖形互動，其差異在於即時建立為彙總/統計函數結果未經處理的圖形。</span><span class="sxs-lookup"><span data-stu-id="32ca6-282">This isn't a problem, but you should understand that you're interacting with a very different shape of data that differs from the original raw shape that gets created on the fly as a result of the aggregation/statistical function.</span></span>

<span data-ttu-id="32ca6-283">第二， **Measure count** 目前只會傳回前 100 個不同結果。</span><span class="sxs-lookup"><span data-stu-id="32ca6-283">Second, **Measure count** currently returns only the top 100 distinct results.</span></span> <span data-ttu-id="32ca6-284">這項限制不適用於其他統計函數。</span><span class="sxs-lookup"><span data-stu-id="32ca6-284">This limit does not apply to the other statistical functions.</span></span> <span data-ttu-id="32ca6-285">因此，您通常必須先使用更精確的篩選器來搜尋特定項目，然後再套用 measure count()。</span><span class="sxs-lookup"><span data-stu-id="32ca6-285">So, you'll usually need to use a more precise filter first to search for specific items before you apply measure count().</span></span>

## <a name="use-the-max-and-min-functions-with-the-measure-command"></a><span data-ttu-id="32ca6-286">透過 measure 命令使用 max 和 min 函數</span><span class="sxs-lookup"><span data-stu-id="32ca6-286">Use the max and min functions with the measure command</span></span>
<span data-ttu-id="32ca6-287">有 **Measure Max()** 和 **Measure Min()** 在其中很有用的各種案例。</span><span class="sxs-lookup"><span data-stu-id="32ca6-287">There are various scenarios where **Measure Max()** and **Measure Min()** are useful.</span></span> <span data-ttu-id="32ca6-288">不過，由於每個函數彼此相反，我們將說明 Max ()，而您可以自己實驗 Min ()。</span><span class="sxs-lookup"><span data-stu-id="32ca6-288">However, since each function is opposite of each other, we'll illustrate Max() and you can experiment with Min() on your own.</span></span>

<span data-ttu-id="32ca6-289">如果您查詢安全性事件，它們會有不同的**層級**屬性。</span><span class="sxs-lookup"><span data-stu-id="32ca6-289">If you query for security events, they have a **Level** property that can vary.</span></span> <span data-ttu-id="32ca6-290">例如：</span><span class="sxs-lookup"><span data-stu-id="32ca6-290">For example:</span></span>

```
Type=SecurityEvent
```

![搜尋 measure count 開始](./media/log-analytics-log-searches/oms-search-measure-max01.png)

<span data-ttu-id="32ca6-292">如果您想要在指定共用「電腦」(根據欄位的分組) 的情況下，檢視所有安全性事件的最高值，您可以使用</span><span class="sxs-lookup"><span data-stu-id="32ca6-292">If you want to view the highest value for all of the security events given a common Computer, the group by field, you can use</span></span>

```
Type=ConfigurationAlert | Measure Max(Level) by Computer
```

![搜尋 measure max 電腦](./media/log-analytics-log-searches/oms-search-measure-max02.png)

<span data-ttu-id="32ca6-294">這將會顯示在具有**層級**記錄的電腦中，大部分都至少為層級 8，而有許多都是層級 16。</span><span class="sxs-lookup"><span data-stu-id="32ca6-294">It will display that for the computers that had **Level** records, most of them have at least level 8, many had a level of 16.</span></span>

```
Type=ConfigurationAlert | Measure Max(Severity) by Computer
```

![搜尋 measure max 時間產生電腦](./media/log-analytics-log-searches/oms-search-measure-max03.png)

<span data-ttu-id="32ca6-296">此函數適用於數字，但它也可以使用日期時間欄位。</span><span class="sxs-lookup"><span data-stu-id="32ca6-296">This function works well with numbers, but it also works with DateTime fields.</span></span> <span data-ttu-id="32ca6-297">您最好檢查最後一個或最新的時間戳記，是否有任何為每台電腦編製索引的資料片段位。</span><span class="sxs-lookup"><span data-stu-id="32ca6-297">It is useful to check for the last or most recent time stamp for any piece of data indexed for each computer.</span></span> <span data-ttu-id="32ca6-298">例如︰何時為每一部電腦回報最新的安全性事件？</span><span class="sxs-lookup"><span data-stu-id="32ca6-298">For example: When was the most recent security event reported for each machine?</span></span>

```
Type=ConfigurationChange | Measure Max(TimeGenerated) by Computer
```

## <a name="use-the-avg-function-with-the-measure-command"></a><span data-ttu-id="32ca6-299">透過 measure 命令使用avg 函數</span><span class="sxs-lookup"><span data-stu-id="32ca6-299">Use the avg function with the measure command</span></span>
<span data-ttu-id="32ca6-300">和 measure 搭配使用的 Avg () 統計函數可讓您計算某些欄位的平均值，並且根據相同或其他欄位將結果分組。</span><span class="sxs-lookup"><span data-stu-id="32ca6-300">The Avg() statistical function used with measure allows you to calculate the average value for some field, and group results by the same or other field.</span></span> <span data-ttu-id="32ca6-301">這適用於各種情況，例如效能資料。</span><span class="sxs-lookup"><span data-stu-id="32ca6-301">This is useful in a variety of cases, such as performance data.</span></span>

<span data-ttu-id="32ca6-302">我們將從效能等級開始介紹。</span><span class="sxs-lookup"><span data-stu-id="32ca6-302">We'll start with performance data.</span></span> <span data-ttu-id="32ca6-303">請注意，OMS 目前會收集 Windows 和 Linux 機器的效能計數器。</span><span class="sxs-lookup"><span data-stu-id="32ca6-303">Note that OMS currently collects performance counters for both Windows and Linux machines.</span></span>

<span data-ttu-id="32ca6-304">若要搜尋「所有」  效能資料，最基本的查詢如下：</span><span class="sxs-lookup"><span data-stu-id="32ca6-304">To search for *all* performance data, the most basic query is:</span></span>

```
Type=Perf
```

![搜尋 avg 開始](./media/log-analytics-log-searches/oms-search-avg01.png)

<span data-ttu-id="32ca6-306">首先您會注意到 Log Analytics 顯示三種觀點︰清單，顯示圖表背後的真正記錄；資料表，顯示效能計數器資料的表格式檢視；度量，顯示效能計數器的圖表。</span><span class="sxs-lookup"><span data-stu-id="32ca6-306">The first thing you'll notice is that Log Analytics shows you three perspectives: List, which shows you which shows the actual records behind the charts; Table, which shows a tabular view of performance counter data; and Metrics, which shows charts for the performance counters.</span></span>

<span data-ttu-id="32ca6-307">在上述映像中，有兩組標示的欄位，指出下列事項：</span><span class="sxs-lookup"><span data-stu-id="32ca6-307">In the image above, there are two sets of fields marked that indicate the following:</span></span>

* <span data-ttu-id="32ca6-308">第一組會識別查詢篩選器中的 Windows 效能計數器名稱、物件名稱和執行個體名稱。</span><span class="sxs-lookup"><span data-stu-id="32ca6-308">The first set identifies Windows Performance Counter Name, Object Name, and Instance Name in the query filter.</span></span> <span data-ttu-id="32ca6-309">這些是您可能會最常用來做為 facet/篩選器的欄位</span><span class="sxs-lookup"><span data-stu-id="32ca6-309">These are the fields you probably will most commonly use as facets/filters</span></span>
* <span data-ttu-id="32ca6-310">**CounterValue** 是計數器的實際值。</span><span class="sxs-lookup"><span data-stu-id="32ca6-310">**CounterValue** is the actual value of the counter.</span></span> <span data-ttu-id="32ca6-311">在此範例中，值是 *75*。</span><span class="sxs-lookup"><span data-stu-id="32ca6-311">In this example, the value is *75*.</span></span>
* <span data-ttu-id="32ca6-312">**TimeGenerated** 為 12:51，採用 24 小時制的時間格式。</span><span class="sxs-lookup"><span data-stu-id="32ca6-312">**TimeGenerated** is 12:51, in 24-hour time format.</span></span>

<span data-ttu-id="32ca6-313">以下是圖形中的度量檢視。</span><span class="sxs-lookup"><span data-stu-id="32ca6-313">Here's a view of the metrics in a graph.</span></span>

![搜尋 avg 開始](./media/log-analytics-log-searches/oms-search-avg02.png)

<span data-ttu-id="32ca6-315">閱讀 Perf 記錄圖形，並閱讀其他搜尋技術之後，您可以使用measure Avg () 來彙總此類型的數值資料。</span><span class="sxs-lookup"><span data-stu-id="32ca6-315">After reading about the Perf record shape, and having read about other search techniques, you can use measure Avg() to aggregate this type of numerical data.</span></span>

<span data-ttu-id="32ca6-316">以下是簡單的範例：</span><span class="sxs-lookup"><span data-stu-id="32ca6-316">Here's a simple example:</span></span>

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" | Measure Avg(CounterValue) by Computer
```

![搜尋 avg samplevalue](./media/log-analytics-log-searches/oms-search-avg03.png)

<span data-ttu-id="32ca6-318">在此範例中，您可以選取 CPU 時間總計效能計數器並根據電腦來平均。</span><span class="sxs-lookup"><span data-stu-id="32ca6-318">In this example, you select the CPU Total Time performance counter and average by Computer.</span></span> <span data-ttu-id="32ca6-319">如果您想要將結果縮小到只有過去 6 小時，您可以使用時間篩選控制項，或如下所示在查詢中指定︰</span><span class="sxs-lookup"><span data-stu-id="32ca6-319">If you want to narrow down your results to only the last 6 hours, you can either use the time filter control or specify in your query as follows:</span></span>

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer
```

### <a name="to-search-using-the-avg-function-with-the-measure-command"></a><span data-ttu-id="32ca6-320">搭配使用 avg 函數和 measure 命令進行搜尋</span><span class="sxs-lookup"><span data-stu-id="32ca6-320">To search using the avg function with the measure command</span></span>
* <span data-ttu-id="32ca6-321">在 [搜尋查詢] 方塊中，輸入 `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`。</span><span class="sxs-lookup"><span data-stu-id="32ca6-321">In the Search query box, type `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.</span></span>

<span data-ttu-id="32ca6-322">您可以「跨」  電腦彙總資料，並將其相互關聯。</span><span class="sxs-lookup"><span data-stu-id="32ca6-322">You can aggregate and correlate data *across* computers.</span></span> <span data-ttu-id="32ca6-323">例如，假設您有一組某種伺服器陣列的主機，其中的節點彼此相等，而且它們執行的工作類型完全相同，負載也應該大致平衡。</span><span class="sxs-lookup"><span data-stu-id="32ca6-323">For example, imagine that you have a set of hosts in some sort of farm where each node is equal to any other one and they just do all the same type of work and load should be roughly balanced.</span></span> <span data-ttu-id="32ca6-324">您可以利用下列查詢一次取得所有計數器，並取得整個伺服器陣列的平均。</span><span class="sxs-lookup"><span data-stu-id="32ca6-324">You could get their counters all in one go with the following query and get averages for the entire farm.</span></span> <span data-ttu-id="32ca6-325">您可以藉由選擇電腦，以下列範例開頭：</span><span class="sxs-lookup"><span data-stu-id="32ca6-325">You can start by choosing the computers with the following example:</span></span>

```
Type=Perf AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

<span data-ttu-id="32ca6-326">您擁有電腦之後，也只會想要選取兩個關鍵效能指標 (KPI)：% CPU 使用量和 % 可用磁碟空間。</span><span class="sxs-lookup"><span data-stu-id="32ca6-326">Now that you have the computers, you also only want to select two key performance indicators (KPIs): % CPU Usage and % Free Disk Space.</span></span> <span data-ttu-id="32ca6-327">因此，查詢的該部分會變成：</span><span class="sxs-lookup"><span data-stu-id="32ca6-327">So, that part of the query becomes:</span></span>

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS
```

<span data-ttu-id="32ca6-328">您現在可以利用下列範例新增電腦和計數器：</span><span class="sxs-lookup"><span data-stu-id="32ca6-328">Now you can add computers and counters with the following example:</span></span>

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

<span data-ttu-id="32ca6-329">因為您有非常明確的選取範圍，只要依據 CounterName 分組， **measure Avg ()** 命令可以傳回不是依電腦算出的平均，而是跨伺服器陣列算出的平均。</span><span class="sxs-lookup"><span data-stu-id="32ca6-329">Because you have a very specific selection, the **measure Avg()** command can return the average not by computer, but across the farm, simply by grouping by CounterName.</span></span> <span data-ttu-id="32ca6-330">例如：</span><span class="sxs-lookup"><span data-stu-id="32ca6-330">For example:</span></span>

```
Type=Perf  InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03") | Measure Avg(CounterValue) by CounterName
```

<span data-ttu-id="32ca6-331">這可提供您數個環境 KPI 的實用精簡檢視。</span><span class="sxs-lookup"><span data-stu-id="32ca6-331">This gives you a useful compact view of a couple of your environment's KPIs.</span></span>

![搜尋 avg grouping](./media/log-analytics-log-searches/oms-search-avg04.png)

<span data-ttu-id="32ca6-333">您可以在儀表板中輕鬆使用搜尋查詢。</span><span class="sxs-lookup"><span data-stu-id="32ca6-333">You can easily use the search query in a dashboard.</span></span> <span data-ttu-id="32ca6-334">例如，您可以儲存搜尋查詢，再利用它來建立名為 *Web 伺服陣列 KPI* 的儀表板。</span><span class="sxs-lookup"><span data-stu-id="32ca6-334">For example, you could save the search query and create a dashboard from it named *Web Farm KPIs*.</span></span> <span data-ttu-id="32ca6-335">若要深入了解如何使用儀表板，請參閱 [在 Log Analytics 中建立自訂的儀表板](log-analytics-dashboards.md)。</span><span class="sxs-lookup"><span data-stu-id="32ca6-335">To learn more about using dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span></span>

![搜尋 avg 儀表板](./media/log-analytics-log-searches/oms-search-avg05.png)

### <a name="use-the-sum-function-with-the-measure-command"></a><span data-ttu-id="32ca6-337">透過 measure 命令使用 sum 函數</span><span class="sxs-lookup"><span data-stu-id="32ca6-337">Use the sum function with the measure command</span></span>
<span data-ttu-id="32ca6-338">sum 函數和 measure 命令的他函數類似。</span><span class="sxs-lookup"><span data-stu-id="32ca6-338">The sum function is similar to other functions of the measure command.</span></span> <span data-ttu-id="32ca6-339">您可以在 [Microsoft Azure Operational Insights 中的 W3C IIS 記錄搜尋](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx)看到如何使用 sum 函數的範例。</span><span class="sxs-lookup"><span data-stu-id="32ca6-339">You can see an example about how to use the sum function at [W3C IIS Logs Search in Microsoft Azure Operational Insights](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).</span></span>

<span data-ttu-id="32ca6-340">您可以搭配使用 Max() 和 Min() 與數字、日期時間和文字字串。</span><span class="sxs-lookup"><span data-stu-id="32ca6-340">You can use Max() and Min() with numbers, date times and text strings.</span></span> <span data-ttu-id="32ca6-341">透過文字字串，它們會依字母順序排序，而您會取得第一個和最後一個。</span><span class="sxs-lookup"><span data-stu-id="32ca6-341">With text strings, they are sorted alphabetically and you get first and last.</span></span>

<span data-ttu-id="32ca6-342">不過，您無法搭配使用 Sum() 與數值欄位以外的任何項目。</span><span class="sxs-lookup"><span data-stu-id="32ca6-342">However, you cannot use Sum() with anything other than numerical fields.</span></span> <span data-ttu-id="32ca6-343">這也適用於 Avg()。</span><span class="sxs-lookup"><span data-stu-id="32ca6-343">This also applies to Avg().</span></span>

### <a name="use-the-percentile-function-with-the-measure-command"></a><span data-ttu-id="32ca6-344">搭配使用 percentile 函數與 measure 命令</span><span class="sxs-lookup"><span data-stu-id="32ca6-344">Use the percentile function with the measure command</span></span>
<span data-ttu-id="32ca6-345">percentile 函數與 Avg() 和 Sum() 的類似之處在於，您只能將它用在數值欄位。</span><span class="sxs-lookup"><span data-stu-id="32ca6-345">The percentile function is similar to Avg() and Sum() in that you can only use it for numerical fields.</span></span> <span data-ttu-id="32ca6-346">您可以在數值欄位中使用 1 到 99 之間的任何百分位數。</span><span class="sxs-lookup"><span data-stu-id="32ca6-346">You can use any percentile between 1 to 99 on a numeric field.</span></span> <span data-ttu-id="32ca6-347">您也可以同時使用 **percentile** 和 **pct** 命令。</span><span class="sxs-lookup"><span data-stu-id="32ca6-347">You can also use both **percentile** and **pct** commands.</span></span> <span data-ttu-id="32ca6-348">以下提供一些範例：</span><span class="sxs-lookup"><span data-stu-id="32ca6-348">Here are few examples:</span></span>  

```
Type:Perf CounterName:"DiskTransers/sec" |measure percentile95(CurrentValue) by Computer
```
```
Type:Perf ObjectName=LogicalDisk CounterName="Current Disk Queue Length" Computer="MyComputerName" | measure pct65(CurrentValue) by InstanceName
```

## <a name="use-the-where-command"></a><span data-ttu-id="32ca6-349">使用 where 命令</span><span class="sxs-lookup"><span data-stu-id="32ca6-349">Use the where command</span></span>
<span data-ttu-id="32ca6-350">where 命令的運作方式和篩選器類似，但它可以套用在管線中，以進一步篩選由 Measure 命令產生的彙總結果 - 而不是在查詢開頭篩選過的未經處理的結果。</span><span class="sxs-lookup"><span data-stu-id="32ca6-350">The where command works like a filter, but it can be applied in the pipeline to further filter aggregated results that have been produced by a Measure command – as opposed to raw results that are filtered at the beginning of a query.</span></span>

<span data-ttu-id="32ca6-351">例如：</span><span class="sxs-lookup"><span data-stu-id="32ca6-351">For example:</span></span>

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer
```

<span data-ttu-id="32ca6-352">您可以利用下列範例，加入另一個縱線 "|" 字元以及 Where 命令，即可只取得平均 CPU 高於 80% 的電腦：</span><span class="sxs-lookup"><span data-stu-id="32ca6-352">You can add another pipe "|" character and the Where command to only get computers whose average CPU is above 80%, with the following example:</span></span>

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer | Where AVGCPU>80
```

<span data-ttu-id="32ca6-353">如果您已熟悉 Microsoft System Center Operations Manager，您可以考慮管理組件詞彙中的 where 命令。</span><span class="sxs-lookup"><span data-stu-id="32ca6-353">If you're familiar with Microsoft System Center - Operations Manager, you can think of the where command in management pack terms.</span></span> <span data-ttu-id="32ca6-354">如果此範例是一項規則，查詢的第一個部分會是資料來源，而 where 命令會是條件偵測。</span><span class="sxs-lookup"><span data-stu-id="32ca6-354">If the example were a rule, the first part of the query would be the data source and the where command would be the condition detection.</span></span>

<span data-ttu-id="32ca6-355">您可以在 [我的儀表板] 中將查詢當做一個磚來使用，做為一種監視器來查看電腦 CPU 是否過度使用。</span><span class="sxs-lookup"><span data-stu-id="32ca6-355">You can use the query as a tile in **My Dashboard**, as a monitor of sorts, to see when computer CPUs are over-utilized.</span></span> <span data-ttu-id="32ca6-356">若要深入了解儀表板，請參閱 [在 Log Analytics 中建立自訂的儀表板](log-analytics-dashboards.md)。</span><span class="sxs-lookup"><span data-stu-id="32ca6-356">To learn more about dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span></span> <span data-ttu-id="32ca6-357">您也可以使用行動應用程式建立和使用儀表板。</span><span class="sxs-lookup"><span data-stu-id="32ca6-357">You can also create and use dashboards using the mobile app.</span></span> <span data-ttu-id="32ca6-358">如需詳細資訊，請參閱 [OMS 行動應用程式 ](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)。</span><span class="sxs-lookup"><span data-stu-id="32ca6-358">For more information, see [OMS Mobile App ](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865).</span></span> <span data-ttu-id="32ca6-359">在下列映像底部的兩個磚中，您可以看到監視器顯示清單並做為一個數字。</span><span class="sxs-lookup"><span data-stu-id="32ca6-359">In the bottom two tiles of the following image, you can see the monitor displayed a list and as a number.</span></span> <span data-ttu-id="32ca6-360">基本上，您一定想要此數字為零且清單是空的。</span><span class="sxs-lookup"><span data-stu-id="32ca6-360">Essentially, you always want the number to be zero and the list to be empty.</span></span> <span data-ttu-id="32ca6-361">否則，它會指出警示條件。</span><span class="sxs-lookup"><span data-stu-id="32ca6-361">Otherwise, it indicates an alert condition.</span></span> <span data-ttu-id="32ca6-362">如有需要，您可以使用它來看看那些電腦承受壓力。</span><span class="sxs-lookup"><span data-stu-id="32ca6-362">If needed, you can use it to take a look at which machines are under pressure.</span></span>

![行動儀表板](./media/log-analytics-log-searches/oms-search-mobile.png)

## <a name="use-the-in-operator"></a><span data-ttu-id="32ca6-364">使用 in 運算子</span><span class="sxs-lookup"><span data-stu-id="32ca6-364">Use the in operator</span></span>
<span data-ttu-id="32ca6-365">*IN* 運算子以及 *NOT IN* 可讓您使用子搜尋，也就是包含另一個搜尋來做為引數的搜尋。</span><span class="sxs-lookup"><span data-stu-id="32ca6-365">The *IN* operator, along with *NOT IN* allows you to use subsearches, which are searches that include another search as an argument.</span></span> <span data-ttu-id="32ca6-366">它們會以大括號 {} 包含在另一個「主要」或「外部」搜尋內。</span><span class="sxs-lookup"><span data-stu-id="32ca6-366">They are contained in braces {} within another *primary* or *outer* search.</span></span> <span data-ttu-id="32ca6-367">子搜尋的結果 (通常是不同結果的清單) 接著會做為其主要搜尋中的引數。</span><span class="sxs-lookup"><span data-stu-id="32ca6-367">The result of a subsearch, often a list of distinct results, is then used as an argument in its primary search.</span></span>

<span data-ttu-id="32ca6-368">您可以使用子搜尋來比對無法在搜尋運算式中直接描述，但可以透過搜尋來產生的資料子集。</span><span class="sxs-lookup"><span data-stu-id="32ca6-368">You can use subsearches to match subsets of your data that you cannot describe directly in a search expression, but which can be generated from a search.</span></span> <span data-ttu-id="32ca6-369">例如，如果您想要使用某個搜尋來尋找「遺漏安全性更新的電腦」中的所有事件，則您必須設計子搜尋來先識別「遺漏安全性更新的電腦」，再找到隸屬於這些主機的事件。</span><span class="sxs-lookup"><span data-stu-id="32ca6-369">For example, if you’re interested in using one search to find all events from *computers missing security updates*, then you need to design a subsearch that first identifies that *computers missing security updates* before it finds events belonging to those hosts.</span></span>

<span data-ttu-id="32ca6-370">因此，您可以使用下列查詢來表示「目前遺漏必要安全性更新的電腦」  ︰</span><span class="sxs-lookup"><span data-stu-id="32ca6-370">So, you could express *computers currently missing required security updates* with the following query:</span></span>

```
Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer
```    

![IN 搜尋範例](./media/log-analytics-log-searches/oms-search-in01-revised.png)

<span data-ttu-id="32ca6-372">有了清單之後，您可以使用此搜尋做為內部搜尋，將電腦清單送入會尋找這些電腦之事件的外部 (主要) 搜尋。</span><span class="sxs-lookup"><span data-stu-id="32ca6-372">Once you have the list, you can use the search as an inner search to feed the list of computers into an outer (primary) search that will look for events for those computers.</span></span> <span data-ttu-id="32ca6-373">若要這麼做，您必須以大括號括住內部搜尋，並使用 IN 運算子將其結果提供做為外部搜尋中篩選條件/欄位的可能值。</span><span class="sxs-lookup"><span data-stu-id="32ca6-373">You do this by enclosing the inner search in braces and feeding its results as possible values for a filter/field in the outer search using the IN operator.</span></span> <span data-ttu-id="32ca6-374">查詢會類似下列內容︰</span><span class="sxs-lookup"><span data-stu-id="32ca6-374">The query would resemble:</span></span>

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer}
```
![IN 搜尋範例](./media/log-analytics-log-searches/oms-search-in02-revised.png)

<span data-ttu-id="32ca6-376">也請注意內部搜尋中使用的時間篩選條件，因為「系統更新評估」每隔 24 小時就會擷取所有電腦的快照。</span><span class="sxs-lookup"><span data-stu-id="32ca6-376">Also notice the time filter used in the inner search because the System Update Assessment takes a snapshot of all computers every 24 hours.</span></span> <span data-ttu-id="32ca6-377">您可以藉由只搜尋一天來讓內部查詢變得更輕巧精確。</span><span class="sxs-lookup"><span data-stu-id="32ca6-377">You can make the inner query more lightweight and precise by only searching for a day.</span></span> <span data-ttu-id="32ca6-378">外部搜尋則會使用使用者介面中的時間選項，擷取過去 7 天的事件。</span><span class="sxs-lookup"><span data-stu-id="32ca6-378">The outer search instead uses the time selection in the user interface, retrieving events from the last 7 days.</span></span> <span data-ttu-id="32ca6-379">如需時間運算子的詳細資訊，請參閱 [布林運算子](#boolean-operators) 。</span><span class="sxs-lookup"><span data-stu-id="32ca6-379">See [Boolean operators](#boolean-operators) for more information about time operators.</span></span>

<span data-ttu-id="32ca6-380">由於您實際上只會使用內部搜尋結果做為外部搜尋的篩選條件值，因此您仍然可以在外部搜尋中套用命令。</span><span class="sxs-lookup"><span data-stu-id="32ca6-380">Because you really only use the results of the inner search as a filter value for the outer one, you can still apply commands in the outer search.</span></span> <span data-ttu-id="32ca6-381">例如，您仍然可以使用另一個 measure 命令來分組上述事件︰</span><span class="sxs-lookup"><span data-stu-id="32ca6-381">For example, you can still group the above events with another measure command:</span></span>

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer} | measure count() by Source
```

![IN 搜尋範例](./media/log-analytics-log-searches/oms-search-in03-revised.png)

<span data-ttu-id="32ca6-383">一般而言，因為 Log Analytics 對內部查詢設定了服務端逾時，因此您會希望它快速執行，並且您也會希望它傳回少量的結果。</span><span class="sxs-lookup"><span data-stu-id="32ca6-383">Generally, you want your inner query to execute quickly because Log Analytics has service-side timeouts for it and also to return a small amount of results.</span></span> <span data-ttu-id="32ca6-384">如果內部查詢傳回較多個結果，結果清單會遭到截斷，這可能會導致外部搜尋傳回不正確的結果。</span><span class="sxs-lookup"><span data-stu-id="32ca6-384">If the inner query returns more results, the result list gets truncated, which could potentially cause the outer search to return incorrect results.</span></span>

<span data-ttu-id="32ca6-385">另一個規則是，內部搜尋目前需要提供「彙總的」  結果。</span><span class="sxs-lookup"><span data-stu-id="32ca6-385">Another rule is that the inner search currently needs to provide *aggregated* results.</span></span> <span data-ttu-id="32ca6-386">換句話說，它必須包含「measure」  命令；您目前無法將未經處理的結果送到外部搜尋。</span><span class="sxs-lookup"><span data-stu-id="32ca6-386">In other words, it must contain a *measure* command; you cannot currently feed raw results into an outer search.</span></span>

<span data-ttu-id="32ca6-387">此外，只能有一個 IN 運算子，而且它必須是查詢中的最後一個篩選條件。</span><span class="sxs-lookup"><span data-stu-id="32ca6-387">Also, there can be only one IN operator and it must be the last filter in the query.</span></span> <span data-ttu-id="32ca6-388">多個 IN 運算子無法使用 OR 來連接，這基本上會防止執行多個子搜尋︰重點是，每個外部搜尋只能有一個子搜尋/內部搜尋。</span><span class="sxs-lookup"><span data-stu-id="32ca6-388">Multiple IN operators cannot be OR’d – this essentially prevents running multiple subsearches: the important point is that only one sub/inner search is possible for each outer search.</span></span>

<span data-ttu-id="32ca6-389">即使有這些限制，IN 仍可實現許多類型的相互關聯搜尋，並可讓您定義類似群組的物件，例如電腦、使用者或檔案，無論您的資料欄位中包含什麼內容。</span><span class="sxs-lookup"><span data-stu-id="32ca6-389">Even with these limits, IN enables many kinds of correlated searches, and allows you to define something similar to groups such as computers, users, or files – whatever the fields in your data contain.</span></span> <span data-ttu-id="32ca6-390">以下還有其他範例：</span><span class="sxs-lookup"><span data-stu-id="32ca6-390">Here are more examples:</span></span>

<span data-ttu-id="32ca6-391">**已停用自動更新設定的電腦中遺失的所有更新**</span><span class="sxs-lookup"><span data-stu-id="32ca6-391">**All updates missing from computers where Automatic Update setting is disabled**</span></span>

```
Type=Update UpdateState=Needed Optional=false Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual | measure count() by Computer} | measure count() by KBID
```

<span data-ttu-id="32ca6-392">**執行 SQL Server (即 SQL 評估執行所在) 的電腦中的所有錯誤事件**</span><span class="sxs-lookup"><span data-stu-id="32ca6-392">**All error events from computers running SQL Server (=where SQL Assessment has run)**</span></span>

```
Type=Event EventLevelName=error Computer IN {Type=SQLAssessmentRecommendation | measure count() by Computer}
```

<span data-ttu-id="32ca6-393">**屬於網域控制站 (即 AD 評估執行所在) 的電腦中的所有安全性事件**</span><span class="sxs-lookup"><span data-stu-id="32ca6-393">**All security events from computers that are Domain Controllers (=where AD Assessment has run)**</span></span>

```
Type=SecurityEvent Computer IN { Type=ADAssessmentRecommendation | measure count() by Computer }
```

<span data-ttu-id="32ca6-394">**帳戶 BACONLAND\jochan 已登入的電腦上，還有其他哪些帳戶已登入？**</span><span class="sxs-lookup"><span data-stu-id="32ca6-394">**Which other accounts have logged on to the same computers where account BACONLAND\jochan has logged on?**</span></span>

```
Type=SecurityEvent EventID=4624   Account!="BACONLAND\\jochan" Computer IN { Type=SecurityEvent EventID=4624   Account="BACONLAND\\jochan" | measure count() by Computer } | measure count() by Account
```

## <a name="use-the-distinct-command"></a><span data-ttu-id="32ca6-395">使用 distinct 命令</span><span class="sxs-lookup"><span data-stu-id="32ca6-395">Use the distinct command</span></span>
<span data-ttu-id="32ca6-396">正如其名，此命令會提供欄位的相異值清單。</span><span class="sxs-lookup"><span data-stu-id="32ca6-396">As the name suggests, this command provides a list of distinct values for a field.</span></span> <span data-ttu-id="32ca6-397">它出乎意料地簡單，但卻相當實用。</span><span class="sxs-lookup"><span data-stu-id="32ca6-397">It's surprisingly simple but quite useful.</span></span> <span data-ttu-id="32ca6-398">使用 measure count() 命令也可達到相同結果，如下所示。</span><span class="sxs-lookup"><span data-stu-id="32ca6-398">The same could be achieved with measure count() command as well, as shown below.</span></span>

```
Type=Event | Measure count() by Computer
```

![DISTINCT 搜尋命令範例](./media/log-analytics-log-searches/oms-search-distinct01-revised.png)

<span data-ttu-id="32ca6-400">不過，如果您只想要相異值清單而不要具有那些值的文件計數，則 DISTINCT 可提供更清晰易懂的輸出和更短的語法，如下所示。</span><span class="sxs-lookup"><span data-stu-id="32ca6-400">However, if all you're interested in is just a list of distinct values and not the count of documents that have that values, then DISTINCT can provide cleaner and easier to read output, and shorter syntax, as shown below.</span></span>

```
Type=Event | Distinct Computer
```
![DISTINCT 搜尋命令範例](./media/log-analytics-log-searches/oms-search-distinct02-revised.png)

## <a name="use-the-countdistinct-function-with-the-measure-command"></a><span data-ttu-id="32ca6-402">搭配使用 countdistinct 函數與 measure 命令</span><span class="sxs-lookup"><span data-stu-id="32ca6-402">Use the countdistinct function with the measure command</span></span>
<span data-ttu-id="32ca6-403">countdistinct 函數會計算每個群組內的相異值數目。</span><span class="sxs-lookup"><span data-stu-id="32ca6-403">The countdistinct function counts the number of distinct values within each group.</span></span> <span data-ttu-id="32ca6-404">例如，它可以用來計算針對每個類型報告的唯一電腦數目︰</span><span class="sxs-lookup"><span data-stu-id="32ca6-404">For example, it could be used to count the number of unique computers reporting for each Type:</span></span>

```
* | measure countdistinct(Computer) by Type
```

![OMS-countdistinct](./media/log-analytics-log-searches/oms-countdistinct.png)

## <a name="use-the-measure-interval-command"></a><span data-ttu-id="32ca6-406">使用 measure interval 命令</span><span class="sxs-lookup"><span data-stu-id="32ca6-406">Use the measure interval command</span></span>
<span data-ttu-id="32ca6-407">透過接近即時的效能資料收集，您可以在 Log Analytics 中收集和視覺化任何效能計數器。</span><span class="sxs-lookup"><span data-stu-id="32ca6-407">With near real-time performance data collection, you can collect and visualize any performance counter in Log Analytics.</span></span> <span data-ttu-id="32ca6-408">只要輸入查詢 **Type:Perf** ，就會根據 Log Analytics 環境中的計數器和伺服器數目傳回數千個度量圖形。</span><span class="sxs-lookup"><span data-stu-id="32ca6-408">Simply entering the query **Type:Perf** will return thousands of metric graphs based on the number of counters and servers in your Log Analytics environment.</span></span> <span data-ttu-id="32ca6-409">透過隨選的度量彙總，您可以在較高的層級查看環境中的整體度量，並視需要深入了解更細微的資料。</span><span class="sxs-lookup"><span data-stu-id="32ca6-409">With on-demand metric aggregation, you can look at the overall metrics in your environment at a high level, and deep dive into more granular data as you need to.</span></span>

<span data-ttu-id="32ca6-410">例如，假設您想要知道您所有電腦的平均 CPU。</span><span class="sxs-lookup"><span data-stu-id="32ca6-410">Let’s say that you want to know what is the average CPU across all your computers.</span></span> <span data-ttu-id="32ca6-411">查看每一部電腦的平均 CPU 可能沒什麼幫助，因為結果可能會變得平順。</span><span class="sxs-lookup"><span data-stu-id="32ca6-411">Looking at the average CPU for every computer might not be helpful because results may get smoothed out.</span></span> <span data-ttu-id="32ca6-412">若要深入查看更多細節，您可以彙總較小時間區塊的結果，並深入查看跨越不同維度的時間序列。</span><span class="sxs-lookup"><span data-stu-id="32ca6-412">To look into more details, you can aggregate your result in a smaller time window chunks, and look into a time series across different dimensions.</span></span> <span data-ttu-id="32ca6-413">例如，您可以跨所有電腦執行每小時的平均 CPU 使用量，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="32ca6-413">For example, you can perform the hourly average of CPU usage across all your computers as follows:</span></span>

```
Type:Perf CounterName="% Processor Time" InstanceName="_Total" | measure avg(CounterValue) by Computer Interval 1HOUR
```

![測量平均間隔](./media/log-analytics-log-searches/oms-measure-avg-interval.png)

<span data-ttu-id="32ca6-415">根據預設，這些結果會顯示在多數列的互動式折線圖中。</span><span class="sxs-lookup"><span data-stu-id="32ca6-415">By default these results will be displayed in a multi-series interactive line chart.</span></span>  <span data-ttu-id="32ca6-416">這個圖表支援數列切換 (透過 y 軸重新調整)、縮放和暫留。</span><span class="sxs-lookup"><span data-stu-id="32ca6-416">This chart supports series toggling (with y-axis rescaling), zooming, and hovering.</span></span>  <span data-ttu-id="32ca6-417">如有必要，資料表顯示選項仍可供檢視原始資料。</span><span class="sxs-lookup"><span data-stu-id="32ca6-417">The table display option is still available for viewing the raw data if necessary.</span></span>

<span data-ttu-id="32ca6-418">您也可以根據其他欄位分組。</span><span class="sxs-lookup"><span data-stu-id="32ca6-418">You can also group by other fields.</span></span> <span data-ttu-id="32ca6-419">在此範例中，我要查看某個特定電腦的所有 % 計數器，我想要知道每個計數器每小時的第 70 個百分位數為何︰</span><span class="sxs-lookup"><span data-stu-id="32ca6-419">In this example, I am looking at all the % counters for one specific computer, and I want to know what is the hourly 70 percentiles of every counter:</span></span>

```
Type:Perf Computer=beefpatty4 CounterName=%* InstanceName=_Total | measure percentile70(CounterValue) by CounterName Interval 1HOUR
```
<span data-ttu-id="32ca6-420">請注意一件事，這些查詢並不限於效能計數器。</span><span class="sxs-lookup"><span data-stu-id="32ca6-420">One thing to note is that these queries are not limited to performance counters.</span></span> <span data-ttu-id="32ca6-421">您可以將它們套用至任何度量。</span><span class="sxs-lookup"><span data-stu-id="32ca6-421">You can apply them to any metric.</span></span> <span data-ttu-id="32ca6-422">在此範例中，我要查看 W3C IIS 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="32ca6-422">In this example, I’m looking at W3C IIS logs.</span></span> <span data-ttu-id="32ca6-423">我想要知道以 5 分鐘做為間隔時，它最多需要花多少時間來處理每個要求︰</span><span class="sxs-lookup"><span data-stu-id="32ca6-423">I want to know what is the maximum time it takes over a 5-minute interval for processing each request:</span></span>

```
Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES
```

### <a name="use-multiple-aggregates-in-one-query"></a><span data-ttu-id="32ca6-424">在單一查詢中使用多個彙總</span><span class="sxs-lookup"><span data-stu-id="32ca6-424">Use multiple aggregates in one query</span></span>
<span data-ttu-id="32ca6-425">您可以在 measure 命令中指定多個彙總子句。</span><span class="sxs-lookup"><span data-stu-id="32ca6-425">You can specify multiple aggregate clauses in a measure command.</span></span>  <span data-ttu-id="32ca6-426">每個子句皆可獨立給予別名。</span><span class="sxs-lookup"><span data-stu-id="32ca6-426">Each one can be aliased independently.</span></span>  <span data-ttu-id="32ca6-427">如果未給予別名，所產生的欄位名稱將會是所使用的彙總函數 (亦即，若使用 avg(CounterValue) 函數，則名稱為 "avg(CounterValue)")。</span><span class="sxs-lookup"><span data-stu-id="32ca6-427">If it is not given an alias the resulting field name will be the aggregate function that was used (i.e. "avg(CounterValue)" for avg(CounterValue)).</span></span>

 ```
Type=WireData | measure avg(ReceivedBytes), avg(SentBytes) by Direction interval 1hour
```
![OMS-multiaggregates1](./media/log-analytics-log-searches/oms-multiaggregates1.png)

<span data-ttu-id="32ca6-429">以下是另一個範例︰</span><span class="sxs-lookup"><span data-stu-id="32ca6-429">Here is another example:</span></span>

 ```
* | measure countdistinct(Computer) as Computers, count() as TotalRecords by Type
```


## <a name="next-steps"></a><span data-ttu-id="32ca6-430">後續步驟</span><span class="sxs-lookup"><span data-stu-id="32ca6-430">Next steps</span></span>
<span data-ttu-id="32ca6-431">如需關於記錄檔搜尋的其他資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="32ca6-431">For additional information about log searches, see:</span></span>

* <span data-ttu-id="32ca6-432">使用 [Log Analytics 中的自訂欄位](log-analytics-custom-fields.md) 來延伸記錄檔搜尋。</span><span class="sxs-lookup"><span data-stu-id="32ca6-432">Use [Custom fields in Log Analytics](log-analytics-custom-fields.md) to extend log searches.</span></span>
* <span data-ttu-id="32ca6-433">檢閱 [Log Analytics 記錄檔搜尋參考資料](log-analytics-search-reference.md) ，以檢視 Log Analytics 中提供的所有搜尋欄位和 Facet。</span><span class="sxs-lookup"><span data-stu-id="32ca6-433">Review the [Log Analytics log search reference](log-analytics-search-reference.md) to view all of the search fields and facets available in Log Analytics.</span></span>
