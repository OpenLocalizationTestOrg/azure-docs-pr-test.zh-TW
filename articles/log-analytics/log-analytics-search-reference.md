---
title: "aaaAzure 記錄分析搜尋參考 |Microsoft 文件"
description: "hello 記錄分析搜尋參考描述 hello 搜尋語言，並提供資料的搜尋和篩選運算式 toohelp 縮小搜尋範圍時，您可以使用 hello 一般查詢語法選項。"
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
ms.openlocfilehash: 7478a1139b88a1ce76ebb7b76027a6ccd66f4f27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-search-reference"></a><span data-ttu-id="1efa5-103">Log Analytics 搜尋參考</span><span class="sxs-lookup"><span data-stu-id="1efa5-103">Log Analytics search reference</span></span>

>[!NOTE]
> <span data-ttu-id="1efa5-104">本文說明的記錄搜尋記錄分析中使用 hello 目前的查詢語言。</span><span class="sxs-lookup"><span data-stu-id="1efa5-104">This article describes log searches using hello current query language in Log Analytics.</span></span>  <span data-ttu-id="1efa5-105">如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，則您應該太參閱[hello hello 新語言的語言參考](https://go.microsoft.com/fwlink/?linkid=856079)。</span><span class="sxs-lookup"><span data-stu-id="1efa5-105">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should refer too[hello language reference for hello new language](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>

<span data-ttu-id="1efa5-106">hello 關於搜尋語言的下列參考章節描述 hello 一般查詢語法選項，您可以搜尋資料及篩選運算式 toohelp 縮小搜尋範圍時使用。</span><span class="sxs-lookup"><span data-stu-id="1efa5-106">hello following reference section about search language describes hello general query syntax options you can use when searching for data and filtering expressions toohelp narrow your search.</span></span> <span data-ttu-id="1efa5-107">此外也說明您可以擷取 hello 資料上使用 tootake 動作的命令。</span><span class="sxs-lookup"><span data-stu-id="1efa5-107">It also describes commands that you can use tootake action on hello data retrieved.</span></span>

<span data-ttu-id="1efa5-108">您可以閱讀搜尋中傳回的 hello 欄位和 hello facet，協助您更深入的資料，請在 hello 類別相似探索[搜尋欄位和 facet 參考章節](#search-field-and-facet-reference)。</span><span class="sxs-lookup"><span data-stu-id="1efa5-108">You can read about hello fields returned in searches, and hello facets that help you discover more about similar categories of data, in hello [Search field and facet reference section](#search-field-and-facet-reference).</span></span>

## <a name="general-query-syntax"></a><span data-ttu-id="1efa5-109">一般查詢語法</span><span class="sxs-lookup"><span data-stu-id="1efa5-109">General query syntax</span></span>
<span data-ttu-id="1efa5-110">hello 一般查詢語法如下所示：</span><span class="sxs-lookup"><span data-stu-id="1efa5-110">hello syntax for general querying is as follows:</span></span>

```
filterExpression | command1 | command2 …
```

<span data-ttu-id="1efa5-111">hello 篩選條件運算式 (`filterExpression`) 定義的 hello"where"條件 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="1efa5-111">hello filter expression (`filterExpression`) defines hello "where" condition for hello query.</span></span> <span data-ttu-id="1efa5-112">hello 命令會套用 toohello hello 查詢所傳回的結果。</span><span class="sxs-lookup"><span data-stu-id="1efa5-112">hello commands apply toohello results returned by hello query.</span></span> <span data-ttu-id="1efa5-113">多個命令必須以 hello 縱線字元 (|) 分隔。</span><span class="sxs-lookup"><span data-stu-id="1efa5-113">Multiple commands must be separated by hello pipe character ( | ).</span></span>

### <a name="general-syntax-examples"></a><span data-ttu-id="1efa5-114">一般語法範例</span><span class="sxs-lookup"><span data-stu-id="1efa5-114">General syntax examples</span></span>
<span data-ttu-id="1efa5-115">範例：</span><span class="sxs-lookup"><span data-stu-id="1efa5-115">Examples:</span></span>

```
system
```

<span data-ttu-id="1efa5-116">此查詢會傳回結果包含 hello 文字*系統*已索引的全文檢索或詞彙搜尋的任何欄位中。</span><span class="sxs-lookup"><span data-stu-id="1efa5-116">This query returns results that contain hello word *system* in any field that has been indexed for full text or terms searching.</span></span>

> [!NOTE]
> <span data-ttu-id="1efa5-117">並非所有的欄位會編製索引如此一來，但最常見的文字欄位 （例如描述和名稱） 通常 hello。</span><span class="sxs-lookup"><span data-stu-id="1efa5-117">Not all fields are indexed this way, but hello most common textual fields (such as descriptions and names) usually are.</span></span>
>
>

```
system error
```

<span data-ttu-id="1efa5-118">此查詢會傳回結果包含 hello 文字*系統*和*錯誤*。</span><span class="sxs-lookup"><span data-stu-id="1efa5-118">This query returns results that contain hello words *system* and *error*.</span></span>

```
system error | sort ManagementGroupName, TimeGenerated desc | top 10
```

<span data-ttu-id="1efa5-119">此查詢會傳回結果包含 hello 文字*系統*和*錯誤*。</span><span class="sxs-lookup"><span data-stu-id="1efa5-119">This query returns results that contain hello words *system* and *error*.</span></span> <span data-ttu-id="1efa5-120">它再依 hello 結果 hello *ManagementGroupName*欄位 （依遞增順序），再以 hello *TimeGenerated*欄位 （依遞減順序）。</span><span class="sxs-lookup"><span data-stu-id="1efa5-120">It then sorts hello results by hello *ManagementGroupName* field (in ascending order), and then by hello *TimeGenerated* field (in descending order).</span></span> <span data-ttu-id="1efa5-121">它會採用只有 hello 前 10 個結果。</span><span class="sxs-lookup"><span data-stu-id="1efa5-121">It takes only hello first 10 results.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1efa5-122">所有 hello 欄位名稱和 hello hello 字串和文字欄位值會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="1efa5-122">All hello field names and hello values for hello string and text fields are case sensitive.</span></span>
>
>

## <a name="filter-expressions"></a><span data-ttu-id="1efa5-123">篩選運算式</span><span class="sxs-lookup"><span data-stu-id="1efa5-123">Filter expressions</span></span>
<span data-ttu-id="1efa5-124">hello 下列小節將詳細說明 hello 篩選運算式。</span><span class="sxs-lookup"><span data-stu-id="1efa5-124">hello following subsections explain hello filter expressions.</span></span>

### <a name="string-literals"></a><span data-ttu-id="1efa5-125">字串常值</span><span class="sxs-lookup"><span data-stu-id="1efa5-125">String literals</span></span>
<span data-ttu-id="1efa5-126">字串常值是無法 hello 剖析器辨識為關鍵字或預先定義的資料類型 （例如，數字或日期） 的任何字串。</span><span class="sxs-lookup"><span data-stu-id="1efa5-126">A string literal is any string that is not recognized by hello parser as a keyword or a predefined data type (for example, a number or date).</span></span>

<span data-ttu-id="1efa5-127">範例：</span><span class="sxs-lookup"><span data-stu-id="1efa5-127">Examples:</span></span>

```
These all are string literals
```

<span data-ttu-id="1efa5-128">此查詢會搜尋包含五個字全都出現的結果。</span><span class="sxs-lookup"><span data-stu-id="1efa5-128">This query searches for results that contain occurrences of all five words.</span></span> <span data-ttu-id="1efa5-129">tooperform 複雜的字串搜尋，請 hello 字串常值以引號括起來。</span><span class="sxs-lookup"><span data-stu-id="1efa5-129">tooperform a complex string search, enclose hello string literal in quotation marks.</span></span> <span data-ttu-id="1efa5-130">例如：</span><span class="sxs-lookup"><span data-stu-id="1efa5-130">For example:</span></span>

```
"Windows Server"
```

<span data-ttu-id="1efa5-131">這只會傳回結果為 Windows Server 的完全相符項目。</span><span class="sxs-lookup"><span data-stu-id="1efa5-131">This only returns results with exact matches for *Windows Server*.</span></span>

### <a name="numbers"></a><span data-ttu-id="1efa5-132">數字</span><span class="sxs-lookup"><span data-stu-id="1efa5-132">Numbers</span></span>
<span data-ttu-id="1efa5-133">hello 剖析器支援數值欄位 hello 十進位整數和浮點數語法。</span><span class="sxs-lookup"><span data-stu-id="1efa5-133">hello parser supports hello decimal integer and floating-point number syntax for numerical fields.</span></span>

<span data-ttu-id="1efa5-134">範例：</span><span class="sxs-lookup"><span data-stu-id="1efa5-134">Examples:</span></span>

```
Type:Perf 0.5
```

```
HTTP 500
```

### <a name="dates-and-times"></a><span data-ttu-id="1efa5-135">日期和時間</span><span class="sxs-lookup"><span data-stu-id="1efa5-135">Dates and times</span></span>
<span data-ttu-id="1efa5-136">Hello 系統中的資料的每個片段都有*TimeGenerated*屬性，代表的 hello 記錄 hello 原始日期和時間。</span><span class="sxs-lookup"><span data-stu-id="1efa5-136">Every piece of data in hello system has a *TimeGenerated* property, which represents hello original date and time of hello record.</span></span> <span data-ttu-id="1efa5-137">某些資料類型可能另外有日期和時間欄位 (例如，*LastModified*)。</span><span class="sxs-lookup"><span data-stu-id="1efa5-137">Some types of data can have additional date and time fields (for example, *LastModified*).</span></span>

<span data-ttu-id="1efa5-138">hello 時間表**圖表/時間**Azure Log Analytics 中的選取器會顯示經過一段時間 （相應 toohello 目前執行的查詢） 的結果分佈。</span><span class="sxs-lookup"><span data-stu-id="1efa5-138">hello timeline **Chart/Time** selector in Azure Log Analytics shows a distribution of results over time (according toohello current query being run).</span></span> <span data-ttu-id="1efa5-139">這根據 hello *TimeGenerated*欄位。</span><span class="sxs-lookup"><span data-stu-id="1efa5-139">This is based on hello *TimeGenerated* field.</span></span> <span data-ttu-id="1efa5-140">日期和時間欄位具有特定字串格式，可用於查詢 toorestrict hello 查詢 tooa 特定時間範圍內。</span><span class="sxs-lookup"><span data-stu-id="1efa5-140">Date and time fields have a specific string format that can be used in queries toorestrict hello query tooa particular timeframe.</span></span> <span data-ttu-id="1efa5-141">您也可以使用語法 toorefer toorelative （比方說，「 3 天前和 2 小時前之間 」） 的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="1efa5-141">You can also use syntax toorefer toorelative time intervals (for example, "between 3 days ago and 2 hours ago").</span></span>

<span data-ttu-id="1efa5-142">hello 下面是語法的供日期和時間的有效形式:</span><span class="sxs-lookup"><span data-stu-id="1efa5-142">hello following are valid forms of syntax for dates and times:</span></span>

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


<span data-ttu-id="1efa5-143">例如：</span><span class="sxs-lookup"><span data-stu-id="1efa5-143">For example:</span></span>

```
TimeGenerated:2013-10-01T12:20
```

<span data-ttu-id="1efa5-144">hello 前一個命令只會傳回*TimeGenerated* 12:20 於 2013 年 10 月 1 日的值。</span><span class="sxs-lookup"><span data-stu-id="1efa5-144">hello previous command returns only records with a *TimeGenerated* value of exactly 12:20 on October 1, 2013.</span></span>

<span data-ttu-id="1efa5-145">hello 剖析器也支援助憶鍵日期/時間值 hello，NOW。</span><span class="sxs-lookup"><span data-stu-id="1efa5-145">hello parser also supports hello mnemonic Date/Time value, NOW.</span></span> <span data-ttu-id="1efa5-146">（它是不太可能，這樣會產生任何結果，因為資料無法這麼快速 hello 系統）。</span><span class="sxs-lookup"><span data-stu-id="1efa5-146">(It is unlikely that this will yield any results, because data doesn’t make it through hello system that fast.)</span></span>

<span data-ttu-id="1efa5-147">這些範例是用於相對與絕對日期的建置組塊 toouse。</span><span class="sxs-lookup"><span data-stu-id="1efa5-147">These examples are building blocks toouse for relative and absolute dates.</span></span> <span data-ttu-id="1efa5-148">在 hello 接下來的三個子節中，您會看到如何 toouse 在更進階的篩選器，透過使用相對日期範圍的範例。</span><span class="sxs-lookup"><span data-stu-id="1efa5-148">In hello next three subsections, you'll see how toouse them in more advanced filters, with examples that use relative date ranges.</span></span>

### <a name="datetime-math"></a><span data-ttu-id="1efa5-149">日期/時間數學</span><span class="sxs-lookup"><span data-stu-id="1efa5-149">Date/Time math</span></span>
<span data-ttu-id="1efa5-150">使用 hello 日期/時間數學運算子 toooffset 或四捨五入 hello 日期/時間值，透過簡單的日期/時間計算。</span><span class="sxs-lookup"><span data-stu-id="1efa5-150">Use hello Date/Time math operators toooffset or round hello Date/Time value, by using simple Date/Time calculations.</span></span>

<span data-ttu-id="1efa5-151">語法：</span><span class="sxs-lookup"><span data-stu-id="1efa5-151">Syntax:</span></span>

```
datetime/unit
```

```
datetime[+|-]count unit
```

| <span data-ttu-id="1efa5-152">運算子</span><span class="sxs-lookup"><span data-stu-id="1efa5-152">Operator</span></span> | <span data-ttu-id="1efa5-153">說明</span><span class="sxs-lookup"><span data-stu-id="1efa5-153">Description</span></span> |
| --- | --- |
| / |<span data-ttu-id="1efa5-154">將日期/時間 toohello 指定單位。</span><span class="sxs-lookup"><span data-stu-id="1efa5-154">Rounds Date/Time toohello specified unit.</span></span> <span data-ttu-id="1efa5-155">例如，現在 / DAY 會四捨五入 hello 目前日期/時間 toomidnight hello 的目前日期。</span><span class="sxs-lookup"><span data-stu-id="1efa5-155">For example, NOW/DAY rounds hello current Date/Time toomidnight of hello current day.</span></span> |
| <span data-ttu-id="1efa5-156">+ 或 -</span><span class="sxs-lookup"><span data-stu-id="1efa5-156">+ or -</span></span> |<span data-ttu-id="1efa5-157">位移日期/時間 hello 所指定單位的數。</span><span class="sxs-lookup"><span data-stu-id="1efa5-157">Offsets Date/Time by hello specified number of units.</span></span> <span data-ttu-id="1efa5-158">例如，NOW + 1hour 會 hello 目前日期/時間往後移一個小時。</span><span class="sxs-lookup"><span data-stu-id="1efa5-158">For example, NOW+1HOUR offsets hello current Date/Time by one hour ahead.</span></span> <span data-ttu-id="1efa5-159">2013-10-01t12: 00-10days hello 日期值往回位移 10 天。</span><span class="sxs-lookup"><span data-stu-id="1efa5-159">2013-10-01T12:00-10DAYS offsets hello Date value back by 10 days.</span></span> |

<span data-ttu-id="1efa5-160">Hello 日期/時間數學運算子可以鏈結在一起。</span><span class="sxs-lookup"><span data-stu-id="1efa5-160">You can chain hello Date/Time math operators together.</span></span> <span data-ttu-id="1efa5-161">例如：</span><span class="sxs-lookup"><span data-stu-id="1efa5-161">For example:</span></span>

```
NOW+1HOUR-10MONTHS/MINUTE
```

<span data-ttu-id="1efa5-162">hello 下表列出支援的 hello 日期/時間單位。</span><span class="sxs-lookup"><span data-stu-id="1efa5-162">hello following table lists hello supported Date/Time units.</span></span>

| <span data-ttu-id="1efa5-163">日期/時間單位</span><span class="sxs-lookup"><span data-stu-id="1efa5-163">Date/Time unit</span></span> | <span data-ttu-id="1efa5-164">說明</span><span class="sxs-lookup"><span data-stu-id="1efa5-164">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1efa5-165">YEAR, YEARS</span><span class="sxs-lookup"><span data-stu-id="1efa5-165">YEAR, YEARS</span></span> |<span data-ttu-id="1efa5-166">重試回合 toocurrent 年份或由 hello 位移指定年的數。</span><span class="sxs-lookup"><span data-stu-id="1efa5-166">Rounds toocurrent year, or offsets by hello specified number of years.</span></span> |
| <span data-ttu-id="1efa5-167">MONTH, MONTHS</span><span class="sxs-lookup"><span data-stu-id="1efa5-167">MONTH, MONTHS</span></span> |<span data-ttu-id="1efa5-168">重試回合 toocurrent 月份或由 hello 位移指定月的數。</span><span class="sxs-lookup"><span data-stu-id="1efa5-168">Rounds toocurrent month, or offsets by hello specified number of months.</span></span> |
| <span data-ttu-id="1efa5-169">DAY, DAYS, DATE</span><span class="sxs-lookup"><span data-stu-id="1efa5-169">DAY, DAYS, DATE</span></span> |<span data-ttu-id="1efa5-170">重試回合 toocurrent 天 hello 月份或由 hello 位移指定的天數。</span><span class="sxs-lookup"><span data-stu-id="1efa5-170">Rounds toocurrent day of hello month, or offsets by hello specified number of days.</span></span> |
| <span data-ttu-id="1efa5-171">HOUR, HOURS</span><span class="sxs-lookup"><span data-stu-id="1efa5-171">HOUR, HOURS</span></span> |<span data-ttu-id="1efa5-172">重試回合 toocurrent 小時或由 hello 位移指定小時的數。</span><span class="sxs-lookup"><span data-stu-id="1efa5-172">Rounds toocurrent hour, or offsets by hello specified number of hours.</span></span> |
| <span data-ttu-id="1efa5-173">MINUTE, MINUTES</span><span class="sxs-lookup"><span data-stu-id="1efa5-173">MINUTE, MINUTES</span></span> |<span data-ttu-id="1efa5-174">重試回合 toocurrent 分鐘或由 hello 位移指定分鐘的數。</span><span class="sxs-lookup"><span data-stu-id="1efa5-174">Rounds toocurrent minute, or offsets by hello specified number of minutes.</span></span> |
| <span data-ttu-id="1efa5-175">SECOND, SECONDS</span><span class="sxs-lookup"><span data-stu-id="1efa5-175">SECOND, SECONDS</span></span> |<span data-ttu-id="1efa5-176">第二，四捨五入 toocurrent 或位移指定的 hello 的秒數字。</span><span class="sxs-lookup"><span data-stu-id="1efa5-176">Rounds toocurrent second, or offsets by hello specified number of seconds.</span></span> |
| <span data-ttu-id="1efa5-177">MILLISECOND, MILLISECONDS, MILLI, MILLIS</span><span class="sxs-lookup"><span data-stu-id="1efa5-177">MILLISECOND, MILLISECONDS, MILLI, MILLIS</span></span> |<span data-ttu-id="1efa5-178">重試回合 toocurrent 毫秒或由 hello 位移指定毫秒的數。</span><span class="sxs-lookup"><span data-stu-id="1efa5-178">Rounds toocurrent millisecond, or offsets by hello specified number of milliseconds.</span></span> |

### <a name="field-facets"></a><span data-ttu-id="1efa5-179">欄位 facet</span><span class="sxs-lookup"><span data-stu-id="1efa5-179">Field facets</span></span>
<span data-ttu-id="1efa5-180">藉由使用欄位 facet，您可以指定 hello 搜尋條件的特定欄位及其實際值。</span><span class="sxs-lookup"><span data-stu-id="1efa5-180">By using field facets, you can specify hello search condition for specific fields and their exact values.</span></span> <span data-ttu-id="1efa5-181">這不同於整個 hello 索引的各種詞彙撰寫 「 任意文字 」 查詢。</span><span class="sxs-lookup"><span data-stu-id="1efa5-181">This differs from writing "free text" queries for various terms throughout hello index.</span></span> <span data-ttu-id="1efa5-182">您已經在數個先前的範例中看過這項技術。</span><span class="sxs-lookup"><span data-stu-id="1efa5-182">You have already seen this technique in several previous examples.</span></span> <span data-ttu-id="1efa5-183">hello 以下是更複雜的範例。</span><span class="sxs-lookup"><span data-stu-id="1efa5-183">hello following are more complex examples.</span></span>

<span data-ttu-id="1efa5-184">**語法**</span><span class="sxs-lookup"><span data-stu-id="1efa5-184">**Syntax**</span></span>

```
field:value
```

```
field=value
```

<span data-ttu-id="1efa5-185">**說明**</span><span class="sxs-lookup"><span data-stu-id="1efa5-185">**Description**</span></span>

<span data-ttu-id="1efa5-186">搜尋 hello hello 特定值的欄位。</span><span class="sxs-lookup"><span data-stu-id="1efa5-186">Searches hello field for hello specific value.</span></span> <span data-ttu-id="1efa5-187">hello 值可以是字串常值、 數字或日期和時間。</span><span class="sxs-lookup"><span data-stu-id="1efa5-187">hello value can be a string literal, number, or date and time.</span></span>

<span data-ttu-id="1efa5-188">例如：</span><span class="sxs-lookup"><span data-stu-id="1efa5-188">For example:</span></span>

```
TimeGenerated:NOW
```

```
ObjectDisplayName:"server01.contoso.com"
```

```
SampleValue:0.3
```

<span data-ttu-id="1efa5-189">**語法**</span><span class="sxs-lookup"><span data-stu-id="1efa5-189">**Syntax**</span></span>

<span data-ttu-id="1efa5-190">field>value</span><span class="sxs-lookup"><span data-stu-id="1efa5-190">*field>value*</span></span>

<span data-ttu-id="1efa5-191">field<value</span><span class="sxs-lookup"><span data-stu-id="1efa5-191">*field<value*</span></span>

<span data-ttu-id="1efa5-192">field>=value</span><span class="sxs-lookup"><span data-stu-id="1efa5-192">*field>=value*</span></span>

<span data-ttu-id="1efa5-193">field<=value</span><span class="sxs-lookup"><span data-stu-id="1efa5-193">*field<=value*</span></span>

<span data-ttu-id="1efa5-194">*field!=value*</span><span class="sxs-lookup"><span data-stu-id="1efa5-194">*field!=value*</span></span>

<span data-ttu-id="1efa5-195">**說明**</span><span class="sxs-lookup"><span data-stu-id="1efa5-195">**Description**</span></span>

<span data-ttu-id="1efa5-196">提供比較。</span><span class="sxs-lookup"><span data-stu-id="1efa5-196">Provides comparisons.</span></span>

<span data-ttu-id="1efa5-197">例如：</span><span class="sxs-lookup"><span data-stu-id="1efa5-197">For example:</span></span>

```
TimeGenerated>NOW+2HOURS
```

<span data-ttu-id="1efa5-198">**語法**</span><span class="sxs-lookup"><span data-stu-id="1efa5-198">**Syntax**</span></span>

```
field:[from..to]
```

<span data-ttu-id="1efa5-199">**說明**</span><span class="sxs-lookup"><span data-stu-id="1efa5-199">**Description**</span></span>

<span data-ttu-id="1efa5-200">提供範圍面相化。</span><span class="sxs-lookup"><span data-stu-id="1efa5-200">Provides range faceting.</span></span>

<span data-ttu-id="1efa5-201">例如：</span><span class="sxs-lookup"><span data-stu-id="1efa5-201">For example:</span></span>

```
TimeGenerated:[NOW..NOW+1DAY]
```

```
SampleValue:[0..2]
```

### <a name="in"></a><span data-ttu-id="1efa5-202">IN</span><span class="sxs-lookup"><span data-stu-id="1efa5-202">IN</span></span>
<span data-ttu-id="1efa5-203">hello **IN**關鍵字可讓您 tooselect 從值清單。</span><span class="sxs-lookup"><span data-stu-id="1efa5-203">hello **IN** keyword allows you tooselect from a list of values.</span></span> <span data-ttu-id="1efa5-204">根據您使用的 hello 語法，這可以是簡單清單所提供，值或彙總從值清單。</span><span class="sxs-lookup"><span data-stu-id="1efa5-204">Depending on hello syntax you use, this can be a simple list of values you provide, or a list of values from an aggregation.</span></span>

<span data-ttu-id="1efa5-205">語法 1：</span><span class="sxs-lookup"><span data-stu-id="1efa5-205">Syntax 1:</span></span>

```
field IN {value1,value2,value3,...}
```

<span data-ttu-id="1efa5-206">此語法可讓您 tooinclude 簡易清單中的所有值。</span><span class="sxs-lookup"><span data-stu-id="1efa5-206">This syntax allows you tooinclude all values in a simple list.</span></span>



<span data-ttu-id="1efa5-207">範例：</span><span class="sxs-lookup"><span data-stu-id="1efa5-207">Examples:</span></span>

```
EventID IN {1201,1204,1210}
```

```
Computer IN {"srv01.contoso.com","srv02.contoso.com"}
```

<span data-ttu-id="1efa5-208">語法 2：</span><span class="sxs-lookup"><span data-stu-id="1efa5-208">Syntax 2:</span></span>

```
(Outer query) (Field toouse with inner query results) IN {Inner query | measure count() by (Field toosend tooouter query)} (rest  of outer query)  
```

<span data-ttu-id="1efa5-209">此語法可讓您 toocreate 彙總。</span><span class="sxs-lookup"><span data-stu-id="1efa5-209">This syntax allows you toocreate an aggregation.</span></span> <span data-ttu-id="1efa5-210">您接著可以從這個彙總到另一個外部的 （主要） 搜尋，尋找具有這些值的事件摘要 hello 值清單。</span><span class="sxs-lookup"><span data-stu-id="1efa5-210">You can then feed hello list of values from that aggregation into another outer (primary) search that looks for events with those value.</span></span> <span data-ttu-id="1efa5-211">做法是以大括號括住 hello 內部搜尋，再饋送其結果為 hello 外部搜尋中欄位的可能值，使用 hello IN 運算子。</span><span class="sxs-lookup"><span data-stu-id="1efa5-211">You do this by enclosing hello inner search in braces, and feeding its results as possible values for a field in hello outer search by using hello IN operator.</span></span>

<span data-ttu-id="1efa5-212">內部查詢範例：*目前遺失安全性更新的電腦*以 hello 下列彙總查詢：</span><span class="sxs-lookup"><span data-stu-id="1efa5-212">Inner query example: *computers currently missing security updates* with hello following aggregation query:</span></span>

```
Type:Update Classification="Security Updates"  UpdateState=needed TimeGenerated>NOW-25HOURS | measure count() by Computer
```    

<span data-ttu-id="1efa5-213">hello 最終查詢，以尋找*目前遺失安全性更新的電腦的所有 Windows 事件*類似 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="1efa5-213">hello final query that finds *all Windows events for computers currently missing security updates* resembles hello following:</span></span>

```
Type=Event Computer IN {Type:Update Classification="Security Updates"  UpdateState=needed TimeGenerated>NOW-25HOURS | measure count() by Computer}
```

### <a name="contains"></a><span data-ttu-id="1efa5-214">Contains</span><span class="sxs-lookup"><span data-stu-id="1efa5-214">Contains</span></span>
<span data-ttu-id="1efa5-215">hello **Contains**關鍵字可讓您 toofilter 記錄與欄位，其中包含指定的字串。</span><span class="sxs-lookup"><span data-stu-id="1efa5-215">hello **Contains** keyword allows you toofilter for records with a field that contains a specified string.</span></span> <span data-ttu-id="1efa5-216">這區分大小寫、僅適用於字串欄位，而且可能不包含任何逸出字元。</span><span class="sxs-lookup"><span data-stu-id="1efa5-216">This is case sensitive, works only with string fields, and may not include any escape characters.</span></span>

<span data-ttu-id="1efa5-217">語法：</span><span class="sxs-lookup"><span data-stu-id="1efa5-217">Syntax:</span></span>

```
field:contains("string")
```

<span data-ttu-id="1efa5-218">範例：</span><span class="sxs-lookup"><span data-stu-id="1efa5-218">Example:</span></span>

```
Type:contains("Event")
```

<span data-ttu-id="1efa5-219">這會傳回包含 hello 字串類型的記錄 「 事件 」。</span><span class="sxs-lookup"><span data-stu-id="1efa5-219">This returns records with a type that contains hello string "Event".</span></span> <span data-ttu-id="1efa5-220">範例包括 **Event**、**SecurityEvent** 和 **ServiceFabricOperationEvent**。</span><span class="sxs-lookup"><span data-stu-id="1efa5-220">Examples include **Event**, **SecurityEvent**, and **ServiceFabricOperationEvent**.</span></span>



### <a name="regular-expressions"></a><span data-ttu-id="1efa5-221">規則運算式</span><span class="sxs-lookup"><span data-stu-id="1efa5-221">Regular expressions</span></span>
<span data-ttu-id="1efa5-222">您也可以使用 hello 與規則運算式，指定欄位的搜尋條件**Regex**關鍵字。</span><span class="sxs-lookup"><span data-stu-id="1efa5-222">You can specify a search condition for a field with a regular expression, by using hello **Regex** keyword.</span></span> <span data-ttu-id="1efa5-223">您可以使用規則運算式中的 hello 語法的完整說明，請參閱[記錄分析中使用規則運算式 toofilter 記錄搜尋](log-analytics-log-searches-regex.md)。</span><span class="sxs-lookup"><span data-stu-id="1efa5-223">For a complete description of hello syntax you can use in regular expressions, see [Using regular expressions toofilter log searches in Log Analytics](log-analytics-log-searches-regex.md).</span></span>

<span data-ttu-id="1efa5-224">語法：</span><span class="sxs-lookup"><span data-stu-id="1efa5-224">Syntax:</span></span>

```
field:Regex("Regular Expression")
```

<span data-ttu-id="1efa5-225">範例：</span><span class="sxs-lookup"><span data-stu-id="1efa5-225">Example:</span></span>

```
Computer:Regex("^C.*")
```

### <a name="logical-operators"></a><span data-ttu-id="1efa5-226">邏輯運算子</span><span class="sxs-lookup"><span data-stu-id="1efa5-226">Logical operators</span></span>
<span data-ttu-id="1efa5-227">hello 查詢語言支援 hello 邏輯運算子 (*AND*，*或者*，和*不*) 及其 C 樣式別名 (*&&*， *||* ，和*！*分別)。</span><span class="sxs-lookup"><span data-stu-id="1efa5-227">hello query languages support hello logical operators (*AND*, *OR*, and *NOT*) and their C-style aliases (*&&*, *||*, and *!*, respectively).</span></span> <span data-ttu-id="1efa5-228">您可以使用括號 toogroup 這些運算子。</span><span class="sxs-lookup"><span data-stu-id="1efa5-228">You can use parentheses toogroup these operators.</span></span>

<span data-ttu-id="1efa5-229">範例：</span><span class="sxs-lookup"><span data-stu-id="1efa5-229">Examples:</span></span>

```
system OR error

```

```
Type:Alert AND NOT(Severity:1 OR ObjectId:"8066bbc0-9ec8-ca83-1edc-6f30d4779bcb8066bbc0-9ec8-ca83-1edc-6f30d4779bcb")
```

<span data-ttu-id="1efa5-230">您可以省略 hello 最上層篩選引數的 hello 邏輯運算子。</span><span class="sxs-lookup"><span data-stu-id="1efa5-230">You can omit hello logical operator for hello top-level filter arguments.</span></span> <span data-ttu-id="1efa5-231">在此情況下，會假設 hello AND 運算子。</span><span class="sxs-lookup"><span data-stu-id="1efa5-231">In this case, hello AND operator is assumed.</span></span>

| <span data-ttu-id="1efa5-232">篩選運算式</span><span class="sxs-lookup"><span data-stu-id="1efa5-232">Filter expression</span></span> | <span data-ttu-id="1efa5-233">對等太</span><span class="sxs-lookup"><span data-stu-id="1efa5-233">Equivalent too</span></span>|
| --- | --- |
| <span data-ttu-id="1efa5-234">system error</span><span class="sxs-lookup"><span data-stu-id="1efa5-234">system error</span></span> |<span data-ttu-id="1efa5-235">system AND error</span><span class="sxs-lookup"><span data-stu-id="1efa5-235">system AND error</span></span> |
| <span data-ttu-id="1efa5-236">system "Windows Server" OR Severity:1</span><span class="sxs-lookup"><span data-stu-id="1efa5-236">system "Windows Server" OR Severity:1</span></span> |<span data-ttu-id="1efa5-237">system AND ("Windows Server" OR Severity:1)</span><span class="sxs-lookup"><span data-stu-id="1efa5-237">system AND ("Windows Server" OR Severity:1)</span></span> |

### <a name="wildcarding"></a><span data-ttu-id="1efa5-238">萬用字元</span><span class="sxs-lookup"><span data-stu-id="1efa5-238">Wildcarding</span></span>
<span data-ttu-id="1efa5-239">hello 查詢語言支援使用 hello ( \* ) 字元太表示值在查詢中的一或多個字元。</span><span class="sxs-lookup"><span data-stu-id="1efa5-239">hello query language supports using hello ( \* ) character too represent one or more characters for a value in a query.</span></span>

<span data-ttu-id="1efa5-240">範例：</span><span class="sxs-lookup"><span data-stu-id="1efa5-240">Example:</span></span>

 <span data-ttu-id="1efa5-241">Hello 名稱，例如"REDMOND-SQL"中尋找具有"SQL"的所有電腦。</span><span class="sxs-lookup"><span data-stu-id="1efa5-241">Find all computers with "SQL" in hello name, such as "Redmond-SQL".</span></span>

```
Type=Event Computer=*SQL*
```

> [!NOTE]
> <span data-ttu-id="1efa5-242">此時，無法在引號內使用萬用字元。</span><span class="sxs-lookup"><span data-stu-id="1efa5-242">At this time, wildcards cannot be used within quotations.</span></span> <span data-ttu-id="1efa5-243">例如，hello 訊息`"*This text*"`會考慮 hello (\*) 做為常值 (\*) 字元。</span><span class="sxs-lookup"><span data-stu-id="1efa5-243">For example, hello message `"*This text*"` considers hello (\*) used as a literal (\*) character.</span></span>


## <a name="commands"></a><span data-ttu-id="1efa5-244">命令</span><span class="sxs-lookup"><span data-stu-id="1efa5-244">Commands</span></span>


<span data-ttu-id="1efa5-245">hello 命令會套用 toohello hello 查詢所傳回的結果。</span><span class="sxs-lookup"><span data-stu-id="1efa5-245">hello commands apply toohello results that are returned by hello query.</span></span> <span data-ttu-id="1efa5-246">使用 hello 管道字元 (|) tooapply 命令 toohello 擷取結果。</span><span class="sxs-lookup"><span data-stu-id="1efa5-246">Use hello pipe character ( | ) tooapply a command toohello retrieved results.</span></span> <span data-ttu-id="1efa5-247">多個命令必須以 hello 縱線字元分隔。</span><span class="sxs-lookup"><span data-stu-id="1efa5-247">Multiple commands must be separated by hello pipe character.</span></span>

> [!NOTE]
> <span data-ttu-id="1efa5-248">命令名稱可以大寫或小寫，不同於 hello 欄位名稱和 hello 資料撰寫。</span><span class="sxs-lookup"><span data-stu-id="1efa5-248">Command names can be written in upper case or lower case, unlike hello field names and hello data.</span></span>
>
>

### <a name="sort"></a><span data-ttu-id="1efa5-249">排序</span><span class="sxs-lookup"><span data-stu-id="1efa5-249">Sort</span></span>
<span data-ttu-id="1efa5-250">語法：</span><span class="sxs-lookup"><span data-stu-id="1efa5-250">Syntax:</span></span>

    sort field1 asc|desc, field2 asc|desc, …

<span data-ttu-id="1efa5-251">依特定欄位排序 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="1efa5-251">Sorts hello results by particular fields.</span></span> <span data-ttu-id="1efa5-252">hello asc/desc 表示後置詞 toosort hello 結果按照遞增或遞減的順序是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="1efa5-252">hello asc/desc suffix toosort hello results in ascending or descending order is optional.</span></span> <span data-ttu-id="1efa5-253">如果省略，hello *asc*會假設採用排序順序。</span><span class="sxs-lookup"><span data-stu-id="1efa5-253">If it is omitted, hello *asc* sort order is assumed.</span></span> <span data-ttu-id="1efa5-254">Hello **TimeGenerated**  欄位中， *desc*假設排序順序，讓它預設會傳回 hello 最新的結果第一次。</span><span class="sxs-lookup"><span data-stu-id="1efa5-254">For hello **TimeGenerated** field, *desc* sort order is assumed, so it returns hello most recent results first by default.</span></span>

### <a name="toplimit"></a><span data-ttu-id="1efa5-255">Top/Limit</span><span class="sxs-lookup"><span data-stu-id="1efa5-255">Top/Limit</span></span>
<span data-ttu-id="1efa5-256">語法：</span><span class="sxs-lookup"><span data-stu-id="1efa5-256">Syntax:</span></span>

    top number


    limit number
<span data-ttu-id="1efa5-257">限制 hello 回應 toohello 前 N 個結果。</span><span class="sxs-lookup"><span data-stu-id="1efa5-257">Limits hello response toohello top N results.</span></span>

<span data-ttu-id="1efa5-258">範例：</span><span class="sxs-lookup"><span data-stu-id="1efa5-258">Example:</span></span>

    Type:Alert errors detected | top 10

<span data-ttu-id="1efa5-259">傳回 hello 前 10 個比對結果。</span><span class="sxs-lookup"><span data-stu-id="1efa5-259">Returns hello top 10 matching results.</span></span>

### <a name="skip"></a><span data-ttu-id="1efa5-260">Skip</span><span class="sxs-lookup"><span data-stu-id="1efa5-260">Skip</span></span>
<span data-ttu-id="1efa5-261">語法：</span><span class="sxs-lookup"><span data-stu-id="1efa5-261">Syntax:</span></span>

    skip number

<span data-ttu-id="1efa5-262">略過 hello 列出的結果數目。</span><span class="sxs-lookup"><span data-stu-id="1efa5-262">Skips hello number of results listed.</span></span>

<span data-ttu-id="1efa5-263">範例：</span><span class="sxs-lookup"><span data-stu-id="1efa5-263">Example:</span></span>

    Type:Alert errors detected | top 10 | skip 200

<span data-ttu-id="1efa5-264">從結果 200 開始傳回 10 個比對結果。</span><span class="sxs-lookup"><span data-stu-id="1efa5-264">Returns top 10 matching results starting at result 200.</span></span>

### <a name="select"></a><span data-ttu-id="1efa5-265">選取</span><span class="sxs-lookup"><span data-stu-id="1efa5-265">Select</span></span>
<span data-ttu-id="1efa5-266">語法：</span><span class="sxs-lookup"><span data-stu-id="1efa5-266">Syntax:</span></span>

    select field1, field2, ...

<span data-ttu-id="1efa5-267">您選擇限制結果 toohello 欄位。</span><span class="sxs-lookup"><span data-stu-id="1efa5-267">Limits results toohello fields you choose.</span></span>

<span data-ttu-id="1efa5-268">範例：</span><span class="sxs-lookup"><span data-stu-id="1efa5-268">Example:</span></span>

    Type:Alert errors detected | select Name, Severity

<span data-ttu-id="1efa5-269">限制太 hello 傳回的結果欄位*名稱*和*嚴重性*。</span><span class="sxs-lookup"><span data-stu-id="1efa5-269">Limits hello returned results fields too*Name* and *Severity*.</span></span>

### <a name="measure"></a><span data-ttu-id="1efa5-270">Measure</span><span class="sxs-lookup"><span data-stu-id="1efa5-270">Measure</span></span>
<span data-ttu-id="1efa5-271">hello*量值*命令是使用的 tooapply 統計函數 toohello 未經處理的搜尋結果。</span><span class="sxs-lookup"><span data-stu-id="1efa5-271">hello *measure* command is used tooapply statistical functions toohello raw search results.</span></span> <span data-ttu-id="1efa5-272">這是很有幫助 tooget*分組*hello 資料的檢視。</span><span class="sxs-lookup"><span data-stu-id="1efa5-272">This is very useful tooget *group-by* views over hello data.</span></span> <span data-ttu-id="1efa5-273">當您使用 hello measure 命令時，記錄分析搜尋會顯示含有彙總結果的資料表。</span><span class="sxs-lookup"><span data-stu-id="1efa5-273">When you use hello measure command, Log Analytics search displays a table with aggregated results.</span></span>

<span data-ttu-id="1efa5-274">**語法：**</span><span class="sxs-lookup"><span data-stu-id="1efa5-274">**Syntax:**</span></span>

    measure aggregateFunction1([aggregatedField]) [as fieldAlias1] [, aggregateFunction2([aggregatedField2]) [as fieldAlias2] [, ...]] by groupField1 [, groupField2 [, groupField3]]  [interval interval]


    measure aggregateFunction1([aggregatedField]) [as fieldAlias1] [, aggregateFunction2([aggregatedField2]) [as fieldAlias2] [, ...]]  interval interval



<span data-ttu-id="1efa5-275">彙總依 hello 結果*groupField*，並使用計算 hello 彙總的量值*aggregatedField*。</span><span class="sxs-lookup"><span data-stu-id="1efa5-275">Aggregates hello results by *groupField*, and calculates hello aggregated measure values by using *aggregatedField*.</span></span>

| <span data-ttu-id="1efa5-276">量值統計函式</span><span class="sxs-lookup"><span data-stu-id="1efa5-276">Measure statistical function</span></span> | <span data-ttu-id="1efa5-277">說明</span><span class="sxs-lookup"><span data-stu-id="1efa5-277">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1efa5-278">*aggregateFunction*</span><span class="sxs-lookup"><span data-stu-id="1efa5-278">*aggregateFunction*</span></span> |<span data-ttu-id="1efa5-279">hello hello 彙總函式 （不區分大小寫） 的名稱。</span><span class="sxs-lookup"><span data-stu-id="1efa5-279">hello name of hello aggregate function (case insensitive).</span></span> <span data-ttu-id="1efa5-280">支援下列彙總函式的 hello： 計數、 MAX、 MIN、 SUM、 AVG、 STDDEV、 COUNTDISTINCT、 百分位數 # # 或 PCT # # (# # 是介於 1 到 99 之間的數字)。</span><span class="sxs-lookup"><span data-stu-id="1efa5-280">hello following aggregate functions are supported: COUNT, MAX, MIN, SUM, AVG, STDDEV, COUNTDISTINCT, PERCENTILE##, or PCT## (## is any number between 1 and 99).</span></span> |
| <span data-ttu-id="1efa5-281">*aggregatedField*</span><span class="sxs-lookup"><span data-stu-id="1efa5-281">*aggregatedField*</span></span> |<span data-ttu-id="1efa5-282">hello 進行彙總的欄位。</span><span class="sxs-lookup"><span data-stu-id="1efa5-282">hello field that is being aggregated.</span></span> <span data-ttu-id="1efa5-283">這個欄位是選擇性的 hello 計數彙總函式，但是具有 toobe SUM、 MAX、 MIN、 AVG、 STDDEV、 百分位數 # # 或 PCT # # 的現有數值欄位 (# # 是介於 1 到 99 之間的數字)。</span><span class="sxs-lookup"><span data-stu-id="1efa5-283">This field is optional for hello COUNT aggregate function, but has toobe an existing numeric field for SUM, MAX, MIN, AVG, STDDEV, PERCENTILE##, or PCT## (## is any number between 1 and 99).</span></span> <span data-ttu-id="1efa5-284">hello aggregatedField 也可以是任何 hello**擴充**支援的函數。</span><span class="sxs-lookup"><span data-stu-id="1efa5-284">hello aggregatedField can also be any of hello **Extend** supported functions.</span></span> |
| <span data-ttu-id="1efa5-285">*fieldAlias*</span><span class="sxs-lookup"><span data-stu-id="1efa5-285">*fieldAlias*</span></span> |<span data-ttu-id="1efa5-286">hello hello （選擇性） 別名計算彙總值。</span><span class="sxs-lookup"><span data-stu-id="1efa5-286">hello (optional) alias for hello calculated aggregated value.</span></span> <span data-ttu-id="1efa5-287">如果未指定，hello 的欄位名稱為**AggregatedValue**。</span><span class="sxs-lookup"><span data-stu-id="1efa5-287">If not specified, hello field name is **AggregatedValue**.</span></span> |
| <span data-ttu-id="1efa5-288">*groupField*</span><span class="sxs-lookup"><span data-stu-id="1efa5-288">*groupField*</span></span> |<span data-ttu-id="1efa5-289">為分組依據的 hello hello hello 結果集的欄位名稱。</span><span class="sxs-lookup"><span data-stu-id="1efa5-289">hello name of hello field that hello result set is grouped by.</span></span> |
| <span data-ttu-id="1efa5-290">*間隔*</span><span class="sxs-lookup"><span data-stu-id="1efa5-290">*Interval*</span></span> |<span data-ttu-id="1efa5-291">hello 時間間隔，hello 格式：**nnnNAME**。</span><span class="sxs-lookup"><span data-stu-id="1efa5-291">hello time interval, in hello format:**nnnNAME**.</span></span> <span data-ttu-id="1efa5-292">**nnn**是 hello 正整數。</span><span class="sxs-lookup"><span data-stu-id="1efa5-292">**nnn** is hello positive integer number.</span></span> <span data-ttu-id="1efa5-293">**名稱**hello 間隔名稱。</span><span class="sxs-lookup"><span data-stu-id="1efa5-293">**NAME** is hello interval name.</span></span> <span data-ttu-id="1efa5-294">支援的間隔名稱區分大小寫，且包括：MILLISECOND[S]、SECOND[S]、MINUTE[S]、HOUR[S]、DAY[S]、MONTH[S] 和 YEAR[S]。</span><span class="sxs-lookup"><span data-stu-id="1efa5-294">Supported interval names are case sensitive, and include:MILLISECOND[S], SECOND[S], MINUTE[S], HOUR[S], DAY[S], MONTH[S], and YEAR[S].</span></span> |

<span data-ttu-id="1efa5-295">hello 間隔選項只可以用於日期/時間群組欄位 (例如*TimeGenerated*和*TimeCreated*)。</span><span class="sxs-lookup"><span data-stu-id="1efa5-295">hello interval option can only be used in Date/Time group fields (such as *TimeGenerated* and *TimeCreated*).</span></span> <span data-ttu-id="1efa5-296">目前，這不會強制執行 hello 服務，但是沒有傳遞 toohello 後端的日期/時間欄位會導致執行階段錯誤。</span><span class="sxs-lookup"><span data-stu-id="1efa5-296">Currently, this is not enforced by hello service, but a field without Date/Time that is passed toohello back end causes a runtime error.</span></span> <span data-ttu-id="1efa5-297">實作 hello 結構描述驗證時，hello 服務 API 會拒絕間隔彙總的使用不含日期/時間欄位的查詢。</span><span class="sxs-lookup"><span data-stu-id="1efa5-297">When hello schema validation is implemented, hello service API rejects queries that use fields without Date/Time for interval aggregation.</span></span> <span data-ttu-id="1efa5-298">目前的 hello*量值*實作支援為任何彙總函式的間隔分組。</span><span class="sxs-lookup"><span data-stu-id="1efa5-298">hello current *Measure* implementation supports interval grouping for any aggregate function.</span></span>

<span data-ttu-id="1efa5-299">如果省略 hello BY 子句，但指定間隔 （作為第二個語法），hello *TimeGenerated*欄位預設會假設。</span><span class="sxs-lookup"><span data-stu-id="1efa5-299">If hello BY clause is omitted, but an interval is specified (as a second syntax), hello *TimeGenerated* field is assumed by default.</span></span>

<span data-ttu-id="1efa5-300">範例：</span><span class="sxs-lookup"><span data-stu-id="1efa5-300">Examples:</span></span>

<span data-ttu-id="1efa5-301">**範例 1**</span><span class="sxs-lookup"><span data-stu-id="1efa5-301">**Example 1**</span></span>

    Type:Alert | measure count() as Count by ObjectId

<span data-ttu-id="1efa5-302">群組 hello 警示*ObjectID*，並計算每個群組的警示的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="1efa5-302">Groups hello alerts by *ObjectID*, and calculates hello number of alerts for each group.</span></span> <span data-ttu-id="1efa5-303">hello 傳回彙的總值為 hello*計數*欄位 （別名）。</span><span class="sxs-lookup"><span data-stu-id="1efa5-303">hello aggregated value is returned as hello *Count* field (alias).</span></span>

<span data-ttu-id="1efa5-304">**範例 2**</span><span class="sxs-lookup"><span data-stu-id="1efa5-304">**Example 2**</span></span>

    Type:Alert | measure count() interval 1HOUR

<span data-ttu-id="1efa5-305">群組依據 1 小時間隔 hello 警示使用 hello *TimeGenerated*欄位，以及每個間隔中的警示傳回 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="1efa5-305">Groups hello alerts by 1-hour intervals by using hello *TimeGenerated* field, and returns hello number of alerts in each interval.</span></span>

<span data-ttu-id="1efa5-306">**範例 3**</span><span class="sxs-lookup"><span data-stu-id="1efa5-306">**Example 3**</span></span>

    Type:Alert | measure count() as AlertsPerHour interval 1HOUR

<span data-ttu-id="1efa5-307">如同 hello 上述範例中，但使用彙總的欄位別名 (*AlertsPerHour*)。</span><span class="sxs-lookup"><span data-stu-id="1efa5-307">Same as hello previous example, but with an aggregated field alias (*AlertsPerHour*).</span></span>

<span data-ttu-id="1efa5-308">**範例 4**</span><span class="sxs-lookup"><span data-stu-id="1efa5-308">**Example 4**</span></span>

    * <span data-ttu-id="1efa5-309">| measure count() by TimeCreated interval 5DAYS</span><span class="sxs-lookup"><span data-stu-id="1efa5-309">| measure count() by TimeCreated interval 5DAYS</span></span>

<span data-ttu-id="1efa5-310">使用 hello，依據 5 天間隔分組 hello 結果*TimeCreated*欄位，以及每個間隔中的結果傳回 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="1efa5-310">Groups hello results by 5-day intervals by using hello *TimeCreated* field, and returns hello number of results in each interval.</span></span>

<span data-ttu-id="1efa5-311">**範例 5**</span><span class="sxs-lookup"><span data-stu-id="1efa5-311">**Example 5**</span></span>

    Type:Alert | measure max(Severity) by WorkflowName

<span data-ttu-id="1efa5-312">群組的工作負載名稱 hello 警示，並傳回 hello 每個工作流程的最大警示嚴重性值。</span><span class="sxs-lookup"><span data-stu-id="1efa5-312">Groups hello alerts by workload name, and returns hello maximum alert severity value for each workflow.</span></span>

<span data-ttu-id="1efa5-313">**範例 6**</span><span class="sxs-lookup"><span data-stu-id="1efa5-313">**Example 6**</span></span>

    Type:Alert | measure min(Severity) by WorkflowName

<span data-ttu-id="1efa5-314">如同 hello 上述範例中，但使用 hello *min*彙總函式。</span><span class="sxs-lookup"><span data-stu-id="1efa5-314">Same as hello previous example, but with hello *min* aggregated function.</span></span>

<span data-ttu-id="1efa5-315">**範例 7**</span><span class="sxs-lookup"><span data-stu-id="1efa5-315">**Example 7**</span></span>

    Type:Perf | measure avg(CounterValue) by Computer

<span data-ttu-id="1efa5-316">效能分組的電腦，然後計算 hello 平均 (avg)。</span><span class="sxs-lookup"><span data-stu-id="1efa5-316">Groups Perf by computer, and calculates hello average (avg).</span></span>

<span data-ttu-id="1efa5-317">**範例 8**</span><span class="sxs-lookup"><span data-stu-id="1efa5-317">**Example 8**</span></span>

    Type:Perf | measure sum(CounterValue) by Computer

<span data-ttu-id="1efa5-318">與 hello 前一個範例相同，但使用*總和*。</span><span class="sxs-lookup"><span data-stu-id="1efa5-318">Same as hello previous example, but uses *sum*.</span></span>

<span data-ttu-id="1efa5-319">**範例 9**</span><span class="sxs-lookup"><span data-stu-id="1efa5-319">**Example 9**</span></span>

    Type:Perf | measure stddev(CounterValue) by Computer

<span data-ttu-id="1efa5-320">與 hello 前一個範例相同，但使用*stddev*。</span><span class="sxs-lookup"><span data-stu-id="1efa5-320">Same as hello previous example, but uses *stddev*.</span></span>

<span data-ttu-id="1efa5-321">**範例 10**</span><span class="sxs-lookup"><span data-stu-id="1efa5-321">**Example 10**</span></span>

    Type:Perf | measure percentile70(CounterValue) by Computer

<span data-ttu-id="1efa5-322">與 hello 前一個範例相同，但使用*percentile70*。</span><span class="sxs-lookup"><span data-stu-id="1efa5-322">Same as hello previous example, but uses *percentile70*.</span></span>

<span data-ttu-id="1efa5-323">**範例 11**</span><span class="sxs-lookup"><span data-stu-id="1efa5-323">**Example 11**</span></span>

    Type:Perf | measure pct70(CounterValue) by Computer

<span data-ttu-id="1efa5-324">與 hello 前一個範例相同，但使用*pct70*。</span><span class="sxs-lookup"><span data-stu-id="1efa5-324">Same as hello previous example, but uses *pct70*.</span></span> <span data-ttu-id="1efa5-325">請注意，PCT## 只是 PERCENTILE## 函式的別名。</span><span class="sxs-lookup"><span data-stu-id="1efa5-325">Note that *PCT##* is only an alias for *PERCENTILE##* function.</span></span>

<span data-ttu-id="1efa5-326">**範例 12**</span><span class="sxs-lookup"><span data-stu-id="1efa5-326">**Example 12**</span></span>

    Type:Perf | measure avg(CounterValue) by Computer, CounterName

<span data-ttu-id="1efa5-327">依電腦第一次群組效能然後 CounterName 和計算 hello 平均 (avg)。</span><span class="sxs-lookup"><span data-stu-id="1efa5-327">Groups Perf first by Computer and then CounterName, and calculates hello average (avg).</span></span>

<span data-ttu-id="1efa5-328">**範例 13**</span><span class="sxs-lookup"><span data-stu-id="1efa5-328">**Example 13**</span></span>

    Type:Alert | measure count() as Count by WorkflowName | sort Count desc | top 5

<span data-ttu-id="1efa5-329">取得 hello 與 hello 警示最大數目的前五個工作流程。</span><span class="sxs-lookup"><span data-stu-id="1efa5-329">Gets hello top five workflows with hello maximum number of alerts.</span></span>

<span data-ttu-id="1efa5-330">**範例 14**</span><span class="sxs-lookup"><span data-stu-id="1efa5-330">**Example 14**</span></span>

    * <span data-ttu-id="1efa5-331">| measure countdistinct(Computer) by Type</span><span class="sxs-lookup"><span data-stu-id="1efa5-331">| measure countdistinct(Computer) by Type</span></span>

<span data-ttu-id="1efa5-332">計算 hello 報告每個類型的唯一電腦數目。</span><span class="sxs-lookup"><span data-stu-id="1efa5-332">Counts hello number of unique computers reporting for each Type.</span></span>

<span data-ttu-id="1efa5-333">**範例 15**</span><span class="sxs-lookup"><span data-stu-id="1efa5-333">**Example 15**</span></span>

    * <span data-ttu-id="1efa5-334">| measure countdistinct(Computer) Interval 1HOUR</span><span class="sxs-lookup"><span data-stu-id="1efa5-334">| measure countdistinct(Computer) Interval 1HOUR</span></span>

<span data-ttu-id="1efa5-335">計算 hello 每小時報告的唯一電腦數目。</span><span class="sxs-lookup"><span data-stu-id="1efa5-335">Counts hello number of unique computers reporting for every hour.</span></span>

<span data-ttu-id="1efa5-336">**範例 16**</span><span class="sxs-lookup"><span data-stu-id="1efa5-336">**Example 16**</span></span>

```
Type:Perf CounterName=”% Processor Time” InstanceName=”_Total” | measure avg(CounterValue) by Computer Interval 1HOUR
```

<span data-ttu-id="1efa5-337">群組 %Processor Time 的電腦，並傳回 hello 平均每小時。</span><span class="sxs-lookup"><span data-stu-id="1efa5-337">Groups % Processor Time by Computer, and returns hello average for every hour.</span></span>

<span data-ttu-id="1efa5-338">**範例 17**</span><span class="sxs-lookup"><span data-stu-id="1efa5-338">**Example 17**</span></span>

    Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES

<span data-ttu-id="1efa5-339">群組 W3CIISLog 方法，並傳回 hello 最大值為每隔 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="1efa5-339">Groups W3CIISLog by method, and returns hello maximum for every 5 minutes.</span></span>

<span data-ttu-id="1efa5-340">**範例 18**</span><span class="sxs-lookup"><span data-stu-id="1efa5-340">**Example 18**</span></span>

```
Type:Perf CounterName=”% Processor Time” InstanceName=”_Total”  | measure min(CounterValue) as MIN, avg(CounterValue) as AVG, percentile75(CounterValue) as PCT75, max(CounterValue) as MAX by Computer Interval 1HOUR
```

<span data-ttu-id="1efa5-341">群組 %Processor Time 的電腦，並傳回 hello 最小值、 平均、 第 75 百分位數 及每小時最大值。</span><span class="sxs-lookup"><span data-stu-id="1efa5-341">Groups % Processor Time by computer, and returns hello minimum, average, 75th percentile, and maximum for every hour.</span></span>

<span data-ttu-id="1efa5-342">**範例 19**</span><span class="sxs-lookup"><span data-stu-id="1efa5-342">**Example 19**</span></span>

```
Type:Perf CounterName=”% Processor Time”  | measure min(CounterValue) as MIN, avg(CounterValue) as AVG, percentile75(CounterValue) as PCT75, max(CounterValue) as MAX by Computer, InstanceName Interval 1HOUR
```

<span data-ttu-id="1efa5-343">群組 %Processor Time 先依電腦和執行個體名稱，以及傳回 hello 最小值、 平均值、 第 75 個百分位數及每小時最大值。</span><span class="sxs-lookup"><span data-stu-id="1efa5-343">Groups % Processor Time first by computer and then by Instance name, and returns hello minimum, average, 75th percentile, and maximum for every hour.</span></span>

<span data-ttu-id="1efa5-344">**範例 20**</span><span class="sxs-lookup"><span data-stu-id="1efa5-344">**Example 20**</span></span>

```
Type= Perf CounterName="Disk Writes/sec" Computer="BaconDC01.BaconLand.com" | measure max(product(CounterValue,60)) as MaxDWPerMin by InstanceName Interval 1HOUR
```

<span data-ttu-id="1efa5-345">計算每個磁碟的每分鐘在您的電腦上的磁碟寫入的 hello 最大值。</span><span class="sxs-lookup"><span data-stu-id="1efa5-345">Calculates hello maximum of disk writes per minute for every disk on your computer.</span></span>

### <a name="where"></a><span data-ttu-id="1efa5-346">Where</span><span class="sxs-lookup"><span data-stu-id="1efa5-346">Where</span></span>
<span data-ttu-id="1efa5-347">語法：</span><span class="sxs-lookup"><span data-stu-id="1efa5-347">Syntax:</span></span>

```
**where** AggregatedValue>20
```

<span data-ttu-id="1efa5-348">僅適用於之後*量值*命令 toofurther 篩選 hello 彙總結果的 hello*量值*彙總函數所產生。</span><span class="sxs-lookup"><span data-stu-id="1efa5-348">Can only be used after a *Measure* command toofurther filter hello aggregated results that hello *Measure* aggregation function has produced.</span></span>

<span data-ttu-id="1efa5-349">範例：</span><span class="sxs-lookup"><span data-stu-id="1efa5-349">Examples:</span></span>

    Type:Perf CounterName:"% Total Run Time" | Measure max(CounterValue) as MAXCPU by Computer

    Type:Perf CounterName:"% Total Run Time" | Measure max(CounterValue) by Computer | where (AggregatedValue>50 and AggregatedValue<90)



### <a name="dedup"></a><span data-ttu-id="1efa5-350">Dedup</span><span class="sxs-lookup"><span data-stu-id="1efa5-350">Dedup</span></span>
<span data-ttu-id="1efa5-351">語法：</span><span class="sxs-lookup"><span data-stu-id="1efa5-351">Syntax:</span></span>

    Dedup FieldName

<span data-ttu-id="1efa5-352">傳回 hello hello 指定欄位的每個唯一值找到的第一個文件。</span><span class="sxs-lookup"><span data-stu-id="1efa5-352">Returns hello first document found for every unique value of hello given field.</span></span>

<span data-ttu-id="1efa5-353">範例：</span><span class="sxs-lookup"><span data-stu-id="1efa5-353">Example:</span></span>

    Type=Event | Dedup EventID | sort TimeGenerated DESC

<span data-ttu-id="1efa5-354">這個範例會傳回一個事件 （hello 最新事件），每個 EventID。</span><span class="sxs-lookup"><span data-stu-id="1efa5-354">This example returns one event (hello latest event) per EventID.</span></span>

### <a name="join"></a><span data-ttu-id="1efa5-355">Join</span><span class="sxs-lookup"><span data-stu-id="1efa5-355">Join</span></span>
<span data-ttu-id="1efa5-356">聯結 hello 結果的兩個查詢 tooform 單一結果集。</span><span class="sxs-lookup"><span data-stu-id="1efa5-356">Joins hello results of two queries tooform a single result set.</span></span>  <span data-ttu-id="1efa5-357">支援多個聯結類型描述 hello 依照資料表。</span><span class="sxs-lookup"><span data-stu-id="1efa5-357">Supports multiple join types described in hello follow table.</span></span>

| <span data-ttu-id="1efa5-358">聯結類型</span><span class="sxs-lookup"><span data-stu-id="1efa5-358">Join type</span></span> | <span data-ttu-id="1efa5-359">說明</span><span class="sxs-lookup"><span data-stu-id="1efa5-359">Description</span></span> |
|:--|:--|
| <span data-ttu-id="1efa5-360">inner</span><span class="sxs-lookup"><span data-stu-id="1efa5-360">inner</span></span> | <span data-ttu-id="1efa5-361">只傳回具有兩個查詢相符值的記錄。</span><span class="sxs-lookup"><span data-stu-id="1efa5-361">Return only records with a matching value in both queries.</span></span> |
| <span data-ttu-id="1efa5-362">outer</span><span class="sxs-lookup"><span data-stu-id="1efa5-362">outer</span></span> | <span data-ttu-id="1efa5-363">傳回兩個查詢的所有記錄。</span><span class="sxs-lookup"><span data-stu-id="1efa5-363">Return all records from both queries.</span></span>  |
| <span data-ttu-id="1efa5-364">left</span><span class="sxs-lookup"><span data-stu-id="1efa5-364">left</span></span>  | <span data-ttu-id="1efa5-365">傳回左查詢的所有記錄，以及傳回右查詢的相符記錄。</span><span class="sxs-lookup"><span data-stu-id="1efa5-365">Return all records from left query and matching records from right query.</span></span> |


- <span data-ttu-id="1efa5-366">聯結目前不支援包含 hello 查詢**IN**關鍵字、 hello**量值**命令或 hello**擴充**命令它是否為目標欄位從 hello 右側的查詢。</span><span class="sxs-lookup"><span data-stu-id="1efa5-366">Joins do not currently support queries that include hello **IN** keyword, hello **Measure** command or hello **Extend** command if it targets a field from hello right query.</span></span>
- <span data-ttu-id="1efa5-367">您目前只可以在一個聯結中包含單一欄位。</span><span class="sxs-lookup"><span data-stu-id="1efa5-367">You can currently include only a single field in a join.</span></span>
- <span data-ttu-id="1efa5-368">單一搜尋可能不包含一個以上的聯結。</span><span class="sxs-lookup"><span data-stu-id="1efa5-368">A single search may not include more than one join.</span></span>

<span data-ttu-id="1efa5-369">**語法**</span><span class="sxs-lookup"><span data-stu-id="1efa5-369">**Syntax**</span></span>

```
<left-query> | JOIN <join-type> <left-query-field-name> (<right-query>) <right-query-field-name>
```

<span data-ttu-id="1efa5-370">**範例**</span><span class="sxs-lookup"><span data-stu-id="1efa5-370">**Examples**</span></span>

<span data-ttu-id="1efa5-371">tooillustrate hello 不同的聯結類型，請考慮加入的資料類型從呼叫 hello 活動訊號 MyBackup_CL 每一部電腦的自訂記錄檔收集。</span><span class="sxs-lookup"><span data-stu-id="1efa5-371">tooillustrate hello different join types, consider joining a data type collected from a custom log called MyBackup_CL with hello heartbeat for each computer.</span></span>  <span data-ttu-id="1efa5-372">這些資料型別具有下列資料的 hello。</span><span class="sxs-lookup"><span data-stu-id="1efa5-372">These datatypes have hello following data.</span></span>

`Type = MyBackup_CL`

| <span data-ttu-id="1efa5-373">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="1efa5-373">TimeGenerated</span></span> | <span data-ttu-id="1efa5-374">電腦</span><span class="sxs-lookup"><span data-stu-id="1efa5-374">Computer</span></span> | <span data-ttu-id="1efa5-375">LastBackupStatus</span><span class="sxs-lookup"><span data-stu-id="1efa5-375">LastBackupStatus</span></span> |
|:---|:---|:---|
| <span data-ttu-id="1efa5-376">4/20/2017 01:26:32.137 AM</span><span class="sxs-lookup"><span data-stu-id="1efa5-376">4/20/2017 01:26:32.137 AM</span></span> | <span data-ttu-id="1efa5-377">srv01.contoso.com</span><span class="sxs-lookup"><span data-stu-id="1efa5-377">srv01.contoso.com</span></span> | <span data-ttu-id="1efa5-378">成功</span><span class="sxs-lookup"><span data-stu-id="1efa5-378">Success</span></span> |
| <span data-ttu-id="1efa5-379">4/20/2017 02:13:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="1efa5-379">4/20/2017 02:13:12.381 AM</span></span> | <span data-ttu-id="1efa5-380">srv02.contoso.com</span><span class="sxs-lookup"><span data-stu-id="1efa5-380">srv02.contoso.com</span></span> | <span data-ttu-id="1efa5-381">成功</span><span class="sxs-lookup"><span data-stu-id="1efa5-381">Success</span></span> |
| <span data-ttu-id="1efa5-382">4/20/2017 02:13:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="1efa5-382">4/20/2017 02:13:12.381 AM</span></span> | <span data-ttu-id="1efa5-383">srv03.contoso.com</span><span class="sxs-lookup"><span data-stu-id="1efa5-383">srv03.contoso.com</span></span> | <span data-ttu-id="1efa5-384">失敗</span><span class="sxs-lookup"><span data-stu-id="1efa5-384">Failure</span></span> |

<span data-ttu-id="1efa5-385">`Type = Hearbeat` (只會顯示部分的欄位)</span><span class="sxs-lookup"><span data-stu-id="1efa5-385">`Type = Hearbeat` (Only a subset of fields shown)</span></span>

| <span data-ttu-id="1efa5-386">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="1efa5-386">TimeGenerated</span></span> | <span data-ttu-id="1efa5-387">電腦</span><span class="sxs-lookup"><span data-stu-id="1efa5-387">Computer</span></span> | <span data-ttu-id="1efa5-388">ComputerIP</span><span class="sxs-lookup"><span data-stu-id="1efa5-388">ComputerIP</span></span> |
|:---|:---|:---|
| <span data-ttu-id="1efa5-389">4/21/2017 12:01:34.482 PM</span><span class="sxs-lookup"><span data-stu-id="1efa5-389">4/21/2017 12:01:34.482 PM</span></span> | <span data-ttu-id="1efa5-390">srv01.contoso.com</span><span class="sxs-lookup"><span data-stu-id="1efa5-390">srv01.contoso.com</span></span> | <span data-ttu-id="1efa5-391">10.10.100.1</span><span class="sxs-lookup"><span data-stu-id="1efa5-391">10.10.100.1</span></span> |
| <span data-ttu-id="1efa5-392">4/21/2017 12:02:21.916 PM</span><span class="sxs-lookup"><span data-stu-id="1efa5-392">4/21/2017 12:02:21.916 PM</span></span> | <span data-ttu-id="1efa5-393">srv02.contoso.com</span><span class="sxs-lookup"><span data-stu-id="1efa5-393">srv02.contoso.com</span></span> | <span data-ttu-id="1efa5-394">10.10.100.2</span><span class="sxs-lookup"><span data-stu-id="1efa5-394">10.10.100.2</span></span> |
| <span data-ttu-id="1efa5-395">4/21/2017 12:01:47.373 PM</span><span class="sxs-lookup"><span data-stu-id="1efa5-395">4/21/2017 12:01:47.373 PM</span></span> | <span data-ttu-id="1efa5-396">srv04.contoso.com</span><span class="sxs-lookup"><span data-stu-id="1efa5-396">srv04.contoso.com</span></span> | <span data-ttu-id="1efa5-397">10.10.100.4</span><span class="sxs-lookup"><span data-stu-id="1efa5-397">10.10.100.4</span></span> |

#### <a name="inner-join"></a><span data-ttu-id="1efa5-398">inner join</span><span class="sxs-lookup"><span data-stu-id="1efa5-398">inner join</span></span>

`Type=MyBackup_CL | join inner Computer (Type=Heartbeat) Computer`

<span data-ttu-id="1efa5-399">傳回 hello 下列記錄其中 hello 電腦欄位必須符合為這兩個資料型別。</span><span class="sxs-lookup"><span data-stu-id="1efa5-399">Returns hello following records where hello computer field matches for both datatypes.</span></span>

| <span data-ttu-id="1efa5-400">電腦</span><span class="sxs-lookup"><span data-stu-id="1efa5-400">Computer</span></span>| <span data-ttu-id="1efa5-401">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="1efa5-401">TimeGenerated</span></span> | <span data-ttu-id="1efa5-402">LastBackupStatus</span><span class="sxs-lookup"><span data-stu-id="1efa5-402">LastBackupStatus</span></span> | <span data-ttu-id="1efa5-403">TimeGenerated_joined</span><span class="sxs-lookup"><span data-stu-id="1efa5-403">TimeGenerated_joined</span></span> | <span data-ttu-id="1efa5-404">ComputerIP_joined</span><span class="sxs-lookup"><span data-stu-id="1efa5-404">ComputerIP_joined</span></span> | <span data-ttu-id="1efa5-405">Type_joined</span><span class="sxs-lookup"><span data-stu-id="1efa5-405">Type_joined</span></span> |
|:---|:---|:---|:---|:---|:---|
| <span data-ttu-id="1efa5-406">srv01.contoso.com</span><span class="sxs-lookup"><span data-stu-id="1efa5-406">srv01.contoso.com</span></span> | <span data-ttu-id="1efa5-407">4/20/2017 01:26:32.137 AM</span><span class="sxs-lookup"><span data-stu-id="1efa5-407">4/20/2017 01:26:32.137 AM</span></span> | <span data-ttu-id="1efa5-408">成功</span><span class="sxs-lookup"><span data-stu-id="1efa5-408">Success</span></span> | <span data-ttu-id="1efa5-409">4/21/2017 12:01:34.482 PM</span><span class="sxs-lookup"><span data-stu-id="1efa5-409">4/21/2017 12:01:34.482 PM</span></span> | <span data-ttu-id="1efa5-410">10.10.100.1</span><span class="sxs-lookup"><span data-stu-id="1efa5-410">10.10.100.1</span></span> | <span data-ttu-id="1efa5-411">Heartbeat</span><span class="sxs-lookup"><span data-stu-id="1efa5-411">Heartbeat</span></span> |
| <span data-ttu-id="1efa5-412">srv02.contoso.com</span><span class="sxs-lookup"><span data-stu-id="1efa5-412">srv02.contoso.com</span></span> | <span data-ttu-id="1efa5-413">4/20/2017 02:13:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="1efa5-413">4/20/2017 02:13:12.381 AM</span></span> | <span data-ttu-id="1efa5-414">成功</span><span class="sxs-lookup"><span data-stu-id="1efa5-414">Success</span></span> | <span data-ttu-id="1efa5-415">4/21/2017 12:02:21.916 PM</span><span class="sxs-lookup"><span data-stu-id="1efa5-415">4/21/2017 12:02:21.916 PM</span></span> | <span data-ttu-id="1efa5-416">10.10.100.2</span><span class="sxs-lookup"><span data-stu-id="1efa5-416">10.10.100.2</span></span> | <span data-ttu-id="1efa5-417">Heartbeat</span><span class="sxs-lookup"><span data-stu-id="1efa5-417">Heartbeat</span></span> |


#### <a name="outer-join"></a><span data-ttu-id="1efa5-418">outer join</span><span class="sxs-lookup"><span data-stu-id="1efa5-418">outer join</span></span>

`Type=MyBackup_CL | join outer Computer (Type=Heartbeat) Computer`

<span data-ttu-id="1efa5-419">傳回 hello 下列這兩種資料類型的記錄。</span><span class="sxs-lookup"><span data-stu-id="1efa5-419">Returns hello following records for both datatypes.</span></span>

| <span data-ttu-id="1efa5-420">電腦</span><span class="sxs-lookup"><span data-stu-id="1efa5-420">Computer</span></span>| <span data-ttu-id="1efa5-421">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="1efa5-421">TimeGenerated</span></span> | <span data-ttu-id="1efa5-422">LastBackupStatus</span><span class="sxs-lookup"><span data-stu-id="1efa5-422">LastBackupStatus</span></span> | <span data-ttu-id="1efa5-423">TimeGenerated_joined</span><span class="sxs-lookup"><span data-stu-id="1efa5-423">TimeGenerated_joined</span></span> | <span data-ttu-id="1efa5-424">ComputerIP_joined</span><span class="sxs-lookup"><span data-stu-id="1efa5-424">ComputerIP_joined</span></span> | <span data-ttu-id="1efa5-425">Type_joined</span><span class="sxs-lookup"><span data-stu-id="1efa5-425">Type_joined</span></span> |
|:---|:---|:---|:---|:---|:---|
| <span data-ttu-id="1efa5-426">srv01.contoso.com</span><span class="sxs-lookup"><span data-stu-id="1efa5-426">srv01.contoso.com</span></span> | <span data-ttu-id="1efa5-427">4/20/2017 01:26:32.137 AM</span><span class="sxs-lookup"><span data-stu-id="1efa5-427">4/20/2017 01:26:32.137 AM</span></span> | <span data-ttu-id="1efa5-428">成功</span><span class="sxs-lookup"><span data-stu-id="1efa5-428">Success</span></span>  | <span data-ttu-id="1efa5-429">4/21/2017 12:01:34.482 PM</span><span class="sxs-lookup"><span data-stu-id="1efa5-429">4/21/2017 12:01:34.482 PM</span></span> | <span data-ttu-id="1efa5-430">10.10.100.1</span><span class="sxs-lookup"><span data-stu-id="1efa5-430">10.10.100.1</span></span> | <span data-ttu-id="1efa5-431">Heartbeat</span><span class="sxs-lookup"><span data-stu-id="1efa5-431">Heartbeat</span></span> |
| <span data-ttu-id="1efa5-432">srv02.contoso.com</span><span class="sxs-lookup"><span data-stu-id="1efa5-432">srv02.contoso.com</span></span> | <span data-ttu-id="1efa5-433">4/20/2017 02:14:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="1efa5-433">4/20/2017 02:14:12.381 AM</span></span> | <span data-ttu-id="1efa5-434">成功</span><span class="sxs-lookup"><span data-stu-id="1efa5-434">Success</span></span>  | <span data-ttu-id="1efa5-435">4/21/2017 12:02:21.916 PM</span><span class="sxs-lookup"><span data-stu-id="1efa5-435">4/21/2017 12:02:21.916 PM</span></span> | <span data-ttu-id="1efa5-436">10.10.100.2</span><span class="sxs-lookup"><span data-stu-id="1efa5-436">10.10.100.2</span></span> | <span data-ttu-id="1efa5-437">Heartbeat</span><span class="sxs-lookup"><span data-stu-id="1efa5-437">Heartbeat</span></span> |
| <span data-ttu-id="1efa5-438">srv03.contoso.com</span><span class="sxs-lookup"><span data-stu-id="1efa5-438">srv03.contoso.com</span></span> | <span data-ttu-id="1efa5-439">4/20/2017 01:33:35.974 AM</span><span class="sxs-lookup"><span data-stu-id="1efa5-439">4/20/2017 01:33:35.974 AM</span></span> | <span data-ttu-id="1efa5-440">失敗</span><span class="sxs-lookup"><span data-stu-id="1efa5-440">Failure</span></span>  | <span data-ttu-id="1efa5-441">4/21/2017 12:01:47.373 PM</span><span class="sxs-lookup"><span data-stu-id="1efa5-441">4/21/2017 12:01:47.373 PM</span></span> | | |
| <span data-ttu-id="1efa5-442">srv04.contoso.com</span><span class="sxs-lookup"><span data-stu-id="1efa5-442">srv04.contoso.com</span></span> |                           |          | <span data-ttu-id="1efa5-443">4/21/2017 12:01:47.373 PM</span><span class="sxs-lookup"><span data-stu-id="1efa5-443">4/21/2017 12:01:47.373 PM</span></span> | <span data-ttu-id="1efa5-444">10.10.100.2</span><span class="sxs-lookup"><span data-stu-id="1efa5-444">10.10.100.2</span></span> | <span data-ttu-id="1efa5-445">Heartbeat</span><span class="sxs-lookup"><span data-stu-id="1efa5-445">Heartbeat</span></span> |



#### <a name="left-join"></a><span data-ttu-id="1efa5-446">left join</span><span class="sxs-lookup"><span data-stu-id="1efa5-446">left join</span></span>

`Type=MyBackup_CL | join left Computer (Type=Heartbeat) Computer`

<span data-ttu-id="1efa5-447">傳回從 MyBackup_CL 下列記錄與任何比對的欄位從 活動訊號的 hello。</span><span class="sxs-lookup"><span data-stu-id="1efa5-447">Returns hello following records from MyBackup_CL with any matching fields from Heartbeat.</span></span>

| <span data-ttu-id="1efa5-448">電腦</span><span class="sxs-lookup"><span data-stu-id="1efa5-448">Computer</span></span>| <span data-ttu-id="1efa5-449">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="1efa5-449">TimeGenerated</span></span> | <span data-ttu-id="1efa5-450">LastBackupStatus</span><span class="sxs-lookup"><span data-stu-id="1efa5-450">LastBackupStatus</span></span> | <span data-ttu-id="1efa5-451">TimeGenerated_joined</span><span class="sxs-lookup"><span data-stu-id="1efa5-451">TimeGenerated_joined</span></span> | <span data-ttu-id="1efa5-452">ComputerIP_joined</span><span class="sxs-lookup"><span data-stu-id="1efa5-452">ComputerIP_joined</span></span> | <span data-ttu-id="1efa5-453">Type_joined</span><span class="sxs-lookup"><span data-stu-id="1efa5-453">Type_joined</span></span> |
|:---|:---|:---|:---|:---|:---|
| <span data-ttu-id="1efa5-454">srv01.contoso.com</span><span class="sxs-lookup"><span data-stu-id="1efa5-454">srv01.contoso.com</span></span> | <span data-ttu-id="1efa5-455">4/20/2017 01:26:32.137 AM</span><span class="sxs-lookup"><span data-stu-id="1efa5-455">4/20/2017 01:26:32.137 AM</span></span> | <span data-ttu-id="1efa5-456">成功</span><span class="sxs-lookup"><span data-stu-id="1efa5-456">Success</span></span> | <span data-ttu-id="1efa5-457">4/21/2017 12:01:34.482 PM</span><span class="sxs-lookup"><span data-stu-id="1efa5-457">4/21/2017 12:01:34.482 PM</span></span> | <span data-ttu-id="1efa5-458">10.10.100.1</span><span class="sxs-lookup"><span data-stu-id="1efa5-458">10.10.100.1</span></span> | <span data-ttu-id="1efa5-459">Heartbeat</span><span class="sxs-lookup"><span data-stu-id="1efa5-459">Heartbeat</span></span> |
| <span data-ttu-id="1efa5-460">srv02.contoso.com</span><span class="sxs-lookup"><span data-stu-id="1efa5-460">srv02.contoso.com</span></span> | <span data-ttu-id="1efa5-461">4/20/2017 02:13:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="1efa5-461">4/20/2017 02:13:12.381 AM</span></span> | <span data-ttu-id="1efa5-462">成功</span><span class="sxs-lookup"><span data-stu-id="1efa5-462">Success</span></span> | <span data-ttu-id="1efa5-463">4/21/2017 12:02:21.916 PM</span><span class="sxs-lookup"><span data-stu-id="1efa5-463">4/21/2017 12:02:21.916 PM</span></span> | <span data-ttu-id="1efa5-464">10.10.100.2</span><span class="sxs-lookup"><span data-stu-id="1efa5-464">10.10.100.2</span></span> | <span data-ttu-id="1efa5-465">Heartbeat</span><span class="sxs-lookup"><span data-stu-id="1efa5-465">Heartbeat</span></span> |
| <span data-ttu-id="1efa5-466">srv03.contoso.com</span><span class="sxs-lookup"><span data-stu-id="1efa5-466">srv03.contoso.com</span></span> | <span data-ttu-id="1efa5-467">4/20/2017 02:13:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="1efa5-467">4/20/2017 02:13:12.381 AM</span></span> | <span data-ttu-id="1efa5-468">失敗</span><span class="sxs-lookup"><span data-stu-id="1efa5-468">Failure</span></span> | | | |


### <a name="extend"></a><span data-ttu-id="1efa5-469">Extend</span><span class="sxs-lookup"><span data-stu-id="1efa5-469">Extend</span></span>
<span data-ttu-id="1efa5-470">可讓您 toocreate 執行階段在查詢欄位中。</span><span class="sxs-lookup"><span data-stu-id="1efa5-470">Allows you toocreate run-time fields in queries.</span></span> <span data-ttu-id="1efa5-471">請注意，執行階段欄位不能與 hello measure 命令 tooperform 彙總。</span><span class="sxs-lookup"><span data-stu-id="1efa5-471">Note that run-time fields cannot be used with hello measure command tooperform aggregation.</span></span>

<span data-ttu-id="1efa5-472">**範例 1**</span><span class="sxs-lookup"><span data-stu-id="1efa5-472">**Example 1**</span></span>

    Type=SQLAssessmentRecommendation | Extend product(RecommendationScore, RecommendationWeight) AS RecommendationWeightedScore
<span data-ttu-id="1efa5-473">顯示 SQL 評估建議的加權建議分數。</span><span class="sxs-lookup"><span data-stu-id="1efa5-473">Shows weighted recommendation score for SQL Assessment recommendations.</span></span>

<span data-ttu-id="1efa5-474">**範例 2**</span><span class="sxs-lookup"><span data-stu-id="1efa5-474">**Example 2**</span></span>

    Type=Perf CounterName="Private Bytes" | EXTEND div(CounterValue,1024) AS KBs | Select CounterValue,Computer,KBs
<span data-ttu-id="1efa5-475">顯示計數器值，單位為 KB，而非位元組。</span><span class="sxs-lookup"><span data-stu-id="1efa5-475">Shows counter value in KBs instead of bytes.</span></span>

<span data-ttu-id="1efa5-476">**範例 3**</span><span class="sxs-lookup"><span data-stu-id="1efa5-476">**Example 3**</span></span>

    Type=WireData | EXTEND scale(TotalBytes,0,100) AS ScaledTotalBytes | Select ScaledTotalBytes,TotalBytes | SORT TotalBytes DESC
<span data-ttu-id="1efa5-477">標尺 hello WireData TotalBytes 的值的所有結果介於 0 到 100 之間。</span><span class="sxs-lookup"><span data-stu-id="1efa5-477">Scales hello value of WireData TotalBytes, such that all results are between 0 and 100.</span></span>

<span data-ttu-id="1efa5-478">**範例 4**</span><span class="sxs-lookup"><span data-stu-id="1efa5-478">**Example 4**</span></span>

```
Type=Perf CounterName="% Processor Time" | EXTEND if(map(CounterValue,0,50,0,1),"HIGH","LOW") as UTILIZATION
```
<span data-ttu-id="1efa5-479">將小於 50% 的效能計數器值標記為 LOW，而將其他值標記為 HIGH。</span><span class="sxs-lookup"><span data-stu-id="1efa5-479">Tags Perf Counter Values less than 50 percent as LOW, and others as HIGH.</span></span>

<span data-ttu-id="1efa5-480">**範例 5**</span><span class="sxs-lookup"><span data-stu-id="1efa5-480">**Example 5**</span></span>

```
Type= Perf CounterName="Disk Writes/sec" Computer="BaconDC01.BaconLand.com" | Extend product(CounterValue,60) as DWPerMin| measure max(DWPerMin) by InstanceName Interval 1HOUR
```
<span data-ttu-id="1efa5-481">計算每個磁碟的每分鐘在您的電腦上的磁碟寫入的 hello 最大值。</span><span class="sxs-lookup"><span data-stu-id="1efa5-481">Calculates hello maximum of disk writes per minute for every disk on your computer.</span></span>

<span data-ttu-id="1efa5-482">**支援的函式**</span><span class="sxs-lookup"><span data-stu-id="1efa5-482">**Supported functions**</span></span>

| <span data-ttu-id="1efa5-483">函式</span><span class="sxs-lookup"><span data-stu-id="1efa5-483">Function</span></span> | <span data-ttu-id="1efa5-484">說明</span><span class="sxs-lookup"><span data-stu-id="1efa5-484">Description</span></span> | <span data-ttu-id="1efa5-485">語法範例</span><span class="sxs-lookup"><span data-stu-id="1efa5-485">Syntax examples</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1efa5-486">abs</span><span class="sxs-lookup"><span data-stu-id="1efa5-486">abs</span></span> |<span data-ttu-id="1efa5-487">傳回 hello 絕對值 hello 指定值或函式。</span><span class="sxs-lookup"><span data-stu-id="1efa5-487">Returns hello absolute value of hello specified value or function.</span></span> |`abs(x)` <br> `abs(-5)` |
| <span data-ttu-id="1efa5-488">acos</span><span class="sxs-lookup"><span data-stu-id="1efa5-488">acos</span></span> |<span data-ttu-id="1efa5-489">傳回值或函式的反餘弦值。</span><span class="sxs-lookup"><span data-stu-id="1efa5-489">Returns arc cosine of a value or a function.</span></span> |`acos(x)` |
| <span data-ttu-id="1efa5-490">和</span><span class="sxs-lookup"><span data-stu-id="1efa5-490">and</span></span> |<span data-ttu-id="1efa5-491">如果且只有全部的運算元都評估 tootrue，則傳回 true 值。</span><span class="sxs-lookup"><span data-stu-id="1efa5-491">Returns a value of true if and only if all of its operands evaluate tootrue.</span></span> |`and(not(exists(popularity)),exists(price))` |
| <span data-ttu-id="1efa5-492">asin</span><span class="sxs-lookup"><span data-stu-id="1efa5-492">asin</span></span> |<span data-ttu-id="1efa5-493">傳回值或函式的反正弦值。</span><span class="sxs-lookup"><span data-stu-id="1efa5-493">Returns arc sine of a value or a function.</span></span> |`asin(x)` |
| <span data-ttu-id="1efa5-494">atan</span><span class="sxs-lookup"><span data-stu-id="1efa5-494">atan</span></span> |<span data-ttu-id="1efa5-495">傳回值或函式的反正切值。</span><span class="sxs-lookup"><span data-stu-id="1efa5-495">Returns arc tangent of a value or a function.</span></span> |`atan(x)` |
| <span data-ttu-id="1efa5-496">atan2</span><span class="sxs-lookup"><span data-stu-id="1efa5-496">atan2</span></span> |<span data-ttu-id="1efa5-497">傳回所產生的 x，y toopolar 座標 hello 矩形座標 hello 轉換 hello 角度。</span><span class="sxs-lookup"><span data-stu-id="1efa5-497">Returns hello angle resulting from hello conversion of hello rectangular coordinates x,y toopolar coordinates.</span></span> |`atan2(x,y)` |
| <span data-ttu-id="1efa5-498">cbrt</span><span class="sxs-lookup"><span data-stu-id="1efa5-498">cbrt</span></span> |<span data-ttu-id="1efa5-499">立方根。</span><span class="sxs-lookup"><span data-stu-id="1efa5-499">Cube root.</span></span> |`cbrt(x)` |
| <span data-ttu-id="1efa5-500">ceil</span><span class="sxs-lookup"><span data-stu-id="1efa5-500">ceil</span></span> |<span data-ttu-id="1efa5-501">Tooan 整數向上四捨五入。</span><span class="sxs-lookup"><span data-stu-id="1efa5-501">Rounds up tooan integer.</span></span> |`ceil(x)`  <br> <span data-ttu-id="1efa5-502">`ceil(5.6)`：傳回 6</span><span class="sxs-lookup"><span data-stu-id="1efa5-502">`ceil(5.6)` Returns 6</span></span> |
| <span data-ttu-id="1efa5-503">cos</span><span class="sxs-lookup"><span data-stu-id="1efa5-503">cos</span></span> |<span data-ttu-id="1efa5-504">傳回角度的餘弦值。</span><span class="sxs-lookup"><span data-stu-id="1efa5-504">Returns cosine of an angle.</span></span> |`cos(x)` |
| <span data-ttu-id="1efa5-505">cosh</span><span class="sxs-lookup"><span data-stu-id="1efa5-505">cosh</span></span> |<span data-ttu-id="1efa5-506">傳回角度的雙曲餘弦值。</span><span class="sxs-lookup"><span data-stu-id="1efa5-506">Returns hyperbolic cosine of an angle.</span></span> |`cosh(x)` |
| <span data-ttu-id="1efa5-507">def</span><span class="sxs-lookup"><span data-stu-id="1efa5-507">def</span></span> |<span data-ttu-id="1efa5-508">預設值的縮寫。</span><span class="sxs-lookup"><span data-stu-id="1efa5-508">Abbreviation for default.</span></span> <span data-ttu-id="1efa5-509">傳回 hello 欄位"field"的值。</span><span class="sxs-lookup"><span data-stu-id="1efa5-509">Returns hello value of field "field".</span></span> <span data-ttu-id="1efa5-510">如果 hello 欄位不存在，傳回指定的 hello 預設值，並產生 hello 第一個值位置： `exists()==true`。</span><span class="sxs-lookup"><span data-stu-id="1efa5-510">If hello field does not exist, returns hello default value specified and yields hello first value where: `exists()==true`.</span></span> |<span data-ttu-id="1efa5-511">`def(rating,5)`。</span><span class="sxs-lookup"><span data-stu-id="1efa5-511">`def(rating,5)`.</span></span> <span data-ttu-id="1efa5-512">此 def() 函式傳回 hello 評等，或如果未分級是 hello 文件中指定，會傳回 5。</span><span class="sxs-lookup"><span data-stu-id="1efa5-512">This def() function returns hello rating, or if no rating is specified in hello document, returns 5.</span></span> <br> <span data-ttu-id="1efa5-513">`def(myfield, 1.0)`相當太`if(exists(myfield),myfield,1.0)`。</span><span class="sxs-lookup"><span data-stu-id="1efa5-513">`def(myfield, 1.0)` is equivalent too`if(exists(myfield),myfield,1.0)`.</span></span> |
| <span data-ttu-id="1efa5-514">度</span><span class="sxs-lookup"><span data-stu-id="1efa5-514">deg</span></span> |<span data-ttu-id="1efa5-515">將弧度 toodegrees 的轉換。</span><span class="sxs-lookup"><span data-stu-id="1efa5-515">Converts radians toodegrees.</span></span> |`deg(x)` |
| <span data-ttu-id="1efa5-516">div</span><span class="sxs-lookup"><span data-stu-id="1efa5-516">div</span></span> |<span data-ttu-id="1efa5-517">`div(x,y)` 除以 x 乘以 y。</span><span class="sxs-lookup"><span data-stu-id="1efa5-517">`div(x,y)` divides x by y.</span></span> |`div(1,y)` <br> `div(sum(x,100),max(y,1))` |
| <span data-ttu-id="1efa5-518">dist</span><span class="sxs-lookup"><span data-stu-id="1efa5-518">dist</span></span> |<span data-ttu-id="1efa5-519">傳回兩個向量之間，（點） n 維度空間中的 hello 距離。</span><span class="sxs-lookup"><span data-stu-id="1efa5-519">Returns hello distance between two vectors, (points) in an n-dimensional space.</span></span> <span data-ttu-id="1efa5-520">採用 hello 電源，加上兩個或多個，ValueSource 執行個體，並計算 hello hello 兩個向量之間的距離。</span><span class="sxs-lookup"><span data-stu-id="1efa5-520">Takes in hello power, plus two or more, ValueSource instances, and calculates hello distances between hello two vectors.</span></span> <span data-ttu-id="1efa5-521">每個 ValueSource 都必須是數字。</span><span class="sxs-lookup"><span data-stu-id="1efa5-521">Each ValueSource must be a number.</span></span> <span data-ttu-id="1efa5-522">必須有偶數的 ValueSource 執行個體傳入，並 hello 方法會假設 hello 前半部代表第一個向量的 hello，hello 半部代表 hello 第二個向量。</span><span class="sxs-lookup"><span data-stu-id="1efa5-522">There must be an even number of ValueSource instances passed in, and hello method assumes that hello first half represent hello first vector and hello second half represent hello second vector.</span></span> |<span data-ttu-id="1efa5-523">`dist(2, x, y, 0, 0)`計算 hello 歐幾里德距離 (0，0) 和 (x，y) 每個文件。</span><span class="sxs-lookup"><span data-stu-id="1efa5-523">`dist(2, x, y, 0, 0)` Calculates hello Euclidean distance between (0,0) and (x,y) for each document.</span></span> <br> <span data-ttu-id="1efa5-524">`dist(1, x, y, 0, 0)`計算 hello 曼哈頓 （計程車） 距離 (0，0) 和 (x，y) 每個文件。</span><span class="sxs-lookup"><span data-stu-id="1efa5-524">`dist(1, x, y, 0, 0)` Calculates hello Manhattan (taxicab) distance between (0,0) and (x,y) for each document.</span></span> <br> <span data-ttu-id="1efa5-525">`dist(2,,x,y,z,0,0,0)`：每個文件的 (0,0,0) 和 (x,y,z) 之間的 Euclidean 距離。</span><span class="sxs-lookup"><span data-stu-id="1efa5-525">`dist(2,,x,y,z,0,0,0)` Euclidean distance between (0,0,0) and (x,y,z) for each document.</span></span><br><span data-ttu-id="1efa5-526">`dist(1,x,y,z,e,f,g)`：(x,y,z) 和 (e,f,g) 之間的 Manhattan 距離，其中每個字母是欄位名稱。</span><span class="sxs-lookup"><span data-stu-id="1efa5-526">`dist(1,x,y,z,e,f,g)` Manhattan distance between (x,y,z) and (e,f,g), where each letter is a field name.</span></span> |
| <span data-ttu-id="1efa5-527">exists</span><span class="sxs-lookup"><span data-stu-id="1efa5-527">exists</span></span> |<span data-ttu-id="1efa5-528">傳回 TRUE，如果有任何欄位成員的 hello 存在。</span><span class="sxs-lookup"><span data-stu-id="1efa5-528">Returns TRUE if any member of hello field exists.</span></span> |<span data-ttu-id="1efa5-529">`exists(author)`傳回在 hello"author"欄位具有數值的任何文件，則為 TRUE。</span><span class="sxs-lookup"><span data-stu-id="1efa5-529">`exists(author)` Returns TRUE for any document that has a value in hello "author" field.</span></span><br><span data-ttu-id="1efa5-530">`exists(query(price:5.00))`：如果 "price" 符合 "5.00" 則傳回 TRUE。</span><span class="sxs-lookup"><span data-stu-id="1efa5-530">`exists(query(price:5.00))` Returns TRUE if "price" matches,"5.00".</span></span> |
| <span data-ttu-id="1efa5-531">exp</span><span class="sxs-lookup"><span data-stu-id="1efa5-531">exp</span></span> |<span data-ttu-id="1efa5-532">傳回歐拉數引發 toopower x。</span><span class="sxs-lookup"><span data-stu-id="1efa5-532">Returns Euler's number raised toopower x.</span></span> |`exp(x)` |
| <span data-ttu-id="1efa5-533">floor</span><span class="sxs-lookup"><span data-stu-id="1efa5-533">floor</span></span> |<span data-ttu-id="1efa5-534">將下 tooan 整數進位。</span><span class="sxs-lookup"><span data-stu-id="1efa5-534">Rounds down tooan integer.</span></span> |`floor(x)`  <br> <span data-ttu-id="1efa5-535">`floor(5.6)`：傳回 5</span><span class="sxs-lookup"><span data-stu-id="1efa5-535">`floor(5.6)` Returns 5</span></span> |
| <span data-ttu-id="1efa5-536">hypo</span><span class="sxs-lookup"><span data-stu-id="1efa5-536">hypo</span></span> |<span data-ttu-id="1efa5-537">傳回 sqrt(sum(pow(x,2),pow(y,2)))，而不需要中繼溢位或反向溢位。</span><span class="sxs-lookup"><span data-stu-id="1efa5-537">Returns sqrt(sum(pow(x,2),pow(y,2))) without intermediate overflow or underflow.</span></span> |`hypo(x,y)`  <br> ` |
| <span data-ttu-id="1efa5-538">if</span><span class="sxs-lookup"><span data-stu-id="1efa5-538">if</span></span> |<span data-ttu-id="1efa5-539">啟用條件式函式查詢。</span><span class="sxs-lookup"><span data-stu-id="1efa5-539">Enables conditional function queries.</span></span> <span data-ttu-id="1efa5-540">在`if(test,value1,value2)`，測試為或稱為 tooa 邏輯值或傳回邏輯值 （TRUE 或 FALSE） 運算式。</span><span class="sxs-lookup"><span data-stu-id="1efa5-540">In `if(test,value1,value2)`, test is or refers tooa logical value or expression that returns a logical value (TRUE or FALSE).</span></span> <span data-ttu-id="1efa5-541">`value1`hello 值傳回 hello 函式如果測試結果為 TRUE。</span><span class="sxs-lookup"><span data-stu-id="1efa5-541">`value1` is hello value returned by hello function if test yields TRUE.</span></span> <span data-ttu-id="1efa5-542">`value2`hello 值傳回 hello 函式如果測試結果 FALSE。</span><span class="sxs-lookup"><span data-stu-id="1efa5-542">`value2` is hello value returned by hello function if test yields FALSE.</span></span> <span data-ttu-id="1efa5-543">運算式可以是輸出布林值的任何函式。</span><span class="sxs-lookup"><span data-stu-id="1efa5-543">An expression can be any function which outputs boolean values.</span></span> <span data-ttu-id="1efa5-544">也可以是傳回數值的函式，在此情況下，值 0 會解譯為 false 或傳回字串，在此情況下，空字串會解譯為 false。</span><span class="sxs-lookup"><span data-stu-id="1efa5-544">It can also be a function returning numeric values, in which case value 0 is interpreted as false, or returning strings, in which case empty string is interpreted as false.</span></span> |<span data-ttu-id="1efa5-545">`if(termfreq(cat,'electronics'),popularity,42)`此函式會檢查每個文件 toosee，如果它包含"electronics"hello cat 欄位中的 hello 一詞。</span><span class="sxs-lookup"><span data-stu-id="1efa5-545">`if(termfreq(cat,'electronics'),popularity,42)` This function checks each document toosee if it contains hello term "electronics" in hello cat field.</span></span> <span data-ttu-id="1efa5-546">如果它，然後 hello hello popularity 欄位的值會傳回。</span><span class="sxs-lookup"><span data-stu-id="1efa5-546">If it does, then hello value of hello popularity field is returned.</span></span> <span data-ttu-id="1efa5-547">否則，傳回 hello 42 一值。</span><span class="sxs-lookup"><span data-stu-id="1efa5-547">Otherwise, hello value of 42 is returned.</span></span> |
| <span data-ttu-id="1efa5-548">linear</span><span class="sxs-lookup"><span data-stu-id="1efa5-548">linear</span></span> |<span data-ttu-id="1efa5-549">實作 `m*x+c`，其中 m 和 c 是常數，而 x 是任意函式。</span><span class="sxs-lookup"><span data-stu-id="1efa5-549">Implements `m*x+c`, where m and c are constants, and x is an arbitrary function.</span></span> <span data-ttu-id="1efa5-550">這相當太`sum(product(m,x),c)`，但當它實作為單一函式稍微更有效率。</span><span class="sxs-lookup"><span data-stu-id="1efa5-550">This is equivalent too`sum(product(m,x),c)`, but slightly more efficient as it is implemented as a single function.</span></span> |<span data-ttu-id="1efa5-551">`linear(x,m,c) linear(x,2,4)` 傳回 `2*x+4`</span><span class="sxs-lookup"><span data-stu-id="1efa5-551">`linear(x,m,c) linear(x,2,4)` returns `2*x+4`</span></span> |
| <span data-ttu-id="1efa5-552">ln</span><span class="sxs-lookup"><span data-stu-id="1efa5-552">ln</span></span> |<span data-ttu-id="1efa5-553">傳回 hello 自然對數的 hello 指定函式。</span><span class="sxs-lookup"><span data-stu-id="1efa5-553">Returns hello natural log of hello specified function.</span></span> |`ln(x)` |
| <span data-ttu-id="1efa5-554">log</span><span class="sxs-lookup"><span data-stu-id="1efa5-554">log</span></span> |<span data-ttu-id="1efa5-555">傳回 hello 記錄檔基底 10 hello 的指定函式。</span><span class="sxs-lookup"><span data-stu-id="1efa5-555">Returns hello log base 10 of hello specified function.</span></span> |`log(x)   log(sum(x,100))` |
| <span data-ttu-id="1efa5-556">map</span><span class="sxs-lookup"><span data-stu-id="1efa5-556">map</span></span> |<span data-ttu-id="1efa5-557">對應任何輸入函式 x 的值落在 min 和 max (含） 之間 toohello 指定的目標。</span><span class="sxs-lookup"><span data-stu-id="1efa5-557">Maps any values of an input function x that fall within min and max, inclusive toohello specified target.</span></span> <span data-ttu-id="1efa5-558">hello 引數的 min 和 max 必須是常數。</span><span class="sxs-lookup"><span data-stu-id="1efa5-558">hello arguments min and max must be constants.</span></span> <span data-ttu-id="1efa5-559">hello 引數的目標和預設值可以是常數或函式。</span><span class="sxs-lookup"><span data-stu-id="1efa5-559">hello arguments target and default can be constants or functions.</span></span> <span data-ttu-id="1efa5-560">如果 x 的 hello 值不在 min 和 max 之間，則會傳回 x 的任一個 hello 值，或若指定做為第 5 個引數，則傳回預設值。</span><span class="sxs-lookup"><span data-stu-id="1efa5-560">If hello value of x does not fall between min and max, then either hello value of x is returned, or a default value is returned if specified as a 5th argument.</span></span> |<span data-ttu-id="1efa5-561">`map(x,min,max,target) map(x,0,0,1)`變更任何 0 too1 的值。</span><span class="sxs-lookup"><span data-stu-id="1efa5-561">`map(x,min,max,target) map(x,0,0,1)` Changes any values of 0 too1.</span></span> <span data-ttu-id="1efa5-562">這可用於處理預設值 0 的值。</span><span class="sxs-lookup"><span data-stu-id="1efa5-562">This can be useful in handling default 0 values.</span></span><br> <span data-ttu-id="1efa5-563">`map(x,min,max,target,default)    map(x,0,100,1,-1)`變更任何 0 和 100 too1 與所有其他值太-1 之間的值。</span><span class="sxs-lookup"><span data-stu-id="1efa5-563">`map(x,min,max,target,default)    map(x,0,100,1,-1)` Changes any values between 0 and 100 too1, and all other values too-1.</span></span><br>  <span data-ttu-id="1efa5-564">`map(x,0,100,sum(x,599),docfreq(text,solr))`變更任何值，介於 0 和 100 toox + 599 和所有其他值 toofrequency 的 hello hello 欄位文字中的 ' solr' 一詞。</span><span class="sxs-lookup"><span data-stu-id="1efa5-564">`map(x,0,100,sum(x,599),docfreq(text,solr))` Changes any values between 0 and 100 toox+599, and all other values toofrequency of hello term 'solr' in hello field text.</span></span> |
| <span data-ttu-id="1efa5-565">max</span><span class="sxs-lookup"><span data-stu-id="1efa5-565">max</span></span> |<span data-ttu-id="1efa5-566">傳回 hello 的多個巢狀函式或常數，指定為引數的最大數值： `max(x,y,...)`。</span><span class="sxs-lookup"><span data-stu-id="1efa5-566">Returns hello maximum numeric value of multiple nested functions or constants, which are specified as arguments: `max(x,y,...)`.</span></span> <span data-ttu-id="1efa5-567">hello max 函式也可用於 「 bottoming"另一個函式位於某些指定常數或欄位。</span><span class="sxs-lookup"><span data-stu-id="1efa5-567">hello max function can also be useful for "bottoming out" another function or field at some specified constant.</span></span>  <span data-ttu-id="1efa5-568">使用 hello`field(myfield,max)`語法選取單一多值欄位的 hello 最大值。</span><span class="sxs-lookup"><span data-stu-id="1efa5-568">Use hello `field(myfield,max)` syntax for selecting hello maximum value of a single multivalued field.</span></span> |`max(myfield,myotherfield,0)` |
| <span data-ttu-id="1efa5-569">Min</span><span class="sxs-lookup"><span data-stu-id="1efa5-569">min</span></span> |<span data-ttu-id="1efa5-570">傳回 hello 的常數，指定為引數的多個巢狀函式的最小數值： `min(x,y,...)`。</span><span class="sxs-lookup"><span data-stu-id="1efa5-570">Returns hello minimum numeric value of multiple nested functions of constants, which are specified as arguments: `min(x,y,...)`.</span></span> <span data-ttu-id="1efa5-571">hello min 函式也可以用來將提供在使用常數的函式 「 上限 」。</span><span class="sxs-lookup"><span data-stu-id="1efa5-571">hello min function can also be useful for providing an "upper bound" on a function using a constant.</span></span> <span data-ttu-id="1efa5-572">使用 hello`field(myfield,min)`語法選取單一多值欄位的 hello 最小值。</span><span class="sxs-lookup"><span data-stu-id="1efa5-572">Use hello `field(myfield,min)` syntax for selecting hello minimum value of a single multivalued field.</span></span> |`min(myfield,myotherfield,0)` |
| <span data-ttu-id="1efa5-573">mod</span><span class="sxs-lookup"><span data-stu-id="1efa5-573">mod</span></span> |<span data-ttu-id="1efa5-574">計算 hello 的 hello 函式 x 的 hello 函式 y 的模數。</span><span class="sxs-lookup"><span data-stu-id="1efa5-574">Computes hello modulus of hello function x by hello function y.</span></span> |`mod(1,x)` <br> `mod(sum(x,100), max(y,1))` |
| <span data-ttu-id="1efa5-575">ms</span><span class="sxs-lookup"><span data-stu-id="1efa5-575">ms</span></span> |<span data-ttu-id="1efa5-576">傳回其引數之間差異的毫秒。</span><span class="sxs-lookup"><span data-stu-id="1efa5-576">Returns milliseconds of difference between its arguments.</span></span> <span data-ttu-id="1efa5-577">日期是相對 toohello Unix 或 POSIX 時間 epoch、 午夜，1970 年 1 月 1 日 UTC。</span><span class="sxs-lookup"><span data-stu-id="1efa5-577">Dates are relative toohello Unix or POSIX time epoch, midnight, January 1, 1970 UTC.</span></span> <span data-ttu-id="1efa5-578">引數可以是 hello 名稱索引的 TrieDateField 或根據常數日期或 NOW。</span><span class="sxs-lookup"><span data-stu-id="1efa5-578">Arguments may be hello name of an indexed TrieDateField, or date math based on a constant date or NOW .</span></span> <span data-ttu-id="1efa5-579">`ms()`相當太`ms(NOW)`，數目 hello 新紀元以來的毫秒數。</span><span class="sxs-lookup"><span data-stu-id="1efa5-579">`ms()` is equivalent too`ms(NOW)`, number of milliseconds since hello epoch.</span></span> <span data-ttu-id="1efa5-580">`ms(a)`傳回 hello 引數代表的 hello 新紀元以來的 hello 的毫秒數。</span><span class="sxs-lookup"><span data-stu-id="1efa5-580">`ms(a)` returns hello number of milliseconds since hello epoch that hello argument represents.</span></span> <span data-ttu-id="1efa5-581">`ms(a,b)`傳回 hello 的毫秒數 b 之前發生，也就是`a - b`。</span><span class="sxs-lookup"><span data-stu-id="1efa5-581">`ms(a,b)` returns hello number of milliseconds that b occurs before a, which is `a - b`.</span></span> |`ms(NOW/DAY)`<br>`ms(2000-01-01T00:00:00Z)`<br>`ms(mydatefield)`<br>`ms(NOW,mydatefield)`<br>`ms(mydatefield,2000-01-01T00:00:00Z)`<br>`ms(datefield1,datefield2)` |
| <span data-ttu-id="1efa5-582">否</span><span class="sxs-lookup"><span data-stu-id="1efa5-582">not</span></span> |<span data-ttu-id="1efa5-583">邏輯否定的 hello hello 值包裝函式。</span><span class="sxs-lookup"><span data-stu-id="1efa5-583">hello logically negated value of hello wrapped function.</span></span> |<span data-ttu-id="1efa5-584">`not(exists(author))`：當 `exists(author)` 為 false 時才為 TRUE。</span><span class="sxs-lookup"><span data-stu-id="1efa5-584">`not(exists(author))` TRUE only when `exists(author)` is false.</span></span> |
| <span data-ttu-id="1efa5-585">或</span><span class="sxs-lookup"><span data-stu-id="1efa5-585">or</span></span> |<span data-ttu-id="1efa5-586">邏輯分離。</span><span class="sxs-lookup"><span data-stu-id="1efa5-586">A logical disjunction.</span></span> |<span data-ttu-id="1efa5-587">`or(value1,value2)`：如果 value1 或 value2 為 true，則為 TRUE。</span><span class="sxs-lookup"><span data-stu-id="1efa5-587">`or(value1,value2)` TRUE if either value1 or value2 is true.</span></span> |
| <span data-ttu-id="1efa5-588">pow</span><span class="sxs-lookup"><span data-stu-id="1efa5-588">pow</span></span> |<span data-ttu-id="1efa5-589">引發 hello 指定指定的基底 toohello 電源。</span><span class="sxs-lookup"><span data-stu-id="1efa5-589">Raises hello specified base toohello specified power.</span></span> <span data-ttu-id="1efa5-590">`pow(x,y)`引發 x toohello 乘 y。</span><span class="sxs-lookup"><span data-stu-id="1efa5-590">`pow(x,y)` raises x toohello power of y.</span></span> |`pow(x,y)`<br>`pow(x,log(y))`<br><span data-ttu-id="1efa5-591">`pow(x,0.5)`hello 與 sqrt 的相同。</span><span class="sxs-lookup"><span data-stu-id="1efa5-591">`pow(x,0.5)` hello same as sqrt.</span></span> |
| <span data-ttu-id="1efa5-592">product</span><span class="sxs-lookup"><span data-stu-id="1efa5-592">product</span></span> |<span data-ttu-id="1efa5-593">傳回 hello 的多個值或函式，以逗號分隔的清單中指定的產品。</span><span class="sxs-lookup"><span data-stu-id="1efa5-593">Returns hello product of multiple values or functions, which are specified in a comma-separated list.</span></span> <span data-ttu-id="1efa5-594">`mul(...)` 也可以作為這個函式的別名。</span><span class="sxs-lookup"><span data-stu-id="1efa5-594">`mul(...)` may also be used as an alias for this function.</span></span> |`product(x,y,...)`<br>`product(x,2)`<br>`product(x,y)`<br>`mul(x,y)` |
| <span data-ttu-id="1efa5-595">recip</span><span class="sxs-lookup"><span data-stu-id="1efa5-595">recip</span></span> |<span data-ttu-id="1efa5-596">執行 `recip(x,m,a,b)` 實作 `a/(m*x+b)` 的倒數函式，其中 m、a 和 b 是常數，而 x 是任何任意複雜函式。</span><span class="sxs-lookup"><span data-stu-id="1efa5-596">Performs a reciprocal function with `recip(x,m,a,b)` implementing `a/(m*x+b)`, where m, a,and b are constants, and x is any arbitrarily complex function.</span></span> <span data-ttu-id="1efa5-597">a 與 b 相等而且 x>=0 時，此函式的最大值為 1，會在 x 增加時減少。</span><span class="sxs-lookup"><span data-stu-id="1efa5-597">When a and b are equal, and x>=0, this function has a maximum value of 1 that drops as x increases.</span></span> <span data-ttu-id="1efa5-598">增加 hello 值 hello 整個函式 tooa 移動 b 一起結果呈現 hello 曲線的一部分。</span><span class="sxs-lookup"><span data-stu-id="1efa5-598">Increasing hello value of a and b together results in a movement of hello entire function tooa flatter part of hello curve.</span></span> <span data-ttu-id="1efa5-599">x 為 `rord(datefield)`時，這些屬性可以將這個設為提升較新文件的理想函式。</span><span class="sxs-lookup"><span data-stu-id="1efa5-599">These properties can make this an ideal function for boosting more recent documents when x is `rord(datefield)`.</span></span> |`recip(myfield,m,a,b)`<br>`recip(rord(creationDate),1,1000,1000)` |
| <span data-ttu-id="1efa5-600">rad</span><span class="sxs-lookup"><span data-stu-id="1efa5-600">rad</span></span> |<span data-ttu-id="1efa5-601">將轉換度 tooradians。</span><span class="sxs-lookup"><span data-stu-id="1efa5-601">Converts degrees tooradians.</span></span> |`rad(x)` |
| <span data-ttu-id="1efa5-602">rint</span><span class="sxs-lookup"><span data-stu-id="1efa5-602">rint</span></span> |<span data-ttu-id="1efa5-603">重試回合 toohello 接近的整數。</span><span class="sxs-lookup"><span data-stu-id="1efa5-603">Rounds toohello nearest integer.</span></span> |`rint(x)`  <br> <span data-ttu-id="1efa5-604">`rint(5.6)`：傳回 6</span><span class="sxs-lookup"><span data-stu-id="1efa5-604">`rint(5.6)` Returns 6</span></span> |
| <span data-ttu-id="1efa5-605">sin</span><span class="sxs-lookup"><span data-stu-id="1efa5-605">sin</span></span> |<span data-ttu-id="1efa5-606">傳回角度的正弦值。</span><span class="sxs-lookup"><span data-stu-id="1efa5-606">Returns sine of an angle.</span></span> |`sin(x)` |
| <span data-ttu-id="1efa5-607">sinh</span><span class="sxs-lookup"><span data-stu-id="1efa5-607">sinh</span></span> |<span data-ttu-id="1efa5-608">傳回角度的雙曲正弦值。</span><span class="sxs-lookup"><span data-stu-id="1efa5-608">Returns hyperbolic sine of an angle.</span></span> |`sinh(x)` |
| <span data-ttu-id="1efa5-609">級別</span><span class="sxs-lookup"><span data-stu-id="1efa5-609">scale</span></span> |<span data-ttu-id="1efa5-610">標尺的 hello 函式 x 的值，例如其落 hello 之間指定的 minTarget 和 maxTarget （含)。</span><span class="sxs-lookup"><span data-stu-id="1efa5-610">Scales values of hello function x, such that they fall between hello specified minTarget and maxTarget inclusive.</span></span> <span data-ttu-id="1efa5-611">hello 目前的實作會周遊所有的 hello 函式值 tooobtain hello min 和 max，因而取得 hello 正確調整規模。</span><span class="sxs-lookup"><span data-stu-id="1efa5-611">hello current implementation traverses all of hello function values tooobtain hello min and max, so it can pick hello correct scale.</span></span> <span data-ttu-id="1efa5-612">hello 目前的實作無法區別已刪除的文件，或沒有值的文件。</span><span class="sxs-lookup"><span data-stu-id="1efa5-612">hello current implementation cannot distinguish when documents have been deleted, or documents that have no value.</span></span> <span data-ttu-id="1efa5-613">在這些情況下，它會使用 0.0 值。</span><span class="sxs-lookup"><span data-stu-id="1efa5-613">It uses 0.0 values for these cases.</span></span> <span data-ttu-id="1efa5-614">這表示，如果值通常都大於 0.0，其中一個可以仍然以 0.0 結束 hello 從最小值 toomap 如下。</span><span class="sxs-lookup"><span data-stu-id="1efa5-614">This means that if values are normally all greater than 0.0, one can still end up with 0.0 as hello min value toomap from.</span></span> <span data-ttu-id="1efa5-615">在這些情況下，適當`map()`函式可用為因應措施 toochange 0.0 tooa hello 實際範圍內值，如下所示：`scale(map(x,0,0,5),1,2)`</span><span class="sxs-lookup"><span data-stu-id="1efa5-615">In these cases, an appropriate `map()` function could be used as a workaround toochange 0.0 tooa value in hello real range, as shown here: `scale(map(x,0,0,5),1,2)`</span></span> |`scale(x,minTarget,maxTarget)`<br><span data-ttu-id="1efa5-616">`scale(x,1,2)`標尺 hello x 的值，使所有值都都介於 1 和 2 （含) 之間。</span><span class="sxs-lookup"><span data-stu-id="1efa5-616">`scale(x,1,2)` Scales hello values of x, such that all values are between 1 and 2 inclusive.</span></span> |
| <span data-ttu-id="1efa5-617">sqrt</span><span class="sxs-lookup"><span data-stu-id="1efa5-617">sqrt</span></span> |<span data-ttu-id="1efa5-618">傳回 hello 平方根 hello 指定值或函式。</span><span class="sxs-lookup"><span data-stu-id="1efa5-618">Returns hello square root of hello specified value or function.</span></span> |`sqrt(x)`<br>`sqrt(100)`<br>`sqrt(sum(x,100))` |
| <span data-ttu-id="1efa5-619">strdist</span><span class="sxs-lookup"><span data-stu-id="1efa5-619">strdist</span></span> |<span data-ttu-id="1efa5-620">計算兩個字串之間的 hello 距離。</span><span class="sxs-lookup"><span data-stu-id="1efa5-620">Calculates hello distance between two strings.</span></span> <span data-ttu-id="1efa5-621">使用 hello Lucene 拼字檢查工具 StringDistance 介面，並支援所有可用該套件中的 hello 實作。</span><span class="sxs-lookup"><span data-stu-id="1efa5-621">Uses hello Lucene spell checker StringDistance interface, and supports all of hello implementations available in that package.</span></span> <span data-ttu-id="1efa5-622">也允許應用程式 tooplug 自己，透過 Solr 的資源載入功能。</span><span class="sxs-lookup"><span data-stu-id="1efa5-622">Also allows applications tooplug in their own, via Solr's resource loading capabilities.</span></span> <span data-ttu-id="1efa5-623">strdist 採用 `(string1, string2, distance measure)`。</span><span class="sxs-lookup"><span data-stu-id="1efa5-623">strdist takes `(string1, string2, distance measure)`.</span></span> <span data-ttu-id="1efa5-624">距離量值的可能值如下︰</span><span class="sxs-lookup"><span data-stu-id="1efa5-624">Possible values for distance measure are:</span></span><ul><li><span data-ttu-id="1efa5-625">jw: Jaro-Winkler</span><span class="sxs-lookup"><span data-stu-id="1efa5-625">jw: Jaro-Winkler</span></span></li><li><span data-ttu-id="1efa5-626">編輯︰Levenstein 或編輯距離</span><span class="sxs-lookup"><span data-stu-id="1efa5-626">edit: Levenstein or Edit distance</span></span></li><li><span data-ttu-id="1efa5-627">ngram: NGramDistance，hello 如果指定，可以選擇傳入 hello ngram 大小太。</span><span class="sxs-lookup"><span data-stu-id="1efa5-627">ngram: hello NGramDistance, if specified, can optionally pass in hello ngram size too.</span></span> <span data-ttu-id="1efa5-628">預設值為 2。</span><span class="sxs-lookup"><span data-stu-id="1efa5-628">Default is 2.</span></span></li><li><span data-ttu-id="1efa5-629">FQN︰ 完整類別名稱 hello StringDistance 介面的實作。</span><span class="sxs-lookup"><span data-stu-id="1efa5-629">FQN: Fully Qualified class Name for an implementation of hello StringDistance interface.</span></span> <span data-ttu-id="1efa5-630">必須要有無引數建構函式。</span><span class="sxs-lookup"><span data-stu-id="1efa5-630">Must have a no-arg constructor.</span></span></li></ul> |`strdist("SOLR",id,edit)` |
| <span data-ttu-id="1efa5-631">sub</span><span class="sxs-lookup"><span data-stu-id="1efa5-631">sub</span></span> |<span data-ttu-id="1efa5-632">從 `sub(x,y)`傳回 x-y。</span><span class="sxs-lookup"><span data-stu-id="1efa5-632">Returns x-y from `sub(x,y)`.</span></span> |`sub(myfield,myfield2)`<br>`sub(100,sqrt(myfield))` |
| <span data-ttu-id="1efa5-633">Sum</span><span class="sxs-lookup"><span data-stu-id="1efa5-633">sum</span></span> |<span data-ttu-id="1efa5-634">傳回 hello 多個值或函式，以逗號分隔的清單中指定的總和。</span><span class="sxs-lookup"><span data-stu-id="1efa5-634">Returns hello sum of multiple values or functions, which are specified in a comma-separated list.</span></span> <span data-ttu-id="1efa5-635">`add(...)` 可以作為這個函式的別名。</span><span class="sxs-lookup"><span data-stu-id="1efa5-635">`add(...)` may be used as an alias for this function.</span></span> |`sum(x,y,...)`<br>`sum(x,1)`<br>`sum(x,y)`<br>`sum(sqrt(x),log(y),z,0.5)`<br>`add(x,y)` |
| <span data-ttu-id="1efa5-636">termfreq</span><span class="sxs-lookup"><span data-stu-id="1efa5-636">termfreq</span></span> |<span data-ttu-id="1efa5-637">傳回 hello 詞彙出現在該文件的 hello 欄位中的 hello 次數。</span><span class="sxs-lookup"><span data-stu-id="1efa5-637">Returns hello number of times hello term appears in hello field for that document.</span></span> |<span data-ttu-id="1efa5-638">termfreq(text,'memory')</span><span class="sxs-lookup"><span data-stu-id="1efa5-638">termfreq(text,'memory')</span></span> |
| <span data-ttu-id="1efa5-639">tan</span><span class="sxs-lookup"><span data-stu-id="1efa5-639">tan</span></span> |<span data-ttu-id="1efa5-640">傳回角度的正切值。</span><span class="sxs-lookup"><span data-stu-id="1efa5-640">Returns tangent of an angle.</span></span> |`tan(x)` |
| <span data-ttu-id="1efa5-641">tanh</span><span class="sxs-lookup"><span data-stu-id="1efa5-641">tanh</span></span> |<span data-ttu-id="1efa5-642">傳回角度的雙曲正切值。</span><span class="sxs-lookup"><span data-stu-id="1efa5-642">Returns hyperbolic tangent of an angle.</span></span> |`tanh(x)` |

## <a name="search-field-and-facet-reference"></a><span data-ttu-id="1efa5-643">搜尋欄位和 Facet 參考 (英文)</span><span class="sxs-lookup"><span data-stu-id="1efa5-643">Search field and facet reference</span></span>
<span data-ttu-id="1efa5-644">當您使用記錄搜尋 toofind 資料時，結果會顯示各種欄位和 facet。</span><span class="sxs-lookup"><span data-stu-id="1efa5-644">When you use Log Search toofind data, results display various field and facets.</span></span> <span data-ttu-id="1efa5-645">Hello 資訊的某些部分可能不會出現太清楚。</span><span class="sxs-lookup"><span data-stu-id="1efa5-645">Some of hello information might not appear very descriptive.</span></span> <span data-ttu-id="1efa5-646">使用下列資訊 toohelp 您了解 hello 結果 hello。</span><span class="sxs-lookup"><span data-stu-id="1efa5-646">Use hello following information toohelp you understand hello results.</span></span>

| <span data-ttu-id="1efa5-647">欄位</span><span class="sxs-lookup"><span data-stu-id="1efa5-647">Field</span></span> | <span data-ttu-id="1efa5-648">搜尋類型</span><span class="sxs-lookup"><span data-stu-id="1efa5-648">Search type</span></span> | <span data-ttu-id="1efa5-649">說明</span><span class="sxs-lookup"><span data-stu-id="1efa5-649">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1efa5-650">TenantId</span><span class="sxs-lookup"><span data-stu-id="1efa5-650">TenantId</span></span> |<span data-ttu-id="1efa5-651">全部</span><span class="sxs-lookup"><span data-stu-id="1efa5-651">All</span></span> |<span data-ttu-id="1efa5-652">使用 toopartition 資料。</span><span class="sxs-lookup"><span data-stu-id="1efa5-652">Used toopartition data.</span></span> |
| <span data-ttu-id="1efa5-653">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="1efa5-653">TimeGenerated</span></span> |<span data-ttu-id="1efa5-654">全部</span><span class="sxs-lookup"><span data-stu-id="1efa5-654">All</span></span> |<span data-ttu-id="1efa5-655">使用 toodrive hello 時間軸，timeselectors （在搜尋和其他螢幕中）。</span><span class="sxs-lookup"><span data-stu-id="1efa5-655">Used toodrive hello timeline, timeselectors (in search and in other screens).</span></span> <span data-ttu-id="1efa5-656">它代表 hello 資料片段的產生 （通常在 hello 代理程式）。</span><span class="sxs-lookup"><span data-stu-id="1efa5-656">It represents when hello piece of data was generated (typically on hello agent).</span></span> <span data-ttu-id="1efa5-657">hello 時間以 ISO 格式表示，且一律為 UTC。</span><span class="sxs-lookup"><span data-stu-id="1efa5-657">hello time is expressed in ISO format, and is always UTC.</span></span> <span data-ttu-id="1efa5-658">在現有的檢測 （也就是記錄檔中的事件） 為基礎之型別的 hello 情況下，這通常是真實時間該 hello 日誌項目/行/記錄 hello。</span><span class="sxs-lookup"><span data-stu-id="1efa5-658">In hello case of types that are based on existing instrumentation (that is, events in a log), this is typically hello real time that hello log entry/line/record was logged.</span></span> <span data-ttu-id="1efa5-659">Hello 的某些其他透過管理組件或 hello 雲端 （例如，建議或警示） 中所產生的型別 hello 一些不同的時間表示。</span><span class="sxs-lookup"><span data-stu-id="1efa5-659">For some of hello other types that are produced either via management packs or in hello cloud (for example, recommendations or alerts), hello time represents something different.</span></span> <span data-ttu-id="1efa5-660">這是當收集到這個新資料片段和某種組態之快照，或根據它產生建議/警示的 hello 時間。</span><span class="sxs-lookup"><span data-stu-id="1efa5-660">This is hello time when this new piece of data with a snapshot of a configuration of some sort was collected, or a recommendation/alert was produced based on it.</span></span> |
| <span data-ttu-id="1efa5-661">EventID</span><span class="sxs-lookup"><span data-stu-id="1efa5-661">EventID</span></span> |<span data-ttu-id="1efa5-662">Event</span><span class="sxs-lookup"><span data-stu-id="1efa5-662">Event</span></span> |<span data-ttu-id="1efa5-663">Hello Windows 事件記錄檔中的 EventID。</span><span class="sxs-lookup"><span data-stu-id="1efa5-663">EventID in hello Windows event log.</span></span> |
| <span data-ttu-id="1efa5-664">EventLog</span><span class="sxs-lookup"><span data-stu-id="1efa5-664">EventLog</span></span> |<span data-ttu-id="1efa5-665">Event</span><span class="sxs-lookup"><span data-stu-id="1efa5-665">Event</span></span> |<span data-ttu-id="1efa5-666">其中 hello 事件記錄的 Windows 事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="1efa5-666">Event log where hello event was logged by Windows.</span></span> |
| <span data-ttu-id="1efa5-667">EventLevelName</span><span class="sxs-lookup"><span data-stu-id="1efa5-667">EventLevelName</span></span> |<span data-ttu-id="1efa5-668">Event</span><span class="sxs-lookup"><span data-stu-id="1efa5-668">Event</span></span> |<span data-ttu-id="1efa5-669">重大/警告/資訊/成功</span><span class="sxs-lookup"><span data-stu-id="1efa5-669">Critical/warning/information/success</span></span> |
| <span data-ttu-id="1efa5-670">EventLevel</span><span class="sxs-lookup"><span data-stu-id="1efa5-670">EventLevel</span></span> |<span data-ttu-id="1efa5-671">Event</span><span class="sxs-lookup"><span data-stu-id="1efa5-671">Event</span></span> |<span data-ttu-id="1efa5-672">重大/警告/資訊/成功的數值 (對於更容易/更適合閱讀的查詢，請改用 EventLevelName)。</span><span class="sxs-lookup"><span data-stu-id="1efa5-672">Numerical value for critical/warning/information/success (use EventLevelName instead for easier/more readable queries).</span></span> |
| <span data-ttu-id="1efa5-673">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="1efa5-673">SourceSystem</span></span> |<span data-ttu-id="1efa5-674">全部</span><span class="sxs-lookup"><span data-stu-id="1efa5-674">All</span></span> |<span data-ttu-id="1efa5-675">Hello 資料來自何處 （的附加模式 toohello 服務）。</span><span class="sxs-lookup"><span data-stu-id="1efa5-675">Where hello data comes from (in terms of attach mode toohello service).</span></span> <span data-ttu-id="1efa5-676">範例包括 Microsoft System Center Operations Manager 和 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="1efa5-676">Examples include Microsoft System Center Operations Manager and Azure Storage.</span></span> |
| <span data-ttu-id="1efa5-677">ObjectName</span><span class="sxs-lookup"><span data-stu-id="1efa5-677">ObjectName</span></span> |<span data-ttu-id="1efa5-678">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="1efa5-678">PerfHourly</span></span> |<span data-ttu-id="1efa5-679">Windows 效能物件名稱。</span><span class="sxs-lookup"><span data-stu-id="1efa5-679">Windows performance object name.</span></span> |
| <span data-ttu-id="1efa5-680">InstanceName</span><span class="sxs-lookup"><span data-stu-id="1efa5-680">InstanceName</span></span> |<span data-ttu-id="1efa5-681">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="1efa5-681">PerfHourly</span></span> |<span data-ttu-id="1efa5-682">Windows 效能計數器執行個體名稱。</span><span class="sxs-lookup"><span data-stu-id="1efa5-682">Windows performance counter instance name.</span></span> |
| <span data-ttu-id="1efa5-683">CounteName</span><span class="sxs-lookup"><span data-stu-id="1efa5-683">CounteName</span></span> |<span data-ttu-id="1efa5-684">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="1efa5-684">PerfHourly</span></span> |<span data-ttu-id="1efa5-685">Windows 效能計數器名稱。</span><span class="sxs-lookup"><span data-stu-id="1efa5-685">Windows performance counter name.</span></span> |
| <span data-ttu-id="1efa5-686">ObjectDisplayName</span><span class="sxs-lookup"><span data-stu-id="1efa5-686">ObjectDisplayName</span></span> |<span data-ttu-id="1efa5-687">PerfHourly、ConfigurationAlert、ConfigurationObject、ConfigurationObjectProperty</span><span class="sxs-lookup"><span data-stu-id="1efa5-687">PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty</span></span> |<span data-ttu-id="1efa5-688">在 Operations Manager 中效能集合規則以其為目標的 hello 物件的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="1efa5-688">Display name of hello object targeted by a performance collection rule in Operations Manager.</span></span> <span data-ttu-id="1efa5-689">也可能是 hello 的 Operational Insights 所探索到的 hello 物件的顯示名稱，或針對哪些 hello 產生警示。</span><span class="sxs-lookup"><span data-stu-id="1efa5-689">Could also be hello display name of hello object discovered by Operational Insights, or against which hello alert was generated.</span></span> |
| <span data-ttu-id="1efa5-690">RootObjectName</span><span class="sxs-lookup"><span data-stu-id="1efa5-690">RootObjectName</span></span> |<span data-ttu-id="1efa5-691">PerfHourly、ConfigurationAlert、ConfigurationObject、ConfigurationObjectProperty</span><span class="sxs-lookup"><span data-stu-id="1efa5-691">PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty</span></span> |<span data-ttu-id="1efa5-692">Hello hello （在雙主控關聯性） 中的父代在 Operations Manager 中效能集合規則以其為目標的 hello 物件父系的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="1efa5-692">Display name of hello parent of hello parent (in a double hosting relationship) of hello object targeted by a performance collection rule in Operations Manager.</span></span> <span data-ttu-id="1efa5-693">也可能是 hello 的 Operational Insights 所探索到的 hello 物件的顯示名稱，或針對哪些 hello 產生警示。</span><span class="sxs-lookup"><span data-stu-id="1efa5-693">Could also be hello display name of hello object discovered by Operational Insights, or against which hello alert was generated.</span></span> |
| <span data-ttu-id="1efa5-694">電腦</span><span class="sxs-lookup"><span data-stu-id="1efa5-694">Computer</span></span> |<span data-ttu-id="1efa5-695">大部分的類型</span><span class="sxs-lookup"><span data-stu-id="1efa5-695">Most types</span></span> |<span data-ttu-id="1efa5-696">Hello 資料所屬的電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="1efa5-696">Computer name that hello data belongs to.</span></span> |
| <span data-ttu-id="1efa5-697">DeviceName</span><span class="sxs-lookup"><span data-stu-id="1efa5-697">DeviceName</span></span> |<span data-ttu-id="1efa5-698">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="1efa5-698">ProtectionStatus</span></span> |<span data-ttu-id="1efa5-699">電腦名稱 hello 資料太所屬 （相同 「 電腦 」）。</span><span class="sxs-lookup"><span data-stu-id="1efa5-699">Computer name hello data belongs too(same as "Computer").</span></span> |
| <span data-ttu-id="1efa5-700">DetectionId</span><span class="sxs-lookup"><span data-stu-id="1efa5-700">DetectionId</span></span> |<span data-ttu-id="1efa5-701">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="1efa5-701">ProtectionStatus</span></span> | |
| <span data-ttu-id="1efa5-702">ThreatStatusRank</span><span class="sxs-lookup"><span data-stu-id="1efa5-702">ThreatStatusRank</span></span> |<span data-ttu-id="1efa5-703">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="1efa5-703">ProtectionStatus</span></span> |<span data-ttu-id="1efa5-704">威脅狀態排名是 hello 威脅狀態的數值表示法。</span><span class="sxs-lookup"><span data-stu-id="1efa5-704">Threat status rank is a numerical representation of hello threat status.</span></span> <span data-ttu-id="1efa5-705">類似 tooHTTP 回應碼，hello 排名有 hello 數字之間的間距 （這就是為什麼沒有威脅是 150 並不是 100 或 0），留出空間 tooadd 新狀態。</span><span class="sxs-lookup"><span data-stu-id="1efa5-705">Similar tooHTTP response codes, hello ranking has gaps between hello numbers (which is why no threats is 150 and not 100 or 0), leaving room tooadd new states.</span></span> <span data-ttu-id="1efa5-706">威脅狀態和防護狀態的彙總，如 hello 意圖會是 tooshow hello 的最差狀態 hello 電腦已在選取的時間週期的 hello 期間。</span><span class="sxs-lookup"><span data-stu-id="1efa5-706">For a rollup of threat status and protection status, hello intention is tooshow hello worst state that hello computer has been in during hello selected time period.</span></span> <span data-ttu-id="1efa5-707">hello 數字排名 hello 不同狀態，讓您可以查看 hello 記錄與 hello 最高數字。</span><span class="sxs-lookup"><span data-stu-id="1efa5-707">hello numbers rank hello different states, so you can look for hello record with hello highest number.</span></span> |
| <span data-ttu-id="1efa5-708">ThreatStatus</span><span class="sxs-lookup"><span data-stu-id="1efa5-708">ThreatStatus</span></span> |<span data-ttu-id="1efa5-709">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="1efa5-709">ProtectionStatus</span></span> |<span data-ttu-id="1efa5-710">ThreatStatus 的描述，與 ThreatStatusRank 1:1 對應。</span><span class="sxs-lookup"><span data-stu-id="1efa5-710">Description of ThreatStatus, maps 1:1 with ThreatStatusRank.</span></span> |
| <span data-ttu-id="1efa5-711">TypeofProtection</span><span class="sxs-lookup"><span data-stu-id="1efa5-711">TypeofProtection</span></span> |<span data-ttu-id="1efa5-712">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="1efa5-712">ProtectionStatus</span></span> |<span data-ttu-id="1efa5-713">Hello 電腦中偵測到的反惡意程式碼產品： 無、 Microsoft 惡意程式碼移除工具、 Forefront 等等。</span><span class="sxs-lookup"><span data-stu-id="1efa5-713">Antimalware product that is detected in hello computer: none, Microsoft Malware Removal tool, Forefront, and so on.</span></span> |
| <span data-ttu-id="1efa5-714">ScanDate</span><span class="sxs-lookup"><span data-stu-id="1efa5-714">ScanDate</span></span> |<span data-ttu-id="1efa5-715">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="1efa5-715">ProtectionStatus</span></span> | |
| <span data-ttu-id="1efa5-716">SourceHealthServiceId</span><span class="sxs-lookup"><span data-stu-id="1efa5-716">SourceHealthServiceId</span></span> |<span data-ttu-id="1efa5-717">ProtectionStatus、RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="1efa5-717">ProtectionStatus, RequiredUpdate</span></span> |<span data-ttu-id="1efa5-718">這台電腦之代理程式的 HealthService 識別碼。</span><span class="sxs-lookup"><span data-stu-id="1efa5-718">HealthService ID for this computer's agent.</span></span> |
| <span data-ttu-id="1efa5-719">HealthServiceId</span><span class="sxs-lookup"><span data-stu-id="1efa5-719">HealthServiceId</span></span> |<span data-ttu-id="1efa5-720">大部分的類型</span><span class="sxs-lookup"><span data-stu-id="1efa5-720">Most types</span></span> |<span data-ttu-id="1efa5-721">這台電腦之代理程式的 HealthService 識別碼。</span><span class="sxs-lookup"><span data-stu-id="1efa5-721">HealthService ID for this computer's agent.</span></span> |
| <span data-ttu-id="1efa5-722">ManagementGroupName</span><span class="sxs-lookup"><span data-stu-id="1efa5-722">ManagementGroupName</span></span> |<span data-ttu-id="1efa5-723">大部分的類型</span><span class="sxs-lookup"><span data-stu-id="1efa5-723">Most types</span></span> |<span data-ttu-id="1efa5-724">Operations Manager 附加代理程式的管理群組名稱。</span><span class="sxs-lookup"><span data-stu-id="1efa5-724">Management Group Name for Operations Manager-attached agents.</span></span> <span data-ttu-id="1efa5-725">否則會是 null/空白。</span><span class="sxs-lookup"><span data-stu-id="1efa5-725">Otherwise, it is null/blank.</span></span> |
| <span data-ttu-id="1efa5-726">ObjectType</span><span class="sxs-lookup"><span data-stu-id="1efa5-726">ObjectType</span></span> |<span data-ttu-id="1efa5-727">ConfigurationObject</span><span class="sxs-lookup"><span data-stu-id="1efa5-727">ConfigurationObject</span></span> |<span data-ttu-id="1efa5-728">由 Log Analytics 組態評估所探索到之這個物件的類型 (例如 Operations Manager 管理組件的類型/類別)。</span><span class="sxs-lookup"><span data-stu-id="1efa5-728">Type (as in Operations Manager management pack's type/class) for this object, discovered by Log Analytics configuration assessment.</span></span> |
| <span data-ttu-id="1efa5-729">UpdateTitle</span><span class="sxs-lookup"><span data-stu-id="1efa5-729">UpdateTitle</span></span> |<span data-ttu-id="1efa5-730">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="1efa5-730">RequiredUpdate</span></span> |<span data-ttu-id="1efa5-731">Hello 已找不到已安裝的更新名稱。</span><span class="sxs-lookup"><span data-stu-id="1efa5-731">Name of hello update that was found not installed.</span></span> |
| <span data-ttu-id="1efa5-732">PublishDate</span><span class="sxs-lookup"><span data-stu-id="1efa5-732">PublishDate</span></span> |<span data-ttu-id="1efa5-733">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="1efa5-733">RequiredUpdate</span></span> |<span data-ttu-id="1efa5-734">當 hello 更新 Microsoft Update 上發佈。</span><span class="sxs-lookup"><span data-stu-id="1efa5-734">When hello update was published on Microsoft Update.</span></span> |
| <span data-ttu-id="1efa5-735">伺服器</span><span class="sxs-lookup"><span data-stu-id="1efa5-735">Server</span></span> |<span data-ttu-id="1efa5-736">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="1efa5-736">RequiredUpdate</span></span> |<span data-ttu-id="1efa5-737">電腦名稱 hello 資料太所屬 （相同 「 電腦 」）。</span><span class="sxs-lookup"><span data-stu-id="1efa5-737">Computer name hello data belongs too(same as "Computer").</span></span> |
| <span data-ttu-id="1efa5-738">產品</span><span class="sxs-lookup"><span data-stu-id="1efa5-738">Product</span></span> |<span data-ttu-id="1efa5-739">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="1efa5-739">RequiredUpdate</span></span> |<span data-ttu-id="1efa5-740">套用於 hello 更新的產品。</span><span class="sxs-lookup"><span data-stu-id="1efa5-740">Product that hello update applies to.</span></span> |
| <span data-ttu-id="1efa5-741">UpdateClassification</span><span class="sxs-lookup"><span data-stu-id="1efa5-741">UpdateClassification</span></span> |<span data-ttu-id="1efa5-742">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="1efa5-742">RequiredUpdate</span></span> |<span data-ttu-id="1efa5-743">更新類型 (例如，更新彙總套件、Service Pack)。</span><span class="sxs-lookup"><span data-stu-id="1efa5-743">Type of update (for example, update rollup or service pack).</span></span> |
| <span data-ttu-id="1efa5-744">KBID</span><span class="sxs-lookup"><span data-stu-id="1efa5-744">KBID</span></span> |<span data-ttu-id="1efa5-745">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="1efa5-745">RequiredUpdate</span></span> |<span data-ttu-id="1efa5-746">描述此最佳做法或更新的 KB 文章識別碼。</span><span class="sxs-lookup"><span data-stu-id="1efa5-746">KB article ID that describes this best practice or update.</span></span> |
| <span data-ttu-id="1efa5-747">WorkflowName</span><span class="sxs-lookup"><span data-stu-id="1efa5-747">WorkflowName</span></span> |<span data-ttu-id="1efa5-748">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="1efa5-748">ConfigurationAlert</span></span> |<span data-ttu-id="1efa5-749">Hello 規則或監視產生 hello 警示的名稱。</span><span class="sxs-lookup"><span data-stu-id="1efa5-749">Name of hello rule or monitor that produced hello alert.</span></span> |
| <span data-ttu-id="1efa5-750">嚴重性</span><span class="sxs-lookup"><span data-stu-id="1efa5-750">Severity</span></span> |<span data-ttu-id="1efa5-751">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="1efa5-751">ConfigurationAlert</span></span> |<span data-ttu-id="1efa5-752">Hello 警示的嚴重性。</span><span class="sxs-lookup"><span data-stu-id="1efa5-752">Severity of hello alert.</span></span> |
| <span data-ttu-id="1efa5-753">優先順序</span><span class="sxs-lookup"><span data-stu-id="1efa5-753">Priority</span></span> |<span data-ttu-id="1efa5-754">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="1efa5-754">ConfigurationAlert</span></span> |<span data-ttu-id="1efa5-755">Hello 警示的優先順序。</span><span class="sxs-lookup"><span data-stu-id="1efa5-755">Priority of hello alert.</span></span> |
| <span data-ttu-id="1efa5-756">IsMonitorAlert</span><span class="sxs-lookup"><span data-stu-id="1efa5-756">IsMonitorAlert</span></span> |<span data-ttu-id="1efa5-757">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="1efa5-757">ConfigurationAlert</span></span> |<span data-ttu-id="1efa5-758">此警示由監視器 (true) 或規則 (false) 所產生？</span><span class="sxs-lookup"><span data-stu-id="1efa5-758">Is this alert generated by a monitor (true) or a rule (false)?</span></span> |
| <span data-ttu-id="1efa5-759">AlertParameters</span><span class="sxs-lookup"><span data-stu-id="1efa5-759">AlertParameters</span></span> |<span data-ttu-id="1efa5-760">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="1efa5-760">ConfigurationAlert</span></span> |<span data-ttu-id="1efa5-761">Hello 記錄分析警示的 hello 參數的 XML。</span><span class="sxs-lookup"><span data-stu-id="1efa5-761">XML with hello parameters of hello Log Analytics alert.</span></span> |
| <span data-ttu-id="1efa5-762">Context</span><span class="sxs-lookup"><span data-stu-id="1efa5-762">Context</span></span> |<span data-ttu-id="1efa5-763">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="1efa5-763">ConfigurationAlert</span></span> |<span data-ttu-id="1efa5-764">Hello 警示內容的 hello 記錄分析的 XML。</span><span class="sxs-lookup"><span data-stu-id="1efa5-764">XML with hello context of hello Log Analytics alert.</span></span> |
| <span data-ttu-id="1efa5-765">工作負載</span><span class="sxs-lookup"><span data-stu-id="1efa5-765">Workload</span></span> |<span data-ttu-id="1efa5-766">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="1efa5-766">ConfigurationAlert</span></span> |<span data-ttu-id="1efa5-767">技術或 hello 警示的工作負載參考。</span><span class="sxs-lookup"><span data-stu-id="1efa5-767">Technology or workload that hello alert refers to.</span></span> |
| <span data-ttu-id="1efa5-768">AdvisorWorkload</span><span class="sxs-lookup"><span data-stu-id="1efa5-768">AdvisorWorkload</span></span> |<span data-ttu-id="1efa5-769">建議</span><span class="sxs-lookup"><span data-stu-id="1efa5-769">Recommendation</span></span> |<span data-ttu-id="1efa5-770">技術或 hello 建議的工作負載參考。</span><span class="sxs-lookup"><span data-stu-id="1efa5-770">Technology or workload that hello recommendation refers to.</span></span> |
| <span data-ttu-id="1efa5-771">說明</span><span class="sxs-lookup"><span data-stu-id="1efa5-771">Description</span></span> |<span data-ttu-id="1efa5-772">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="1efa5-772">ConfigurationAlert</span></span> |<span data-ttu-id="1efa5-773">警示描述 (簡短)。</span><span class="sxs-lookup"><span data-stu-id="1efa5-773">Alert description (short).</span></span> |
| <span data-ttu-id="1efa5-774">DaysSinceLastUpdate</span><span class="sxs-lookup"><span data-stu-id="1efa5-774">DaysSinceLastUpdate</span></span> |<span data-ttu-id="1efa5-775">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="1efa5-775">UpdateAgent</span></span> |<span data-ttu-id="1efa5-776">幾天前 (這筆記錄的相對 tooTimeGenerated) 沒有此代理程式安裝任何更新從 Windows Server Update Service (WSUS) 或 Microsoft Update？</span><span class="sxs-lookup"><span data-stu-id="1efa5-776">How many days ago (relative tooTimeGenerated of this record) did this agent install any update from Windows Server Update Service (WSUS) or Microsoft Update?</span></span> |
| <span data-ttu-id="1efa5-777">DaysSinceLastUpdateBucket</span><span class="sxs-lookup"><span data-stu-id="1efa5-777">DaysSinceLastUpdateBucket</span></span> |<span data-ttu-id="1efa5-778">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="1efa5-778">UpdateAgent</span></span> |<span data-ttu-id="1efa5-779">根據 DaysSinceLastUpdate，多久以前的時間值區分類是上一次從 WSUS/Microsoft Update 安裝任何更新的電腦。</span><span class="sxs-lookup"><span data-stu-id="1efa5-779">Based on DaysSinceLastUpdate, a categorization in time buckets of how long ago a computer last installed any update from WSUS/Microsoft Update.</span></span> |
| <span data-ttu-id="1efa5-780">AutomaticUpdateEnabled</span><span class="sxs-lookup"><span data-stu-id="1efa5-780">AutomaticUpdateEnabled</span></span> |<span data-ttu-id="1efa5-781">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="1efa5-781">UpdateAgent</span></span> |<span data-ttu-id="1efa5-782">自動更新檢查是在此代理程式上啟用或停用的嗎？</span><span class="sxs-lookup"><span data-stu-id="1efa5-782">Is automatic update checking enabled or disabled on this agent?</span></span> |
| <span data-ttu-id="1efa5-783">AutomaticUpdateValue</span><span class="sxs-lookup"><span data-stu-id="1efa5-783">AutomaticUpdateValue</span></span> |<span data-ttu-id="1efa5-784">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="1efa5-784">UpdateAgent</span></span> |<span data-ttu-id="1efa5-785">是用來自動更新檢查設定 tooautomatically 下載和安裝、 只下載，或只檢查嗎？</span><span class="sxs-lookup"><span data-stu-id="1efa5-785">Is automatic update checking set tooautomatically download and install, only download, or only check?</span></span> |
| <span data-ttu-id="1efa5-786">WindowsUpdateAgentVersion</span><span class="sxs-lookup"><span data-stu-id="1efa5-786">WindowsUpdateAgentVersion</span></span> |<span data-ttu-id="1efa5-787">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="1efa5-787">UpdateAgent</span></span> |<span data-ttu-id="1efa5-788">Hello Microsoft Update 代理程式版本號碼。</span><span class="sxs-lookup"><span data-stu-id="1efa5-788">Version number of hello Microsoft Update agent.</span></span> |
| <span data-ttu-id="1efa5-789">WSUSServer</span><span class="sxs-lookup"><span data-stu-id="1efa5-789">WSUSServer</span></span> |<span data-ttu-id="1efa5-790">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="1efa5-790">UpdateAgent</span></span> |<span data-ttu-id="1efa5-791">此更新代理程式的目標是哪個 WSUS 伺服器？</span><span class="sxs-lookup"><span data-stu-id="1efa5-791">Which WSUS server is this update agent targeting?</span></span> |
| <span data-ttu-id="1efa5-792">OSVersion</span><span class="sxs-lookup"><span data-stu-id="1efa5-792">OSVersion</span></span> |<span data-ttu-id="1efa5-793">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="1efa5-793">UpdateAgent</span></span> |<span data-ttu-id="1efa5-794">Hello 作業系統版本上執行此更新代理程式。</span><span class="sxs-lookup"><span data-stu-id="1efa5-794">Version of hello operating system this update agent is running on.</span></span> |
| <span data-ttu-id="1efa5-795">名稱</span><span class="sxs-lookup"><span data-stu-id="1efa5-795">Name</span></span> |<span data-ttu-id="1efa5-796">建議，ConfigurationObjectProperty</span><span class="sxs-lookup"><span data-stu-id="1efa5-796">Recommendation, ConfigurationObjectProperty</span></span> |<span data-ttu-id="1efa5-797">名稱/標題 hello 建議，或記錄分析 configuration assessment 中的 hello 屬性的名稱。</span><span class="sxs-lookup"><span data-stu-id="1efa5-797">Name/title of hello recommendation, or name of hello property from Log Analytics configuration assessment.</span></span> |
| <span data-ttu-id="1efa5-798">值</span><span class="sxs-lookup"><span data-stu-id="1efa5-798">Value</span></span> |<span data-ttu-id="1efa5-799">ConfigurationObjectProperty</span><span class="sxs-lookup"><span data-stu-id="1efa5-799">ConfigurationObjectProperty</span></span> |<span data-ttu-id="1efa5-800">來自 Log Analytics 組態評估的屬性值。</span><span class="sxs-lookup"><span data-stu-id="1efa5-800">Value of a property from Log Analytics configuration assessment.</span></span> |
| <span data-ttu-id="1efa5-801">KBLink</span><span class="sxs-lookup"><span data-stu-id="1efa5-801">KBLink</span></span> |<span data-ttu-id="1efa5-802">建議</span><span class="sxs-lookup"><span data-stu-id="1efa5-802">Recommendation</span></span> |<span data-ttu-id="1efa5-803">描述此最佳作法或更新的 URL toohello KB 文章。</span><span class="sxs-lookup"><span data-stu-id="1efa5-803">URL toohello KB article that describes this best practice or update.</span></span> |
| <span data-ttu-id="1efa5-804">RecommendationStatus</span><span class="sxs-lookup"><span data-stu-id="1efa5-804">RecommendationStatus</span></span> |<span data-ttu-id="1efa5-805">建議</span><span class="sxs-lookup"><span data-stu-id="1efa5-805">Recommendation</span></span> |<span data-ttu-id="1efa5-806">建議 hello 為一些類型，其記錄取得更新，剛加入 toohello 搜尋索引。</span><span class="sxs-lookup"><span data-stu-id="1efa5-806">Recommendations are among hello few types whose records get updated, not just added toohello search index.</span></span> <span data-ttu-id="1efa5-807">此狀態會變更 hello 建議是否作用中/開啟，或如果記錄分析偵測到它已解決。</span><span class="sxs-lookup"><span data-stu-id="1efa5-807">This status changes whether hello recommendation is active/open, or if Log Analytics detects that it has been resolved.</span></span> |
| <span data-ttu-id="1efa5-808">RenderedDescription</span><span class="sxs-lookup"><span data-stu-id="1efa5-808">RenderedDescription</span></span> |<span data-ttu-id="1efa5-809">Event</span><span class="sxs-lookup"><span data-stu-id="1efa5-809">Event</span></span> |<span data-ttu-id="1efa5-810">Windows 事件的呈現描述 (具有填入參數的重複使用文字)。</span><span class="sxs-lookup"><span data-stu-id="1efa5-810">Rendered description (reused text with populated parameters) of a Windows event.</span></span> |
| <span data-ttu-id="1efa5-811">ParameterXml</span><span class="sxs-lookup"><span data-stu-id="1efa5-811">ParameterXml</span></span> |<span data-ttu-id="1efa5-812">Event</span><span class="sxs-lookup"><span data-stu-id="1efa5-812">Event</span></span> |<span data-ttu-id="1efa5-813">Windows 事件 （如事件檢視器中所見） hello data 區段中的 hello 參數的 XML。</span><span class="sxs-lookup"><span data-stu-id="1efa5-813">XML with hello parameters in hello data section of a Windows Event (as seen in event viewer).</span></span> |
| <span data-ttu-id="1efa5-814">EventData</span><span class="sxs-lookup"><span data-stu-id="1efa5-814">EventData</span></span> |<span data-ttu-id="1efa5-815">Event</span><span class="sxs-lookup"><span data-stu-id="1efa5-815">Event</span></span> |<span data-ttu-id="1efa5-816">Hello 整個資料一節中的 Windows 事件 （如同在事件檢視器） 的 XML。</span><span class="sxs-lookup"><span data-stu-id="1efa5-816">XML with hello whole data section of a Windows Event (as seen in event viewer).</span></span> |
| <span data-ttu-id="1efa5-817">來源</span><span class="sxs-lookup"><span data-stu-id="1efa5-817">Source</span></span> |<span data-ttu-id="1efa5-818">Event</span><span class="sxs-lookup"><span data-stu-id="1efa5-818">Event</span></span> |<span data-ttu-id="1efa5-819">產生 hello 事件的事件記錄檔來源。</span><span class="sxs-lookup"><span data-stu-id="1efa5-819">Event log source that generated hello event.</span></span> |
| <span data-ttu-id="1efa5-820">EventCategory</span><span class="sxs-lookup"><span data-stu-id="1efa5-820">EventCategory</span></span> |<span data-ttu-id="1efa5-821">Event</span><span class="sxs-lookup"><span data-stu-id="1efa5-821">Event</span></span> |<span data-ttu-id="1efa5-822">直接從 hello Windows 事件記錄檔的 hello 事件類別目錄。</span><span class="sxs-lookup"><span data-stu-id="1efa5-822">Category of hello event, directly from hello Windows event log.</span></span> |
| <span data-ttu-id="1efa5-823">UserName</span><span class="sxs-lookup"><span data-stu-id="1efa5-823">UserName</span></span> |<span data-ttu-id="1efa5-824">Event</span><span class="sxs-lookup"><span data-stu-id="1efa5-824">Event</span></span> |<span data-ttu-id="1efa5-825">Hello Windows 事件 (通常是 NT AUTHORITY\LOCALSYSTEM) 的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="1efa5-825">User name of hello Windows event (typically, NT AUTHORITY\LOCALSYSTEM).</span></span> |
| <span data-ttu-id="1efa5-826">SampleValue</span><span class="sxs-lookup"><span data-stu-id="1efa5-826">SampleValue</span></span> |<span data-ttu-id="1efa5-827">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="1efa5-827">PerfHourly</span></span> |<span data-ttu-id="1efa5-828">Hello 每小時彙總效能計數器的平均值。</span><span class="sxs-lookup"><span data-stu-id="1efa5-828">Average value for hello hourly aggregation of a performance counter.</span></span> |
| <span data-ttu-id="1efa5-829">Min</span><span class="sxs-lookup"><span data-stu-id="1efa5-829">Min</span></span> |<span data-ttu-id="1efa5-830">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="1efa5-830">PerfHourly</span></span> |<span data-ttu-id="1efa5-831">Hello 效能計數器每小時彙總的每小時間隔內的最小值。</span><span class="sxs-lookup"><span data-stu-id="1efa5-831">Minimum value in hello hourly interval of a performance counter hourly aggregate.</span></span> |
| <span data-ttu-id="1efa5-832">max</span><span class="sxs-lookup"><span data-stu-id="1efa5-832">Max</span></span> |<span data-ttu-id="1efa5-833">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="1efa5-833">PerfHourly</span></span> |<span data-ttu-id="1efa5-834">Hello 效能計數器每小時彙總的每小時間隔內的最大值。</span><span class="sxs-lookup"><span data-stu-id="1efa5-834">Maximum value in hello hourly interval of a performance counter hourly aggregate.</span></span> |
| <span data-ttu-id="1efa5-835">Percentile95</span><span class="sxs-lookup"><span data-stu-id="1efa5-835">Percentile95</span></span> |<span data-ttu-id="1efa5-836">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="1efa5-836">PerfHourly</span></span> |<span data-ttu-id="1efa5-837">hello 第 95 個百分 hello 效能計數器每小時彙總的每小時間隔。</span><span class="sxs-lookup"><span data-stu-id="1efa5-837">hello 95th percentile value for hello hourly interval of a performance counter hourly aggregate.</span></span> |
| <span data-ttu-id="1efa5-838">SampleCount</span><span class="sxs-lookup"><span data-stu-id="1efa5-838">SampleCount</span></span> |<span data-ttu-id="1efa5-839">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="1efa5-839">PerfHourly</span></span> |<span data-ttu-id="1efa5-840">多少 「 未經處理的效能計數器範例已使用的 tooproduce 此每小時彙總記錄。</span><span class="sxs-lookup"><span data-stu-id="1efa5-840">How many raw performance counter samples were used tooproduce this hourly aggregate record.</span></span> |
| <span data-ttu-id="1efa5-841">Threat</span><span class="sxs-lookup"><span data-stu-id="1efa5-841">Threat</span></span> |<span data-ttu-id="1efa5-842">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="1efa5-842">ProtectionStatus</span></span> |<span data-ttu-id="1efa5-843">找到的惡意程式碼名稱。</span><span class="sxs-lookup"><span data-stu-id="1efa5-843">Name of malware found.</span></span> |
| <span data-ttu-id="1efa5-844">StorageAccount</span><span class="sxs-lookup"><span data-stu-id="1efa5-844">StorageAccount</span></span> |<span data-ttu-id="1efa5-845">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="1efa5-845">W3CIISLog</span></span> |<span data-ttu-id="1efa5-846">Azure 儲存體帳戶 hello 記錄被讀取。</span><span class="sxs-lookup"><span data-stu-id="1efa5-846">Azure Storage account hello log was read from.</span></span> |
| <span data-ttu-id="1efa5-847">AzureDeploymentID</span><span class="sxs-lookup"><span data-stu-id="1efa5-847">AzureDeploymentID</span></span> |<span data-ttu-id="1efa5-848">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="1efa5-848">W3CIISLog</span></span> |<span data-ttu-id="1efa5-849">所屬的 azure 部署識別碼 hello 雲端服務 hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="1efa5-849">Azure deployment ID of hello cloud service hello log belongs to.</span></span> |
| <span data-ttu-id="1efa5-850">角色</span><span class="sxs-lookup"><span data-stu-id="1efa5-850">Role</span></span> |<span data-ttu-id="1efa5-851">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="1efa5-851">W3CIISLog</span></span> |<span data-ttu-id="1efa5-852">所屬的 hello Azure 雲端服務 hello 記錄檔的角色。</span><span class="sxs-lookup"><span data-stu-id="1efa5-852">Role of hello Azure cloud service hello log belongs to.</span></span> |
| <span data-ttu-id="1efa5-853">RoleInstance</span><span class="sxs-lookup"><span data-stu-id="1efa5-853">RoleInstance</span></span> |<span data-ttu-id="1efa5-854">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="1efa5-854">W3CIISLog</span></span> |<span data-ttu-id="1efa5-855">Hello hello 記錄的 Azure 角色的 RoleInstance 所屬。</span><span class="sxs-lookup"><span data-stu-id="1efa5-855">RoleInstance of hello Azure role that hello log belongs to.</span></span> |
| <span data-ttu-id="1efa5-856">sSiteName</span><span class="sxs-lookup"><span data-stu-id="1efa5-856">sSiteName</span></span> |<span data-ttu-id="1efa5-857">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="1efa5-857">W3CIISLog</span></span> |<span data-ttu-id="1efa5-858">Hello 記錄檔的 IIS 網站所屬 too(metabase notation);hello hello 原始記錄中的 s-sitename 欄位。</span><span class="sxs-lookup"><span data-stu-id="1efa5-858">IIS website that hello log belongs too(metabase notation); hello s-sitename field in hello original log.</span></span> |
| <span data-ttu-id="1efa5-859">sComputerName</span><span class="sxs-lookup"><span data-stu-id="1efa5-859">sComputerName</span></span> |<span data-ttu-id="1efa5-860">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="1efa5-860">W3CIISLog</span></span> |<span data-ttu-id="1efa5-861">hello hello 原始記錄中的 s-computername 欄位。</span><span class="sxs-lookup"><span data-stu-id="1efa5-861">hello s-computername field in hello original log.</span></span> |
| <span data-ttu-id="1efa5-862">sIP</span><span class="sxs-lookup"><span data-stu-id="1efa5-862">sIP</span></span> |<span data-ttu-id="1efa5-863">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="1efa5-863">W3CIISLog</span></span> |<span data-ttu-id="1efa5-864">伺服器 IP 位址 hello HTTP 要求被定址的目標。</span><span class="sxs-lookup"><span data-stu-id="1efa5-864">Server IP address hello HTTP request was addressed to.</span></span> <span data-ttu-id="1efa5-865">hello hello 原始記錄中的 s-ip 欄位。</span><span class="sxs-lookup"><span data-stu-id="1efa5-865">hello s-ip field in hello original log.</span></span> |
| <span data-ttu-id="1efa5-866">csMethod</span><span class="sxs-lookup"><span data-stu-id="1efa5-866">csMethod</span></span> |<span data-ttu-id="1efa5-867">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="1efa5-867">W3CIISLog</span></span> |<span data-ttu-id="1efa5-868">HTTP 方法 （例如，GET/POST） hello hello HTTP 要求中的用戶端使用。</span><span class="sxs-lookup"><span data-stu-id="1efa5-868">HTTP method (for example, GET/POST) used by hello client in hello HTTP request.</span></span> <span data-ttu-id="1efa5-869">hello cs 方法 hello 原始記錄中。</span><span class="sxs-lookup"><span data-stu-id="1efa5-869">hello cs-method in hello original log.</span></span> |
| <span data-ttu-id="1efa5-870">cIP</span><span class="sxs-lookup"><span data-stu-id="1efa5-870">cIP</span></span> |<span data-ttu-id="1efa5-871">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="1efa5-871">W3CIISLog</span></span> |<span data-ttu-id="1efa5-872">用戶端 IP 位址 hello HTTP 要求的來源。</span><span class="sxs-lookup"><span data-stu-id="1efa5-872">Client IP address hello HTTP request came from.</span></span> <span data-ttu-id="1efa5-873">hello hello 原始記錄中的 c-ip 欄位。</span><span class="sxs-lookup"><span data-stu-id="1efa5-873">hello c-ip field in hello original log.</span></span> |
| <span data-ttu-id="1efa5-874">csUserAgent</span><span class="sxs-lookup"><span data-stu-id="1efa5-874">csUserAgent</span></span> |<span data-ttu-id="1efa5-875">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="1efa5-875">W3CIISLog</span></span> |<span data-ttu-id="1efa5-876">Hello 用戶端所宣告的 HTTP User-agent (瀏覽器或其他)。</span><span class="sxs-lookup"><span data-stu-id="1efa5-876">HTTP User-Agent declared by hello client (browser or otherwise).</span></span> <span data-ttu-id="1efa5-877">hello cs-使用者代理程式 hello 原始記錄中。</span><span class="sxs-lookup"><span data-stu-id="1efa5-877">hello cs-user-agent in hello original log.</span></span> |
| <span data-ttu-id="1efa5-878">scStatus</span><span class="sxs-lookup"><span data-stu-id="1efa5-878">scStatus</span></span> |<span data-ttu-id="1efa5-879">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="1efa5-879">W3CIISLog</span></span> |<span data-ttu-id="1efa5-880">用戶端-伺服器 toohello hello 傳回 HTTP 狀態碼 (例如 200/403/500)。</span><span class="sxs-lookup"><span data-stu-id="1efa5-880">HTTP Status code (for example, 200/403/500) returned by hello server toohello client.</span></span> <span data-ttu-id="1efa5-881">hello 中 cs-status hello 原始記錄檔。</span><span class="sxs-lookup"><span data-stu-id="1efa5-881">hello cs-status in hello original log.</span></span> |
| <span data-ttu-id="1efa5-882">TimeTaken</span><span class="sxs-lookup"><span data-stu-id="1efa5-882">TimeTaken</span></span> |<span data-ttu-id="1efa5-883">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="1efa5-883">W3CIISLog</span></span> |<span data-ttu-id="1efa5-884">時間長度 （以毫秒為單位） 的 hello 要求所花費 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="1efa5-884">How long (in milliseconds) that hello request took toocomplete.</span></span> <span data-ttu-id="1efa5-885">hello hello 原始記錄中的 timetaken 欄位。</span><span class="sxs-lookup"><span data-stu-id="1efa5-885">hello timetaken field in hello original log.</span></span> |
| <span data-ttu-id="1efa5-886">csUriStem</span><span class="sxs-lookup"><span data-stu-id="1efa5-886">csUriStem</span></span> |<span data-ttu-id="1efa5-887">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="1efa5-887">W3CIISLog</span></span> |<span data-ttu-id="1efa5-888">要求的相對 URI (沒有主機位址，也就是 /search) 的要求。</span><span class="sxs-lookup"><span data-stu-id="1efa5-888">Relative URI (without host address, that is, /search ) that was requested.</span></span> <span data-ttu-id="1efa5-889">hello hello 原始記錄中的 cs-uristem 欄位。</span><span class="sxs-lookup"><span data-stu-id="1efa5-889">hello cs-uristem field in hello original log.</span></span> |
| <span data-ttu-id="1efa5-890">csUriQuery</span><span class="sxs-lookup"><span data-stu-id="1efa5-890">csUriQuery</span></span> |<span data-ttu-id="1efa5-891">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="1efa5-891">W3CIISLog</span></span> |<span data-ttu-id="1efa5-892">URI 查詢。</span><span class="sxs-lookup"><span data-stu-id="1efa5-892">URI query.</span></span> <span data-ttu-id="1efa5-893">只有 ASP 頁面等動態頁面才需要 URI 查詢，所以此欄位通常包含靜態網頁的連字號。</span><span class="sxs-lookup"><span data-stu-id="1efa5-893">URI queries are necessary only for dynamic pages, such as ASP pages, so this field usually contains a hyphen for static pages.</span></span> |
| <span data-ttu-id="1efa5-894">sPort</span><span class="sxs-lookup"><span data-stu-id="1efa5-894">sPort</span></span> |<span data-ttu-id="1efa5-895">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="1efa5-895">W3CIISLog</span></span> |<span data-ttu-id="1efa5-896">已傳送 hello HTTP 要求的伺服器連接埠 （和 IIS 所接聽，因為它會挑選它）。</span><span class="sxs-lookup"><span data-stu-id="1efa5-896">Server port that hello HTTP request was sent too(and that IIS listens to, since it picked it up).</span></span> |
| <span data-ttu-id="1efa5-897">csUserName</span><span class="sxs-lookup"><span data-stu-id="1efa5-897">csUserName</span></span> |<span data-ttu-id="1efa5-898">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="1efa5-898">W3CIISLog</span></span> |<span data-ttu-id="1efa5-899">如果 hello 要求已通過驗證且不匿名，驗證使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="1efa5-899">Authenticated user name, if hello request is authenticated and not anonymous.</span></span> |
| <span data-ttu-id="1efa5-900">csVersion</span><span class="sxs-lookup"><span data-stu-id="1efa5-900">csVersion</span></span> |<span data-ttu-id="1efa5-901">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="1efa5-901">W3CIISLog</span></span> |<span data-ttu-id="1efa5-902">Hello 要求 (例如，HTTP/1.1) 中使用的 HTTP 通訊協定版本。</span><span class="sxs-lookup"><span data-stu-id="1efa5-902">HTTP Protocol version used in hello request (for example, HTTP/1.1).</span></span> |
| <span data-ttu-id="1efa5-903">csCookie</span><span class="sxs-lookup"><span data-stu-id="1efa5-903">csCookie</span></span> |<span data-ttu-id="1efa5-904">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="1efa5-904">W3CIISLog</span></span> |<span data-ttu-id="1efa5-905">Cookie 資訊。</span><span class="sxs-lookup"><span data-stu-id="1efa5-905">Cookie information.</span></span> |
| <span data-ttu-id="1efa5-906">csReferer</span><span class="sxs-lookup"><span data-stu-id="1efa5-906">csReferer</span></span> |<span data-ttu-id="1efa5-907">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="1efa5-907">W3CIISLog</span></span> |<span data-ttu-id="1efa5-908">Hello 使用者上次造訪的網站。</span><span class="sxs-lookup"><span data-stu-id="1efa5-908">Site that hello user last visited.</span></span> <span data-ttu-id="1efa5-909">這個網站提供連結 toohello 目前站台。</span><span class="sxs-lookup"><span data-stu-id="1efa5-909">This site provided a link toohello current site.</span></span> |
| <span data-ttu-id="1efa5-910">csHost</span><span class="sxs-lookup"><span data-stu-id="1efa5-910">csHost</span></span> |<span data-ttu-id="1efa5-911">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="1efa5-911">W3CIISLog</span></span> |<span data-ttu-id="1efa5-912">要求的主機標頭 (例如，www.mysite.com)。</span><span class="sxs-lookup"><span data-stu-id="1efa5-912">Host header (for example, www.mysite.com) that was requested.</span></span> |
| <span data-ttu-id="1efa5-913">scSubStatus</span><span class="sxs-lookup"><span data-stu-id="1efa5-913">scSubStatus</span></span> |<span data-ttu-id="1efa5-914">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="1efa5-914">W3CIISLog</span></span> |<span data-ttu-id="1efa5-915">子狀態錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="1efa5-915">Substatus error code.</span></span> |
| <span data-ttu-id="1efa5-916">scWin32Status</span><span class="sxs-lookup"><span data-stu-id="1efa5-916">scWin32Status</span></span> |<span data-ttu-id="1efa5-917">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="1efa5-917">W3CIISLog</span></span> |<span data-ttu-id="1efa5-918">Windows 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="1efa5-918">Windows status code.</span></span> |
| <span data-ttu-id="1efa5-919">csBytes</span><span class="sxs-lookup"><span data-stu-id="1efa5-919">csBytes</span></span> |<span data-ttu-id="1efa5-920">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="1efa5-920">W3CIISLog</span></span> |<span data-ttu-id="1efa5-921">從 hello 用戶端 toohello 伺服器 hello 要求中傳送的位元組。</span><span class="sxs-lookup"><span data-stu-id="1efa5-921">Bytes sent in hello request from hello client toohello server.</span></span> |
| <span data-ttu-id="1efa5-922">scBytes</span><span class="sxs-lookup"><span data-stu-id="1efa5-922">scBytes</span></span> |<span data-ttu-id="1efa5-923">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="1efa5-923">W3CIISLog</span></span> |<span data-ttu-id="1efa5-924">在 hello 伺服器 toohello 用戶端 hello 回應中傳回的位元組。</span><span class="sxs-lookup"><span data-stu-id="1efa5-924">Bytes returned back in hello response from hello server toohello client.</span></span> |
| <span data-ttu-id="1efa5-925">ConfigChangeType</span><span class="sxs-lookup"><span data-stu-id="1efa5-925">ConfigChangeType</span></span> |<span data-ttu-id="1efa5-926">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="1efa5-926">ConfigurationChange</span></span> |<span data-ttu-id="1efa5-927">變更的類別 (例如，WindowsServices/Software)。</span><span class="sxs-lookup"><span data-stu-id="1efa5-927">Type of change (for example, WindowsServices/Software).</span></span> |
| <span data-ttu-id="1efa5-928">ChangeCategory</span><span class="sxs-lookup"><span data-stu-id="1efa5-928">ChangeCategory</span></span> |<span data-ttu-id="1efa5-929">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="1efa5-929">ConfigurationChange</span></span> |<span data-ttu-id="1efa5-930">Hello 變更 （已修改/新增/移除） 類別。</span><span class="sxs-lookup"><span data-stu-id="1efa5-930">Category of hello change (Modified/Added/Removed).</span></span> |
| <span data-ttu-id="1efa5-931">SoftwareType</span><span class="sxs-lookup"><span data-stu-id="1efa5-931">SoftwareType</span></span> |<span data-ttu-id="1efa5-932">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="1efa5-932">ConfigurationChange</span></span> |<span data-ttu-id="1efa5-933">軟體的類型 (更新/應用程式)。</span><span class="sxs-lookup"><span data-stu-id="1efa5-933">Type of software (Update/Application).</span></span> |
| <span data-ttu-id="1efa5-934">SoftwareName</span><span class="sxs-lookup"><span data-stu-id="1efa5-934">SoftwareName</span></span> |<span data-ttu-id="1efa5-935">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="1efa5-935">ConfigurationChange</span></span> |<span data-ttu-id="1efa5-936">Hello 軟體 （僅適用 toosoftware 變更） 的名稱。</span><span class="sxs-lookup"><span data-stu-id="1efa5-936">Name of hello software (only applicable toosoftware changes).</span></span> |
| <span data-ttu-id="1efa5-937">發佈者</span><span class="sxs-lookup"><span data-stu-id="1efa5-937">Publisher</span></span> |<span data-ttu-id="1efa5-938">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="1efa5-938">ConfigurationChange</span></span> |<span data-ttu-id="1efa5-939">發佈 hello 軟體 （僅適用 toosoftware 變更） 供應商。</span><span class="sxs-lookup"><span data-stu-id="1efa5-939">Vendor who publishes hello software (only applicable toosoftware changes).</span></span> |
| <span data-ttu-id="1efa5-940">SvcChangeType</span><span class="sxs-lookup"><span data-stu-id="1efa5-940">SvcChangeType</span></span> |<span data-ttu-id="1efa5-941">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="1efa5-941">ConfigurationChange</span></span> |<span data-ttu-id="1efa5-942">已套用在 Windows 服務的變更類型 (State/StartupType/Path/ServiceAccount)。</span><span class="sxs-lookup"><span data-stu-id="1efa5-942">Type of change that was applied on a Windows service (State/StartupType/Path/ServiceAccount).</span></span> <span data-ttu-id="1efa5-943">這是適用於 tooWindows 服務變更。</span><span class="sxs-lookup"><span data-stu-id="1efa5-943">This is only applicable tooWindows service changes.</span></span> |
| <span data-ttu-id="1efa5-944">SvcDisplayName</span><span class="sxs-lookup"><span data-stu-id="1efa5-944">SvcDisplayName</span></span> |<span data-ttu-id="1efa5-945">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="1efa5-945">ConfigurationChange</span></span> |<span data-ttu-id="1efa5-946">已變更的 hello 服務顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="1efa5-946">Display name of hello service that was changed.</span></span> |
| <span data-ttu-id="1efa5-947">SvcName</span><span class="sxs-lookup"><span data-stu-id="1efa5-947">SvcName</span></span> |<span data-ttu-id="1efa5-948">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="1efa5-948">ConfigurationChange</span></span> |<span data-ttu-id="1efa5-949">已變更的 hello 服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="1efa5-949">Name of hello service that was changed.</span></span> |
| <span data-ttu-id="1efa5-950">SvcState</span><span class="sxs-lookup"><span data-stu-id="1efa5-950">SvcState</span></span> |<span data-ttu-id="1efa5-951">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="1efa5-951">ConfigurationChange</span></span> |<span data-ttu-id="1efa5-952">Hello 服務新 （目前） 狀態。</span><span class="sxs-lookup"><span data-stu-id="1efa5-952">New (current) state of hello service.</span></span> |
| <span data-ttu-id="1efa5-953">SvcPreviousState</span><span class="sxs-lookup"><span data-stu-id="1efa5-953">SvcPreviousState</span></span> |<span data-ttu-id="1efa5-954">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="1efa5-954">ConfigurationChange</span></span> |<span data-ttu-id="1efa5-955">上一個已知 hello 服務 （僅適用於服務狀態變更） 的狀態。</span><span class="sxs-lookup"><span data-stu-id="1efa5-955">Previous known state of hello service (only applicable if service state changed).</span></span> |
| <span data-ttu-id="1efa5-956">SvcStartupType</span><span class="sxs-lookup"><span data-stu-id="1efa5-956">SvcStartupType</span></span> |<span data-ttu-id="1efa5-957">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="1efa5-957">ConfigurationChange</span></span> |<span data-ttu-id="1efa5-958">服務啟動類型。</span><span class="sxs-lookup"><span data-stu-id="1efa5-958">Service startup type.</span></span> |
| <span data-ttu-id="1efa5-959">SvcPreviousStartupType</span><span class="sxs-lookup"><span data-stu-id="1efa5-959">SvcPreviousStartupType</span></span> |<span data-ttu-id="1efa5-960">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="1efa5-960">ConfigurationChange</span></span> |<span data-ttu-id="1efa5-961">上一個服務啟動類型 (僅適用於服務啟動類型變更時)。</span><span class="sxs-lookup"><span data-stu-id="1efa5-961">Previous service startup type (only applicable if service startup type changed).</span></span> |
| <span data-ttu-id="1efa5-962">SvcAccount</span><span class="sxs-lookup"><span data-stu-id="1efa5-962">SvcAccount</span></span> |<span data-ttu-id="1efa5-963">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="1efa5-963">ConfigurationChange</span></span> |<span data-ttu-id="1efa5-964">服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="1efa5-964">Service account.</span></span> |
| <span data-ttu-id="1efa5-965">SvcPreviousAccount</span><span class="sxs-lookup"><span data-stu-id="1efa5-965">SvcPreviousAccount</span></span> |<span data-ttu-id="1efa5-966">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="1efa5-966">ConfigurationChange</span></span> |<span data-ttu-id="1efa5-967">先前的服務帳戶 (僅適用於服務帳戶變更時)。</span><span class="sxs-lookup"><span data-stu-id="1efa5-967">Previous service account (only applicable if service account changed).</span></span> |
| <span data-ttu-id="1efa5-968">SvcPath</span><span class="sxs-lookup"><span data-stu-id="1efa5-968">SvcPath</span></span> |<span data-ttu-id="1efa5-969">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="1efa5-969">ConfigurationChange</span></span> |<span data-ttu-id="1efa5-970">路徑 toohello 可執行檔的 hello Windows 服務。</span><span class="sxs-lookup"><span data-stu-id="1efa5-970">Path toohello executable of hello Windows service.</span></span> |
| <span data-ttu-id="1efa5-971">SvcPreviousPath</span><span class="sxs-lookup"><span data-stu-id="1efa5-971">SvcPreviousPath</span></span> |<span data-ttu-id="1efa5-972">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="1efa5-972">ConfigurationChange</span></span> |<span data-ttu-id="1efa5-973">上一個 hello hello （僅適用於其變更） 的 Windows 服務的可執行檔的路徑。</span><span class="sxs-lookup"><span data-stu-id="1efa5-973">Previous path of hello executable for hello Windows service (only applicable if it changed).</span></span> |
| <span data-ttu-id="1efa5-974">SvcDescription</span><span class="sxs-lookup"><span data-stu-id="1efa5-974">SvcDescription</span></span> |<span data-ttu-id="1efa5-975">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="1efa5-975">ConfigurationChange</span></span> |<span data-ttu-id="1efa5-976">Hello 服務的描述。</span><span class="sxs-lookup"><span data-stu-id="1efa5-976">Description of hello service.</span></span> |
| <span data-ttu-id="1efa5-977">上一步</span><span class="sxs-lookup"><span data-stu-id="1efa5-977">Previous</span></span> |<span data-ttu-id="1efa5-978">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="1efa5-978">ConfigurationChange</span></span> |<span data-ttu-id="1efa5-979">此軟體先前的狀態 (已安裝/未安裝/上一個版本)。</span><span class="sxs-lookup"><span data-stu-id="1efa5-979">Previous state of this software (Installed/Not Installed/previous version).</span></span> |
| <span data-ttu-id="1efa5-980">Current</span><span class="sxs-lookup"><span data-stu-id="1efa5-980">Current</span></span> |<span data-ttu-id="1efa5-981">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="1efa5-981">ConfigurationChange</span></span> |<span data-ttu-id="1efa5-982">此軟體最新的狀態 (已安裝/未安裝/上一個版本)。</span><span class="sxs-lookup"><span data-stu-id="1efa5-982">Latest state of this software (Installed/Not Installed/current version).</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1efa5-983">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1efa5-983">Next steps</span></span>
<span data-ttu-id="1efa5-984">如需記錄搜尋的其他資訊：</span><span class="sxs-lookup"><span data-stu-id="1efa5-984">For additional information about log searches:</span></span>

* <span data-ttu-id="1efa5-985">讓您熟悉[記錄搜尋](log-analytics-log-searches.md)tooview 詳細解決方案所收集的資訊。</span><span class="sxs-lookup"><span data-stu-id="1efa5-985">Get familiar with [log searches](log-analytics-log-searches.md) tooview detailed information gathered by solutions.</span></span>
* <span data-ttu-id="1efa5-986">使用[記錄分析中的自訂欄位](log-analytics-custom-fields.md)tooextend 記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="1efa5-986">Use [custom fields in Log Analytics](log-analytics-custom-fields.md) tooextend log searches.</span></span>
