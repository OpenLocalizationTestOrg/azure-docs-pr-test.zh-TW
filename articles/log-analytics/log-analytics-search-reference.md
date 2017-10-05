---
title: "Azure Log Analytics 搜尋參考 | Microsoft Docs"
description: "Log Analytics 搜尋參考描述搜尋語言，並且提供一般查詢語法選項，您可以在搜尋資料及篩選運算式時用來幫助您縮小搜尋範圍。"
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: 402615a2-bed0-4831-ba69-53be49059718
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fc9c9b0a6292dab256997a86a6db16367fc48cd3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="log-analytics-search-reference"></a><span data-ttu-id="17c4d-103">Log Analytics 搜尋參考</span><span class="sxs-lookup"><span data-stu-id="17c4d-103">Log Analytics search reference</span></span>

>[!NOTE]
> <span data-ttu-id="17c4d-104">本文說明在 Azure Log Analytics 中使用目前查詢語言的記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="17c4d-104">This article describes log searches using the current query language in Log Analytics.</span></span>  <span data-ttu-id="17c4d-105">如果您的工作區已升級為[新的 Log Analytics 查詢語言](log-analytics-log-search-upgrade.md)，則您應該參閱[新語言的語言參考](https://go.microsoft.com/fwlink/?linkid=856079)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-105">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should refer to [the language reference for the new language](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>

<span data-ttu-id="17c4d-106">下列關於搜尋語言的參考章節描述一般查詢語法選項，您可以在搜尋資料及篩選運算式時用來幫助您縮小搜尋範圍。</span><span class="sxs-lookup"><span data-stu-id="17c4d-106">The following reference section about search language describes the general query syntax options you can use when searching for data and filtering expressions to help narrow your search.</span></span> <span data-ttu-id="17c4d-107">它也會描述您可以用來在已擷取的資料上採取動作的命令。</span><span class="sxs-lookup"><span data-stu-id="17c4d-107">It also describes commands that you can use to take action on the data retrieved.</span></span>

<span data-ttu-id="17c4d-108">您可以在[搜尋欄位和 Facet 參考](#search-field-and-facet-reference)小節中閱讀搜尋中傳回的欄位，以及協助您深入探討相似資料類別的 Facet。</span><span class="sxs-lookup"><span data-stu-id="17c4d-108">You can read about the fields returned in searches, and the facets that help you discover more about similar categories of data, in the [Search field and facet reference section](#search-field-and-facet-reference).</span></span>

## <a name="general-query-syntax"></a><span data-ttu-id="17c4d-109">一般查詢語法</span><span class="sxs-lookup"><span data-stu-id="17c4d-109">General query syntax</span></span>
<span data-ttu-id="17c4d-110">一般查詢的語法如下︰</span><span class="sxs-lookup"><span data-stu-id="17c4d-110">The syntax for general querying is as follows:</span></span>

```
filterExpression | command1 | command2 …
```

<span data-ttu-id="17c4d-111">篩選運算式 (`filterExpression`) 會定義查詢的 "where" 條件。</span><span class="sxs-lookup"><span data-stu-id="17c4d-111">The filter expression (`filterExpression`) defines the "where" condition for the query.</span></span> <span data-ttu-id="17c4d-112">命令會套用至查詢所傳回的結果。</span><span class="sxs-lookup"><span data-stu-id="17c4d-112">The commands apply to the results returned by the query.</span></span> <span data-ttu-id="17c4d-113">多個命令必須以縱線字元 ( | ) 分隔。</span><span class="sxs-lookup"><span data-stu-id="17c4d-113">Multiple commands must be separated by the pipe character ( | ).</span></span>

### <a name="general-syntax-examples"></a><span data-ttu-id="17c4d-114">一般語法範例</span><span class="sxs-lookup"><span data-stu-id="17c4d-114">General syntax examples</span></span>
<span data-ttu-id="17c4d-115">範例：</span><span class="sxs-lookup"><span data-stu-id="17c4d-115">Examples:</span></span>

```
system
```

<span data-ttu-id="17c4d-116">此查詢會傳回在已編製索引的任何欄位中進行全文檢索或詞彙搜尋時包含 system 這個單字的結果。</span><span class="sxs-lookup"><span data-stu-id="17c4d-116">This query returns results that contain the word *system* in any field that has been indexed for full text or terms searching.</span></span>

> [!NOTE]
> <span data-ttu-id="17c4d-117">並非所有的欄位都以此方式編製索引，不過最常見的文字欄位 (例如描述和名稱) 通常都是。</span><span class="sxs-lookup"><span data-stu-id="17c4d-117">Not all fields are indexed this way, but the most common textual fields (such as descriptions and names) usually are.</span></span>
>
>

```
system error
```

<span data-ttu-id="17c4d-118">此查詢會傳回包含 system 和 error 單字的結果。</span><span class="sxs-lookup"><span data-stu-id="17c4d-118">This query returns results that contain the words *system* and *error*.</span></span>

```
system error | sort ManagementGroupName, TimeGenerated desc | top 10
```

<span data-ttu-id="17c4d-119">此查詢會傳回包含 system 和 error 單字的結果。</span><span class="sxs-lookup"><span data-stu-id="17c4d-119">This query returns results that contain the words *system* and *error*.</span></span> <span data-ttu-id="17c4d-120">然後會依據 ManagementGroupName 欄位 (依遞增順序)，再依據 TimeGenerated 欄位 (依遞減順序) 排序結果。</span><span class="sxs-lookup"><span data-stu-id="17c4d-120">It then sorts the results by the *ManagementGroupName* field (in ascending order), and then by the *TimeGenerated* field (in descending order).</span></span> <span data-ttu-id="17c4d-121">它只會採用前 10 個結果。</span><span class="sxs-lookup"><span data-stu-id="17c4d-121">It takes only the first 10 results.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="17c4d-122">所有的欄位名稱以及字串和文字欄位的值都會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="17c4d-122">All the field names and the values for the string and text fields are case sensitive.</span></span>
>
>

## <a name="filter-expressions"></a><span data-ttu-id="17c4d-123">篩選運算式</span><span class="sxs-lookup"><span data-stu-id="17c4d-123">Filter expressions</span></span>
<span data-ttu-id="17c4d-124">下列小節說明篩選運算式。</span><span class="sxs-lookup"><span data-stu-id="17c4d-124">The following subsections explain the filter expressions.</span></span>

### <a name="string-literals"></a><span data-ttu-id="17c4d-125">字串常值</span><span class="sxs-lookup"><span data-stu-id="17c4d-125">String literals</span></span>
<span data-ttu-id="17c4d-126">字串常值是未經由剖析器辨識為關鍵字或預先定義資料類型 (例如，數字或日期) 的任何字串。</span><span class="sxs-lookup"><span data-stu-id="17c4d-126">A string literal is any string that is not recognized by the parser as a keyword or a predefined data type (for example, a number or date).</span></span>

<span data-ttu-id="17c4d-127">範例：</span><span class="sxs-lookup"><span data-stu-id="17c4d-127">Examples:</span></span>

```
These all are string literals
```

<span data-ttu-id="17c4d-128">此查詢會搜尋包含五個字全都出現的結果。</span><span class="sxs-lookup"><span data-stu-id="17c4d-128">This query searches for results that contain occurrences of all five words.</span></span> <span data-ttu-id="17c4d-129">若要執行複雜的字串搜尋，請將字串常值以引號括起來。</span><span class="sxs-lookup"><span data-stu-id="17c4d-129">To perform a complex string search, enclose the string literal in quotation marks.</span></span> <span data-ttu-id="17c4d-130">例如：</span><span class="sxs-lookup"><span data-stu-id="17c4d-130">For example:</span></span>

```
"Windows Server"
```

<span data-ttu-id="17c4d-131">這只會傳回結果為 Windows Server 的完全相符項目。</span><span class="sxs-lookup"><span data-stu-id="17c4d-131">This only returns results with exact matches for *Windows Server*.</span></span>

### <a name="numbers"></a><span data-ttu-id="17c4d-132">數字</span><span class="sxs-lookup"><span data-stu-id="17c4d-132">Numbers</span></span>
<span data-ttu-id="17c4d-133">剖析器支援數值欄位的十進位整數和浮點數語法。</span><span class="sxs-lookup"><span data-stu-id="17c4d-133">The parser supports the decimal integer and floating-point number syntax for numerical fields.</span></span>

<span data-ttu-id="17c4d-134">範例：</span><span class="sxs-lookup"><span data-stu-id="17c4d-134">Examples:</span></span>

```
Type:Perf 0.5
```

```
HTTP 500
```

### <a name="dates-and-times"></a><span data-ttu-id="17c4d-135">日期和時間</span><span class="sxs-lookup"><span data-stu-id="17c4d-135">Dates and times</span></span>
<span data-ttu-id="17c4d-136">系統中的每個資料片段都有 *TimeGenerated* 屬性，代表記錄的原始日期和時間。</span><span class="sxs-lookup"><span data-stu-id="17c4d-136">Every piece of data in the system has a *TimeGenerated* property, which represents the original date and time of the record.</span></span> <span data-ttu-id="17c4d-137">某些資料類型可能另外有日期和時間欄位 (例如，*LastModified*)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-137">Some types of data can have additional date and time fields (for example, *LastModified*).</span></span>

<span data-ttu-id="17c4d-138">Azure Log Analytics 中的 [時間表/時間] 選取器會顯示經過一段時間的結果分佈 (根據目前執行的查詢)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-138">The timeline **Chart/Time** selector in Azure Log Analytics shows a distribution of results over time (according to the current query being run).</span></span> <span data-ttu-id="17c4d-139">這是根據 *TimeGenerated* 欄位。</span><span class="sxs-lookup"><span data-stu-id="17c4d-139">This is based on the *TimeGenerated* field.</span></span> <span data-ttu-id="17c4d-140">日期和時間欄位具有特定字串格式，可以在查詢中用來將查詢限制在特定時間範圍內。</span><span class="sxs-lookup"><span data-stu-id="17c4d-140">Date and time fields have a specific string format that can be used in queries to restrict the query to a particular timeframe.</span></span> <span data-ttu-id="17c4d-141">您也可以使用語法來參考相對的時間間隔 (例如，「3 天前和 2 小時前之間」)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-141">You can also use syntax to refer to relative time intervals (for example, "between 3 days ago and 2 hours ago").</span></span>

<span data-ttu-id="17c4d-142">以下是有效形式的日期和時間語法：</span><span class="sxs-lookup"><span data-stu-id="17c4d-142">The following are valid forms of syntax for dates and times:</span></span>

```
yyyy-mm-ddThh:mm:ss.dddZ
```

```
yyyy-mm-ddThh:mm:ss.ddd
```

```
yyyy-mm-ddThh:mm:ss
```

```
yyyy-mm-ddThh:mm:ss
```

```
yyyy-mm-ddThh:mm
```

```
yyyy-mm-dd
```


<span data-ttu-id="17c4d-143">例如：</span><span class="sxs-lookup"><span data-stu-id="17c4d-143">For example:</span></span>

```
TimeGenerated:2013-10-01T12:20
```

<span data-ttu-id="17c4d-144">前一個命令只會傳回 *TimeGenerated* 值剛好等於 2013 年 10 月 1 日 12:20 的記錄。</span><span class="sxs-lookup"><span data-stu-id="17c4d-144">The previous command returns only records with a *TimeGenerated* value of exactly 12:20 on October 1, 2013.</span></span>

<span data-ttu-id="17c4d-145">剖析器也支援助憶鍵的日期/時間值，NOW。</span><span class="sxs-lookup"><span data-stu-id="17c4d-145">The parser also supports the mnemonic Date/Time value, NOW.</span></span> <span data-ttu-id="17c4d-146">(這也不太可能產生任何結果，因為資料無法這麼快速地通過系統)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-146">(It is unlikely that this will yield any results, because data doesn’t make it through the system that fast.)</span></span>

<span data-ttu-id="17c4d-147">這些範例是用於相對與絕對日期的建置組塊。</span><span class="sxs-lookup"><span data-stu-id="17c4d-147">These examples are building blocks to use for relative and absolute dates.</span></span> <span data-ttu-id="17c4d-148">在接下來的三個子節中，您會透過使用相對日期範圍的範例，看到如何在更進階的篩選條件中使用它們。</span><span class="sxs-lookup"><span data-stu-id="17c4d-148">In the next three subsections, you'll see how to use them in more advanced filters, with examples that use relative date ranges.</span></span>

### <a name="datetime-math"></a><span data-ttu-id="17c4d-149">日期/時間數學</span><span class="sxs-lookup"><span data-stu-id="17c4d-149">Date/Time math</span></span>
<span data-ttu-id="17c4d-150">使用日期/時間數學運算子，透過簡單的計算位移或四捨五入日期/時間值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-150">Use the Date/Time math operators to offset or round the Date/Time value, by using simple Date/Time calculations.</span></span>

<span data-ttu-id="17c4d-151">語法：</span><span class="sxs-lookup"><span data-stu-id="17c4d-151">Syntax:</span></span>

```
datetime/unit
```

```
datetime[+|-]count unit
```

| <span data-ttu-id="17c4d-152">運算子</span><span class="sxs-lookup"><span data-stu-id="17c4d-152">Operator</span></span> | <span data-ttu-id="17c4d-153">說明</span><span class="sxs-lookup"><span data-stu-id="17c4d-153">Description</span></span> |
| --- | --- |
| / |<span data-ttu-id="17c4d-154">將日期/時間四捨五入到指定的單位。</span><span class="sxs-lookup"><span data-stu-id="17c4d-154">Rounds Date/Time to the specified unit.</span></span> <span data-ttu-id="17c4d-155">例如，NOW/DAY 會將目前的日期/時間四捨五入至目前日期的午夜。</span><span class="sxs-lookup"><span data-stu-id="17c4d-155">For example, NOW/DAY rounds the current Date/Time to midnight of the current day.</span></span> |
| <span data-ttu-id="17c4d-156">+ 或 -</span><span class="sxs-lookup"><span data-stu-id="17c4d-156">+ or -</span></span> |<span data-ttu-id="17c4d-157">將日期/時間位移指定的單位數。</span><span class="sxs-lookup"><span data-stu-id="17c4d-157">Offsets Date/Time by the specified number of units.</span></span> <span data-ttu-id="17c4d-158">例如，NOW+1HOUR 會將目前日期/時間位移晚一個小時。</span><span class="sxs-lookup"><span data-stu-id="17c4d-158">For example, NOW+1HOUR offsets the current Date/Time by one hour ahead.</span></span> <span data-ttu-id="17c4d-159">2013-10-01T12:00-10DAYS 會將日期值位移回 10 天。</span><span class="sxs-lookup"><span data-stu-id="17c4d-159">2013-10-01T12:00-10DAYS offsets the Date value back by 10 days.</span></span> |

<span data-ttu-id="17c4d-160">您可以將日期/時間數學運算子鏈結在一起。</span><span class="sxs-lookup"><span data-stu-id="17c4d-160">You can chain the Date/Time math operators together.</span></span> <span data-ttu-id="17c4d-161">例如：</span><span class="sxs-lookup"><span data-stu-id="17c4d-161">For example:</span></span>

```
NOW+1HOUR-10MONTHS/MINUTE
```

<span data-ttu-id="17c4d-162">下表列出受支援的日期/時間單位。</span><span class="sxs-lookup"><span data-stu-id="17c4d-162">The following table lists the supported Date/Time units.</span></span>

| <span data-ttu-id="17c4d-163">日期/時間單位</span><span class="sxs-lookup"><span data-stu-id="17c4d-163">Date/Time unit</span></span> | <span data-ttu-id="17c4d-164">說明</span><span class="sxs-lookup"><span data-stu-id="17c4d-164">Description</span></span> |
| --- | --- |
| <span data-ttu-id="17c4d-165">YEAR, YEARS</span><span class="sxs-lookup"><span data-stu-id="17c4d-165">YEAR, YEARS</span></span> |<span data-ttu-id="17c4d-166">四捨五入為目前的年份，或位移指定的年數。</span><span class="sxs-lookup"><span data-stu-id="17c4d-166">Rounds to current year, or offsets by the specified number of years.</span></span> |
| <span data-ttu-id="17c4d-167">MONTH, MONTHS</span><span class="sxs-lookup"><span data-stu-id="17c4d-167">MONTH, MONTHS</span></span> |<span data-ttu-id="17c4d-168">四捨五入為目前的月份，或位移指定的月數。</span><span class="sxs-lookup"><span data-stu-id="17c4d-168">Rounds to current month, or offsets by the specified number of months.</span></span> |
| <span data-ttu-id="17c4d-169">DAY, DAYS, DATE</span><span class="sxs-lookup"><span data-stu-id="17c4d-169">DAY, DAYS, DATE</span></span> |<span data-ttu-id="17c4d-170">四捨五入為目前的月份日期，或位移指定的天數。</span><span class="sxs-lookup"><span data-stu-id="17c4d-170">Rounds to current day of the month, or offsets by the specified number of days.</span></span> |
| <span data-ttu-id="17c4d-171">HOUR, HOURS</span><span class="sxs-lookup"><span data-stu-id="17c4d-171">HOUR, HOURS</span></span> |<span data-ttu-id="17c4d-172">四捨五入為目前的小時，或位移指定的小時數。</span><span class="sxs-lookup"><span data-stu-id="17c4d-172">Rounds to current hour, or offsets by the specified number of hours.</span></span> |
| <span data-ttu-id="17c4d-173">MINUTE, MINUTES</span><span class="sxs-lookup"><span data-stu-id="17c4d-173">MINUTE, MINUTES</span></span> |<span data-ttu-id="17c4d-174">四捨五入為目前的分鐘，或位移指定的分鐘數。</span><span class="sxs-lookup"><span data-stu-id="17c4d-174">Rounds to current minute, or offsets by the specified number of minutes.</span></span> |
| <span data-ttu-id="17c4d-175">SECOND, SECONDS</span><span class="sxs-lookup"><span data-stu-id="17c4d-175">SECOND, SECONDS</span></span> |<span data-ttu-id="17c4d-176">四捨五入為目前的秒，或位移指定的秒數。</span><span class="sxs-lookup"><span data-stu-id="17c4d-176">Rounds to current second, or offsets by the specified number of seconds.</span></span> |
| <span data-ttu-id="17c4d-177">MILLISECOND, MILLISECONDS, MILLI, MILLIS</span><span class="sxs-lookup"><span data-stu-id="17c4d-177">MILLISECOND, MILLISECONDS, MILLI, MILLIS</span></span> |<span data-ttu-id="17c4d-178">四捨五入為目前的毫秒，或位移指定的毫秒數。</span><span class="sxs-lookup"><span data-stu-id="17c4d-178">Rounds to current millisecond, or offsets by the specified number of milliseconds.</span></span> |

### <a name="field-facets"></a><span data-ttu-id="17c4d-179">欄位 facet</span><span class="sxs-lookup"><span data-stu-id="17c4d-179">Field facets</span></span>
<span data-ttu-id="17c4d-180">使用欄位 Facet，您可以指定特定欄位的搜尋條件及其實際值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-180">By using field facets, you can specify the search condition for specific fields and their exact values.</span></span> <span data-ttu-id="17c4d-181">這與針對整個索引的各種詞彙撰寫「任意文字」查詢不同。</span><span class="sxs-lookup"><span data-stu-id="17c4d-181">This differs from writing "free text" queries for various terms throughout the index.</span></span> <span data-ttu-id="17c4d-182">您已經在數個先前的範例中看過這項技術。</span><span class="sxs-lookup"><span data-stu-id="17c4d-182">You have already seen this technique in several previous examples.</span></span> <span data-ttu-id="17c4d-183">下列是更複雜的範例。</span><span class="sxs-lookup"><span data-stu-id="17c4d-183">The following are more complex examples.</span></span>

<span data-ttu-id="17c4d-184">**語法**</span><span class="sxs-lookup"><span data-stu-id="17c4d-184">**Syntax**</span></span>

```
field:value
```

```
field=value
```

<span data-ttu-id="17c4d-185">**說明**</span><span class="sxs-lookup"><span data-stu-id="17c4d-185">**Description**</span></span>

<span data-ttu-id="17c4d-186">搜尋特定值的欄位。</span><span class="sxs-lookup"><span data-stu-id="17c4d-186">Searches the field for the specific value.</span></span> <span data-ttu-id="17c4d-187">此值可以是字串常值、數字或日期和時間。</span><span class="sxs-lookup"><span data-stu-id="17c4d-187">The value can be a string literal, number, or date and time.</span></span>

<span data-ttu-id="17c4d-188">例如：</span><span class="sxs-lookup"><span data-stu-id="17c4d-188">For example:</span></span>

```
TimeGenerated:NOW
```

```
ObjectDisplayName:"server01.contoso.com"
```

```
SampleValue:0.3
```

<span data-ttu-id="17c4d-189">**語法**</span><span class="sxs-lookup"><span data-stu-id="17c4d-189">**Syntax**</span></span>

<span data-ttu-id="17c4d-190">field>value</span><span class="sxs-lookup"><span data-stu-id="17c4d-190">*field>value*</span></span>

<span data-ttu-id="17c4d-191">field<value</span><span class="sxs-lookup"><span data-stu-id="17c4d-191">*field<value*</span></span>

<span data-ttu-id="17c4d-192">field>=value</span><span class="sxs-lookup"><span data-stu-id="17c4d-192">*field>=value*</span></span>

<span data-ttu-id="17c4d-193">field<=value</span><span class="sxs-lookup"><span data-stu-id="17c4d-193">*field<=value*</span></span>

<span data-ttu-id="17c4d-194">*field!=value*</span><span class="sxs-lookup"><span data-stu-id="17c4d-194">*field!=value*</span></span>

<span data-ttu-id="17c4d-195">**說明**</span><span class="sxs-lookup"><span data-stu-id="17c4d-195">**Description**</span></span>

<span data-ttu-id="17c4d-196">提供比較。</span><span class="sxs-lookup"><span data-stu-id="17c4d-196">Provides comparisons.</span></span>

<span data-ttu-id="17c4d-197">例如：</span><span class="sxs-lookup"><span data-stu-id="17c4d-197">For example:</span></span>

```
TimeGenerated>NOW+2HOURS
```

<span data-ttu-id="17c4d-198">**語法**</span><span class="sxs-lookup"><span data-stu-id="17c4d-198">**Syntax**</span></span>

```
field:[from..to]
```

<span data-ttu-id="17c4d-199">**說明**</span><span class="sxs-lookup"><span data-stu-id="17c4d-199">**Description**</span></span>

<span data-ttu-id="17c4d-200">提供範圍面相化。</span><span class="sxs-lookup"><span data-stu-id="17c4d-200">Provides range faceting.</span></span>

<span data-ttu-id="17c4d-201">例如：</span><span class="sxs-lookup"><span data-stu-id="17c4d-201">For example:</span></span>

```
TimeGenerated:[NOW..NOW+1DAY]
```

```
SampleValue:[0..2]
```

### <a name="in"></a><span data-ttu-id="17c4d-202">IN</span><span class="sxs-lookup"><span data-stu-id="17c4d-202">IN</span></span>
<span data-ttu-id="17c4d-203">**IN** 關鍵字可讓您從值清單中選取。</span><span class="sxs-lookup"><span data-stu-id="17c4d-203">The **IN** keyword allows you to select from a list of values.</span></span> <span data-ttu-id="17c4d-204">根據您使用的語法，這可以是您所提供值的簡易清單或彙總值的清單。</span><span class="sxs-lookup"><span data-stu-id="17c4d-204">Depending on the syntax you use, this can be a simple list of values you provide, or a list of values from an aggregation.</span></span>

<span data-ttu-id="17c4d-205">語法 1：</span><span class="sxs-lookup"><span data-stu-id="17c4d-205">Syntax 1:</span></span>

```
field IN {value1,value2,value3,...}
```

<span data-ttu-id="17c4d-206">此語法可讓您在簡易清單中包含所有的值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-206">This syntax allows you to include all values in a simple list.</span></span>



<span data-ttu-id="17c4d-207">範例：</span><span class="sxs-lookup"><span data-stu-id="17c4d-207">Examples:</span></span>

```
EventID IN {1201,1204,1210}
```

```
Computer IN {"srv01.contoso.com","srv02.contoso.com"}
```

<span data-ttu-id="17c4d-208">語法 2：</span><span class="sxs-lookup"><span data-stu-id="17c4d-208">Syntax 2:</span></span>

```
(Outer query) (Field to use with inner query results) IN {Inner query | measure count() by (Field to send to outer query)} (rest  of outer query)  
```

<span data-ttu-id="17c4d-209">此語法可讓您建立彙總。</span><span class="sxs-lookup"><span data-stu-id="17c4d-209">This syntax allows you to create an aggregation.</span></span> <span data-ttu-id="17c4d-210">您可以將值清單從該彙總提供到另一個外部 (主要) 搜尋，這個搜尋會尋找具有那些值的事件。</span><span class="sxs-lookup"><span data-stu-id="17c4d-210">You can then feed the list of values from that aggregation into another outer (primary) search that looks for events with those value.</span></span> <span data-ttu-id="17c4d-211">若要這麼做，您必須以大括號括住內部搜尋，並使用 IN 運算子將其結果提供作為外部搜尋中欄位的可能值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-211">You do this by enclosing the inner search in braces, and feeding its results as possible values for a field in the outer search by using the IN operator.</span></span>

<span data-ttu-id="17c4d-212">內部查詢範例︰*目前遺漏安全性更新的電腦*，並使用下列彙總查詢：</span><span class="sxs-lookup"><span data-stu-id="17c4d-212">Inner query example: *computers currently missing security updates* with the following aggregation query:</span></span>

```
Type:Update Classification="Security Updates"  UpdateState=needed TimeGenerated>NOW-25HOURS | measure count() by Computer
```    

<span data-ttu-id="17c4d-213">尋找 *目前遺漏安全性更新之電腦的所有 Windows 事件* 的最後查詢與下列類似：</span><span class="sxs-lookup"><span data-stu-id="17c4d-213">The final query that finds *all Windows events for computers currently missing security updates* resembles the following:</span></span>

```
Type=Event Computer IN {Type:Update Classification="Security Updates"  UpdateState=needed TimeGenerated>NOW-25HOURS | measure count() by Computer}
```

### <a name="contains"></a><span data-ttu-id="17c4d-214">Contains</span><span class="sxs-lookup"><span data-stu-id="17c4d-214">Contains</span></span>
<span data-ttu-id="17c4d-215">**Contains** 關鍵字可讓您篩選欄位包含所指定字串的記錄。</span><span class="sxs-lookup"><span data-stu-id="17c4d-215">The **Contains** keyword allows you to filter for records with a field that contains a specified string.</span></span> <span data-ttu-id="17c4d-216">這區分大小寫、僅適用於字串欄位，而且可能不包含任何逸出字元。</span><span class="sxs-lookup"><span data-stu-id="17c4d-216">This is case sensitive, works only with string fields, and may not include any escape characters.</span></span>

<span data-ttu-id="17c4d-217">語法：</span><span class="sxs-lookup"><span data-stu-id="17c4d-217">Syntax:</span></span>

```
field:contains("string")
```

<span data-ttu-id="17c4d-218">範例：</span><span class="sxs-lookup"><span data-stu-id="17c4d-218">Example:</span></span>

```
Type:contains("Event")
```

<span data-ttu-id="17c4d-219">這會傳回類型包含字串 "Event" 的記錄。</span><span class="sxs-lookup"><span data-stu-id="17c4d-219">This returns records with a type that contains the string "Event".</span></span> <span data-ttu-id="17c4d-220">範例包括 **Event**、**SecurityEvent** 和 **ServiceFabricOperationEvent**。</span><span class="sxs-lookup"><span data-stu-id="17c4d-220">Examples include **Event**, **SecurityEvent**, and **ServiceFabricOperationEvent**.</span></span>



### <a name="regular-expressions"></a><span data-ttu-id="17c4d-221">規則運算式</span><span class="sxs-lookup"><span data-stu-id="17c4d-221">Regular expressions</span></span>
<span data-ttu-id="17c4d-222">您可以使用 **Regex** 關鍵字，以規則運算式指定欄位的搜尋條件。</span><span class="sxs-lookup"><span data-stu-id="17c4d-222">You can specify a search condition for a field with a regular expression, by using the **Regex** keyword.</span></span> <span data-ttu-id="17c4d-223">如需您可以在規則運算式中使用之語法的完整描述，請參閱[使用規則運算式在 Log Analytics 中篩選記錄搜尋](log-analytics-log-searches-regex.md)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-223">For a complete description of the syntax you can use in regular expressions, see [Using regular expressions to filter log searches in Log Analytics](log-analytics-log-searches-regex.md).</span></span>

<span data-ttu-id="17c4d-224">語法：</span><span class="sxs-lookup"><span data-stu-id="17c4d-224">Syntax:</span></span>

```
field:Regex("Regular Expression")
```

<span data-ttu-id="17c4d-225">範例：</span><span class="sxs-lookup"><span data-stu-id="17c4d-225">Example:</span></span>

```
Computer:Regex("^C.*")
```

### <a name="logical-operators"></a><span data-ttu-id="17c4d-226">邏輯運算子</span><span class="sxs-lookup"><span data-stu-id="17c4d-226">Logical operators</span></span>
<span data-ttu-id="17c4d-227">查詢語言支援邏輯運算子 (AND、OR 和 NOT) 和它們的 C 樣式別名 (分別是 *&&*、*||* 和 *!*)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-227">The query languages support the logical operators (*AND*, *OR*, and *NOT*) and their C-style aliases (*&&*, *||*, and *!*, respectively).</span></span> <span data-ttu-id="17c4d-228">您可以使用括號來分組這些運算子。</span><span class="sxs-lookup"><span data-stu-id="17c4d-228">You can use parentheses to group these operators.</span></span>

<span data-ttu-id="17c4d-229">範例：</span><span class="sxs-lookup"><span data-stu-id="17c4d-229">Examples:</span></span>

```
system OR error

```

```
Type:Alert AND NOT(Severity:1 OR ObjectId:"8066bbc0-9ec8-ca83-1edc-6f30d4779bcb8066bbc0-9ec8-ca83-1edc-6f30d4779bcb")
```

<span data-ttu-id="17c4d-230">您可以略過最上層篩選引數的邏輯運算子。</span><span class="sxs-lookup"><span data-stu-id="17c4d-230">You can omit the logical operator for the top-level filter arguments.</span></span> <span data-ttu-id="17c4d-231">在此情況下，會假設採用 AND 運算子。</span><span class="sxs-lookup"><span data-stu-id="17c4d-231">In this case, the AND operator is assumed.</span></span>

| <span data-ttu-id="17c4d-232">篩選運算式</span><span class="sxs-lookup"><span data-stu-id="17c4d-232">Filter expression</span></span> | <span data-ttu-id="17c4d-233">相當於</span><span class="sxs-lookup"><span data-stu-id="17c4d-233">Equivalent to</span></span> |
| --- | --- |
| <span data-ttu-id="17c4d-234">system error</span><span class="sxs-lookup"><span data-stu-id="17c4d-234">system error</span></span> |<span data-ttu-id="17c4d-235">system AND error</span><span class="sxs-lookup"><span data-stu-id="17c4d-235">system AND error</span></span> |
| <span data-ttu-id="17c4d-236">system "Windows Server" OR Severity:1</span><span class="sxs-lookup"><span data-stu-id="17c4d-236">system "Windows Server" OR Severity:1</span></span> |<span data-ttu-id="17c4d-237">system AND ("Windows Server" OR Severity:1)</span><span class="sxs-lookup"><span data-stu-id="17c4d-237">system AND ("Windows Server" OR Severity:1)</span></span> |

### <a name="wildcarding"></a><span data-ttu-id="17c4d-238">萬用字元</span><span class="sxs-lookup"><span data-stu-id="17c4d-238">Wildcarding</span></span>
<span data-ttu-id="17c4d-239">查詢語言支援使用 ( \* ) 字元來代表查詢中值的一個或多個字元。</span><span class="sxs-lookup"><span data-stu-id="17c4d-239">The query language supports using the ( \* ) character to  represent one or more characters for a value in a query.</span></span>

<span data-ttu-id="17c4d-240">範例：</span><span class="sxs-lookup"><span data-stu-id="17c4d-240">Example:</span></span>

 <span data-ttu-id="17c4d-241">尋找名稱中有 "SQL" 的所有電腦 (例如 "Redmond SQL")。</span><span class="sxs-lookup"><span data-stu-id="17c4d-241">Find all computers with "SQL" in the name, such as "Redmond-SQL".</span></span>

```
Type=Event Computer=*SQL*
```

> [!NOTE]
> <span data-ttu-id="17c4d-242">此時，無法在引號內使用萬用字元。</span><span class="sxs-lookup"><span data-stu-id="17c4d-242">At this time, wildcards cannot be used within quotations.</span></span> <span data-ttu-id="17c4d-243">例如，訊息 `"*This text*"` 將考慮使用 (\*) 作為常值 (\*) 字元。</span><span class="sxs-lookup"><span data-stu-id="17c4d-243">For example, the message `"*This text*"` considers the (\*) used as a literal (\*) character.</span></span>


## <a name="commands"></a><span data-ttu-id="17c4d-244">命令</span><span class="sxs-lookup"><span data-stu-id="17c4d-244">Commands</span></span>


<span data-ttu-id="17c4d-245">命令會套用至查詢所傳回的結果。</span><span class="sxs-lookup"><span data-stu-id="17c4d-245">The commands apply to the results that are returned by the query.</span></span> <span data-ttu-id="17c4d-246">使用縱線字元 ( | ) 將命令套用至擷取的結果。</span><span class="sxs-lookup"><span data-stu-id="17c4d-246">Use the pipe character ( | ) to apply a command to the retrieved results.</span></span> <span data-ttu-id="17c4d-247">多個命令必須以縱線字元分隔。</span><span class="sxs-lookup"><span data-stu-id="17c4d-247">Multiple commands must be separated by the pipe character.</span></span>

> [!NOTE]
> <span data-ttu-id="17c4d-248">命令名稱可以大寫或小寫撰寫，與欄位名稱和資料不同。</span><span class="sxs-lookup"><span data-stu-id="17c4d-248">Command names can be written in upper case or lower case, unlike the field names and the data.</span></span>
>
>

### <a name="sort"></a><span data-ttu-id="17c4d-249">排序</span><span class="sxs-lookup"><span data-stu-id="17c4d-249">Sort</span></span>
<span data-ttu-id="17c4d-250">語法：</span><span class="sxs-lookup"><span data-stu-id="17c4d-250">Syntax:</span></span>

    sort field1 asc|desc, field2 asc|desc, …

<span data-ttu-id="17c4d-251">依特定欄位排序結果。</span><span class="sxs-lookup"><span data-stu-id="17c4d-251">Sorts the results by particular fields.</span></span> <span data-ttu-id="17c4d-252">依遞增或遞減順序排序結果的 asc/desc 尾碼是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="17c4d-252">The asc/desc suffix to sort the results in ascending or descending order is optional.</span></span> <span data-ttu-id="17c4d-253">如果將其省略，則會假設採用 *asc* 排序順序。</span><span class="sxs-lookup"><span data-stu-id="17c4d-253">If it is omitted, the *asc* sort order is assumed.</span></span> <span data-ttu-id="17c4d-254">在 **TimeGenerated** 位中，採用 *desc* 排序順序，因此預設會先傳回最新的結果。</span><span class="sxs-lookup"><span data-stu-id="17c4d-254">For the **TimeGenerated** field, *desc* sort order is assumed, so it returns the most recent results first by default.</span></span>

### <a name="toplimit"></a><span data-ttu-id="17c4d-255">Top/Limit</span><span class="sxs-lookup"><span data-stu-id="17c4d-255">Top/Limit</span></span>
<span data-ttu-id="17c4d-256">語法：</span><span class="sxs-lookup"><span data-stu-id="17c4d-256">Syntax:</span></span>

    top number


    limit number
<span data-ttu-id="17c4d-257">將回應限制為前 N 個結果。</span><span class="sxs-lookup"><span data-stu-id="17c4d-257">Limits the response to the top N results.</span></span>

<span data-ttu-id="17c4d-258">範例：</span><span class="sxs-lookup"><span data-stu-id="17c4d-258">Example:</span></span>

    Type:Alert errors detected | top 10

<span data-ttu-id="17c4d-259">傳回前 10 個比對結果。</span><span class="sxs-lookup"><span data-stu-id="17c4d-259">Returns the top 10 matching results.</span></span>

### <a name="skip"></a><span data-ttu-id="17c4d-260">Skip</span><span class="sxs-lookup"><span data-stu-id="17c4d-260">Skip</span></span>
<span data-ttu-id="17c4d-261">語法：</span><span class="sxs-lookup"><span data-stu-id="17c4d-261">Syntax:</span></span>

    skip number

<span data-ttu-id="17c4d-262">略過列出結果的數目。</span><span class="sxs-lookup"><span data-stu-id="17c4d-262">Skips the number of results listed.</span></span>

<span data-ttu-id="17c4d-263">範例：</span><span class="sxs-lookup"><span data-stu-id="17c4d-263">Example:</span></span>

    Type:Alert errors detected | top 10 | skip 200

<span data-ttu-id="17c4d-264">從結果 200 開始傳回 10 個比對結果。</span><span class="sxs-lookup"><span data-stu-id="17c4d-264">Returns top 10 matching results starting at result 200.</span></span>

### <a name="select"></a><span data-ttu-id="17c4d-265">選取</span><span class="sxs-lookup"><span data-stu-id="17c4d-265">Select</span></span>
<span data-ttu-id="17c4d-266">語法：</span><span class="sxs-lookup"><span data-stu-id="17c4d-266">Syntax:</span></span>

    select field1, field2, ...

<span data-ttu-id="17c4d-267">將結果限制為您選擇的欄位。</span><span class="sxs-lookup"><span data-stu-id="17c4d-267">Limits results to the fields you choose.</span></span>

<span data-ttu-id="17c4d-268">範例：</span><span class="sxs-lookup"><span data-stu-id="17c4d-268">Example:</span></span>

    Type:Alert errors detected | select Name, Severity

<span data-ttu-id="17c4d-269">將傳回的結果欄位限制為 *Name* and *Severity*小節中閱讀搜尋中傳回的欄位，以及協助您深入鑽研相似資料類別的 Facet。</span><span class="sxs-lookup"><span data-stu-id="17c4d-269">Limits the returned results fields to *Name* and *Severity*.</span></span>

### <a name="measure"></a><span data-ttu-id="17c4d-270">Measure</span><span class="sxs-lookup"><span data-stu-id="17c4d-270">Measure</span></span>
<span data-ttu-id="17c4d-271">*measure* 命令可用來將統計函式套用至未經處理的搜尋結果。</span><span class="sxs-lookup"><span data-stu-id="17c4d-271">The *measure* command is used to apply statistical functions to the raw search results.</span></span> <span data-ttu-id="17c4d-272">需要取得資料的 *群組依據* 檢視時，這非常有用。</span><span class="sxs-lookup"><span data-stu-id="17c4d-272">This is very useful to get *group-by* views over the data.</span></span> <span data-ttu-id="17c4d-273">當您使用 measure 命令時，Log Analytics 搜尋會顯示含有彙總結果的資料表。</span><span class="sxs-lookup"><span data-stu-id="17c4d-273">When you use the measure command, Log Analytics search displays a table with aggregated results.</span></span>

<span data-ttu-id="17c4d-274">**語法：**</span><span class="sxs-lookup"><span data-stu-id="17c4d-274">**Syntax:**</span></span>

    measure aggregateFunction1([aggregatedField]) [as fieldAlias1] [, aggregateFunction2([aggregatedField2]) [as fieldAlias2] [, ...]] by groupField1 [, groupField2 [, groupField3]]  [interval interval]


    measure aggregateFunction1([aggregatedField]) [as fieldAlias1] [, aggregateFunction2([aggregatedField2]) [as fieldAlias2] [, ...]]  interval interval



<span data-ttu-id="17c4d-275">根據 groupField 彙總結果，並使用 aggregatedField 計算彙總的測量值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-275">Aggregates the results by *groupField*, and calculates the aggregated measure values by using *aggregatedField*.</span></span>

| <span data-ttu-id="17c4d-276">量值統計函式</span><span class="sxs-lookup"><span data-stu-id="17c4d-276">Measure statistical function</span></span> | <span data-ttu-id="17c4d-277">說明</span><span class="sxs-lookup"><span data-stu-id="17c4d-277">Description</span></span> |
| --- | --- |
| <span data-ttu-id="17c4d-278">*aggregateFunction*</span><span class="sxs-lookup"><span data-stu-id="17c4d-278">*aggregateFunction*</span></span> |<span data-ttu-id="17c4d-279">彙總函式的名稱 (不區分大小寫)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-279">The name of the aggregate function (case insensitive).</span></span> <span data-ttu-id="17c4d-280">支援下列彙總函式：COUNT、MAX、MIN、SUM、AVG、STDDEV、COUNTDISTINCT、PERCENTILE## 或 PCT## (## 是 1 與 99 之間的任意數字)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-280">The following aggregate functions are supported: COUNT, MAX, MIN, SUM, AVG, STDDEV, COUNTDISTINCT, PERCENTILE##, or PCT## (## is any number between 1 and 99).</span></span> |
| <span data-ttu-id="17c4d-281">*aggregatedField*</span><span class="sxs-lookup"><span data-stu-id="17c4d-281">*aggregatedField*</span></span> |<span data-ttu-id="17c4d-282">正在彙總的欄位。</span><span class="sxs-lookup"><span data-stu-id="17c4d-282">The field that is being aggregated.</span></span> <span data-ttu-id="17c4d-283">這是 COUNT 彙總函式的選擇性欄位，但必須是 SUM、MAX、MIN、AVG、STDDEV、PERCENTILE## 或 PCT## 的現有數值欄位 (## 是 1 與 99 之間的任意數字)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-283">This field is optional for the COUNT aggregate function, but has to be an existing numeric field for SUM, MAX, MIN, AVG, STDDEV, PERCENTILE##, or PCT## (## is any number between 1 and 99).</span></span> <span data-ttu-id="17c4d-284">aggregatedField 也可以是任一 **Extend** 支援的函式。</span><span class="sxs-lookup"><span data-stu-id="17c4d-284">The aggregatedField can also be any of the **Extend** supported functions.</span></span> |
| <span data-ttu-id="17c4d-285">*fieldAlias*</span><span class="sxs-lookup"><span data-stu-id="17c4d-285">*fieldAlias*</span></span> |<span data-ttu-id="17c4d-286">計算彙總值 (選擇性) 別名。</span><span class="sxs-lookup"><span data-stu-id="17c4d-286">The (optional) alias for the calculated aggregated value.</span></span> <span data-ttu-id="17c4d-287">如果未指定，欄位名稱會是 **AggregatedValue**。</span><span class="sxs-lookup"><span data-stu-id="17c4d-287">If not specified, the field name is **AggregatedValue**.</span></span> |
| <span data-ttu-id="17c4d-288">*groupField*</span><span class="sxs-lookup"><span data-stu-id="17c4d-288">*groupField*</span></span> |<span data-ttu-id="17c4d-289">用來分組結果集的欄位名稱。</span><span class="sxs-lookup"><span data-stu-id="17c4d-289">The name of the field that the result set is grouped by.</span></span> |
| <span data-ttu-id="17c4d-290">*間隔*</span><span class="sxs-lookup"><span data-stu-id="17c4d-290">*Interval*</span></span> |<span data-ttu-id="17c4d-291">時間間隔，格式為：**nnnNAME**。</span><span class="sxs-lookup"><span data-stu-id="17c4d-291">The time interval, in the format:**nnnNAME**.</span></span> <span data-ttu-id="17c4d-292">**nnn** 是正整數。</span><span class="sxs-lookup"><span data-stu-id="17c4d-292">**nnn** is the positive integer number.</span></span> <span data-ttu-id="17c4d-293">**NAME** 是間隔名稱。</span><span class="sxs-lookup"><span data-stu-id="17c4d-293">**NAME** is the interval name.</span></span> <span data-ttu-id="17c4d-294">支援的間隔名稱區分大小寫，且包括：MILLISECOND[S]、SECOND[S]、MINUTE[S]、HOUR[S]、DAY[S]、MONTH[S] 和 YEAR[S]。</span><span class="sxs-lookup"><span data-stu-id="17c4d-294">Supported interval names are case sensitive, and include:MILLISECOND[S], SECOND[S], MINUTE[S], HOUR[S], DAY[S], MONTH[S], and YEAR[S].</span></span> |

<span data-ttu-id="17c4d-295">間隔選項只能用於日期/時間群組欄位中 (例如 *TimeGenerated* and *TimeCreated*)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-295">The interval option can only be used in Date/Time group fields (such as *TimeGenerated* and *TimeCreated*).</span></span> <span data-ttu-id="17c4d-296">目前，服務不會強制執行，但是沒有傳遞至後端之日期/時間的欄位會造成執行階段錯誤。</span><span class="sxs-lookup"><span data-stu-id="17c4d-296">Currently, this is not enforced by the service, but a field without Date/Time that is passed to the back end causes a runtime error.</span></span> <span data-ttu-id="17c4d-297">實作結構描述驗證時，服務 API 會拒絕某些查詢，其使用的欄位沒有間隔彙總的日期/時間。</span><span class="sxs-lookup"><span data-stu-id="17c4d-297">When the schema validation is implemented, the service API rejects queries that use fields without Date/Time for interval aggregation.</span></span> <span data-ttu-id="17c4d-298">目前的 *Measure* 實作支援任何彙總函式的間隔分組。</span><span class="sxs-lookup"><span data-stu-id="17c4d-298">The current *Measure* implementation supports interval grouping for any aggregate function.</span></span>

<span data-ttu-id="17c4d-299">如果省略 BY 子句，但指定間隔 (作為第二個語法)，則預設採用 TimeGenerated 欄位。</span><span class="sxs-lookup"><span data-stu-id="17c4d-299">If the BY clause is omitted, but an interval is specified (as a second syntax), the *TimeGenerated* field is assumed by default.</span></span>

<span data-ttu-id="17c4d-300">範例：</span><span class="sxs-lookup"><span data-stu-id="17c4d-300">Examples:</span></span>

<span data-ttu-id="17c4d-301">**範例 1**</span><span class="sxs-lookup"><span data-stu-id="17c4d-301">**Example 1**</span></span>

    Type:Alert | measure count() as Count by ObjectId

<span data-ttu-id="17c4d-302">依據 ObjectID 將警示分組，並計算每個群組的警示數目。</span><span class="sxs-lookup"><span data-stu-id="17c4d-302">Groups the alerts by *ObjectID*, and calculates the number of alerts for each group.</span></span> <span data-ttu-id="17c4d-303">傳回的彙總值為 *Count* 欄位 (別名)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-303">The aggregated value is returned as the *Count* field (alias).</span></span>

<span data-ttu-id="17c4d-304">**範例 2**</span><span class="sxs-lookup"><span data-stu-id="17c4d-304">**Example 2**</span></span>

    Type:Alert | measure count() interval 1HOUR

<span data-ttu-id="17c4d-305">使用 *TimeGenerated* 欄位，依據 1 小時間隔將警示分組，並傳回每個間隔中的警示數目。</span><span class="sxs-lookup"><span data-stu-id="17c4d-305">Groups the alerts by 1-hour intervals by using the *TimeGenerated* field, and returns the number of alerts in each interval.</span></span>

<span data-ttu-id="17c4d-306">**範例 3**</span><span class="sxs-lookup"><span data-stu-id="17c4d-306">**Example 3**</span></span>

    Type:Alert | measure count() as AlertsPerHour interval 1HOUR

<span data-ttu-id="17c4d-307">如同上述範例，但使用彙總欄位別名 (*AlertsPerHour*)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-307">Same as the previous example, but with an aggregated field alias (*AlertsPerHour*).</span></span>

<span data-ttu-id="17c4d-308">**範例 4**</span><span class="sxs-lookup"><span data-stu-id="17c4d-308">**Example 4**</span></span>

    * <span data-ttu-id="17c4d-309">| measure count() by TimeCreated interval 5DAYS</span><span class="sxs-lookup"><span data-stu-id="17c4d-309">| measure count() by TimeCreated interval 5DAYS</span></span>

<span data-ttu-id="17c4d-310">使用 *TimeCreated* 欄位，依據 5 天間隔將結果分組，並傳回每個間隔中的結果數目。</span><span class="sxs-lookup"><span data-stu-id="17c4d-310">Groups the results by 5-day intervals by using the *TimeCreated* field, and returns the number of results in each interval.</span></span>

<span data-ttu-id="17c4d-311">**範例 5**</span><span class="sxs-lookup"><span data-stu-id="17c4d-311">**Example 5**</span></span>

    Type:Alert | measure max(Severity) by WorkflowName

<span data-ttu-id="17c4d-312">跟據工作負載名稱分組警示，並傳回每個工作流程的最大警示嚴重性值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-312">Groups the alerts by workload name, and returns the maximum alert severity value for each workflow.</span></span>

<span data-ttu-id="17c4d-313">**範例 6**</span><span class="sxs-lookup"><span data-stu-id="17c4d-313">**Example 6**</span></span>

    Type:Alert | measure min(Severity) by WorkflowName

<span data-ttu-id="17c4d-314">如同上述範例，但使用 min 彙總函式。</span><span class="sxs-lookup"><span data-stu-id="17c4d-314">Same as the previous example, but with the *min* aggregated function.</span></span>

<span data-ttu-id="17c4d-315">**範例 7**</span><span class="sxs-lookup"><span data-stu-id="17c4d-315">**Example 7**</span></span>

    Type:Perf | measure avg(CounterValue) by Computer

<span data-ttu-id="17c4d-316">根據 computer 分組 Perf，並計算平均值 (avg)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-316">Groups Perf by computer, and calculates the average (avg).</span></span>

<span data-ttu-id="17c4d-317">**範例 8**</span><span class="sxs-lookup"><span data-stu-id="17c4d-317">**Example 8**</span></span>

    Type:Perf | measure sum(CounterValue) by Computer

<span data-ttu-id="17c4d-318">如同上述範例，但使用 sum。</span><span class="sxs-lookup"><span data-stu-id="17c4d-318">Same as the previous example, but uses *sum*.</span></span>

<span data-ttu-id="17c4d-319">**範例 9**</span><span class="sxs-lookup"><span data-stu-id="17c4d-319">**Example 9**</span></span>

    Type:Perf | measure stddev(CounterValue) by Computer

<span data-ttu-id="17c4d-320">如同上述範例，但使用 stddev。</span><span class="sxs-lookup"><span data-stu-id="17c4d-320">Same as the previous example, but uses *stddev*.</span></span>

<span data-ttu-id="17c4d-321">**範例 10**</span><span class="sxs-lookup"><span data-stu-id="17c4d-321">**Example 10**</span></span>

    Type:Perf | measure percentile70(CounterValue) by Computer

<span data-ttu-id="17c4d-322">如同上述範例，但使用 percentile70。</span><span class="sxs-lookup"><span data-stu-id="17c4d-322">Same as the previous example, but uses *percentile70*.</span></span>

<span data-ttu-id="17c4d-323">**範例 11**</span><span class="sxs-lookup"><span data-stu-id="17c4d-323">**Example 11**</span></span>

    Type:Perf | measure pct70(CounterValue) by Computer

<span data-ttu-id="17c4d-324">如同上述範例，但使用 pct70。</span><span class="sxs-lookup"><span data-stu-id="17c4d-324">Same as the previous example, but uses *pct70*.</span></span> <span data-ttu-id="17c4d-325">請注意，PCT## 只是 PERCENTILE## 函式的別名。</span><span class="sxs-lookup"><span data-stu-id="17c4d-325">Note that *PCT##* is only an alias for *PERCENTILE##* function.</span></span>

<span data-ttu-id="17c4d-326">**範例 12**</span><span class="sxs-lookup"><span data-stu-id="17c4d-326">**Example 12**</span></span>

    Type:Perf | measure avg(CounterValue) by Computer, CounterName

<span data-ttu-id="17c4d-327">先根據 Computer 然後根據 CounterName 分組 Perf，並計算平均 (avg)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-327">Groups Perf first by Computer and then CounterName, and calculates the average (avg).</span></span>

<span data-ttu-id="17c4d-328">**範例 13**</span><span class="sxs-lookup"><span data-stu-id="17c4d-328">**Example 13**</span></span>

    Type:Alert | measure count() as Count by WorkflowName | sort Count desc | top 5

<span data-ttu-id="17c4d-329">取得最大數目警示的前五個工作流程。</span><span class="sxs-lookup"><span data-stu-id="17c4d-329">Gets the top five workflows with the maximum number of alerts.</span></span>

<span data-ttu-id="17c4d-330">**範例 14**</span><span class="sxs-lookup"><span data-stu-id="17c4d-330">**Example 14**</span></span>

    * <span data-ttu-id="17c4d-331">| measure countdistinct(Computer) by Type</span><span class="sxs-lookup"><span data-stu-id="17c4d-331">| measure countdistinct(Computer) by Type</span></span>

<span data-ttu-id="17c4d-332">計算針對每種類型報告的唯一電腦數目。</span><span class="sxs-lookup"><span data-stu-id="17c4d-332">Counts the number of unique computers reporting for each Type.</span></span>

<span data-ttu-id="17c4d-333">**範例 15**</span><span class="sxs-lookup"><span data-stu-id="17c4d-333">**Example 15**</span></span>

    * <span data-ttu-id="17c4d-334">| measure countdistinct(Computer) Interval 1HOUR</span><span class="sxs-lookup"><span data-stu-id="17c4d-334">| measure countdistinct(Computer) Interval 1HOUR</span></span>

<span data-ttu-id="17c4d-335">計算針對每個小時報告的唯一電腦數目。</span><span class="sxs-lookup"><span data-stu-id="17c4d-335">Counts the number of unique computers reporting for every hour.</span></span>

<span data-ttu-id="17c4d-336">**範例 16**</span><span class="sxs-lookup"><span data-stu-id="17c4d-336">**Example 16**</span></span>

```
Type:Perf CounterName=”% Processor Time” InstanceName=”_Total” | measure avg(CounterValue) by Computer Interval 1HOUR
```

<span data-ttu-id="17c4d-337">根據 Computer 分組 % Processor Time，並傳回每小時的平均值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-337">Groups % Processor Time by Computer, and returns the average for every hour.</span></span>

<span data-ttu-id="17c4d-338">**範例 17**</span><span class="sxs-lookup"><span data-stu-id="17c4d-338">**Example 17**</span></span>

    Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES

<span data-ttu-id="17c4d-339">根據 method 分組 W3CIISLog，並傳回代表每 5 分鐘的最大值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-339">Groups W3CIISLog by method, and returns the maximum for every 5 minutes.</span></span>

<span data-ttu-id="17c4d-340">**範例 18**</span><span class="sxs-lookup"><span data-stu-id="17c4d-340">**Example 18**</span></span>

```
Type:Perf CounterName=”% Processor Time” InstanceName=”_Total”  | measure min(CounterValue) as MIN, avg(CounterValue) as AVG, percentile75(CounterValue) as PCT75, max(CounterValue) as MAX by Computer Interval 1HOUR
```

<span data-ttu-id="17c4d-341">根據電腦分組 % Processor Time，並傳回每小時的最小值、平均值、第 75 百分位數和最大值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-341">Groups % Processor Time by computer, and returns the minimum, average, 75th percentile, and maximum for every hour.</span></span>

<span data-ttu-id="17c4d-342">**範例 19**</span><span class="sxs-lookup"><span data-stu-id="17c4d-342">**Example 19**</span></span>

```
Type:Perf CounterName=”% Processor Time”  | measure min(CounterValue) as MIN, avg(CounterValue) as AVG, percentile75(CounterValue) as PCT75, max(CounterValue) as MAX by Computer, InstanceName Interval 1HOUR
```

<span data-ttu-id="17c4d-343">先根據 computer 然後根據 Instance name 分組 % Processor Time，並傳回每小時的最小值、平均值、第 75 百分位數和最大值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-343">Groups % Processor Time first by computer and then by Instance name, and returns the minimum, average, 75th percentile, and maximum for every hour.</span></span>

<span data-ttu-id="17c4d-344">**範例 20**</span><span class="sxs-lookup"><span data-stu-id="17c4d-344">**Example 20**</span></span>

```
Type= Perf CounterName="Disk Writes/sec" Computer="BaconDC01.BaconLand.com" | measure max(product(CounterValue,60)) as MaxDWPerMin by InstanceName Interval 1HOUR
```

<span data-ttu-id="17c4d-345">計算您電腦上每個磁碟每分鐘磁碟寫入的最大值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-345">Calculates the maximum of disk writes per minute for every disk on your computer.</span></span>

### <a name="where"></a><span data-ttu-id="17c4d-346">Where</span><span class="sxs-lookup"><span data-stu-id="17c4d-346">Where</span></span>
<span data-ttu-id="17c4d-347">語法：</span><span class="sxs-lookup"><span data-stu-id="17c4d-347">Syntax:</span></span>

```
**where** AggregatedValue>20
```

<span data-ttu-id="17c4d-348">只能用於 Measure 命令之後，以進一步篩選 Measure 彙總函式所產生的彙總結果。</span><span class="sxs-lookup"><span data-stu-id="17c4d-348">Can only be used after a *Measure* command to further filter the aggregated results that the *Measure* aggregation function has produced.</span></span>

<span data-ttu-id="17c4d-349">範例：</span><span class="sxs-lookup"><span data-stu-id="17c4d-349">Examples:</span></span>

    Type:Perf CounterName:"% Total Run Time" | Measure max(CounterValue) as MAXCPU by Computer

    Type:Perf CounterName:"% Total Run Time" | Measure max(CounterValue) by Computer | where (AggregatedValue>50 and AggregatedValue<90)



### <a name="dedup"></a><span data-ttu-id="17c4d-350">Dedup</span><span class="sxs-lookup"><span data-stu-id="17c4d-350">Dedup</span></span>
<span data-ttu-id="17c4d-351">語法：</span><span class="sxs-lookup"><span data-stu-id="17c4d-351">Syntax:</span></span>

    Dedup FieldName

<span data-ttu-id="17c4d-352">針對所指定欄位的每個唯一值，傳回第一份找到的文件。</span><span class="sxs-lookup"><span data-stu-id="17c4d-352">Returns the first document found for every unique value of the given field.</span></span>

<span data-ttu-id="17c4d-353">範例：</span><span class="sxs-lookup"><span data-stu-id="17c4d-353">Example:</span></span>

    Type=Event | Dedup EventID | sort TimeGenerated DESC

<span data-ttu-id="17c4d-354">這個範例會為每個 EventID 傳回一個事件 (最新事件)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-354">This example returns one event (the latest event) per EventID.</span></span>

### <a name="join"></a><span data-ttu-id="17c4d-355">Join</span><span class="sxs-lookup"><span data-stu-id="17c4d-355">Join</span></span>
<span data-ttu-id="17c4d-356">聯結兩個查詢的結果以形成單一結果集。</span><span class="sxs-lookup"><span data-stu-id="17c4d-356">Joins the results of two queries to form a single result set.</span></span>  <span data-ttu-id="17c4d-357">支援下表所述的多個聯結類型。</span><span class="sxs-lookup"><span data-stu-id="17c4d-357">Supports multiple join types described in the follow table.</span></span>

| <span data-ttu-id="17c4d-358">聯結類型</span><span class="sxs-lookup"><span data-stu-id="17c4d-358">Join type</span></span> | <span data-ttu-id="17c4d-359">說明</span><span class="sxs-lookup"><span data-stu-id="17c4d-359">Description</span></span> |
|:--|:--|
| <span data-ttu-id="17c4d-360">inner</span><span class="sxs-lookup"><span data-stu-id="17c4d-360">inner</span></span> | <span data-ttu-id="17c4d-361">只傳回具有兩個查詢相符值的記錄。</span><span class="sxs-lookup"><span data-stu-id="17c4d-361">Return only records with a matching value in both queries.</span></span> |
| <span data-ttu-id="17c4d-362">outer</span><span class="sxs-lookup"><span data-stu-id="17c4d-362">outer</span></span> | <span data-ttu-id="17c4d-363">傳回兩個查詢的所有記錄。</span><span class="sxs-lookup"><span data-stu-id="17c4d-363">Return all records from both queries.</span></span>  |
| <span data-ttu-id="17c4d-364">left</span><span class="sxs-lookup"><span data-stu-id="17c4d-364">left</span></span>  | <span data-ttu-id="17c4d-365">傳回左查詢的所有記錄，以及傳回右查詢的相符記錄。</span><span class="sxs-lookup"><span data-stu-id="17c4d-365">Return all records from left query and matching records from right query.</span></span> |


- <span data-ttu-id="17c4d-366">聯結目前不支援下列查詢：包含 **IN**關鍵字、**Measure** 命令或 (如果目標為右側查詢的欄位) **Extend** 命令。</span><span class="sxs-lookup"><span data-stu-id="17c4d-366">Joins do not currently support queries that include the **IN** keyword, the **Measure** command or the **Extend** command if it targets a field from the right query.</span></span>
- <span data-ttu-id="17c4d-367">您目前只可以在一個聯結中包含單一欄位。</span><span class="sxs-lookup"><span data-stu-id="17c4d-367">You can currently include only a single field in a join.</span></span>
- <span data-ttu-id="17c4d-368">單一搜尋可能不包含一個以上的聯結。</span><span class="sxs-lookup"><span data-stu-id="17c4d-368">A single search may not include more than one join.</span></span>

<span data-ttu-id="17c4d-369">**語法**</span><span class="sxs-lookup"><span data-stu-id="17c4d-369">**Syntax**</span></span>

```
<left-query> | JOIN <join-type> <left-query-field-name> (<right-query>) <right-query-field-name>
```

<span data-ttu-id="17c4d-370">**範例**</span><span class="sxs-lookup"><span data-stu-id="17c4d-370">**Examples**</span></span>

<span data-ttu-id="17c4d-371">若要說明不同的聯結類型，請考慮聯結從稱為 MyBackup_CL 的自訂記錄收集的資料類型與每部電腦的活動訊號。</span><span class="sxs-lookup"><span data-stu-id="17c4d-371">To illustrate the different join types, consider joining a data type collected from a custom log called MyBackup_CL with the heartbeat for each computer.</span></span>  <span data-ttu-id="17c4d-372">這些資料類型具有下列資料。</span><span class="sxs-lookup"><span data-stu-id="17c4d-372">These datatypes have the following data.</span></span>

`Type = MyBackup_CL`

| <span data-ttu-id="17c4d-373">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="17c4d-373">TimeGenerated</span></span> | <span data-ttu-id="17c4d-374">電腦</span><span class="sxs-lookup"><span data-stu-id="17c4d-374">Computer</span></span> | <span data-ttu-id="17c4d-375">LastBackupStatus</span><span class="sxs-lookup"><span data-stu-id="17c4d-375">LastBackupStatus</span></span> |
|:---|:---|:---|
| <span data-ttu-id="17c4d-376">4/20/2017 01:26:32.137 AM</span><span class="sxs-lookup"><span data-stu-id="17c4d-376">4/20/2017 01:26:32.137 AM</span></span> | <span data-ttu-id="17c4d-377">srv01.contoso.com</span><span class="sxs-lookup"><span data-stu-id="17c4d-377">srv01.contoso.com</span></span> | <span data-ttu-id="17c4d-378">成功</span><span class="sxs-lookup"><span data-stu-id="17c4d-378">Success</span></span> |
| <span data-ttu-id="17c4d-379">4/20/2017 02:13:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="17c4d-379">4/20/2017 02:13:12.381 AM</span></span> | <span data-ttu-id="17c4d-380">srv02.contoso.com</span><span class="sxs-lookup"><span data-stu-id="17c4d-380">srv02.contoso.com</span></span> | <span data-ttu-id="17c4d-381">成功</span><span class="sxs-lookup"><span data-stu-id="17c4d-381">Success</span></span> |
| <span data-ttu-id="17c4d-382">4/20/2017 02:13:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="17c4d-382">4/20/2017 02:13:12.381 AM</span></span> | <span data-ttu-id="17c4d-383">srv03.contoso.com</span><span class="sxs-lookup"><span data-stu-id="17c4d-383">srv03.contoso.com</span></span> | <span data-ttu-id="17c4d-384">失敗</span><span class="sxs-lookup"><span data-stu-id="17c4d-384">Failure</span></span> |

<span data-ttu-id="17c4d-385">`Type = Hearbeat` (只會顯示部分的欄位)</span><span class="sxs-lookup"><span data-stu-id="17c4d-385">`Type = Hearbeat` (Only a subset of fields shown)</span></span>

| <span data-ttu-id="17c4d-386">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="17c4d-386">TimeGenerated</span></span> | <span data-ttu-id="17c4d-387">電腦</span><span class="sxs-lookup"><span data-stu-id="17c4d-387">Computer</span></span> | <span data-ttu-id="17c4d-388">ComputerIP</span><span class="sxs-lookup"><span data-stu-id="17c4d-388">ComputerIP</span></span> |
|:---|:---|:---|
| <span data-ttu-id="17c4d-389">4/21/2017 12:01:34.482 PM</span><span class="sxs-lookup"><span data-stu-id="17c4d-389">4/21/2017 12:01:34.482 PM</span></span> | <span data-ttu-id="17c4d-390">srv01.contoso.com</span><span class="sxs-lookup"><span data-stu-id="17c4d-390">srv01.contoso.com</span></span> | <span data-ttu-id="17c4d-391">10.10.100.1</span><span class="sxs-lookup"><span data-stu-id="17c4d-391">10.10.100.1</span></span> |
| <span data-ttu-id="17c4d-392">4/21/2017 12:02:21.916 PM</span><span class="sxs-lookup"><span data-stu-id="17c4d-392">4/21/2017 12:02:21.916 PM</span></span> | <span data-ttu-id="17c4d-393">srv02.contoso.com</span><span class="sxs-lookup"><span data-stu-id="17c4d-393">srv02.contoso.com</span></span> | <span data-ttu-id="17c4d-394">10.10.100.2</span><span class="sxs-lookup"><span data-stu-id="17c4d-394">10.10.100.2</span></span> |
| <span data-ttu-id="17c4d-395">4/21/2017 12:01:47.373 PM</span><span class="sxs-lookup"><span data-stu-id="17c4d-395">4/21/2017 12:01:47.373 PM</span></span> | <span data-ttu-id="17c4d-396">srv04.contoso.com</span><span class="sxs-lookup"><span data-stu-id="17c4d-396">srv04.contoso.com</span></span> | <span data-ttu-id="17c4d-397">10.10.100.4</span><span class="sxs-lookup"><span data-stu-id="17c4d-397">10.10.100.4</span></span> |

#### <a name="inner-join"></a><span data-ttu-id="17c4d-398">inner join</span><span class="sxs-lookup"><span data-stu-id="17c4d-398">inner join</span></span>

`Type=MyBackup_CL | join inner Computer (Type=Heartbeat) Computer`

<span data-ttu-id="17c4d-399">當電腦欄位符合兩個資料類型時，傳回下列記錄。</span><span class="sxs-lookup"><span data-stu-id="17c4d-399">Returns the following records where the computer field matches for both datatypes.</span></span>

| <span data-ttu-id="17c4d-400">電腦</span><span class="sxs-lookup"><span data-stu-id="17c4d-400">Computer</span></span>| <span data-ttu-id="17c4d-401">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="17c4d-401">TimeGenerated</span></span> | <span data-ttu-id="17c4d-402">LastBackupStatus</span><span class="sxs-lookup"><span data-stu-id="17c4d-402">LastBackupStatus</span></span> | <span data-ttu-id="17c4d-403">TimeGenerated_joined</span><span class="sxs-lookup"><span data-stu-id="17c4d-403">TimeGenerated_joined</span></span> | <span data-ttu-id="17c4d-404">ComputerIP_joined</span><span class="sxs-lookup"><span data-stu-id="17c4d-404">ComputerIP_joined</span></span> | <span data-ttu-id="17c4d-405">Type_joined</span><span class="sxs-lookup"><span data-stu-id="17c4d-405">Type_joined</span></span> |
|:---|:---|:---|:---|:---|:---|
| <span data-ttu-id="17c4d-406">srv01.contoso.com</span><span class="sxs-lookup"><span data-stu-id="17c4d-406">srv01.contoso.com</span></span> | <span data-ttu-id="17c4d-407">4/20/2017 01:26:32.137 AM</span><span class="sxs-lookup"><span data-stu-id="17c4d-407">4/20/2017 01:26:32.137 AM</span></span> | <span data-ttu-id="17c4d-408">成功</span><span class="sxs-lookup"><span data-stu-id="17c4d-408">Success</span></span> | <span data-ttu-id="17c4d-409">4/21/2017 12:01:34.482 PM</span><span class="sxs-lookup"><span data-stu-id="17c4d-409">4/21/2017 12:01:34.482 PM</span></span> | <span data-ttu-id="17c4d-410">10.10.100.1</span><span class="sxs-lookup"><span data-stu-id="17c4d-410">10.10.100.1</span></span> | <span data-ttu-id="17c4d-411">Heartbeat</span><span class="sxs-lookup"><span data-stu-id="17c4d-411">Heartbeat</span></span> |
| <span data-ttu-id="17c4d-412">srv02.contoso.com</span><span class="sxs-lookup"><span data-stu-id="17c4d-412">srv02.contoso.com</span></span> | <span data-ttu-id="17c4d-413">4/20/2017 02:13:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="17c4d-413">4/20/2017 02:13:12.381 AM</span></span> | <span data-ttu-id="17c4d-414">成功</span><span class="sxs-lookup"><span data-stu-id="17c4d-414">Success</span></span> | <span data-ttu-id="17c4d-415">4/21/2017 12:02:21.916 PM</span><span class="sxs-lookup"><span data-stu-id="17c4d-415">4/21/2017 12:02:21.916 PM</span></span> | <span data-ttu-id="17c4d-416">10.10.100.2</span><span class="sxs-lookup"><span data-stu-id="17c4d-416">10.10.100.2</span></span> | <span data-ttu-id="17c4d-417">Heartbeat</span><span class="sxs-lookup"><span data-stu-id="17c4d-417">Heartbeat</span></span> |


#### <a name="outer-join"></a><span data-ttu-id="17c4d-418">outer join</span><span class="sxs-lookup"><span data-stu-id="17c4d-418">outer join</span></span>

`Type=MyBackup_CL | join outer Computer (Type=Heartbeat) Computer`

<span data-ttu-id="17c4d-419">傳回兩個資料類型的下列記錄。</span><span class="sxs-lookup"><span data-stu-id="17c4d-419">Returns the following records for both datatypes.</span></span>

| <span data-ttu-id="17c4d-420">電腦</span><span class="sxs-lookup"><span data-stu-id="17c4d-420">Computer</span></span>| <span data-ttu-id="17c4d-421">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="17c4d-421">TimeGenerated</span></span> | <span data-ttu-id="17c4d-422">LastBackupStatus</span><span class="sxs-lookup"><span data-stu-id="17c4d-422">LastBackupStatus</span></span> | <span data-ttu-id="17c4d-423">TimeGenerated_joined</span><span class="sxs-lookup"><span data-stu-id="17c4d-423">TimeGenerated_joined</span></span> | <span data-ttu-id="17c4d-424">ComputerIP_joined</span><span class="sxs-lookup"><span data-stu-id="17c4d-424">ComputerIP_joined</span></span> | <span data-ttu-id="17c4d-425">Type_joined</span><span class="sxs-lookup"><span data-stu-id="17c4d-425">Type_joined</span></span> |
|:---|:---|:---|:---|:---|:---|
| <span data-ttu-id="17c4d-426">srv01.contoso.com</span><span class="sxs-lookup"><span data-stu-id="17c4d-426">srv01.contoso.com</span></span> | <span data-ttu-id="17c4d-427">4/20/2017 01:26:32.137 AM</span><span class="sxs-lookup"><span data-stu-id="17c4d-427">4/20/2017 01:26:32.137 AM</span></span> | <span data-ttu-id="17c4d-428">成功</span><span class="sxs-lookup"><span data-stu-id="17c4d-428">Success</span></span>  | <span data-ttu-id="17c4d-429">4/21/2017 12:01:34.482 PM</span><span class="sxs-lookup"><span data-stu-id="17c4d-429">4/21/2017 12:01:34.482 PM</span></span> | <span data-ttu-id="17c4d-430">10.10.100.1</span><span class="sxs-lookup"><span data-stu-id="17c4d-430">10.10.100.1</span></span> | <span data-ttu-id="17c4d-431">Heartbeat</span><span class="sxs-lookup"><span data-stu-id="17c4d-431">Heartbeat</span></span> |
| <span data-ttu-id="17c4d-432">srv02.contoso.com</span><span class="sxs-lookup"><span data-stu-id="17c4d-432">srv02.contoso.com</span></span> | <span data-ttu-id="17c4d-433">4/20/2017 02:14:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="17c4d-433">4/20/2017 02:14:12.381 AM</span></span> | <span data-ttu-id="17c4d-434">成功</span><span class="sxs-lookup"><span data-stu-id="17c4d-434">Success</span></span>  | <span data-ttu-id="17c4d-435">4/21/2017 12:02:21.916 PM</span><span class="sxs-lookup"><span data-stu-id="17c4d-435">4/21/2017 12:02:21.916 PM</span></span> | <span data-ttu-id="17c4d-436">10.10.100.2</span><span class="sxs-lookup"><span data-stu-id="17c4d-436">10.10.100.2</span></span> | <span data-ttu-id="17c4d-437">Heartbeat</span><span class="sxs-lookup"><span data-stu-id="17c4d-437">Heartbeat</span></span> |
| <span data-ttu-id="17c4d-438">srv03.contoso.com</span><span class="sxs-lookup"><span data-stu-id="17c4d-438">srv03.contoso.com</span></span> | <span data-ttu-id="17c4d-439">4/20/2017 01:33:35.974 AM</span><span class="sxs-lookup"><span data-stu-id="17c4d-439">4/20/2017 01:33:35.974 AM</span></span> | <span data-ttu-id="17c4d-440">失敗</span><span class="sxs-lookup"><span data-stu-id="17c4d-440">Failure</span></span>  | <span data-ttu-id="17c4d-441">4/21/2017 12:01:47.373 PM</span><span class="sxs-lookup"><span data-stu-id="17c4d-441">4/21/2017 12:01:47.373 PM</span></span> | | |
| <span data-ttu-id="17c4d-442">srv04.contoso.com</span><span class="sxs-lookup"><span data-stu-id="17c4d-442">srv04.contoso.com</span></span> |                           |          | <span data-ttu-id="17c4d-443">4/21/2017 12:01:47.373 PM</span><span class="sxs-lookup"><span data-stu-id="17c4d-443">4/21/2017 12:01:47.373 PM</span></span> | <span data-ttu-id="17c4d-444">10.10.100.2</span><span class="sxs-lookup"><span data-stu-id="17c4d-444">10.10.100.2</span></span> | <span data-ttu-id="17c4d-445">Heartbeat</span><span class="sxs-lookup"><span data-stu-id="17c4d-445">Heartbeat</span></span> |



#### <a name="left-join"></a><span data-ttu-id="17c4d-446">left join</span><span class="sxs-lookup"><span data-stu-id="17c4d-446">left join</span></span>

`Type=MyBackup_CL | join left Computer (Type=Heartbeat) Computer`

<span data-ttu-id="17c4d-447">從 MyBackup_CL 傳回下列記錄，以及 Heartbeat 的任何相符欄位。</span><span class="sxs-lookup"><span data-stu-id="17c4d-447">Returns the following records from MyBackup_CL with any matching fields from Heartbeat.</span></span>

| <span data-ttu-id="17c4d-448">電腦</span><span class="sxs-lookup"><span data-stu-id="17c4d-448">Computer</span></span>| <span data-ttu-id="17c4d-449">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="17c4d-449">TimeGenerated</span></span> | <span data-ttu-id="17c4d-450">LastBackupStatus</span><span class="sxs-lookup"><span data-stu-id="17c4d-450">LastBackupStatus</span></span> | <span data-ttu-id="17c4d-451">TimeGenerated_joined</span><span class="sxs-lookup"><span data-stu-id="17c4d-451">TimeGenerated_joined</span></span> | <span data-ttu-id="17c4d-452">ComputerIP_joined</span><span class="sxs-lookup"><span data-stu-id="17c4d-452">ComputerIP_joined</span></span> | <span data-ttu-id="17c4d-453">Type_joined</span><span class="sxs-lookup"><span data-stu-id="17c4d-453">Type_joined</span></span> |
|:---|:---|:---|:---|:---|:---|
| <span data-ttu-id="17c4d-454">srv01.contoso.com</span><span class="sxs-lookup"><span data-stu-id="17c4d-454">srv01.contoso.com</span></span> | <span data-ttu-id="17c4d-455">4/20/2017 01:26:32.137 AM</span><span class="sxs-lookup"><span data-stu-id="17c4d-455">4/20/2017 01:26:32.137 AM</span></span> | <span data-ttu-id="17c4d-456">成功</span><span class="sxs-lookup"><span data-stu-id="17c4d-456">Success</span></span> | <span data-ttu-id="17c4d-457">4/21/2017 12:01:34.482 PM</span><span class="sxs-lookup"><span data-stu-id="17c4d-457">4/21/2017 12:01:34.482 PM</span></span> | <span data-ttu-id="17c4d-458">10.10.100.1</span><span class="sxs-lookup"><span data-stu-id="17c4d-458">10.10.100.1</span></span> | <span data-ttu-id="17c4d-459">Heartbeat</span><span class="sxs-lookup"><span data-stu-id="17c4d-459">Heartbeat</span></span> |
| <span data-ttu-id="17c4d-460">srv02.contoso.com</span><span class="sxs-lookup"><span data-stu-id="17c4d-460">srv02.contoso.com</span></span> | <span data-ttu-id="17c4d-461">4/20/2017 02:13:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="17c4d-461">4/20/2017 02:13:12.381 AM</span></span> | <span data-ttu-id="17c4d-462">成功</span><span class="sxs-lookup"><span data-stu-id="17c4d-462">Success</span></span> | <span data-ttu-id="17c4d-463">4/21/2017 12:02:21.916 PM</span><span class="sxs-lookup"><span data-stu-id="17c4d-463">4/21/2017 12:02:21.916 PM</span></span> | <span data-ttu-id="17c4d-464">10.10.100.2</span><span class="sxs-lookup"><span data-stu-id="17c4d-464">10.10.100.2</span></span> | <span data-ttu-id="17c4d-465">Heartbeat</span><span class="sxs-lookup"><span data-stu-id="17c4d-465">Heartbeat</span></span> |
| <span data-ttu-id="17c4d-466">srv03.contoso.com</span><span class="sxs-lookup"><span data-stu-id="17c4d-466">srv03.contoso.com</span></span> | <span data-ttu-id="17c4d-467">4/20/2017 02:13:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="17c4d-467">4/20/2017 02:13:12.381 AM</span></span> | <span data-ttu-id="17c4d-468">失敗</span><span class="sxs-lookup"><span data-stu-id="17c4d-468">Failure</span></span> | | | |


### <a name="extend"></a><span data-ttu-id="17c4d-469">Extend</span><span class="sxs-lookup"><span data-stu-id="17c4d-469">Extend</span></span>
<span data-ttu-id="17c4d-470">可讓您在查詢中建立執行階段欄位。</span><span class="sxs-lookup"><span data-stu-id="17c4d-470">Allows you to create run-time fields in queries.</span></span> <span data-ttu-id="17c4d-471">請注意，執行階段欄位不能使用量值命令執行彙總。</span><span class="sxs-lookup"><span data-stu-id="17c4d-471">Note that run-time fields cannot be used with the measure command to perform aggregation.</span></span>

<span data-ttu-id="17c4d-472">**範例 1**</span><span class="sxs-lookup"><span data-stu-id="17c4d-472">**Example 1**</span></span>

    Type=SQLAssessmentRecommendation | Extend product(RecommendationScore, RecommendationWeight) AS RecommendationWeightedScore
<span data-ttu-id="17c4d-473">顯示 SQL 評估建議的加權建議分數。</span><span class="sxs-lookup"><span data-stu-id="17c4d-473">Shows weighted recommendation score for SQL Assessment recommendations.</span></span>

<span data-ttu-id="17c4d-474">**範例 2**</span><span class="sxs-lookup"><span data-stu-id="17c4d-474">**Example 2**</span></span>

    Type=Perf CounterName="Private Bytes" | EXTEND div(CounterValue,1024) AS KBs | Select CounterValue,Computer,KBs
<span data-ttu-id="17c4d-475">顯示計數器值，單位為 KB，而非位元組。</span><span class="sxs-lookup"><span data-stu-id="17c4d-475">Shows counter value in KBs instead of bytes.</span></span>

<span data-ttu-id="17c4d-476">**範例 3**</span><span class="sxs-lookup"><span data-stu-id="17c4d-476">**Example 3**</span></span>

    Type=WireData | EXTEND scale(TotalBytes,0,100) AS ScaledTotalBytes | Select ScaledTotalBytes,TotalBytes | SORT TotalBytes DESC
<span data-ttu-id="17c4d-477">調整 WireData TotalBytes 的值，讓所有結果都落在 0 與 100 之間。</span><span class="sxs-lookup"><span data-stu-id="17c4d-477">Scales the value of WireData TotalBytes, such that all results are between 0 and 100.</span></span>

<span data-ttu-id="17c4d-478">**範例 4**</span><span class="sxs-lookup"><span data-stu-id="17c4d-478">**Example 4**</span></span>

```
Type=Perf CounterName="% Processor Time" | EXTEND if(map(CounterValue,0,50,0,1),"HIGH","LOW") as UTILIZATION
```
<span data-ttu-id="17c4d-479">將小於 50% 的效能計數器值標記為 LOW，而將其他值標記為 HIGH。</span><span class="sxs-lookup"><span data-stu-id="17c4d-479">Tags Perf Counter Values less than 50 percent as LOW, and others as HIGH.</span></span>

<span data-ttu-id="17c4d-480">**範例 5**</span><span class="sxs-lookup"><span data-stu-id="17c4d-480">**Example 5**</span></span>

```
Type= Perf CounterName="Disk Writes/sec" Computer="BaconDC01.BaconLand.com" | Extend product(CounterValue,60) as DWPerMin| measure max(DWPerMin) by InstanceName Interval 1HOUR
```
<span data-ttu-id="17c4d-481">計算您電腦上每個磁碟每分鐘磁碟寫入的最大值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-481">Calculates the maximum of disk writes per minute for every disk on your computer.</span></span>

<span data-ttu-id="17c4d-482">**支援的函式**</span><span class="sxs-lookup"><span data-stu-id="17c4d-482">**Supported functions**</span></span>

| <span data-ttu-id="17c4d-483">函式</span><span class="sxs-lookup"><span data-stu-id="17c4d-483">Function</span></span> | <span data-ttu-id="17c4d-484">說明</span><span class="sxs-lookup"><span data-stu-id="17c4d-484">Description</span></span> | <span data-ttu-id="17c4d-485">語法範例</span><span class="sxs-lookup"><span data-stu-id="17c4d-485">Syntax examples</span></span> |
| --- | --- | --- |
| <span data-ttu-id="17c4d-486">abs</span><span class="sxs-lookup"><span data-stu-id="17c4d-486">abs</span></span> |<span data-ttu-id="17c4d-487">傳回所指定數值或函式的絕對值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-487">Returns the absolute value of the specified value or function.</span></span> |`abs(x)` <br> `abs(-5)` |
| <span data-ttu-id="17c4d-488">acos</span><span class="sxs-lookup"><span data-stu-id="17c4d-488">acos</span></span> |<span data-ttu-id="17c4d-489">傳回值或函式的反餘弦值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-489">Returns arc cosine of a value or a function.</span></span> |`acos(x)` |
| <span data-ttu-id="17c4d-490">和</span><span class="sxs-lookup"><span data-stu-id="17c4d-490">and</span></span> |<span data-ttu-id="17c4d-491">只有在其所有運算元都評估為 true 時，才會傳回 true 值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-491">Returns a value of true if and only if all of its operands evaluate to true.</span></span> |`and(not(exists(popularity)),exists(price))` |
| <span data-ttu-id="17c4d-492">asin</span><span class="sxs-lookup"><span data-stu-id="17c4d-492">asin</span></span> |<span data-ttu-id="17c4d-493">傳回值或函式的反正弦值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-493">Returns arc sine of a value or a function.</span></span> |`asin(x)` |
| <span data-ttu-id="17c4d-494">atan</span><span class="sxs-lookup"><span data-stu-id="17c4d-494">atan</span></span> |<span data-ttu-id="17c4d-495">傳回值或函式的反正切值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-495">Returns arc tangent of a value or a function.</span></span> |`atan(x)` |
| <span data-ttu-id="17c4d-496">atan2</span><span class="sxs-lookup"><span data-stu-id="17c4d-496">atan2</span></span> |<span data-ttu-id="17c4d-497">傳回矩形座標 x、y 轉換為極座標所產生的角度。</span><span class="sxs-lookup"><span data-stu-id="17c4d-497">Returns the angle resulting from the conversion of the rectangular coordinates x,y to polar coordinates.</span></span> |`atan2(x,y)` |
| <span data-ttu-id="17c4d-498">cbrt</span><span class="sxs-lookup"><span data-stu-id="17c4d-498">cbrt</span></span> |<span data-ttu-id="17c4d-499">立方根。</span><span class="sxs-lookup"><span data-stu-id="17c4d-499">Cube root.</span></span> |`cbrt(x)` |
| <span data-ttu-id="17c4d-500">ceil</span><span class="sxs-lookup"><span data-stu-id="17c4d-500">ceil</span></span> |<span data-ttu-id="17c4d-501">無條件進位到整數。</span><span class="sxs-lookup"><span data-stu-id="17c4d-501">Rounds up to an integer.</span></span> |`ceil(x)`  <br> <span data-ttu-id="17c4d-502">`ceil(5.6)`：傳回 6</span><span class="sxs-lookup"><span data-stu-id="17c4d-502">`ceil(5.6)` Returns 6</span></span> |
| <span data-ttu-id="17c4d-503">cos</span><span class="sxs-lookup"><span data-stu-id="17c4d-503">cos</span></span> |<span data-ttu-id="17c4d-504">傳回角度的餘弦值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-504">Returns cosine of an angle.</span></span> |`cos(x)` |
| <span data-ttu-id="17c4d-505">cosh</span><span class="sxs-lookup"><span data-stu-id="17c4d-505">cosh</span></span> |<span data-ttu-id="17c4d-506">傳回角度的雙曲餘弦值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-506">Returns hyperbolic cosine of an angle.</span></span> |`cosh(x)` |
| <span data-ttu-id="17c4d-507">def</span><span class="sxs-lookup"><span data-stu-id="17c4d-507">def</span></span> |<span data-ttu-id="17c4d-508">預設值的縮寫。</span><span class="sxs-lookup"><span data-stu-id="17c4d-508">Abbreviation for default.</span></span> <span data-ttu-id="17c4d-509">傳回欄位 "field" 的值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-509">Returns the value of field "field".</span></span> <span data-ttu-id="17c4d-510">如果欄位不存在，則會傳回所指定的預設值，並產生第一個值，其中：`exists()==true`。</span><span class="sxs-lookup"><span data-stu-id="17c4d-510">If the field does not exist, returns the default value specified and yields the first value where: `exists()==true`.</span></span> |<span data-ttu-id="17c4d-511">`def(rating,5)`。</span><span class="sxs-lookup"><span data-stu-id="17c4d-511">`def(rating,5)`.</span></span> <span data-ttu-id="17c4d-512">此 def() 函式傳回分級，或如果在文件中未指定分級，則傳回 5。</span><span class="sxs-lookup"><span data-stu-id="17c4d-512">This def() function returns the rating, or if no rating is specified in the document, returns 5.</span></span> <br> <span data-ttu-id="17c4d-513">`def(myfield, 1.0)` 相當於 `if(exists(myfield),myfield,1.0)`。</span><span class="sxs-lookup"><span data-stu-id="17c4d-513">`def(myfield, 1.0)` is equivalent to `if(exists(myfield),myfield,1.0)`.</span></span> |
| <span data-ttu-id="17c4d-514">度</span><span class="sxs-lookup"><span data-stu-id="17c4d-514">deg</span></span> |<span data-ttu-id="17c4d-515">將弧度轉換為度。</span><span class="sxs-lookup"><span data-stu-id="17c4d-515">Converts radians to degrees.</span></span> |`deg(x)` |
| <span data-ttu-id="17c4d-516">div</span><span class="sxs-lookup"><span data-stu-id="17c4d-516">div</span></span> |<span data-ttu-id="17c4d-517">`div(x,y)` 除以 x 乘以 y。</span><span class="sxs-lookup"><span data-stu-id="17c4d-517">`div(x,y)` divides x by y.</span></span> |`div(1,y)` <br> `div(sum(x,100),max(y,1))` |
| <span data-ttu-id="17c4d-518">dist</span><span class="sxs-lookup"><span data-stu-id="17c4d-518">dist</span></span> |<span data-ttu-id="17c4d-519">傳回 n 維度空間中兩個向量之間的距離 (點)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-519">Returns the distance between two vectors, (points) in an n-dimensional space.</span></span> <span data-ttu-id="17c4d-520">在次方中，使用 ValueSource 執行個體加上二以上的值，並計算兩個向量之間的距離。</span><span class="sxs-lookup"><span data-stu-id="17c4d-520">Takes in the power, plus two or more, ValueSource instances, and calculates the distances between the two vectors.</span></span> <span data-ttu-id="17c4d-521">每個 ValueSource 都必須是數字。</span><span class="sxs-lookup"><span data-stu-id="17c4d-521">Each ValueSource must be a number.</span></span> <span data-ttu-id="17c4d-522">必須傳入偶數的 ValueSource 執行個體，而且此方法假設前半部分代表第一個向量，而後半部分代表第二個向量。</span><span class="sxs-lookup"><span data-stu-id="17c4d-522">There must be an even number of ValueSource instances passed in, and the method assumes that the first half represent the first vector and the second half represent the second vector.</span></span> |<span data-ttu-id="17c4d-523">`dist(2, x, y, 0, 0)`：計算每個文件的 (0,0) 和 (x,y) 之間的 Euclidean 距離。</span><span class="sxs-lookup"><span data-stu-id="17c4d-523">`dist(2, x, y, 0, 0)` Calculates the Euclidean distance between (0,0) and (x,y) for each document.</span></span> <br> <span data-ttu-id="17c4d-524">`dist(1, x, y, 0, 0)`：計算每個文件的 (0,0) 和 (x,y) 之間的 Manhattan (計程車) 距離。</span><span class="sxs-lookup"><span data-stu-id="17c4d-524">`dist(1, x, y, 0, 0)` Calculates the Manhattan (taxicab) distance between (0,0) and (x,y) for each document.</span></span> <br> <span data-ttu-id="17c4d-525">`dist(2,,x,y,z,0,0,0)`：每個文件的 (0,0,0) 和 (x,y,z) 之間的 Euclidean 距離。</span><span class="sxs-lookup"><span data-stu-id="17c4d-525">`dist(2,,x,y,z,0,0,0)` Euclidean distance between (0,0,0) and (x,y,z) for each document.</span></span><br><span data-ttu-id="17c4d-526">`dist(1,x,y,z,e,f,g)`：(x,y,z) 和 (e,f,g) 之間的 Manhattan 距離，其中每個字母是欄位名稱。</span><span class="sxs-lookup"><span data-stu-id="17c4d-526">`dist(1,x,y,z,e,f,g)` Manhattan distance between (x,y,z) and (e,f,g), where each letter is a field name.</span></span> |
| <span data-ttu-id="17c4d-527">exists</span><span class="sxs-lookup"><span data-stu-id="17c4d-527">exists</span></span> |<span data-ttu-id="17c4d-528">如果有欄位的任何成員，請傳回 TRUE。</span><span class="sxs-lookup"><span data-stu-id="17c4d-528">Returns TRUE if any member of the field exists.</span></span> |<span data-ttu-id="17c4d-529">`exists(author)`：如果任何文件在 "author" 欄位中有值，則傳回 TRUE。</span><span class="sxs-lookup"><span data-stu-id="17c4d-529">`exists(author)` Returns TRUE for any document that has a value in the "author" field.</span></span><br><span data-ttu-id="17c4d-530">`exists(query(price:5.00))`：如果 "price" 符合 "5.00" 則傳回 TRUE。</span><span class="sxs-lookup"><span data-stu-id="17c4d-530">`exists(query(price:5.00))` Returns TRUE if "price" matches,"5.00".</span></span> |
| <span data-ttu-id="17c4d-531">exp</span><span class="sxs-lookup"><span data-stu-id="17c4d-531">exp</span></span> |<span data-ttu-id="17c4d-532">傳回歐拉數字乘冪 x。</span><span class="sxs-lookup"><span data-stu-id="17c4d-532">Returns Euler's number raised to power x.</span></span> |`exp(x)` |
| <span data-ttu-id="17c4d-533">floor</span><span class="sxs-lookup"><span data-stu-id="17c4d-533">floor</span></span> |<span data-ttu-id="17c4d-534">無條件捨去到整數。</span><span class="sxs-lookup"><span data-stu-id="17c4d-534">Rounds down to an integer.</span></span> |`floor(x)`  <br> <span data-ttu-id="17c4d-535">`floor(5.6)`：傳回 5</span><span class="sxs-lookup"><span data-stu-id="17c4d-535">`floor(5.6)` Returns 5</span></span> |
| <span data-ttu-id="17c4d-536">hypo</span><span class="sxs-lookup"><span data-stu-id="17c4d-536">hypo</span></span> |<span data-ttu-id="17c4d-537">傳回 sqrt(sum(pow(x,2),pow(y,2)))，而不需要中繼溢位或反向溢位。</span><span class="sxs-lookup"><span data-stu-id="17c4d-537">Returns sqrt(sum(pow(x,2),pow(y,2))) without intermediate overflow or underflow.</span></span> |`hypo(x,y)`  <br> ` |
| <span data-ttu-id="17c4d-538">if</span><span class="sxs-lookup"><span data-stu-id="17c4d-538">if</span></span> |<span data-ttu-id="17c4d-539">啟用條件式函式查詢。</span><span class="sxs-lookup"><span data-stu-id="17c4d-539">Enables conditional function queries.</span></span> <span data-ttu-id="17c4d-540">在 `if(test,value1,value2)` 中：test 是或參照可傳回邏輯值 (TRUE 或 FALSE) 的邏輯值或運算式。</span><span class="sxs-lookup"><span data-stu-id="17c4d-540">In `if(test,value1,value2)`, test is or refers to a logical value or expression that returns a logical value (TRUE or FALSE).</span></span> <span data-ttu-id="17c4d-541">`value1` 是函式在 test 產生 TRUE 時所傳回的值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-541">`value1` is the value returned by the function if test yields TRUE.</span></span> <span data-ttu-id="17c4d-542">`value2` 是函式在 test 產生 FALSE 時所傳回的值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-542">`value2` is the value returned by the function if test yields FALSE.</span></span> <span data-ttu-id="17c4d-543">運算式可以是輸出布林值的任何函式。</span><span class="sxs-lookup"><span data-stu-id="17c4d-543">An expression can be any function which outputs boolean values.</span></span> <span data-ttu-id="17c4d-544">也可以是傳回數值的函式，在此情況下，值 0 會解譯為 false 或傳回字串，在此情況下，空字串會解譯為 false。</span><span class="sxs-lookup"><span data-stu-id="17c4d-544">It can also be a function returning numeric values, in which case value 0 is interpreted as false, or returning strings, in which case empty string is interpreted as false.</span></span> |<span data-ttu-id="17c4d-545">`if(termfreq(cat,'electronics'),popularity,42)`：這個函式會檢查每個文件，確認 cat 欄位中是否包含 "electronics" 這個字。</span><span class="sxs-lookup"><span data-stu-id="17c4d-545">`if(termfreq(cat,'electronics'),popularity,42)` This function checks each document to see if it contains the term "electronics" in the cat field.</span></span> <span data-ttu-id="17c4d-546">如果是的話，會傳回 popularity 欄位的值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-546">If it does, then the value of the popularity field is returned.</span></span> <span data-ttu-id="17c4d-547">否則會傳回值 42。</span><span class="sxs-lookup"><span data-stu-id="17c4d-547">Otherwise, the value of 42 is returned.</span></span> |
| <span data-ttu-id="17c4d-548">linear</span><span class="sxs-lookup"><span data-stu-id="17c4d-548">linear</span></span> |<span data-ttu-id="17c4d-549">實作 `m*x+c`，其中 m 和 c 是常數，而 x 是任意函式。</span><span class="sxs-lookup"><span data-stu-id="17c4d-549">Implements `m*x+c`, where m and c are constants, and x is an arbitrary function.</span></span> <span data-ttu-id="17c4d-550">這相當於 `sum(product(m,x),c)`，但較具效率，因為它實作為單一函式。</span><span class="sxs-lookup"><span data-stu-id="17c4d-550">This is equivalent to `sum(product(m,x),c)`, but slightly more efficient as it is implemented as a single function.</span></span> |<span data-ttu-id="17c4d-551">`linear(x,m,c) linear(x,2,4)` 傳回 `2*x+4`</span><span class="sxs-lookup"><span data-stu-id="17c4d-551">`linear(x,m,c) linear(x,2,4)` returns `2*x+4`</span></span> |
| <span data-ttu-id="17c4d-552">ln</span><span class="sxs-lookup"><span data-stu-id="17c4d-552">ln</span></span> |<span data-ttu-id="17c4d-553">傳回所指定函式的自然對數。</span><span class="sxs-lookup"><span data-stu-id="17c4d-553">Returns the natural log of the specified function.</span></span> |`ln(x)` |
| <span data-ttu-id="17c4d-554">log</span><span class="sxs-lookup"><span data-stu-id="17c4d-554">log</span></span> |<span data-ttu-id="17c4d-555">傳回所指定函式的對數底數 10。</span><span class="sxs-lookup"><span data-stu-id="17c4d-555">Returns the log base 10 of the specified function.</span></span> |`log(x)   log(sum(x,100))` |
| <span data-ttu-id="17c4d-556">map</span><span class="sxs-lookup"><span data-stu-id="17c4d-556">map</span></span> |<span data-ttu-id="17c4d-557">將輸入函式 x 的任何落在 min 與 max (含) 之間的值對應到指定的目標。</span><span class="sxs-lookup"><span data-stu-id="17c4d-557">Maps any values of an input function x that fall within min and max, inclusive to the specified target.</span></span> <span data-ttu-id="17c4d-558">min 和 max 引數必須是常數。</span><span class="sxs-lookup"><span data-stu-id="17c4d-558">The arguments min and max must be constants.</span></span> <span data-ttu-id="17c4d-559">target 和 default 引數可以是常數或函式。</span><span class="sxs-lookup"><span data-stu-id="17c4d-559">The arguments target and default can be constants or functions.</span></span> <span data-ttu-id="17c4d-560">如果值 x 未落在 min 與 max 之間，則會傳回值 x，或者，如果指定為第 5 個引數，則會傳回預設值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-560">If the value of x does not fall between min and max, then either the value of x is returned, or a default value is returned if specified as a 5th argument.</span></span> |<span data-ttu-id="17c4d-561">`map(x,min,max,target) map(x,0,0,1)`：將任何 0 的值變更為 1。</span><span class="sxs-lookup"><span data-stu-id="17c4d-561">`map(x,min,max,target) map(x,0,0,1)` Changes any values of 0 to 1.</span></span> <span data-ttu-id="17c4d-562">這可用於處理預設值 0 的值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-562">This can be useful in handling default 0 values.</span></span><br> <span data-ttu-id="17c4d-563">`map(x,min,max,target,default)    map(x,0,100,1,-1)`：變更 0 和 100 到 1 之間的任何值，所有其他值為 -1。</span><span class="sxs-lookup"><span data-stu-id="17c4d-563">`map(x,min,max,target,default)    map(x,0,100,1,-1)` Changes any values between 0 and 100 to 1, and all other values to -1.</span></span><br>  <span data-ttu-id="17c4d-564">`map(x,0,100,sum(x,599),docfreq(text,solr))`：變更介於 0 和 100 到 x+599 之間的任何值和所有其他值，成為欄位文字中詞彙 'solr' 的頻率。</span><span class="sxs-lookup"><span data-stu-id="17c4d-564">`map(x,0,100,sum(x,599),docfreq(text,solr))` Changes any values between 0 and 100 to x+599, and all other values to frequency of the term 'solr' in the field text.</span></span> |
| <span data-ttu-id="17c4d-565">max</span><span class="sxs-lookup"><span data-stu-id="17c4d-565">max</span></span> |<span data-ttu-id="17c4d-566">傳回多個巢狀函式或常數的最大數值 (指定為引數：`max(x,y,...)`。</span><span class="sxs-lookup"><span data-stu-id="17c4d-566">Returns the maximum numeric value of multiple nested functions or constants, which are specified as arguments: `max(x,y,...)`.</span></span> <span data-ttu-id="17c4d-567">max 函式也適用於將某個指定常數上的另一個函式或欄位「降到最小值」</span><span class="sxs-lookup"><span data-stu-id="17c4d-567">The max function can also be useful for "bottoming out" another function or field at some specified constant.</span></span>  <span data-ttu-id="17c4d-568">使用 `field(myfield,max)` 語法來選取單一多值欄位的最大值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-568">Use the `field(myfield,max)` syntax for selecting the maximum value of a single multivalued field.</span></span> |`max(myfield,myotherfield,0)` |
| <span data-ttu-id="17c4d-569">Min</span><span class="sxs-lookup"><span data-stu-id="17c4d-569">min</span></span> |<span data-ttu-id="17c4d-570">傳回常數之多個巢狀函式的最小數值 (指定為引數︰`min(x,y,...)`。</span><span class="sxs-lookup"><span data-stu-id="17c4d-570">Returns the minimum numeric value of multiple nested functions of constants, which are specified as arguments: `min(x,y,...)`.</span></span> <span data-ttu-id="17c4d-571">min 函式也適用於使用常數提供函式的「上限」</span><span class="sxs-lookup"><span data-stu-id="17c4d-571">The min function can also be useful for providing an "upper bound" on a function using a constant.</span></span> <span data-ttu-id="17c4d-572">使用 `field(myfield,min)` 語法來選取單一多值欄位的最小值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-572">Use the `field(myfield,min)` syntax for selecting the minimum value of a single multivalued field.</span></span> |`min(myfield,myotherfield,0)` |
| <span data-ttu-id="17c4d-573">mod</span><span class="sxs-lookup"><span data-stu-id="17c4d-573">mod</span></span> |<span data-ttu-id="17c4d-574">計算函式 x 乘以函式 y 的模數。</span><span class="sxs-lookup"><span data-stu-id="17c4d-574">Computes the modulus of the function x by the function y.</span></span> |`mod(1,x)` <br> `mod(sum(x,100), max(y,1))` |
| <span data-ttu-id="17c4d-575">ms</span><span class="sxs-lookup"><span data-stu-id="17c4d-575">ms</span></span> |<span data-ttu-id="17c4d-576">傳回其引數之間差異的毫秒。</span><span class="sxs-lookup"><span data-stu-id="17c4d-576">Returns milliseconds of difference between its arguments.</span></span> <span data-ttu-id="17c4d-577">日期相對於 Unix 或 POSIX 時間新紀元：1970 年 1 月 1 日午夜 UTC。</span><span class="sxs-lookup"><span data-stu-id="17c4d-577">Dates are relative to the Unix or POSIX time epoch, midnight, January 1, 1970 UTC.</span></span> <span data-ttu-id="17c4d-578">引數可以是索引 TrieDateField 的名稱，或根據常數日期或 NOW 的日期算術。</span><span class="sxs-lookup"><span data-stu-id="17c4d-578">Arguments may be the name of an indexed TrieDateField, or date math based on a constant date or NOW .</span></span> <span data-ttu-id="17c4d-579">`ms()` 相當於 `ms(NOW)`，epoch 以來毫秒數的數字。</span><span class="sxs-lookup"><span data-stu-id="17c4d-579">`ms()` is equivalent to `ms(NOW)`, number of milliseconds since the epoch.</span></span> <span data-ttu-id="17c4d-580">`ms(a)` 傳回引數所代表之新紀元後的毫秒數。</span><span class="sxs-lookup"><span data-stu-id="17c4d-580">`ms(a)` returns the number of milliseconds since the epoch that the argument represents.</span></span> <span data-ttu-id="17c4d-581">`ms(a,b)` 傳回 b 之前發生的毫秒數，也就是 `a - b`。</span><span class="sxs-lookup"><span data-stu-id="17c4d-581">`ms(a,b)` returns the number of milliseconds that b occurs before a, which is `a - b`.</span></span> |`ms(NOW/DAY)`<br>`ms(2000-01-01T00:00:00Z)`<br>`ms(mydatefield)`<br>`ms(NOW,mydatefield)`<br>`ms(mydatefield,2000-01-01T00:00:00Z)`<br>`ms(datefield1,datefield2)` |
| <span data-ttu-id="17c4d-582">否</span><span class="sxs-lookup"><span data-stu-id="17c4d-582">not</span></span> |<span data-ttu-id="17c4d-583">所包裝函式的邏輯負值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-583">The logically negated value of the wrapped function.</span></span> |<span data-ttu-id="17c4d-584">`not(exists(author))`：當 `exists(author)` 為 false 時才為 TRUE。</span><span class="sxs-lookup"><span data-stu-id="17c4d-584">`not(exists(author))` TRUE only when `exists(author)` is false.</span></span> |
| <span data-ttu-id="17c4d-585">或</span><span class="sxs-lookup"><span data-stu-id="17c4d-585">or</span></span> |<span data-ttu-id="17c4d-586">邏輯分離。</span><span class="sxs-lookup"><span data-stu-id="17c4d-586">A logical disjunction.</span></span> |<span data-ttu-id="17c4d-587">`or(value1,value2)`：如果 value1 或 value2 為 true，則為 TRUE。</span><span class="sxs-lookup"><span data-stu-id="17c4d-587">`or(value1,value2)` TRUE if either value1 or value2 is true.</span></span> |
| <span data-ttu-id="17c4d-588">pow</span><span class="sxs-lookup"><span data-stu-id="17c4d-588">pow</span></span> |<span data-ttu-id="17c4d-589">將指定的基底提升為指定的次方。</span><span class="sxs-lookup"><span data-stu-id="17c4d-589">Raises the specified base to the specified power.</span></span> <span data-ttu-id="17c4d-590">`pow(x,y)` 將 x 提升為次方 y。</span><span class="sxs-lookup"><span data-stu-id="17c4d-590">`pow(x,y)` raises x to the power of y.</span></span> |`pow(x,y)`<br>`pow(x,log(y))`<br><span data-ttu-id="17c4d-591">`pow(x,0.5)`：與 sqrt 相同。</span><span class="sxs-lookup"><span data-stu-id="17c4d-591">`pow(x,0.5)` The same as sqrt.</span></span> |
| <span data-ttu-id="17c4d-592">product</span><span class="sxs-lookup"><span data-stu-id="17c4d-592">product</span></span> |<span data-ttu-id="17c4d-593">傳回多個數值或函式 (指定為逗號分隔的清單) 的乘積。</span><span class="sxs-lookup"><span data-stu-id="17c4d-593">Returns the product of multiple values or functions, which are specified in a comma-separated list.</span></span> <span data-ttu-id="17c4d-594">`mul(...)` 也可以作為這個函式的別名。</span><span class="sxs-lookup"><span data-stu-id="17c4d-594">`mul(...)` may also be used as an alias for this function.</span></span> |`product(x,y,...)`<br>`product(x,2)`<br>`product(x,y)`<br>`mul(x,y)` |
| <span data-ttu-id="17c4d-595">recip</span><span class="sxs-lookup"><span data-stu-id="17c4d-595">recip</span></span> |<span data-ttu-id="17c4d-596">執行 `recip(x,m,a,b)` 實作 `a/(m*x+b)` 的倒數函式，其中 m、a 和 b 是常數，而 x 是任何任意複雜函式。</span><span class="sxs-lookup"><span data-stu-id="17c4d-596">Performs a reciprocal function with `recip(x,m,a,b)` implementing `a/(m*x+b)`, where m, a,and b are constants, and x is any arbitrarily complex function.</span></span> <span data-ttu-id="17c4d-597">a 與 b 相等而且 x>=0 時，此函式的最大值為 1，會在 x 增加時減少。</span><span class="sxs-lookup"><span data-stu-id="17c4d-597">When a and b are equal, and x>=0, this function has a maximum value of 1 that drops as x increases.</span></span> <span data-ttu-id="17c4d-598">同時增加 a 和 b 的值，可將整個函式移到曲線最平緩的部分。</span><span class="sxs-lookup"><span data-stu-id="17c4d-598">Increasing the value of a and b together results in a movement of the entire function to a flatter part of the curve.</span></span> <span data-ttu-id="17c4d-599">x 為 `rord(datefield)`時，這些屬性可以將這個設為提升較新文件的理想函式。</span><span class="sxs-lookup"><span data-stu-id="17c4d-599">These properties can make this an ideal function for boosting more recent documents when x is `rord(datefield)`.</span></span> |`recip(myfield,m,a,b)`<br>`recip(rord(creationDate),1,1000,1000)` |
| <span data-ttu-id="17c4d-600">rad</span><span class="sxs-lookup"><span data-stu-id="17c4d-600">rad</span></span> |<span data-ttu-id="17c4d-601">將度數轉換為弧度。</span><span class="sxs-lookup"><span data-stu-id="17c4d-601">Converts degrees to radians.</span></span> |`rad(x)` |
| <span data-ttu-id="17c4d-602">rint</span><span class="sxs-lookup"><span data-stu-id="17c4d-602">rint</span></span> |<span data-ttu-id="17c4d-603">四捨五入為最接近的整數。</span><span class="sxs-lookup"><span data-stu-id="17c4d-603">Rounds to the nearest integer.</span></span> |`rint(x)`  <br> <span data-ttu-id="17c4d-604">`rint(5.6)`：傳回 6</span><span class="sxs-lookup"><span data-stu-id="17c4d-604">`rint(5.6)` Returns 6</span></span> |
| <span data-ttu-id="17c4d-605">sin</span><span class="sxs-lookup"><span data-stu-id="17c4d-605">sin</span></span> |<span data-ttu-id="17c4d-606">傳回角度的正弦值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-606">Returns sine of an angle.</span></span> |`sin(x)` |
| <span data-ttu-id="17c4d-607">sinh</span><span class="sxs-lookup"><span data-stu-id="17c4d-607">sinh</span></span> |<span data-ttu-id="17c4d-608">傳回角度的雙曲正弦值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-608">Returns hyperbolic sine of an angle.</span></span> |`sinh(x)` |
| <span data-ttu-id="17c4d-609">級別</span><span class="sxs-lookup"><span data-stu-id="17c4d-609">scale</span></span> |<span data-ttu-id="17c4d-610">調整函式 x 的值，讓它們落在指定的 minTarget 與 maxTarget (含) 之間。</span><span class="sxs-lookup"><span data-stu-id="17c4d-610">Scales values of the function x, such that they fall between the specified minTarget and maxTarget inclusive.</span></span> <span data-ttu-id="17c4d-611">目前的實作會周遊所有函式值以取得最小值和最大值，讓它可以取得正確的小數位數。</span><span class="sxs-lookup"><span data-stu-id="17c4d-611">The current implementation traverses all of the function values to obtain the min and max, so it can pick the correct scale.</span></span> <span data-ttu-id="17c4d-612">目前的實作無法區別何時刪除文件或文件是否沒有值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-612">The current implementation cannot distinguish when documents have been deleted, or documents that have no value.</span></span> <span data-ttu-id="17c4d-613">在這些情況下，它會使用 0.0 值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-613">It uses 0.0 values for these cases.</span></span> <span data-ttu-id="17c4d-614">這表示，如果值通常都大於 0.0，其中一個還是可以將 0.0 當成要對應來源的最小值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-614">This means that if values are normally all greater than 0.0, one can still end up with 0.0 as the min value to map from.</span></span> <span data-ttu-id="17c4d-615">在這些情況下，適當的 `map()` 函式可以用做將 0.0 變更為實際範圍內之值的因應措施，如這裡所示：`scale(map(x,0,0,5),1,2)`</span><span class="sxs-lookup"><span data-stu-id="17c4d-615">In these cases, an appropriate `map()` function could be used as a workaround to change 0.0 to a value in the real range, as shown here: `scale(map(x,0,0,5),1,2)`</span></span> |`scale(x,minTarget,maxTarget)`<br><span data-ttu-id="17c4d-616">`scale(x,1,2)`：調整 x 值，讓所有值都在 1 與 2 (含) 之間。</span><span class="sxs-lookup"><span data-stu-id="17c4d-616">`scale(x,1,2)` Scales the values of x, such that all values are between 1 and 2 inclusive.</span></span> |
| <span data-ttu-id="17c4d-617">sqrt</span><span class="sxs-lookup"><span data-stu-id="17c4d-617">sqrt</span></span> |<span data-ttu-id="17c4d-618">傳回所指定數值或函式的平方根。</span><span class="sxs-lookup"><span data-stu-id="17c4d-618">Returns the square root of the specified value or function.</span></span> |`sqrt(x)`<br>`sqrt(100)`<br>`sqrt(sum(x,100))` |
| <span data-ttu-id="17c4d-619">strdist</span><span class="sxs-lookup"><span data-stu-id="17c4d-619">strdist</span></span> |<span data-ttu-id="17c4d-620">計算兩個字串之間的距離。</span><span class="sxs-lookup"><span data-stu-id="17c4d-620">Calculates the distance between two strings.</span></span> <span data-ttu-id="17c4d-621">使用 Lucene 拼字檢查程式 StringDistance 介面並支援該套件中可用的所有實作。</span><span class="sxs-lookup"><span data-stu-id="17c4d-621">Uses the Lucene spell checker StringDistance interface, and supports all of the implementations available in that package.</span></span> <span data-ttu-id="17c4d-622">也允許應用程式透過 Solr 的資源載入功能插入專屬的實作。</span><span class="sxs-lookup"><span data-stu-id="17c4d-622">Also allows applications to plug in their own, via Solr's resource loading capabilities.</span></span> <span data-ttu-id="17c4d-623">strdist 採用 `(string1, string2, distance measure)`。</span><span class="sxs-lookup"><span data-stu-id="17c4d-623">strdist takes `(string1, string2, distance measure)`.</span></span> <span data-ttu-id="17c4d-624">距離量值的可能值如下︰</span><span class="sxs-lookup"><span data-stu-id="17c4d-624">Possible values for distance measure are:</span></span><ul><li><span data-ttu-id="17c4d-625">jw: Jaro-Winkler</span><span class="sxs-lookup"><span data-stu-id="17c4d-625">jw: Jaro-Winkler</span></span></li><li><span data-ttu-id="17c4d-626">編輯︰Levenstein 或編輯距離</span><span class="sxs-lookup"><span data-stu-id="17c4d-626">edit: Levenstein or Edit distance</span></span></li><li><span data-ttu-id="17c4d-627">ngram：NGramDistance，如果指定，也可以選擇性地傳入 ngram 大小。</span><span class="sxs-lookup"><span data-stu-id="17c4d-627">ngram: The NGramDistance, if specified, can optionally pass in the ngram size too.</span></span> <span data-ttu-id="17c4d-628">預設值為 2。</span><span class="sxs-lookup"><span data-stu-id="17c4d-628">Default is 2.</span></span></li><li><span data-ttu-id="17c4d-629">FQN：StringDistance 介面實作的完整類別名稱。</span><span class="sxs-lookup"><span data-stu-id="17c4d-629">FQN: Fully Qualified class Name for an implementation of the StringDistance interface.</span></span> <span data-ttu-id="17c4d-630">必須要有無引數建構函式。</span><span class="sxs-lookup"><span data-stu-id="17c4d-630">Must have a no-arg constructor.</span></span></li></ul> |`strdist("SOLR",id,edit)` |
| <span data-ttu-id="17c4d-631">sub</span><span class="sxs-lookup"><span data-stu-id="17c4d-631">sub</span></span> |<span data-ttu-id="17c4d-632">從 `sub(x,y)`傳回 x-y。</span><span class="sxs-lookup"><span data-stu-id="17c4d-632">Returns x-y from `sub(x,y)`.</span></span> |`sub(myfield,myfield2)`<br>`sub(100,sqrt(myfield))` |
| <span data-ttu-id="17c4d-633">Sum</span><span class="sxs-lookup"><span data-stu-id="17c4d-633">sum</span></span> |<span data-ttu-id="17c4d-634">傳回多個數值或函式 (指定為逗號分隔的清單) 的總和。</span><span class="sxs-lookup"><span data-stu-id="17c4d-634">Returns the sum of multiple values or functions, which are specified in a comma-separated list.</span></span> <span data-ttu-id="17c4d-635">`add(...)` 可以作為這個函式的別名。</span><span class="sxs-lookup"><span data-stu-id="17c4d-635">`add(...)` may be used as an alias for this function.</span></span> |`sum(x,y,...)`<br>`sum(x,1)`<br>`sum(x,y)`<br>`sum(sqrt(x),log(y),z,0.5)`<br>`add(x,y)` |
| <span data-ttu-id="17c4d-636">termfreq</span><span class="sxs-lookup"><span data-stu-id="17c4d-636">termfreq</span></span> |<span data-ttu-id="17c4d-637">傳回在該文件欄位中字詞出現的次數。</span><span class="sxs-lookup"><span data-stu-id="17c4d-637">Returns the number of times the term appears in the field for that document.</span></span> |<span data-ttu-id="17c4d-638">termfreq(text,'memory')</span><span class="sxs-lookup"><span data-stu-id="17c4d-638">termfreq(text,'memory')</span></span> |
| <span data-ttu-id="17c4d-639">tan</span><span class="sxs-lookup"><span data-stu-id="17c4d-639">tan</span></span> |<span data-ttu-id="17c4d-640">傳回角度的正切值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-640">Returns tangent of an angle.</span></span> |`tan(x)` |
| <span data-ttu-id="17c4d-641">tanh</span><span class="sxs-lookup"><span data-stu-id="17c4d-641">tanh</span></span> |<span data-ttu-id="17c4d-642">傳回角度的雙曲正切值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-642">Returns hyperbolic tangent of an angle.</span></span> |`tanh(x)` |

## <a name="search-field-and-facet-reference"></a><span data-ttu-id="17c4d-643">搜尋欄位和 Facet 參考 (英文)</span><span class="sxs-lookup"><span data-stu-id="17c4d-643">Search field and facet reference</span></span>
<span data-ttu-id="17c4d-644">當您使用記錄搜尋來尋找資料時，結果會顯示各種欄位和 Facet。</span><span class="sxs-lookup"><span data-stu-id="17c4d-644">When you use Log Search to find data, results display various field and facets.</span></span> <span data-ttu-id="17c4d-645">資訊的某些部分可能不太清楚。</span><span class="sxs-lookup"><span data-stu-id="17c4d-645">Some of the information might not appear very descriptive.</span></span> <span data-ttu-id="17c4d-646">使用下列資訊來協助了解結果。</span><span class="sxs-lookup"><span data-stu-id="17c4d-646">Use the following information to help you understand the results.</span></span>

| <span data-ttu-id="17c4d-647">欄位</span><span class="sxs-lookup"><span data-stu-id="17c4d-647">Field</span></span> | <span data-ttu-id="17c4d-648">搜尋類型</span><span class="sxs-lookup"><span data-stu-id="17c4d-648">Search type</span></span> | <span data-ttu-id="17c4d-649">說明</span><span class="sxs-lookup"><span data-stu-id="17c4d-649">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="17c4d-650">TenantId</span><span class="sxs-lookup"><span data-stu-id="17c4d-650">TenantId</span></span> |<span data-ttu-id="17c4d-651">全部</span><span class="sxs-lookup"><span data-stu-id="17c4d-651">All</span></span> |<span data-ttu-id="17c4d-652">用來分割資料。</span><span class="sxs-lookup"><span data-stu-id="17c4d-652">Used to partition data.</span></span> |
| <span data-ttu-id="17c4d-653">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="17c4d-653">TimeGenerated</span></span> |<span data-ttu-id="17c4d-654">全部</span><span class="sxs-lookup"><span data-stu-id="17c4d-654">All</span></span> |<span data-ttu-id="17c4d-655">用來驅動時間軸，timeselectors (在搜尋和其他螢幕中)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-655">Used to drive the timeline, timeselectors (in search and in other screens).</span></span> <span data-ttu-id="17c4d-656">它代表資料片段的產生 (通常在代理程式上) 時間。</span><span class="sxs-lookup"><span data-stu-id="17c4d-656">It represents when the piece of data was generated (typically on the agent).</span></span> <span data-ttu-id="17c4d-657">時間以 ISO 格式表示，且一律為 UTC。</span><span class="sxs-lookup"><span data-stu-id="17c4d-657">The time is expressed in ISO format, and is always UTC.</span></span> <span data-ttu-id="17c4d-658">如果類型是根據現有檢測 (也就是，記錄中的事件)，這通常是記錄項目/列/記錄的實際記錄時間。</span><span class="sxs-lookup"><span data-stu-id="17c4d-658">In the case of types that are based on existing instrumentation (that is, events in a log), this is typically the real time that the log entry/line/record was logged.</span></span> <span data-ttu-id="17c4d-659">針對某些透過管理組件或在雲端 (例如，建議或警示) 所產生的其他類型，時間代表不同的東西。</span><span class="sxs-lookup"><span data-stu-id="17c4d-659">For some of the other types that are produced either via management packs or in the cloud (for example, recommendations or alerts), the time represents something different.</span></span> <span data-ttu-id="17c4d-660">這是收集到含某種組態之快照集資料的這個新部分的時間，或根據它產生建議/警示的時間。</span><span class="sxs-lookup"><span data-stu-id="17c4d-660">This is the time when this new piece of data with a snapshot of a configuration of some sort was collected, or a recommendation/alert was produced based on it.</span></span> |
| <span data-ttu-id="17c4d-661">EventID</span><span class="sxs-lookup"><span data-stu-id="17c4d-661">EventID</span></span> |<span data-ttu-id="17c4d-662">Event</span><span class="sxs-lookup"><span data-stu-id="17c4d-662">Event</span></span> |<span data-ttu-id="17c4d-663">Windows 事件記錄中的 EventID。</span><span class="sxs-lookup"><span data-stu-id="17c4d-663">EventID in the Windows event log.</span></span> |
| <span data-ttu-id="17c4d-664">EventLog</span><span class="sxs-lookup"><span data-stu-id="17c4d-664">EventLog</span></span> |<span data-ttu-id="17c4d-665">Event</span><span class="sxs-lookup"><span data-stu-id="17c4d-665">Event</span></span> |<span data-ttu-id="17c4d-666">Windows 在其中記錄事件的事件記錄。</span><span class="sxs-lookup"><span data-stu-id="17c4d-666">Event log where the event was logged by Windows.</span></span> |
| <span data-ttu-id="17c4d-667">EventLevelName</span><span class="sxs-lookup"><span data-stu-id="17c4d-667">EventLevelName</span></span> |<span data-ttu-id="17c4d-668">Event</span><span class="sxs-lookup"><span data-stu-id="17c4d-668">Event</span></span> |<span data-ttu-id="17c4d-669">重大/警告/資訊/成功</span><span class="sxs-lookup"><span data-stu-id="17c4d-669">Critical/warning/information/success</span></span> |
| <span data-ttu-id="17c4d-670">EventLevel</span><span class="sxs-lookup"><span data-stu-id="17c4d-670">EventLevel</span></span> |<span data-ttu-id="17c4d-671">Event</span><span class="sxs-lookup"><span data-stu-id="17c4d-671">Event</span></span> |<span data-ttu-id="17c4d-672">重大/警告/資訊/成功的數值 (對於更容易/更適合閱讀的查詢，請改用 EventLevelName)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-672">Numerical value for critical/warning/information/success (use EventLevelName instead for easier/more readable queries).</span></span> |
| <span data-ttu-id="17c4d-673">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="17c4d-673">SourceSystem</span></span> |<span data-ttu-id="17c4d-674">全部</span><span class="sxs-lookup"><span data-stu-id="17c4d-674">All</span></span> |<span data-ttu-id="17c4d-675">資料來自何處 (根據服務的附加模式)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-675">Where the data comes from (in terms of attach mode to the service).</span></span> <span data-ttu-id="17c4d-676">範例包括 Microsoft System Center Operations Manager 和 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="17c4d-676">Examples include Microsoft System Center Operations Manager and Azure Storage.</span></span> |
| <span data-ttu-id="17c4d-677">ObjectName</span><span class="sxs-lookup"><span data-stu-id="17c4d-677">ObjectName</span></span> |<span data-ttu-id="17c4d-678">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="17c4d-678">PerfHourly</span></span> |<span data-ttu-id="17c4d-679">Windows 效能物件名稱。</span><span class="sxs-lookup"><span data-stu-id="17c4d-679">Windows performance object name.</span></span> |
| <span data-ttu-id="17c4d-680">InstanceName</span><span class="sxs-lookup"><span data-stu-id="17c4d-680">InstanceName</span></span> |<span data-ttu-id="17c4d-681">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="17c4d-681">PerfHourly</span></span> |<span data-ttu-id="17c4d-682">Windows 效能計數器執行個體名稱。</span><span class="sxs-lookup"><span data-stu-id="17c4d-682">Windows performance counter instance name.</span></span> |
| <span data-ttu-id="17c4d-683">CounteName</span><span class="sxs-lookup"><span data-stu-id="17c4d-683">CounteName</span></span> |<span data-ttu-id="17c4d-684">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="17c4d-684">PerfHourly</span></span> |<span data-ttu-id="17c4d-685">Windows 效能計數器名稱。</span><span class="sxs-lookup"><span data-stu-id="17c4d-685">Windows performance counter name.</span></span> |
| <span data-ttu-id="17c4d-686">ObjectDisplayName</span><span class="sxs-lookup"><span data-stu-id="17c4d-686">ObjectDisplayName</span></span> |<span data-ttu-id="17c4d-687">PerfHourly、ConfigurationAlert、ConfigurationObject、ConfigurationObjectProperty</span><span class="sxs-lookup"><span data-stu-id="17c4d-687">PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty</span></span> |<span data-ttu-id="17c4d-688">Operations Manager 中效能集合規則設為目標之物件的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="17c4d-688">Display name of the object targeted by a performance collection rule in Operations Manager.</span></span> <span data-ttu-id="17c4d-689">也可以是 Operational Insights 探索到之物件的顯示名稱，或針對其產生警示之物件的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="17c4d-689">Could also be the display name of the object discovered by Operational Insights, or against which the alert was generated.</span></span> |
| <span data-ttu-id="17c4d-690">RootObjectName</span><span class="sxs-lookup"><span data-stu-id="17c4d-690">RootObjectName</span></span> |<span data-ttu-id="17c4d-691">PerfHourly、ConfigurationAlert、ConfigurationObject、ConfigurationObjectProperty</span><span class="sxs-lookup"><span data-stu-id="17c4d-691">PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty</span></span> |<span data-ttu-id="17c4d-692">Operations Manager 中效能集合規則設為目標之物件的父系的父系 (在雙主控關聯性中) 的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="17c4d-692">Display name of the parent of the parent (in a double hosting relationship) of the object targeted by a performance collection rule in Operations Manager.</span></span> <span data-ttu-id="17c4d-693">也可以是 Operational Insights 探索到之物件的顯示名稱，或針對其產生警示之物件的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="17c4d-693">Could also be the display name of the object discovered by Operational Insights, or against which the alert was generated.</span></span> |
| <span data-ttu-id="17c4d-694">電腦</span><span class="sxs-lookup"><span data-stu-id="17c4d-694">Computer</span></span> |<span data-ttu-id="17c4d-695">大部分的類型</span><span class="sxs-lookup"><span data-stu-id="17c4d-695">Most types</span></span> |<span data-ttu-id="17c4d-696">資料所屬的電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="17c4d-696">Computer name that the data belongs to.</span></span> |
| <span data-ttu-id="17c4d-697">DeviceName</span><span class="sxs-lookup"><span data-stu-id="17c4d-697">DeviceName</span></span> |<span data-ttu-id="17c4d-698">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="17c4d-698">ProtectionStatus</span></span> |<span data-ttu-id="17c4d-699">資料所屬的電腦名稱 (如同 "Computer")。</span><span class="sxs-lookup"><span data-stu-id="17c4d-699">Computer name the data belongs to (same as "Computer").</span></span> |
| <span data-ttu-id="17c4d-700">DetectionId</span><span class="sxs-lookup"><span data-stu-id="17c4d-700">DetectionId</span></span> |<span data-ttu-id="17c4d-701">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="17c4d-701">ProtectionStatus</span></span> | |
| <span data-ttu-id="17c4d-702">ThreatStatusRank</span><span class="sxs-lookup"><span data-stu-id="17c4d-702">ThreatStatusRank</span></span> |<span data-ttu-id="17c4d-703">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="17c4d-703">ProtectionStatus</span></span> |<span data-ttu-id="17c4d-704">威脅狀態排名是威脅狀態的數字表示。</span><span class="sxs-lookup"><span data-stu-id="17c4d-704">Threat status rank is a numerical representation of the threat status.</span></span> <span data-ttu-id="17c4d-705">與 HTTP 回應碼類似，排名在數字之間會有間距 (這是無威脅為 150 而不是 100 或 0 的原因)，以留下空間來新增狀態。</span><span class="sxs-lookup"><span data-stu-id="17c4d-705">Similar to HTTP response codes, the ranking has gaps between the numbers (which is why no threats is 150 and not 100 or 0), leaving room to add new states.</span></span> <span data-ttu-id="17c4d-706">針對威脅狀態和防護狀態的彙總，目的是要顯示電腦在選取時間間隔中所經歷的最差狀態。</span><span class="sxs-lookup"><span data-stu-id="17c4d-706">For a rollup of threat status and protection status, the intention is to show the worst state that the computer has been in during the selected time period.</span></span> <span data-ttu-id="17c4d-707">數字可排名不同的狀態，以查看最高數字的記錄。</span><span class="sxs-lookup"><span data-stu-id="17c4d-707">The numbers rank the different states, so you can look for the record with the highest number.</span></span> |
| <span data-ttu-id="17c4d-708">ThreatStatus</span><span class="sxs-lookup"><span data-stu-id="17c4d-708">ThreatStatus</span></span> |<span data-ttu-id="17c4d-709">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="17c4d-709">ProtectionStatus</span></span> |<span data-ttu-id="17c4d-710">ThreatStatus 的描述，與 ThreatStatusRank 1:1 對應。</span><span class="sxs-lookup"><span data-stu-id="17c4d-710">Description of ThreatStatus, maps 1:1 with ThreatStatusRank.</span></span> |
| <span data-ttu-id="17c4d-711">TypeofProtection</span><span class="sxs-lookup"><span data-stu-id="17c4d-711">TypeofProtection</span></span> |<span data-ttu-id="17c4d-712">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="17c4d-712">ProtectionStatus</span></span> |<span data-ttu-id="17c4d-713">在電腦中偵測到的反惡意程式碼產品：無、Microsoft 惡意程式碼移除工具、Forefront 等等。</span><span class="sxs-lookup"><span data-stu-id="17c4d-713">Antimalware product that is detected in the computer: none, Microsoft Malware Removal tool, Forefront, and so on.</span></span> |
| <span data-ttu-id="17c4d-714">ScanDate</span><span class="sxs-lookup"><span data-stu-id="17c4d-714">ScanDate</span></span> |<span data-ttu-id="17c4d-715">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="17c4d-715">ProtectionStatus</span></span> | |
| <span data-ttu-id="17c4d-716">SourceHealthServiceId</span><span class="sxs-lookup"><span data-stu-id="17c4d-716">SourceHealthServiceId</span></span> |<span data-ttu-id="17c4d-717">ProtectionStatus、RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="17c4d-717">ProtectionStatus, RequiredUpdate</span></span> |<span data-ttu-id="17c4d-718">這台電腦之代理程式的 HealthService 識別碼。</span><span class="sxs-lookup"><span data-stu-id="17c4d-718">HealthService ID for this computer's agent.</span></span> |
| <span data-ttu-id="17c4d-719">HealthServiceId</span><span class="sxs-lookup"><span data-stu-id="17c4d-719">HealthServiceId</span></span> |<span data-ttu-id="17c4d-720">大部分的類型</span><span class="sxs-lookup"><span data-stu-id="17c4d-720">Most types</span></span> |<span data-ttu-id="17c4d-721">這台電腦之代理程式的 HealthService 識別碼。</span><span class="sxs-lookup"><span data-stu-id="17c4d-721">HealthService ID for this computer's agent.</span></span> |
| <span data-ttu-id="17c4d-722">ManagementGroupName</span><span class="sxs-lookup"><span data-stu-id="17c4d-722">ManagementGroupName</span></span> |<span data-ttu-id="17c4d-723">大部分的類型</span><span class="sxs-lookup"><span data-stu-id="17c4d-723">Most types</span></span> |<span data-ttu-id="17c4d-724">Operations Manager 附加代理程式的管理群組名稱。</span><span class="sxs-lookup"><span data-stu-id="17c4d-724">Management Group Name for Operations Manager-attached agents.</span></span> <span data-ttu-id="17c4d-725">否則會是 null/空白。</span><span class="sxs-lookup"><span data-stu-id="17c4d-725">Otherwise, it is null/blank.</span></span> |
| <span data-ttu-id="17c4d-726">ObjectType</span><span class="sxs-lookup"><span data-stu-id="17c4d-726">ObjectType</span></span> |<span data-ttu-id="17c4d-727">ConfigurationObject</span><span class="sxs-lookup"><span data-stu-id="17c4d-727">ConfigurationObject</span></span> |<span data-ttu-id="17c4d-728">由 Log Analytics 組態評估所探索到之這個物件的類型 (例如 Operations Manager 管理組件的類型/類別)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-728">Type (as in Operations Manager management pack's type/class) for this object, discovered by Log Analytics configuration assessment.</span></span> |
| <span data-ttu-id="17c4d-729">UpdateTitle</span><span class="sxs-lookup"><span data-stu-id="17c4d-729">UpdateTitle</span></span> |<span data-ttu-id="17c4d-730">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="17c4d-730">RequiredUpdate</span></span> |<span data-ttu-id="17c4d-731">找到未安裝的更新名稱。</span><span class="sxs-lookup"><span data-stu-id="17c4d-731">Name of the update that was found not installed.</span></span> |
| <span data-ttu-id="17c4d-732">PublishDate</span><span class="sxs-lookup"><span data-stu-id="17c4d-732">PublishDate</span></span> |<span data-ttu-id="17c4d-733">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="17c4d-733">RequiredUpdate</span></span> |<span data-ttu-id="17c4d-734">更新何時在 Microsoft Update 上發佈。</span><span class="sxs-lookup"><span data-stu-id="17c4d-734">When the update was published on Microsoft Update.</span></span> |
| <span data-ttu-id="17c4d-735">伺服器</span><span class="sxs-lookup"><span data-stu-id="17c4d-735">Server</span></span> |<span data-ttu-id="17c4d-736">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="17c4d-736">RequiredUpdate</span></span> |<span data-ttu-id="17c4d-737">資料所屬的電腦名稱 (如同 "Computer")。</span><span class="sxs-lookup"><span data-stu-id="17c4d-737">Computer name the data belongs to (same as "Computer").</span></span> |
| <span data-ttu-id="17c4d-738">產品</span><span class="sxs-lookup"><span data-stu-id="17c4d-738">Product</span></span> |<span data-ttu-id="17c4d-739">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="17c4d-739">RequiredUpdate</span></span> |<span data-ttu-id="17c4d-740">更新適用的產品。</span><span class="sxs-lookup"><span data-stu-id="17c4d-740">Product that the update applies to.</span></span> |
| <span data-ttu-id="17c4d-741">UpdateClassification</span><span class="sxs-lookup"><span data-stu-id="17c4d-741">UpdateClassification</span></span> |<span data-ttu-id="17c4d-742">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="17c4d-742">RequiredUpdate</span></span> |<span data-ttu-id="17c4d-743">更新類型 (例如，更新彙總套件、Service Pack)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-743">Type of update (for example, update rollup or service pack).</span></span> |
| <span data-ttu-id="17c4d-744">KBID</span><span class="sxs-lookup"><span data-stu-id="17c4d-744">KBID</span></span> |<span data-ttu-id="17c4d-745">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="17c4d-745">RequiredUpdate</span></span> |<span data-ttu-id="17c4d-746">描述此最佳做法或更新的 KB 文章識別碼。</span><span class="sxs-lookup"><span data-stu-id="17c4d-746">KB article ID that describes this best practice or update.</span></span> |
| <span data-ttu-id="17c4d-747">WorkflowName</span><span class="sxs-lookup"><span data-stu-id="17c4d-747">WorkflowName</span></span> |<span data-ttu-id="17c4d-748">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="17c4d-748">ConfigurationAlert</span></span> |<span data-ttu-id="17c4d-749">產生警示之規則或監視器的名稱。</span><span class="sxs-lookup"><span data-stu-id="17c4d-749">Name of the rule or monitor that produced the alert.</span></span> |
| <span data-ttu-id="17c4d-750">嚴重性</span><span class="sxs-lookup"><span data-stu-id="17c4d-750">Severity</span></span> |<span data-ttu-id="17c4d-751">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="17c4d-751">ConfigurationAlert</span></span> |<span data-ttu-id="17c4d-752">警示的嚴重性。</span><span class="sxs-lookup"><span data-stu-id="17c4d-752">Severity of the alert.</span></span> |
| <span data-ttu-id="17c4d-753">優先順序</span><span class="sxs-lookup"><span data-stu-id="17c4d-753">Priority</span></span> |<span data-ttu-id="17c4d-754">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="17c4d-754">ConfigurationAlert</span></span> |<span data-ttu-id="17c4d-755">警示的優先順序。</span><span class="sxs-lookup"><span data-stu-id="17c4d-755">Priority of the alert.</span></span> |
| <span data-ttu-id="17c4d-756">IsMonitorAlert</span><span class="sxs-lookup"><span data-stu-id="17c4d-756">IsMonitorAlert</span></span> |<span data-ttu-id="17c4d-757">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="17c4d-757">ConfigurationAlert</span></span> |<span data-ttu-id="17c4d-758">此警示由監視器 (true) 或規則 (false) 所產生？</span><span class="sxs-lookup"><span data-stu-id="17c4d-758">Is this alert generated by a monitor (true) or a rule (false)?</span></span> |
| <span data-ttu-id="17c4d-759">AlertParameters</span><span class="sxs-lookup"><span data-stu-id="17c4d-759">AlertParameters</span></span> |<span data-ttu-id="17c4d-760">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="17c4d-760">ConfigurationAlert</span></span> |<span data-ttu-id="17c4d-761">使用 Log Analytics 警示之參數的 XML。</span><span class="sxs-lookup"><span data-stu-id="17c4d-761">XML with the parameters of the Log Analytics alert.</span></span> |
| <span data-ttu-id="17c4d-762">Context</span><span class="sxs-lookup"><span data-stu-id="17c4d-762">Context</span></span> |<span data-ttu-id="17c4d-763">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="17c4d-763">ConfigurationAlert</span></span> |<span data-ttu-id="17c4d-764">使用 Log Analytics 警示之內容的 XML。</span><span class="sxs-lookup"><span data-stu-id="17c4d-764">XML with the context of the Log Analytics alert.</span></span> |
| <span data-ttu-id="17c4d-765">工作負載</span><span class="sxs-lookup"><span data-stu-id="17c4d-765">Workload</span></span> |<span data-ttu-id="17c4d-766">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="17c4d-766">ConfigurationAlert</span></span> |<span data-ttu-id="17c4d-767">警示所參考的技術或工作負載。</span><span class="sxs-lookup"><span data-stu-id="17c4d-767">Technology or workload that the alert refers to.</span></span> |
| <span data-ttu-id="17c4d-768">AdvisorWorkload</span><span class="sxs-lookup"><span data-stu-id="17c4d-768">AdvisorWorkload</span></span> |<span data-ttu-id="17c4d-769">建議</span><span class="sxs-lookup"><span data-stu-id="17c4d-769">Recommendation</span></span> |<span data-ttu-id="17c4d-770">建議所參考的技術或工作負載。</span><span class="sxs-lookup"><span data-stu-id="17c4d-770">Technology or workload that the recommendation refers to.</span></span> |
| <span data-ttu-id="17c4d-771">說明</span><span class="sxs-lookup"><span data-stu-id="17c4d-771">Description</span></span> |<span data-ttu-id="17c4d-772">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="17c4d-772">ConfigurationAlert</span></span> |<span data-ttu-id="17c4d-773">警示描述 (簡短)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-773">Alert description (short).</span></span> |
| <span data-ttu-id="17c4d-774">DaysSinceLastUpdate</span><span class="sxs-lookup"><span data-stu-id="17c4d-774">DaysSinceLastUpdate</span></span> |<span data-ttu-id="17c4d-775">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="17c4d-775">UpdateAgent</span></span> |<span data-ttu-id="17c4d-776">此代理程式在幾天前 (相對於記錄的 TimeGenerated) 從 Windows Server Update Service (WSUS) 或 Microsoft Update 安裝了任何更新？</span><span class="sxs-lookup"><span data-stu-id="17c4d-776">How many days ago (relative to TimeGenerated of this record) did this agent install any update from Windows Server Update Service (WSUS) or Microsoft Update?</span></span> |
| <span data-ttu-id="17c4d-777">DaysSinceLastUpdateBucket</span><span class="sxs-lookup"><span data-stu-id="17c4d-777">DaysSinceLastUpdateBucket</span></span> |<span data-ttu-id="17c4d-778">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="17c4d-778">UpdateAgent</span></span> |<span data-ttu-id="17c4d-779">根據 DaysSinceLastUpdate，多久以前的時間值區分類是上一次從 WSUS/Microsoft Update 安裝任何更新的電腦。</span><span class="sxs-lookup"><span data-stu-id="17c4d-779">Based on DaysSinceLastUpdate, a categorization in time buckets of how long ago a computer last installed any update from WSUS/Microsoft Update.</span></span> |
| <span data-ttu-id="17c4d-780">AutomaticUpdateEnabled</span><span class="sxs-lookup"><span data-stu-id="17c4d-780">AutomaticUpdateEnabled</span></span> |<span data-ttu-id="17c4d-781">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="17c4d-781">UpdateAgent</span></span> |<span data-ttu-id="17c4d-782">自動更新檢查是在此代理程式上啟用或停用的嗎？</span><span class="sxs-lookup"><span data-stu-id="17c4d-782">Is automatic update checking enabled or disabled on this agent?</span></span> |
| <span data-ttu-id="17c4d-783">AutomaticUpdateValue</span><span class="sxs-lookup"><span data-stu-id="17c4d-783">AutomaticUpdateValue</span></span> |<span data-ttu-id="17c4d-784">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="17c4d-784">UpdateAgent</span></span> |<span data-ttu-id="17c4d-785">自動更新檢查會設為自動下載和安裝、只下載，或只檢查嗎？</span><span class="sxs-lookup"><span data-stu-id="17c4d-785">Is automatic update checking set to automatically download and install, only download, or only check?</span></span> |
| <span data-ttu-id="17c4d-786">WindowsUpdateAgentVersion</span><span class="sxs-lookup"><span data-stu-id="17c4d-786">WindowsUpdateAgentVersion</span></span> |<span data-ttu-id="17c4d-787">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="17c4d-787">UpdateAgent</span></span> |<span data-ttu-id="17c4d-788">Microsoft Update 代理程式的版本號碼。</span><span class="sxs-lookup"><span data-stu-id="17c4d-788">Version number of the Microsoft Update agent.</span></span> |
| <span data-ttu-id="17c4d-789">WSUSServer</span><span class="sxs-lookup"><span data-stu-id="17c4d-789">WSUSServer</span></span> |<span data-ttu-id="17c4d-790">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="17c4d-790">UpdateAgent</span></span> |<span data-ttu-id="17c4d-791">此更新代理程式的目標是哪個 WSUS 伺服器？</span><span class="sxs-lookup"><span data-stu-id="17c4d-791">Which WSUS server is this update agent targeting?</span></span> |
| <span data-ttu-id="17c4d-792">OSVersion</span><span class="sxs-lookup"><span data-stu-id="17c4d-792">OSVersion</span></span> |<span data-ttu-id="17c4d-793">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="17c4d-793">UpdateAgent</span></span> |<span data-ttu-id="17c4d-794">此更新代理程式在其上執行的作業系統版本。</span><span class="sxs-lookup"><span data-stu-id="17c4d-794">Version of the operating system this update agent is running on.</span></span> |
| <span data-ttu-id="17c4d-795">名稱</span><span class="sxs-lookup"><span data-stu-id="17c4d-795">Name</span></span> |<span data-ttu-id="17c4d-796">建議，ConfigurationObjectProperty</span><span class="sxs-lookup"><span data-stu-id="17c4d-796">Recommendation, ConfigurationObjectProperty</span></span> |<span data-ttu-id="17c4d-797">來自 Log Analytics 組態評估的建議名稱/標題或屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="17c4d-797">Name/title of the recommendation, or name of the property from Log Analytics configuration assessment.</span></span> |
| <span data-ttu-id="17c4d-798">值</span><span class="sxs-lookup"><span data-stu-id="17c4d-798">Value</span></span> |<span data-ttu-id="17c4d-799">ConfigurationObjectProperty</span><span class="sxs-lookup"><span data-stu-id="17c4d-799">ConfigurationObjectProperty</span></span> |<span data-ttu-id="17c4d-800">來自 Log Analytics 組態評估的屬性值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-800">Value of a property from Log Analytics configuration assessment.</span></span> |
| <span data-ttu-id="17c4d-801">KBLink</span><span class="sxs-lookup"><span data-stu-id="17c4d-801">KBLink</span></span> |<span data-ttu-id="17c4d-802">建議</span><span class="sxs-lookup"><span data-stu-id="17c4d-802">Recommendation</span></span> |<span data-ttu-id="17c4d-803">描述此最佳做法或更新的 KB 文章 URL。</span><span class="sxs-lookup"><span data-stu-id="17c4d-803">URL to the KB article that describes this best practice or update.</span></span> |
| <span data-ttu-id="17c4d-804">RecommendationStatus</span><span class="sxs-lookup"><span data-stu-id="17c4d-804">RecommendationStatus</span></span> |<span data-ttu-id="17c4d-805">建議</span><span class="sxs-lookup"><span data-stu-id="17c4d-805">Recommendation</span></span> |<span data-ttu-id="17c4d-806">建議為一些類型，其記錄會更新，而不只是新增至搜尋索引。</span><span class="sxs-lookup"><span data-stu-id="17c4d-806">Recommendations are among the few types whose records get updated, not just added to the search index.</span></span> <span data-ttu-id="17c4d-807">此狀態會變更建議是否為作用中/開啟，或者 Log Analytics 是否偵測到狀態已解決。</span><span class="sxs-lookup"><span data-stu-id="17c4d-807">This status changes whether the recommendation is active/open, or if Log Analytics detects that it has been resolved.</span></span> |
| <span data-ttu-id="17c4d-808">RenderedDescription</span><span class="sxs-lookup"><span data-stu-id="17c4d-808">RenderedDescription</span></span> |<span data-ttu-id="17c4d-809">Event</span><span class="sxs-lookup"><span data-stu-id="17c4d-809">Event</span></span> |<span data-ttu-id="17c4d-810">Windows 事件的呈現描述 (具有填入參數的重複使用文字)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-810">Rendered description (reused text with populated parameters) of a Windows event.</span></span> |
| <span data-ttu-id="17c4d-811">ParameterXml</span><span class="sxs-lookup"><span data-stu-id="17c4d-811">ParameterXml</span></span> |<span data-ttu-id="17c4d-812">Event</span><span class="sxs-lookup"><span data-stu-id="17c4d-812">Event</span></span> |<span data-ttu-id="17c4d-813">使用 Windows 事件之資料區段中參數的 XML (如同在事件檢視器中所見)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-813">XML with the parameters in the data section of a Windows Event (as seen in event viewer).</span></span> |
| <span data-ttu-id="17c4d-814">EventData</span><span class="sxs-lookup"><span data-stu-id="17c4d-814">EventData</span></span> |<span data-ttu-id="17c4d-815">Event</span><span class="sxs-lookup"><span data-stu-id="17c4d-815">Event</span></span> |<span data-ttu-id="17c4d-816">使用 Windows 事件之完整資料區段的 XML (如同在事件檢視器中所見)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-816">XML with the whole data section of a Windows Event (as seen in event viewer).</span></span> |
| <span data-ttu-id="17c4d-817">來源</span><span class="sxs-lookup"><span data-stu-id="17c4d-817">Source</span></span> |<span data-ttu-id="17c4d-818">Event</span><span class="sxs-lookup"><span data-stu-id="17c4d-818">Event</span></span> |<span data-ttu-id="17c4d-819">產生事件的事件記錄來源。</span><span class="sxs-lookup"><span data-stu-id="17c4d-819">Event log source that generated the event.</span></span> |
| <span data-ttu-id="17c4d-820">EventCategory</span><span class="sxs-lookup"><span data-stu-id="17c4d-820">EventCategory</span></span> |<span data-ttu-id="17c4d-821">Event</span><span class="sxs-lookup"><span data-stu-id="17c4d-821">Event</span></span> |<span data-ttu-id="17c4d-822">事件的類別，直接來自 Windows 事件記錄。</span><span class="sxs-lookup"><span data-stu-id="17c4d-822">Category of the event, directly from the Windows event log.</span></span> |
| <span data-ttu-id="17c4d-823">UserName</span><span class="sxs-lookup"><span data-stu-id="17c4d-823">UserName</span></span> |<span data-ttu-id="17c4d-824">Event</span><span class="sxs-lookup"><span data-stu-id="17c4d-824">Event</span></span> |<span data-ttu-id="17c4d-825">Windows 事件的使用者名稱 (通常是 NT AUTHORITY\LOCALSYSTEM)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-825">User name of the Windows event (typically, NT AUTHORITY\LOCALSYSTEM).</span></span> |
| <span data-ttu-id="17c4d-826">SampleValue</span><span class="sxs-lookup"><span data-stu-id="17c4d-826">SampleValue</span></span> |<span data-ttu-id="17c4d-827">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="17c4d-827">PerfHourly</span></span> |<span data-ttu-id="17c4d-828">效能計數器每小時彙總的平均值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-828">Average value for the hourly aggregation of a performance counter.</span></span> |
| <span data-ttu-id="17c4d-829">Min</span><span class="sxs-lookup"><span data-stu-id="17c4d-829">Min</span></span> |<span data-ttu-id="17c4d-830">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="17c4d-830">PerfHourly</span></span> |<span data-ttu-id="17c4d-831">效能計數器每小時彙總的每小時間隔內最小值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-831">Minimum value in the hourly interval of a performance counter hourly aggregate.</span></span> |
| <span data-ttu-id="17c4d-832">max</span><span class="sxs-lookup"><span data-stu-id="17c4d-832">Max</span></span> |<span data-ttu-id="17c4d-833">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="17c4d-833">PerfHourly</span></span> |<span data-ttu-id="17c4d-834">效能計數器每小時彙總的每小時間隔內最大值。</span><span class="sxs-lookup"><span data-stu-id="17c4d-834">Maximum value in the hourly interval of a performance counter hourly aggregate.</span></span> |
| <span data-ttu-id="17c4d-835">Percentile95</span><span class="sxs-lookup"><span data-stu-id="17c4d-835">Percentile95</span></span> |<span data-ttu-id="17c4d-836">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="17c4d-836">PerfHourly</span></span> |<span data-ttu-id="17c4d-837">效能計數器每小時彙總的每小時間隔內第 95 個百分位數。</span><span class="sxs-lookup"><span data-stu-id="17c4d-837">The 95th percentile value for the hourly interval of a performance counter hourly aggregate.</span></span> |
| <span data-ttu-id="17c4d-838">SampleCount</span><span class="sxs-lookup"><span data-stu-id="17c4d-838">SampleCount</span></span> |<span data-ttu-id="17c4d-839">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="17c4d-839">PerfHourly</span></span> |<span data-ttu-id="17c4d-840">多少未經處理的效能計數器範例用來產生此每小時彙總記錄。</span><span class="sxs-lookup"><span data-stu-id="17c4d-840">How many raw performance counter samples were used to produce this hourly aggregate record.</span></span> |
| <span data-ttu-id="17c4d-841">Threat</span><span class="sxs-lookup"><span data-stu-id="17c4d-841">Threat</span></span> |<span data-ttu-id="17c4d-842">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="17c4d-842">ProtectionStatus</span></span> |<span data-ttu-id="17c4d-843">找到的惡意程式碼名稱。</span><span class="sxs-lookup"><span data-stu-id="17c4d-843">Name of malware found.</span></span> |
| <span data-ttu-id="17c4d-844">StorageAccount</span><span class="sxs-lookup"><span data-stu-id="17c4d-844">StorageAccount</span></span> |<span data-ttu-id="17c4d-845">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="17c4d-845">W3CIISLog</span></span> |<span data-ttu-id="17c4d-846">從其中讀取記錄的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="17c4d-846">Azure Storage account the log was read from.</span></span> |
| <span data-ttu-id="17c4d-847">AzureDeploymentID</span><span class="sxs-lookup"><span data-stu-id="17c4d-847">AzureDeploymentID</span></span> |<span data-ttu-id="17c4d-848">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="17c4d-848">W3CIISLog</span></span> |<span data-ttu-id="17c4d-849">記錄所屬之雲端服務的 Azure 部署識別碼。</span><span class="sxs-lookup"><span data-stu-id="17c4d-849">Azure deployment ID of the cloud service the log belongs to.</span></span> |
| <span data-ttu-id="17c4d-850">角色</span><span class="sxs-lookup"><span data-stu-id="17c4d-850">Role</span></span> |<span data-ttu-id="17c4d-851">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="17c4d-851">W3CIISLog</span></span> |<span data-ttu-id="17c4d-852">記錄所屬之 Azure 雲端服務的角色。</span><span class="sxs-lookup"><span data-stu-id="17c4d-852">Role of the Azure cloud service the log belongs to.</span></span> |
| <span data-ttu-id="17c4d-853">RoleInstance</span><span class="sxs-lookup"><span data-stu-id="17c4d-853">RoleInstance</span></span> |<span data-ttu-id="17c4d-854">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="17c4d-854">W3CIISLog</span></span> |<span data-ttu-id="17c4d-855">記錄所屬之 Azure 角色的 RoleInstance。</span><span class="sxs-lookup"><span data-stu-id="17c4d-855">RoleInstance of the Azure role that the log belongs to.</span></span> |
| <span data-ttu-id="17c4d-856">sSiteName</span><span class="sxs-lookup"><span data-stu-id="17c4d-856">sSiteName</span></span> |<span data-ttu-id="17c4d-857">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="17c4d-857">W3CIISLog</span></span> |<span data-ttu-id="17c4d-858">記錄所屬的 IIS 網站 (metabase 標記法)；在原始記錄中的 s-sitename 欄位。</span><span class="sxs-lookup"><span data-stu-id="17c4d-858">IIS website that the log belongs to (metabase notation); the s-sitename field in the original log.</span></span> |
| <span data-ttu-id="17c4d-859">sComputerName</span><span class="sxs-lookup"><span data-stu-id="17c4d-859">sComputerName</span></span> |<span data-ttu-id="17c4d-860">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="17c4d-860">W3CIISLog</span></span> |<span data-ttu-id="17c4d-861">原始記錄中的 s-computername 欄位。</span><span class="sxs-lookup"><span data-stu-id="17c4d-861">The s-computername field in the original log.</span></span> |
| <span data-ttu-id="17c4d-862">sIP</span><span class="sxs-lookup"><span data-stu-id="17c4d-862">sIP</span></span> |<span data-ttu-id="17c4d-863">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="17c4d-863">W3CIISLog</span></span> |<span data-ttu-id="17c4d-864">HTTP 要求被定址的目標伺服器 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="17c4d-864">Server IP address the HTTP request was addressed to.</span></span> <span data-ttu-id="17c4d-865">原始記錄中的 s-ip 欄位。</span><span class="sxs-lookup"><span data-stu-id="17c4d-865">The s-ip field in the original log.</span></span> |
| <span data-ttu-id="17c4d-866">csMethod</span><span class="sxs-lookup"><span data-stu-id="17c4d-866">csMethod</span></span> |<span data-ttu-id="17c4d-867">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="17c4d-867">W3CIISLog</span></span> |<span data-ttu-id="17c4d-868">用戶端在 HTTP 要求中使用的 HTTP 方法 (例如，GET/POST)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-868">HTTP method (for example, GET/POST) used by the client in the HTTP request.</span></span> <span data-ttu-id="17c4d-869">原始記錄中的 cs-method。</span><span class="sxs-lookup"><span data-stu-id="17c4d-869">The cs-method in the original log.</span></span> |
| <span data-ttu-id="17c4d-870">cIP</span><span class="sxs-lookup"><span data-stu-id="17c4d-870">cIP</span></span> |<span data-ttu-id="17c4d-871">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="17c4d-871">W3CIISLog</span></span> |<span data-ttu-id="17c4d-872">HTTP 要求的來源用戶端 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="17c4d-872">Client IP address the HTTP request came from.</span></span> <span data-ttu-id="17c4d-873">原始記錄中的 c-ip 欄位。</span><span class="sxs-lookup"><span data-stu-id="17c4d-873">The c-ip field in the original log.</span></span> |
| <span data-ttu-id="17c4d-874">csUserAgent</span><span class="sxs-lookup"><span data-stu-id="17c4d-874">csUserAgent</span></span> |<span data-ttu-id="17c4d-875">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="17c4d-875">W3CIISLog</span></span> |<span data-ttu-id="17c4d-876">由用戶端宣告的 HTTP 使用者代理程式 (瀏覽器或其他方式)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-876">HTTP User-Agent declared by the client (browser or otherwise).</span></span> <span data-ttu-id="17c4d-877">原始記錄中的 cs-user-agent。</span><span class="sxs-lookup"><span data-stu-id="17c4d-877">The cs-user-agent in the original log.</span></span> |
| <span data-ttu-id="17c4d-878">scStatus</span><span class="sxs-lookup"><span data-stu-id="17c4d-878">scStatus</span></span> |<span data-ttu-id="17c4d-879">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="17c4d-879">W3CIISLog</span></span> |<span data-ttu-id="17c4d-880">由伺服器傳回給用戶端的 HTTP 狀態碼 (例如，200/403/500)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-880">HTTP Status code (for example, 200/403/500) returned by the server to the client.</span></span> <span data-ttu-id="17c4d-881">原始記錄中的 cs-status。</span><span class="sxs-lookup"><span data-stu-id="17c4d-881">The cs-status in the original log.</span></span> |
| <span data-ttu-id="17c4d-882">TimeTaken</span><span class="sxs-lookup"><span data-stu-id="17c4d-882">TimeTaken</span></span> |<span data-ttu-id="17c4d-883">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="17c4d-883">W3CIISLog</span></span> |<span data-ttu-id="17c4d-884">完成要求所花費的時間 (以毫秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-884">How long (in milliseconds) that the request took to complete.</span></span> <span data-ttu-id="17c4d-885">原始記錄中的 timetaken 欄位。</span><span class="sxs-lookup"><span data-stu-id="17c4d-885">The timetaken field in the original log.</span></span> |
| <span data-ttu-id="17c4d-886">csUriStem</span><span class="sxs-lookup"><span data-stu-id="17c4d-886">csUriStem</span></span> |<span data-ttu-id="17c4d-887">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="17c4d-887">W3CIISLog</span></span> |<span data-ttu-id="17c4d-888">要求的相對 URI (沒有主機位址，也就是 /search) 的要求。</span><span class="sxs-lookup"><span data-stu-id="17c4d-888">Relative URI (without host address, that is, /search ) that was requested.</span></span> <span data-ttu-id="17c4d-889">原始記錄中的 cs-uristem 欄位。</span><span class="sxs-lookup"><span data-stu-id="17c4d-889">The cs-uristem field in the original log.</span></span> |
| <span data-ttu-id="17c4d-890">csUriQuery</span><span class="sxs-lookup"><span data-stu-id="17c4d-890">csUriQuery</span></span> |<span data-ttu-id="17c4d-891">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="17c4d-891">W3CIISLog</span></span> |<span data-ttu-id="17c4d-892">URI 查詢。</span><span class="sxs-lookup"><span data-stu-id="17c4d-892">URI query.</span></span> <span data-ttu-id="17c4d-893">只有 ASP 頁面等動態頁面才需要 URI 查詢，所以此欄位通常包含靜態網頁的連字號。</span><span class="sxs-lookup"><span data-stu-id="17c4d-893">URI queries are necessary only for dynamic pages, such as ASP pages, so this field usually contains a hyphen for static pages.</span></span> |
| <span data-ttu-id="17c4d-894">sPort</span><span class="sxs-lookup"><span data-stu-id="17c4d-894">sPort</span></span> |<span data-ttu-id="17c4d-895">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="17c4d-895">W3CIISLog</span></span> |<span data-ttu-id="17c4d-896">傳送 HTTP 要求的目標伺服器連接埠 (也是 IIS 接聽的目標，因為 IIS 會挑選該連接埠)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-896">Server port that the HTTP request was sent to (and that IIS listens to, since it picked it up).</span></span> |
| <span data-ttu-id="17c4d-897">csUserName</span><span class="sxs-lookup"><span data-stu-id="17c4d-897">csUserName</span></span> |<span data-ttu-id="17c4d-898">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="17c4d-898">W3CIISLog</span></span> |<span data-ttu-id="17c4d-899">已驗證的使用者名稱，如果要求已通過驗證且不匿名。</span><span class="sxs-lookup"><span data-stu-id="17c4d-899">Authenticated user name, if the request is authenticated and not anonymous.</span></span> |
| <span data-ttu-id="17c4d-900">csVersion</span><span class="sxs-lookup"><span data-stu-id="17c4d-900">csVersion</span></span> |<span data-ttu-id="17c4d-901">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="17c4d-901">W3CIISLog</span></span> |<span data-ttu-id="17c4d-902">使用於要求中的 HTTP 通訊協定版本 (例如，HTTP/1.1)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-902">HTTP Protocol version used in the request (for example, HTTP/1.1).</span></span> |
| <span data-ttu-id="17c4d-903">csCookie</span><span class="sxs-lookup"><span data-stu-id="17c4d-903">csCookie</span></span> |<span data-ttu-id="17c4d-904">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="17c4d-904">W3CIISLog</span></span> |<span data-ttu-id="17c4d-905">Cookie 資訊。</span><span class="sxs-lookup"><span data-stu-id="17c4d-905">Cookie information.</span></span> |
| <span data-ttu-id="17c4d-906">csReferer</span><span class="sxs-lookup"><span data-stu-id="17c4d-906">csReferer</span></span> |<span data-ttu-id="17c4d-907">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="17c4d-907">W3CIISLog</span></span> |<span data-ttu-id="17c4d-908">使用者上次造訪的網站。</span><span class="sxs-lookup"><span data-stu-id="17c4d-908">Site that the user last visited.</span></span> <span data-ttu-id="17c4d-909">這個網站提供目前網站的連結。</span><span class="sxs-lookup"><span data-stu-id="17c4d-909">This site provided a link to the current site.</span></span> |
| <span data-ttu-id="17c4d-910">csHost</span><span class="sxs-lookup"><span data-stu-id="17c4d-910">csHost</span></span> |<span data-ttu-id="17c4d-911">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="17c4d-911">W3CIISLog</span></span> |<span data-ttu-id="17c4d-912">要求的主機標頭 (例如，www.mysite.com)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-912">Host header (for example, www.mysite.com) that was requested.</span></span> |
| <span data-ttu-id="17c4d-913">scSubStatus</span><span class="sxs-lookup"><span data-stu-id="17c4d-913">scSubStatus</span></span> |<span data-ttu-id="17c4d-914">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="17c4d-914">W3CIISLog</span></span> |<span data-ttu-id="17c4d-915">子狀態錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="17c4d-915">Substatus error code.</span></span> |
| <span data-ttu-id="17c4d-916">scWin32Status</span><span class="sxs-lookup"><span data-stu-id="17c4d-916">scWin32Status</span></span> |<span data-ttu-id="17c4d-917">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="17c4d-917">W3CIISLog</span></span> |<span data-ttu-id="17c4d-918">Windows 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="17c4d-918">Windows status code.</span></span> |
| <span data-ttu-id="17c4d-919">csBytes</span><span class="sxs-lookup"><span data-stu-id="17c4d-919">csBytes</span></span> |<span data-ttu-id="17c4d-920">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="17c4d-920">W3CIISLog</span></span> |<span data-ttu-id="17c4d-921">在要求中從用戶端傳送到伺服器的位元組。</span><span class="sxs-lookup"><span data-stu-id="17c4d-921">Bytes sent in the request from the client to the server.</span></span> |
| <span data-ttu-id="17c4d-922">scBytes</span><span class="sxs-lookup"><span data-stu-id="17c4d-922">scBytes</span></span> |<span data-ttu-id="17c4d-923">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="17c4d-923">W3CIISLog</span></span> |<span data-ttu-id="17c4d-924">在回應中從伺服器傳回給用戶端的位元組。</span><span class="sxs-lookup"><span data-stu-id="17c4d-924">Bytes returned back in the response from the server to the client.</span></span> |
| <span data-ttu-id="17c4d-925">ConfigChangeType</span><span class="sxs-lookup"><span data-stu-id="17c4d-925">ConfigChangeType</span></span> |<span data-ttu-id="17c4d-926">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="17c4d-926">ConfigurationChange</span></span> |<span data-ttu-id="17c4d-927">變更的類別 (例如，WindowsServices/Software)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-927">Type of change (for example, WindowsServices/Software).</span></span> |
| <span data-ttu-id="17c4d-928">ChangeCategory</span><span class="sxs-lookup"><span data-stu-id="17c4d-928">ChangeCategory</span></span> |<span data-ttu-id="17c4d-929">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="17c4d-929">ConfigurationChange</span></span> |<span data-ttu-id="17c4d-930">變更的類別 (已修改/已新增/已移除)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-930">Category of the change (Modified/Added/Removed).</span></span> |
| <span data-ttu-id="17c4d-931">SoftwareType</span><span class="sxs-lookup"><span data-stu-id="17c4d-931">SoftwareType</span></span> |<span data-ttu-id="17c4d-932">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="17c4d-932">ConfigurationChange</span></span> |<span data-ttu-id="17c4d-933">軟體的類型 (更新/應用程式)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-933">Type of software (Update/Application).</span></span> |
| <span data-ttu-id="17c4d-934">SoftwareName</span><span class="sxs-lookup"><span data-stu-id="17c4d-934">SoftwareName</span></span> |<span data-ttu-id="17c4d-935">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="17c4d-935">ConfigurationChange</span></span> |<span data-ttu-id="17c4d-936">軟體的名稱 (僅適用於軟體變更)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-936">Name of the software (only applicable to software changes).</span></span> |
| <span data-ttu-id="17c4d-937">發佈者</span><span class="sxs-lookup"><span data-stu-id="17c4d-937">Publisher</span></span> |<span data-ttu-id="17c4d-938">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="17c4d-938">ConfigurationChange</span></span> |<span data-ttu-id="17c4d-939">發佈軟體的供應商 (僅適用於軟體變更)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-939">Vendor who publishes the software (only applicable to software changes).</span></span> |
| <span data-ttu-id="17c4d-940">SvcChangeType</span><span class="sxs-lookup"><span data-stu-id="17c4d-940">SvcChangeType</span></span> |<span data-ttu-id="17c4d-941">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="17c4d-941">ConfigurationChange</span></span> |<span data-ttu-id="17c4d-942">已套用在 Windows 服務的變更類型 (State/StartupType/Path/ServiceAccount)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-942">Type of change that was applied on a Windows service (State/StartupType/Path/ServiceAccount).</span></span> <span data-ttu-id="17c4d-943">這僅適用於 Windows 服務變更。</span><span class="sxs-lookup"><span data-stu-id="17c4d-943">This is only applicable to Windows service changes.</span></span> |
| <span data-ttu-id="17c4d-944">SvcDisplayName</span><span class="sxs-lookup"><span data-stu-id="17c4d-944">SvcDisplayName</span></span> |<span data-ttu-id="17c4d-945">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="17c4d-945">ConfigurationChange</span></span> |<span data-ttu-id="17c4d-946">顯示已變更的服務名稱。</span><span class="sxs-lookup"><span data-stu-id="17c4d-946">Display name of the service that was changed.</span></span> |
| <span data-ttu-id="17c4d-947">SvcName</span><span class="sxs-lookup"><span data-stu-id="17c4d-947">SvcName</span></span> |<span data-ttu-id="17c4d-948">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="17c4d-948">ConfigurationChange</span></span> |<span data-ttu-id="17c4d-949">已變更的服務名稱。</span><span class="sxs-lookup"><span data-stu-id="17c4d-949">Name of the service that was changed.</span></span> |
| <span data-ttu-id="17c4d-950">SvcState</span><span class="sxs-lookup"><span data-stu-id="17c4d-950">SvcState</span></span> |<span data-ttu-id="17c4d-951">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="17c4d-951">ConfigurationChange</span></span> |<span data-ttu-id="17c4d-952">要求的新 (目前) 狀態。</span><span class="sxs-lookup"><span data-stu-id="17c4d-952">New (current) state of the service.</span></span> |
| <span data-ttu-id="17c4d-953">SvcPreviousState</span><span class="sxs-lookup"><span data-stu-id="17c4d-953">SvcPreviousState</span></span> |<span data-ttu-id="17c4d-954">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="17c4d-954">ConfigurationChange</span></span> |<span data-ttu-id="17c4d-955">服務的上一個已知狀態 (僅適用於服務狀態變更時)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-955">Previous known state of the service (only applicable if service state changed).</span></span> |
| <span data-ttu-id="17c4d-956">SvcStartupType</span><span class="sxs-lookup"><span data-stu-id="17c4d-956">SvcStartupType</span></span> |<span data-ttu-id="17c4d-957">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="17c4d-957">ConfigurationChange</span></span> |<span data-ttu-id="17c4d-958">服務啟動類型。</span><span class="sxs-lookup"><span data-stu-id="17c4d-958">Service startup type.</span></span> |
| <span data-ttu-id="17c4d-959">SvcPreviousStartupType</span><span class="sxs-lookup"><span data-stu-id="17c4d-959">SvcPreviousStartupType</span></span> |<span data-ttu-id="17c4d-960">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="17c4d-960">ConfigurationChange</span></span> |<span data-ttu-id="17c4d-961">上一個服務啟動類型 (僅適用於服務啟動類型變更時)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-961">Previous service startup type (only applicable if service startup type changed).</span></span> |
| <span data-ttu-id="17c4d-962">SvcAccount</span><span class="sxs-lookup"><span data-stu-id="17c4d-962">SvcAccount</span></span> |<span data-ttu-id="17c4d-963">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="17c4d-963">ConfigurationChange</span></span> |<span data-ttu-id="17c4d-964">服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="17c4d-964">Service account.</span></span> |
| <span data-ttu-id="17c4d-965">SvcPreviousAccount</span><span class="sxs-lookup"><span data-stu-id="17c4d-965">SvcPreviousAccount</span></span> |<span data-ttu-id="17c4d-966">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="17c4d-966">ConfigurationChange</span></span> |<span data-ttu-id="17c4d-967">先前的服務帳戶 (僅適用於服務帳戶變更時)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-967">Previous service account (only applicable if service account changed).</span></span> |
| <span data-ttu-id="17c4d-968">SvcPath</span><span class="sxs-lookup"><span data-stu-id="17c4d-968">SvcPath</span></span> |<span data-ttu-id="17c4d-969">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="17c4d-969">ConfigurationChange</span></span> |<span data-ttu-id="17c4d-970">Windows 服務的可執行檔路徑。</span><span class="sxs-lookup"><span data-stu-id="17c4d-970">Path to the executable of the Windows service.</span></span> |
| <span data-ttu-id="17c4d-971">SvcPreviousPath</span><span class="sxs-lookup"><span data-stu-id="17c4d-971">SvcPreviousPath</span></span> |<span data-ttu-id="17c4d-972">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="17c4d-972">ConfigurationChange</span></span> |<span data-ttu-id="17c4d-973">Windows 服務先前的可執行檔路徑 (僅適用於其變更時)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-973">Previous path of the executable for the Windows service (only applicable if it changed).</span></span> |
| <span data-ttu-id="17c4d-974">SvcDescription</span><span class="sxs-lookup"><span data-stu-id="17c4d-974">SvcDescription</span></span> |<span data-ttu-id="17c4d-975">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="17c4d-975">ConfigurationChange</span></span> |<span data-ttu-id="17c4d-976">服務的描述。</span><span class="sxs-lookup"><span data-stu-id="17c4d-976">Description of the service.</span></span> |
| <span data-ttu-id="17c4d-977">上一步</span><span class="sxs-lookup"><span data-stu-id="17c4d-977">Previous</span></span> |<span data-ttu-id="17c4d-978">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="17c4d-978">ConfigurationChange</span></span> |<span data-ttu-id="17c4d-979">此軟體先前的狀態 (已安裝/未安裝/上一個版本)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-979">Previous state of this software (Installed/Not Installed/previous version).</span></span> |
| <span data-ttu-id="17c4d-980">Current</span><span class="sxs-lookup"><span data-stu-id="17c4d-980">Current</span></span> |<span data-ttu-id="17c4d-981">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="17c4d-981">ConfigurationChange</span></span> |<span data-ttu-id="17c4d-982">此軟體最新的狀態 (已安裝/未安裝/上一個版本)。</span><span class="sxs-lookup"><span data-stu-id="17c4d-982">Latest state of this software (Installed/Not Installed/current version).</span></span> |

## <a name="next-steps"></a><span data-ttu-id="17c4d-983">後續步驟</span><span class="sxs-lookup"><span data-stu-id="17c4d-983">Next steps</span></span>
<span data-ttu-id="17c4d-984">如需記錄搜尋的其他資訊：</span><span class="sxs-lookup"><span data-stu-id="17c4d-984">For additional information about log searches:</span></span>

* <span data-ttu-id="17c4d-985">熟悉 [記錄搜尋](log-analytics-log-searches.md) 以檢視方案所收集的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="17c4d-985">Get familiar with [log searches](log-analytics-log-searches.md) to view detailed information gathered by solutions.</span></span>
* <span data-ttu-id="17c4d-986">使用 [Log Analytics 中的自訂欄位](log-analytics-custom-fields.md)來延伸記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="17c4d-986">Use [custom fields in Log Analytics](log-analytics-custom-fields.md) to extend log searches.</span></span>
