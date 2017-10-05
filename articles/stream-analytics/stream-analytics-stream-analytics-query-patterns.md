---
title: "串流分析中一般使用模式的查詢範例 | Microsoft Docs"
description: "常見的 Azure 串流分析查詢模式"
keywords: "查詢範例"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jenniehubbard
editor: cgronlun
ms.assetid: 6b9a7d00-fbcc-42f6-9cbb-8bbf0bbd3d0e
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/08/2017
ms.author: jenniehubbard
ms.openlocfilehash: a00855c200b3fb365073bad4c5773b02c4c2c7fe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="query-examples-for-common-stream-analytics-usage-patterns"></a><span data-ttu-id="efc07-104">一般串流分析使用模式的查詢範例</span><span class="sxs-lookup"><span data-stu-id="efc07-104">Query examples for common Stream Analytics usage patterns</span></span>
## <a name="introduction"></a><span data-ttu-id="efc07-105">簡介</span><span class="sxs-lookup"><span data-stu-id="efc07-105">Introduction</span></span>
<span data-ttu-id="efc07-106">Azure 串流分析的查詢會以類似 SQL 的查詢語言表達。</span><span class="sxs-lookup"><span data-stu-id="efc07-106">Queries in Azure Stream Analytics are expressed in a SQL-like query language.</span></span> <span data-ttu-id="efc07-107">這些查詢記載在[串流分析查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)指南中。</span><span class="sxs-lookup"><span data-stu-id="efc07-107">These queries are documented in the [Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) guide.</span></span> <span data-ttu-id="efc07-108">本文章根據真實世界案例概述幾個常見查詢模式的解決方案。</span><span class="sxs-lookup"><span data-stu-id="efc07-108">This article outlines solutions to several common query patterns, based on real-world scenarios.</span></span> <span data-ttu-id="efc07-109">這是進行中的工作，會繼續不間斷使用新模式進行更新。</span><span class="sxs-lookup"><span data-stu-id="efc07-109">It is a work in progress and continues to be updated with new patterns on an ongoing basis.</span></span>

## <a name="query-example-convert-data-types"></a><span data-ttu-id="efc07-110">查詢範例：轉換資料類型</span><span class="sxs-lookup"><span data-stu-id="efc07-110">Query example: Convert data types</span></span>
<span data-ttu-id="efc07-111">**描述**：在輸入資料流上定義屬性類型。</span><span class="sxs-lookup"><span data-stu-id="efc07-111">**Description**: Define the types of properties on the input stream.</span></span>
<span data-ttu-id="efc07-112">例如，汽車重量即將以字串形式出現在輸入資料流，並且需要轉換為 **INT** 以執行 **SUM** 來將它加總。</span><span class="sxs-lookup"><span data-stu-id="efc07-112">For example, the car weight is coming on the input stream as strings and needs to be converted to **INT** to perform **SUM** it up.</span></span>

<span data-ttu-id="efc07-113">**輸入**：</span><span class="sxs-lookup"><span data-stu-id="efc07-113">**Input**:</span></span>

| <span data-ttu-id="efc07-114">Make</span><span class="sxs-lookup"><span data-stu-id="efc07-114">Make</span></span> | <span data-ttu-id="efc07-115">時間</span><span class="sxs-lookup"><span data-stu-id="efc07-115">Time</span></span> | <span data-ttu-id="efc07-116">Weight</span><span class="sxs-lookup"><span data-stu-id="efc07-116">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="efc07-117">Honda</span><span class="sxs-lookup"><span data-stu-id="efc07-117">Honda</span></span> |<span data-ttu-id="efc07-118">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-118">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="efc07-119">"1000"</span><span class="sxs-lookup"><span data-stu-id="efc07-119">"1000"</span></span> |
| <span data-ttu-id="efc07-120">Honda</span><span class="sxs-lookup"><span data-stu-id="efc07-120">Honda</span></span> |<span data-ttu-id="efc07-121">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-121">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="efc07-122">"2000"</span><span class="sxs-lookup"><span data-stu-id="efc07-122">"2000"</span></span> |

<span data-ttu-id="efc07-123">**輸出**：</span><span class="sxs-lookup"><span data-stu-id="efc07-123">**Output**:</span></span>

| <span data-ttu-id="efc07-124">Make</span><span class="sxs-lookup"><span data-stu-id="efc07-124">Make</span></span> | <span data-ttu-id="efc07-125">Weight</span><span class="sxs-lookup"><span data-stu-id="efc07-125">Weight</span></span> |
| --- | --- |
| <span data-ttu-id="efc07-126">Honda</span><span class="sxs-lookup"><span data-stu-id="efc07-126">Honda</span></span> |<span data-ttu-id="efc07-127">3000</span><span class="sxs-lookup"><span data-stu-id="efc07-127">3000</span></span> |

<span data-ttu-id="efc07-128">**解決方案**：</span><span class="sxs-lookup"><span data-stu-id="efc07-128">**Solution**:</span></span>

    SELECT
        Make,
        SUM(CAST(Weight AS BIGINT)) AS Weight
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

<span data-ttu-id="efc07-129">**說明**：在 [Weight]\(加權\) 欄位中使用 **CAST** 陳述式來指定其資料類型。</span><span class="sxs-lookup"><span data-stu-id="efc07-129">**Explanation**: Use a **CAST** statement in the **Weight** field to specify its data type.</span></span> <span data-ttu-id="efc07-130">請參閱[資料類型 (Azure 串流分析)](https://msdn.microsoft.com/library/azure/dn835065.aspx) 中的支援資料類型清單。</span><span class="sxs-lookup"><span data-stu-id="efc07-130">See the list of supported data types in [Data types (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span></span>

## <a name="query-example-use-likenot-like-to-do-pattern-matching"></a><span data-ttu-id="efc07-131">查詢範例：使用 Like/Not like 進行模式比對</span><span class="sxs-lookup"><span data-stu-id="efc07-131">Query example: Use Like/Not like to do pattern matching</span></span>
<span data-ttu-id="efc07-132">**描述**：檢查事件的欄位值是否符合特定模式。</span><span class="sxs-lookup"><span data-stu-id="efc07-132">**Description**: Check that a field value on the event matches a certain pattern.</span></span>
<span data-ttu-id="efc07-133">例如，檢查結果是否會傳回開頭為 A 且結尾為 9 的車牌。</span><span class="sxs-lookup"><span data-stu-id="efc07-133">For example, check that the result returns license plates that start with A and end with 9.</span></span>

<span data-ttu-id="efc07-134">**輸入**：</span><span class="sxs-lookup"><span data-stu-id="efc07-134">**Input**:</span></span>

| <span data-ttu-id="efc07-135">Make</span><span class="sxs-lookup"><span data-stu-id="efc07-135">Make</span></span> | <span data-ttu-id="efc07-136">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="efc07-136">LicensePlate</span></span> | <span data-ttu-id="efc07-137">時間</span><span class="sxs-lookup"><span data-stu-id="efc07-137">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="efc07-138">Honda</span><span class="sxs-lookup"><span data-stu-id="efc07-138">Honda</span></span> |<span data-ttu-id="efc07-139">ABC-123</span><span class="sxs-lookup"><span data-stu-id="efc07-139">ABC-123</span></span> |<span data-ttu-id="efc07-140">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-140">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="efc07-141">Toyota</span><span class="sxs-lookup"><span data-stu-id="efc07-141">Toyota</span></span> |<span data-ttu-id="efc07-142">AAA-999</span><span class="sxs-lookup"><span data-stu-id="efc07-142">AAA-999</span></span> |<span data-ttu-id="efc07-143">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-143">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="efc07-144">Nissan</span><span class="sxs-lookup"><span data-stu-id="efc07-144">Nissan</span></span> |<span data-ttu-id="efc07-145">ABC-369</span><span class="sxs-lookup"><span data-stu-id="efc07-145">ABC-369</span></span> |<span data-ttu-id="efc07-146">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-146">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="efc07-147">**輸出**：</span><span class="sxs-lookup"><span data-stu-id="efc07-147">**Output**:</span></span>

| <span data-ttu-id="efc07-148">Make</span><span class="sxs-lookup"><span data-stu-id="efc07-148">Make</span></span> | <span data-ttu-id="efc07-149">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="efc07-149">LicensePlate</span></span> | <span data-ttu-id="efc07-150">時間</span><span class="sxs-lookup"><span data-stu-id="efc07-150">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="efc07-151">Toyota</span><span class="sxs-lookup"><span data-stu-id="efc07-151">Toyota</span></span> |<span data-ttu-id="efc07-152">AAA-999</span><span class="sxs-lookup"><span data-stu-id="efc07-152">AAA-999</span></span> |<span data-ttu-id="efc07-153">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-153">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="efc07-154">Nissan</span><span class="sxs-lookup"><span data-stu-id="efc07-154">Nissan</span></span> |<span data-ttu-id="efc07-155">ABC-369</span><span class="sxs-lookup"><span data-stu-id="efc07-155">ABC-369</span></span> |<span data-ttu-id="efc07-156">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-156">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="efc07-157">**解決方案**：</span><span class="sxs-lookup"><span data-stu-id="efc07-157">**Solution**:</span></span>

    SELECT
        *
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LicensePlate LIKE 'A%9'

<span data-ttu-id="efc07-158">**說明**：使用 **LIKE** 陳述式檢查 [LicensePlate] 欄位值。</span><span class="sxs-lookup"><span data-stu-id="efc07-158">**Explanation**: Use the **LIKE** statement to check the **LicensePlate** field value.</span></span> <span data-ttu-id="efc07-159">開頭應該為 A，接著是長度為零或更多字元的字串，並以 9 結尾。</span><span class="sxs-lookup"><span data-stu-id="efc07-159">It should start with an A, then have any string of zero or more characters, and then end with a 9.</span></span> 

## <a name="query-example-specify-logic-for-different-casesvalues-case-statements"></a><span data-ttu-id="efc07-160">查詢範例：為不同的案例/值指定邏輯 (CASE 陳述式)</span><span class="sxs-lookup"><span data-stu-id="efc07-160">Query example: Specify logic for different cases/values (CASE statements)</span></span>
<span data-ttu-id="efc07-161">**描述**：根據特定準則，提供不同的欄位計算方式。</span><span class="sxs-lookup"><span data-stu-id="efc07-161">**Description**: Provide a different computation for a field, based on a particular criterion.</span></span>
<span data-ttu-id="efc07-162">例如，針對通過的相同廠牌汽車中有多少部符合 1 的特殊情況提供字串描述。</span><span class="sxs-lookup"><span data-stu-id="efc07-162">For example, provide a string description for how many cars of the same make passed, with a special case for 1.</span></span>

<span data-ttu-id="efc07-163">**輸入**：</span><span class="sxs-lookup"><span data-stu-id="efc07-163">**Input**:</span></span>

| <span data-ttu-id="efc07-164">Make</span><span class="sxs-lookup"><span data-stu-id="efc07-164">Make</span></span> | <span data-ttu-id="efc07-165">時間</span><span class="sxs-lookup"><span data-stu-id="efc07-165">Time</span></span> |
| --- | --- |
| <span data-ttu-id="efc07-166">Honda</span><span class="sxs-lookup"><span data-stu-id="efc07-166">Honda</span></span> |<span data-ttu-id="efc07-167">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-167">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="efc07-168">Toyota</span><span class="sxs-lookup"><span data-stu-id="efc07-168">Toyota</span></span> |<span data-ttu-id="efc07-169">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-169">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="efc07-170">Toyota</span><span class="sxs-lookup"><span data-stu-id="efc07-170">Toyota</span></span> |<span data-ttu-id="efc07-171">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-171">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="efc07-172">**輸出**：</span><span class="sxs-lookup"><span data-stu-id="efc07-172">**Output**:</span></span>

| <span data-ttu-id="efc07-173">CarsPassed</span><span class="sxs-lookup"><span data-stu-id="efc07-173">CarsPassed</span></span> | <span data-ttu-id="efc07-174">時間</span><span class="sxs-lookup"><span data-stu-id="efc07-174">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="efc07-175">1 Honda</span><span class="sxs-lookup"><span data-stu-id="efc07-175">1 Honda</span></span> |<span data-ttu-id="efc07-176">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-176">2015-01-01T00:00:10.0000000Z</span></span> |
| <span data-ttu-id="efc07-177">2 Toyotas</span><span class="sxs-lookup"><span data-stu-id="efc07-177">2 Toyotas</span></span> |<span data-ttu-id="efc07-178">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-178">2015-01-01T00:00:10.0000000Z</span></span> |

<span data-ttu-id="efc07-179">**解決方案**：</span><span class="sxs-lookup"><span data-stu-id="efc07-179">**Solution**:</span></span>

    SELECT
        CASE
            WHEN COUNT(*) = 1 THEN CONCAT('1 ', Make)
            ELSE CONCAT(CAST(COUNT(*) AS NVARCHAR(MAX)), ' ', Make, 's')
        END AS CarsPassed,
        System.TimeStamp AS Time
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

<span data-ttu-id="efc07-180">**說明**：**CASE** 子句可讓我們根據一些準則提供不同的運算 (在我們的案例中，汽車計數在彙總視窗中)。</span><span class="sxs-lookup"><span data-stu-id="efc07-180">**Explanation**: The **CASE** clause allows us to provide a different computation, based on some criteria (in our case, the count of the cars in the aggregate window).</span></span>

## <a name="query-example-send-data-to-multiple-outputs"></a><span data-ttu-id="efc07-181">查詢範例：將資料傳送至多個輸出</span><span class="sxs-lookup"><span data-stu-id="efc07-181">Query example: Send data to multiple outputs</span></span>
<span data-ttu-id="efc07-182">**描述**：將資料從單一工作傳送到多個輸出目標。</span><span class="sxs-lookup"><span data-stu-id="efc07-182">**Description**: Send data to multiple output targets from a single job.</span></span>
<span data-ttu-id="efc07-183">例如，分析臨界值警示的資料，並將所有事件封存到 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="efc07-183">For example, analyze data for a threshold-based alert and archive all events to blob storage.</span></span>

<span data-ttu-id="efc07-184">**輸入**：</span><span class="sxs-lookup"><span data-stu-id="efc07-184">**Input**:</span></span>

| <span data-ttu-id="efc07-185">Make</span><span class="sxs-lookup"><span data-stu-id="efc07-185">Make</span></span> | <span data-ttu-id="efc07-186">時間</span><span class="sxs-lookup"><span data-stu-id="efc07-186">Time</span></span> |
| --- | --- |
| <span data-ttu-id="efc07-187">Honda</span><span class="sxs-lookup"><span data-stu-id="efc07-187">Honda</span></span> |<span data-ttu-id="efc07-188">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-188">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="efc07-189">Honda</span><span class="sxs-lookup"><span data-stu-id="efc07-189">Honda</span></span> |<span data-ttu-id="efc07-190">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-190">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="efc07-191">Toyota</span><span class="sxs-lookup"><span data-stu-id="efc07-191">Toyota</span></span> |<span data-ttu-id="efc07-192">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-192">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="efc07-193">Toyota</span><span class="sxs-lookup"><span data-stu-id="efc07-193">Toyota</span></span> |<span data-ttu-id="efc07-194">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-194">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="efc07-195">Toyota</span><span class="sxs-lookup"><span data-stu-id="efc07-195">Toyota</span></span> |<span data-ttu-id="efc07-196">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-196">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="efc07-197">**Output1**：</span><span class="sxs-lookup"><span data-stu-id="efc07-197">**Output1**:</span></span>

| <span data-ttu-id="efc07-198">Make</span><span class="sxs-lookup"><span data-stu-id="efc07-198">Make</span></span> | <span data-ttu-id="efc07-199">時間</span><span class="sxs-lookup"><span data-stu-id="efc07-199">Time</span></span> |
| --- | --- |
| <span data-ttu-id="efc07-200">Honda</span><span class="sxs-lookup"><span data-stu-id="efc07-200">Honda</span></span> |<span data-ttu-id="efc07-201">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-201">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="efc07-202">Honda</span><span class="sxs-lookup"><span data-stu-id="efc07-202">Honda</span></span> |<span data-ttu-id="efc07-203">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-203">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="efc07-204">Toyota</span><span class="sxs-lookup"><span data-stu-id="efc07-204">Toyota</span></span> |<span data-ttu-id="efc07-205">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-205">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="efc07-206">Toyota</span><span class="sxs-lookup"><span data-stu-id="efc07-206">Toyota</span></span> |<span data-ttu-id="efc07-207">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-207">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="efc07-208">Toyota</span><span class="sxs-lookup"><span data-stu-id="efc07-208">Toyota</span></span> |<span data-ttu-id="efc07-209">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-209">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="efc07-210">**Output2**：</span><span class="sxs-lookup"><span data-stu-id="efc07-210">**Output2**:</span></span>

| <span data-ttu-id="efc07-211">Make</span><span class="sxs-lookup"><span data-stu-id="efc07-211">Make</span></span> | <span data-ttu-id="efc07-212">時間</span><span class="sxs-lookup"><span data-stu-id="efc07-212">Time</span></span> | <span data-ttu-id="efc07-213">Count</span><span class="sxs-lookup"><span data-stu-id="efc07-213">Count</span></span> |
| --- | --- | --- |
| <span data-ttu-id="efc07-214">Toyota</span><span class="sxs-lookup"><span data-stu-id="efc07-214">Toyota</span></span> |<span data-ttu-id="efc07-215">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-215">2015-01-01T00:00:10.0000000Z</span></span> |<span data-ttu-id="efc07-216">3</span><span class="sxs-lookup"><span data-stu-id="efc07-216">3</span></span> |

<span data-ttu-id="efc07-217">**解決方案**：</span><span class="sxs-lookup"><span data-stu-id="efc07-217">**Solution**:</span></span>

    SELECT
        *
    INTO
        ArchiveOutput
    FROM
        Input TIMESTAMP BY Time

    SELECT
        Make,
        System.TimeStamp AS Time,
        COUNT(*) AS [Count]
    INTO
        AlertOutput
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)
    HAVING
        [Count] >= 3

<span data-ttu-id="efc07-218">**說明**：**INTO** 子句會告訴串流分析要從此陳述式將資料寫入哪個輸出。</span><span class="sxs-lookup"><span data-stu-id="efc07-218">**Explanation**: The **INTO** clause tells Stream Analytics which of the outputs to write the data to from this statement.</span></span>
<span data-ttu-id="efc07-219">第一個查詢將我們接收到的資料傳遞至我們命名為 **ArchiveOutput** 的輸出。</span><span class="sxs-lookup"><span data-stu-id="efc07-219">The first query is a pass-through of the data we received to an output that we named **ArchiveOutput**.</span></span>
<span data-ttu-id="efc07-220">第二個查詢會執行一些簡單的彙總和篩選，並將結果傳送至下游的警示系統。</span><span class="sxs-lookup"><span data-stu-id="efc07-220">The second query does some simple aggregation and filtering, and it sends the results to a downstream alerting system.</span></span>

<span data-ttu-id="efc07-221">請注意，您也可以在多個輸出陳述式中重複使用通用資料表運算式 (CTE) 的結果 (例如 **WITH** 陳述式)。</span><span class="sxs-lookup"><span data-stu-id="efc07-221">Note that you can also reuse the results of the common table expressions (CTEs) (such as **WITH** statements) in multiple output statements.</span></span> <span data-ttu-id="efc07-222">此選項多了一項優點，就是對輸入來源開放的讀取器較少。</span><span class="sxs-lookup"><span data-stu-id="efc07-222">This option has the added benefit of opening fewer readers to the input source.</span></span>
<span data-ttu-id="efc07-223">例如：</span><span class="sxs-lookup"><span data-stu-id="efc07-223">For example:</span></span> 

    WITH AllRedCars AS (
        SELECT
            *
        FROM
            Input TIMESTAMP BY Time
        WHERE
            Color = 'red'
    )
    SELECT * INTO HondaOutput FROM AllRedCars WHERE Make = 'Honda'
    SELECT * INTO ToyotaOutput FROM AllRedCars WHERE Make = 'Toyota'

## <a name="query-example-count-unique-values"></a><span data-ttu-id="efc07-224">查詢範例：計算唯一值</span><span class="sxs-lookup"><span data-stu-id="efc07-224">Query example: Count unique values</span></span>
<span data-ttu-id="efc07-225">**描述**：計算某個時間範圍內在串流中所出現唯一欄位值的數目。</span><span class="sxs-lookup"><span data-stu-id="efc07-225">**Description**: Count the number of unique field values that appear in the stream within a time window.</span></span>
<span data-ttu-id="efc07-226">例如，在 2 秒鐘時間範圍內有多少部某一獨特廠牌的汽車通過收費亭？</span><span class="sxs-lookup"><span data-stu-id="efc07-226">For example, how many unique makes of cars passed through the toll booth in a 2-second window?</span></span>

<span data-ttu-id="efc07-227">**輸入**：</span><span class="sxs-lookup"><span data-stu-id="efc07-227">**Input**:</span></span>

| <span data-ttu-id="efc07-228">Make</span><span class="sxs-lookup"><span data-stu-id="efc07-228">Make</span></span> | <span data-ttu-id="efc07-229">時間</span><span class="sxs-lookup"><span data-stu-id="efc07-229">Time</span></span> |
| --- | --- |
| <span data-ttu-id="efc07-230">Honda</span><span class="sxs-lookup"><span data-stu-id="efc07-230">Honda</span></span> |<span data-ttu-id="efc07-231">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-231">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="efc07-232">Honda</span><span class="sxs-lookup"><span data-stu-id="efc07-232">Honda</span></span> |<span data-ttu-id="efc07-233">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-233">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="efc07-234">Toyota</span><span class="sxs-lookup"><span data-stu-id="efc07-234">Toyota</span></span> |<span data-ttu-id="efc07-235">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-235">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="efc07-236">Toyota</span><span class="sxs-lookup"><span data-stu-id="efc07-236">Toyota</span></span> |<span data-ttu-id="efc07-237">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-237">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="efc07-238">Toyota</span><span class="sxs-lookup"><span data-stu-id="efc07-238">Toyota</span></span> |<span data-ttu-id="efc07-239">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-239">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="efc07-240">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="efc07-240">**Output:**</span></span>

| <span data-ttu-id="efc07-241">Count</span><span class="sxs-lookup"><span data-stu-id="efc07-241">Count</span></span> | <span data-ttu-id="efc07-242">時間</span><span class="sxs-lookup"><span data-stu-id="efc07-242">Time</span></span> |
| --- | --- |
| <span data-ttu-id="efc07-243">2</span><span class="sxs-lookup"><span data-stu-id="efc07-243">2</span></span> |<span data-ttu-id="efc07-244">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-244">2015-01-01T00:00:02.000Z</span></span> |
| <span data-ttu-id="efc07-245">1</span><span class="sxs-lookup"><span data-stu-id="efc07-245">1</span></span> |<span data-ttu-id="efc07-246">2015-01-01T00:00:04.000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-246">2015-01-01T00:00:04.000Z</span></span> |

<span data-ttu-id="efc07-247">**解決方案：**</span><span class="sxs-lookup"><span data-stu-id="efc07-247">**Solution:**</span></span>

````
SELECT
     COUNT(DISTINCT Make) AS CountMake,
     System.TIMESTAMP AS TIME
FROM Input TIMESTAMP BY TIME
GROUP BY 
     TumblingWindow(second, 2)
````


<span data-ttu-id="efc07-248">**說明：**
**COUNT(DISTINCT Make)** 會傳回一個時間範圍內 **Make** 資料行的相異值數目。</span><span class="sxs-lookup"><span data-stu-id="efc07-248">**Explanation:**
**COUNT(DISTINCT Make)** returns the number of distinct values in the **Make** column within a time window.</span></span>

## <a name="query-example-determine-if-a-value-has-changed"></a><span data-ttu-id="efc07-249">查詢範例：判斷值是否已變更</span><span class="sxs-lookup"><span data-stu-id="efc07-249">Query example: Determine if a value has changed</span></span>
<span data-ttu-id="efc07-250">**描述**：查看前一個值來判斷該值是否與目前的值不同。</span><span class="sxs-lookup"><span data-stu-id="efc07-250">**Description**: Look at a previous value to determine if it is different than the current value.</span></span>
<span data-ttu-id="efc07-251">例如收費道路上前一輛汽車的品牌，是否與目前汽車的品牌相同？</span><span class="sxs-lookup"><span data-stu-id="efc07-251">For example, is the previous car on the toll road the same make as the current car?</span></span>

<span data-ttu-id="efc07-252">**輸入**：</span><span class="sxs-lookup"><span data-stu-id="efc07-252">**Input**:</span></span>

| <span data-ttu-id="efc07-253">Make</span><span class="sxs-lookup"><span data-stu-id="efc07-253">Make</span></span> | <span data-ttu-id="efc07-254">時間</span><span class="sxs-lookup"><span data-stu-id="efc07-254">Time</span></span> |
| --- | --- |
| <span data-ttu-id="efc07-255">Honda</span><span class="sxs-lookup"><span data-stu-id="efc07-255">Honda</span></span> |<span data-ttu-id="efc07-256">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-256">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="efc07-257">Toyota</span><span class="sxs-lookup"><span data-stu-id="efc07-257">Toyota</span></span> |<span data-ttu-id="efc07-258">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-258">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="efc07-259">**輸出**：</span><span class="sxs-lookup"><span data-stu-id="efc07-259">**Output**:</span></span>

| <span data-ttu-id="efc07-260">Make</span><span class="sxs-lookup"><span data-stu-id="efc07-260">Make</span></span> | <span data-ttu-id="efc07-261">時間</span><span class="sxs-lookup"><span data-stu-id="efc07-261">Time</span></span> |
| --- | --- |
| <span data-ttu-id="efc07-262">Toyota</span><span class="sxs-lookup"><span data-stu-id="efc07-262">Toyota</span></span> |<span data-ttu-id="efc07-263">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-263">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="efc07-264">**解決方案**：</span><span class="sxs-lookup"><span data-stu-id="efc07-264">**Solution**:</span></span>

    SELECT
        Make,
        Time
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(minute, 1)) <> Make

<span data-ttu-id="efc07-265">**說明**：使用 **LAG** 查看前一個事件的輸入資料流，並取得 **Make** 值。</span><span class="sxs-lookup"><span data-stu-id="efc07-265">**Explanation**: Use **LAG** to peek into the input stream one event back and get the **Make** value.</span></span> <span data-ttu-id="efc07-266">然後將其和目前事件中的 **Make** 值比較，並且在兩者不同時輸出事件。</span><span class="sxs-lookup"><span data-stu-id="efc07-266">Then compare it to the **Make** value on the current event and output the event if they are different.</span></span>

## <a name="query-example-find-the-first-event-in-a-window"></a><span data-ttu-id="efc07-267">查詢範例：尋找時間範圍內的第一個事件</span><span class="sxs-lookup"><span data-stu-id="efc07-267">Query example: Find the first event in a window</span></span>
<span data-ttu-id="efc07-268">**描述**：是否要每隔 10 分鐘尋找第一輛車。</span><span class="sxs-lookup"><span data-stu-id="efc07-268">**Description**: Find the first car in every 10-minute interval.</span></span>

<span data-ttu-id="efc07-269">**輸入**：</span><span class="sxs-lookup"><span data-stu-id="efc07-269">**Input**:</span></span>

| <span data-ttu-id="efc07-270">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="efc07-270">LicensePlate</span></span> | <span data-ttu-id="efc07-271">Make</span><span class="sxs-lookup"><span data-stu-id="efc07-271">Make</span></span> | <span data-ttu-id="efc07-272">時間</span><span class="sxs-lookup"><span data-stu-id="efc07-272">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="efc07-273">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="efc07-273">DXE 5291</span></span> |<span data-ttu-id="efc07-274">Honda</span><span class="sxs-lookup"><span data-stu-id="efc07-274">Honda</span></span> |<span data-ttu-id="efc07-275">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-275">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="efc07-276">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="efc07-276">YZK 5704</span></span> |<span data-ttu-id="efc07-277">Ford</span><span class="sxs-lookup"><span data-stu-id="efc07-277">Ford</span></span> |<span data-ttu-id="efc07-278">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-278">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="efc07-279">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="efc07-279">RMV 8282</span></span> |<span data-ttu-id="efc07-280">Honda</span><span class="sxs-lookup"><span data-stu-id="efc07-280">Honda</span></span> |<span data-ttu-id="efc07-281">2015-07-27T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-281">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="efc07-282">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="efc07-282">YHN 6970</span></span> |<span data-ttu-id="efc07-283">Toyota</span><span class="sxs-lookup"><span data-stu-id="efc07-283">Toyota</span></span> |<span data-ttu-id="efc07-284">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-284">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="efc07-285">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="efc07-285">VFE 1616</span></span> |<span data-ttu-id="efc07-286">Toyota</span><span class="sxs-lookup"><span data-stu-id="efc07-286">Toyota</span></span> |<span data-ttu-id="efc07-287">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-287">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="efc07-288">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="efc07-288">QYF 9358</span></span> |<span data-ttu-id="efc07-289">Honda</span><span class="sxs-lookup"><span data-stu-id="efc07-289">Honda</span></span> |<span data-ttu-id="efc07-290">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-290">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="efc07-291">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="efc07-291">MDR 6128</span></span> |<span data-ttu-id="efc07-292">BMW</span><span class="sxs-lookup"><span data-stu-id="efc07-292">BMW</span></span> |<span data-ttu-id="efc07-293">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-293">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="efc07-294">**輸出**：</span><span class="sxs-lookup"><span data-stu-id="efc07-294">**Output**:</span></span>

| <span data-ttu-id="efc07-295">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="efc07-295">LicensePlate</span></span> | <span data-ttu-id="efc07-296">Make</span><span class="sxs-lookup"><span data-stu-id="efc07-296">Make</span></span> | <span data-ttu-id="efc07-297">時間</span><span class="sxs-lookup"><span data-stu-id="efc07-297">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="efc07-298">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="efc07-298">DXE 5291</span></span> |<span data-ttu-id="efc07-299">Honda</span><span class="sxs-lookup"><span data-stu-id="efc07-299">Honda</span></span> |<span data-ttu-id="efc07-300">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-300">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="efc07-301">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="efc07-301">QYF 9358</span></span> |<span data-ttu-id="efc07-302">Honda</span><span class="sxs-lookup"><span data-stu-id="efc07-302">Honda</span></span> |<span data-ttu-id="efc07-303">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-303">2015-07-27T00:12:02.0000000Z</span></span> |

<span data-ttu-id="efc07-304">**解決方案**：</span><span class="sxs-lookup"><span data-stu-id="efc07-304">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) = 1

<span data-ttu-id="efc07-305">現在讓我們來變更問題，每隔 10 分鐘尋找特定廠牌的第一輛車。</span><span class="sxs-lookup"><span data-stu-id="efc07-305">Now let’s change the problem and find the first car of a particular make in every 10-minute interval.</span></span>

| <span data-ttu-id="efc07-306">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="efc07-306">LicensePlate</span></span> | <span data-ttu-id="efc07-307">Make</span><span class="sxs-lookup"><span data-stu-id="efc07-307">Make</span></span> | <span data-ttu-id="efc07-308">時間</span><span class="sxs-lookup"><span data-stu-id="efc07-308">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="efc07-309">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="efc07-309">DXE 5291</span></span> |<span data-ttu-id="efc07-310">Honda</span><span class="sxs-lookup"><span data-stu-id="efc07-310">Honda</span></span> |<span data-ttu-id="efc07-311">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-311">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="efc07-312">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="efc07-312">YZK 5704</span></span> |<span data-ttu-id="efc07-313">Ford</span><span class="sxs-lookup"><span data-stu-id="efc07-313">Ford</span></span> |<span data-ttu-id="efc07-314">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-314">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="efc07-315">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="efc07-315">YHN 6970</span></span> |<span data-ttu-id="efc07-316">Toyota</span><span class="sxs-lookup"><span data-stu-id="efc07-316">Toyota</span></span> |<span data-ttu-id="efc07-317">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-317">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="efc07-318">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="efc07-318">QYF 9358</span></span> |<span data-ttu-id="efc07-319">Honda</span><span class="sxs-lookup"><span data-stu-id="efc07-319">Honda</span></span> |<span data-ttu-id="efc07-320">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-320">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="efc07-321">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="efc07-321">MDR 6128</span></span> |<span data-ttu-id="efc07-322">BMW</span><span class="sxs-lookup"><span data-stu-id="efc07-322">BMW</span></span> |<span data-ttu-id="efc07-323">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-323">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="efc07-324">**解決方案**：</span><span class="sxs-lookup"><span data-stu-id="efc07-324">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) OVER (PARTITION BY Make) = 1

## <a name="query-example-find-the-last-event-in-a-window"></a><span data-ttu-id="efc07-325">查詢範例：尋找時間範圍內的上一個事件</span><span class="sxs-lookup"><span data-stu-id="efc07-325">Query example: Find the last event in a window</span></span>
<span data-ttu-id="efc07-326">**描述**：每隔 10 分鐘尋找上一輛車。</span><span class="sxs-lookup"><span data-stu-id="efc07-326">**Description**: Find the last car in every 10-minute interval.</span></span>

<span data-ttu-id="efc07-327">**輸入**：</span><span class="sxs-lookup"><span data-stu-id="efc07-327">**Input**:</span></span>

| <span data-ttu-id="efc07-328">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="efc07-328">LicensePlate</span></span> | <span data-ttu-id="efc07-329">Make</span><span class="sxs-lookup"><span data-stu-id="efc07-329">Make</span></span> | <span data-ttu-id="efc07-330">時間</span><span class="sxs-lookup"><span data-stu-id="efc07-330">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="efc07-331">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="efc07-331">DXE 5291</span></span> |<span data-ttu-id="efc07-332">Honda</span><span class="sxs-lookup"><span data-stu-id="efc07-332">Honda</span></span> |<span data-ttu-id="efc07-333">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-333">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="efc07-334">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="efc07-334">YZK 5704</span></span> |<span data-ttu-id="efc07-335">Ford</span><span class="sxs-lookup"><span data-stu-id="efc07-335">Ford</span></span> |<span data-ttu-id="efc07-336">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-336">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="efc07-337">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="efc07-337">RMV 8282</span></span> |<span data-ttu-id="efc07-338">Honda</span><span class="sxs-lookup"><span data-stu-id="efc07-338">Honda</span></span> |<span data-ttu-id="efc07-339">2015-07-27T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-339">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="efc07-340">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="efc07-340">YHN 6970</span></span> |<span data-ttu-id="efc07-341">Toyota</span><span class="sxs-lookup"><span data-stu-id="efc07-341">Toyota</span></span> |<span data-ttu-id="efc07-342">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-342">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="efc07-343">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="efc07-343">VFE 1616</span></span> |<span data-ttu-id="efc07-344">Toyota</span><span class="sxs-lookup"><span data-stu-id="efc07-344">Toyota</span></span> |<span data-ttu-id="efc07-345">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-345">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="efc07-346">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="efc07-346">QYF 9358</span></span> |<span data-ttu-id="efc07-347">Honda</span><span class="sxs-lookup"><span data-stu-id="efc07-347">Honda</span></span> |<span data-ttu-id="efc07-348">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-348">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="efc07-349">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="efc07-349">MDR 6128</span></span> |<span data-ttu-id="efc07-350">BMW</span><span class="sxs-lookup"><span data-stu-id="efc07-350">BMW</span></span> |<span data-ttu-id="efc07-351">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-351">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="efc07-352">**輸出**：</span><span class="sxs-lookup"><span data-stu-id="efc07-352">**Output**:</span></span>

| <span data-ttu-id="efc07-353">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="efc07-353">LicensePlate</span></span> | <span data-ttu-id="efc07-354">Make</span><span class="sxs-lookup"><span data-stu-id="efc07-354">Make</span></span> | <span data-ttu-id="efc07-355">時間</span><span class="sxs-lookup"><span data-stu-id="efc07-355">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="efc07-356">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="efc07-356">VFE 1616</span></span> |<span data-ttu-id="efc07-357">Toyota</span><span class="sxs-lookup"><span data-stu-id="efc07-357">Toyota</span></span> |<span data-ttu-id="efc07-358">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-358">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="efc07-359">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="efc07-359">MDR 6128</span></span> |<span data-ttu-id="efc07-360">BMW</span><span class="sxs-lookup"><span data-stu-id="efc07-360">BMW</span></span> |<span data-ttu-id="efc07-361">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-361">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="efc07-362">**解決方案**：</span><span class="sxs-lookup"><span data-stu-id="efc07-362">**Solution**:</span></span>

    WITH LastInWindow AS
    (
        SELECT 
            MAX(Time) AS LastEventTime
        FROM 
            Input TIMESTAMP BY Time
        GROUP BY 
            TumblingWindow(minute, 10)
    )
    SELECT 
        Input.LicensePlate,
        Input.Make,
        Input.Time
    FROM
        Input TIMESTAMP BY Time 
        INNER JOIN LastInWindow
        ON DATEDIFF(minute, Input, LastInWindow) BETWEEN 0 AND 10
        AND Input.Time = LastInWindow.LastEventTime

<span data-ttu-id="efc07-363">**說明**：查詢中有兩個步驟。</span><span class="sxs-lookup"><span data-stu-id="efc07-363">**Explanation**: There are two steps in the query.</span></span> <span data-ttu-id="efc07-364">第一個步驟會尋找 10 分鐘時間範圍內最新的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="efc07-364">The first one finds the latest time stamp in 10-minute windows.</span></span> <span data-ttu-id="efc07-365">第二個步驟會將第一個查詢的結果與原始串流聯結在一起，在每個時間範圍內尋找符合最後一個時間戳記的事件。</span><span class="sxs-lookup"><span data-stu-id="efc07-365">The second step joins the results of the first query with the original stream to find the events that match the last time stamps in each window.</span></span> 

## <a name="query-example-detect-the-absence-of-events"></a><span data-ttu-id="efc07-366">查詢範例：偵測到事件不存在</span><span class="sxs-lookup"><span data-stu-id="efc07-366">Query example: Detect the absence of events</span></span>
<span data-ttu-id="efc07-367">**描述**：檢查串流中是否沒有和特定準則相符的值。</span><span class="sxs-lookup"><span data-stu-id="efc07-367">**Description**: Check that a stream has no value that matches a certain criterion.</span></span>
<span data-ttu-id="efc07-368">例如，在最後的 90 秒內連續有 2 部相同廠牌的車輛進入收費道路？</span><span class="sxs-lookup"><span data-stu-id="efc07-368">For example, have 2 consecutive cars from the same make entered the toll road within the last 90 seconds?</span></span>

<span data-ttu-id="efc07-369">**輸入**：</span><span class="sxs-lookup"><span data-stu-id="efc07-369">**Input**:</span></span>

| <span data-ttu-id="efc07-370">Make</span><span class="sxs-lookup"><span data-stu-id="efc07-370">Make</span></span> | <span data-ttu-id="efc07-371">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="efc07-371">LicensePlate</span></span> | <span data-ttu-id="efc07-372">時間</span><span class="sxs-lookup"><span data-stu-id="efc07-372">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="efc07-373">Honda</span><span class="sxs-lookup"><span data-stu-id="efc07-373">Honda</span></span> |<span data-ttu-id="efc07-374">ABC-123</span><span class="sxs-lookup"><span data-stu-id="efc07-374">ABC-123</span></span> |<span data-ttu-id="efc07-375">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-375">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="efc07-376">Honda</span><span class="sxs-lookup"><span data-stu-id="efc07-376">Honda</span></span> |<span data-ttu-id="efc07-377">AAA-999</span><span class="sxs-lookup"><span data-stu-id="efc07-377">AAA-999</span></span> |<span data-ttu-id="efc07-378">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-378">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="efc07-379">Toyota</span><span class="sxs-lookup"><span data-stu-id="efc07-379">Toyota</span></span> |<span data-ttu-id="efc07-380">DEF-987</span><span class="sxs-lookup"><span data-stu-id="efc07-380">DEF-987</span></span> |<span data-ttu-id="efc07-381">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-381">2015-01-01T00:00:03.0000000Z</span></span> |
| <span data-ttu-id="efc07-382">Honda</span><span class="sxs-lookup"><span data-stu-id="efc07-382">Honda</span></span> |<span data-ttu-id="efc07-383">GHI-345</span><span class="sxs-lookup"><span data-stu-id="efc07-383">GHI-345</span></span> |<span data-ttu-id="efc07-384">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-384">2015-01-01T00:00:04.0000000Z</span></span> |

<span data-ttu-id="efc07-385">**輸出**：</span><span class="sxs-lookup"><span data-stu-id="efc07-385">**Output**:</span></span>

| <span data-ttu-id="efc07-386">Make</span><span class="sxs-lookup"><span data-stu-id="efc07-386">Make</span></span> | <span data-ttu-id="efc07-387">時間</span><span class="sxs-lookup"><span data-stu-id="efc07-387">Time</span></span> | <span data-ttu-id="efc07-388">CurrentCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="efc07-388">CurrentCarLicensePlate</span></span> | <span data-ttu-id="efc07-389">FirstCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="efc07-389">FirstCarLicensePlate</span></span> | <span data-ttu-id="efc07-390">FirstCarTime</span><span class="sxs-lookup"><span data-stu-id="efc07-390">FirstCarTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="efc07-391">Honda</span><span class="sxs-lookup"><span data-stu-id="efc07-391">Honda</span></span> |<span data-ttu-id="efc07-392">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-392">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="efc07-393">AAA-999</span><span class="sxs-lookup"><span data-stu-id="efc07-393">AAA-999</span></span> |<span data-ttu-id="efc07-394">ABC-123</span><span class="sxs-lookup"><span data-stu-id="efc07-394">ABC-123</span></span> |<span data-ttu-id="efc07-395">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-395">2015-01-01T00:00:01.0000000Z</span></span> |

<span data-ttu-id="efc07-396">**解決方案**：</span><span class="sxs-lookup"><span data-stu-id="efc07-396">**Solution**:</span></span>

    SELECT
        Make,
        Time,
        LicensePlate AS CurrentCarLicensePlate,
        LAG(LicensePlate, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarLicensePlate,
        LAG(Time, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarTime
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(second, 90)) = Make

<span data-ttu-id="efc07-397">**說明**：使用 **LAG** 查看前一個事件的輸入資料流，並取得 **Make** 值。</span><span class="sxs-lookup"><span data-stu-id="efc07-397">**Explanation**: Use **LAG** to peek into the input stream one event back and get the **Make** value.</span></span> <span data-ttu-id="efc07-398">將該值和目前事件中的 **MAKE** 值比較，如果相同則輸出該事件。</span><span class="sxs-lookup"><span data-stu-id="efc07-398">Compare it to the **MAKE** value in the current event, and then output the event if they are the same.</span></span> <span data-ttu-id="efc07-399">您也可以使用 **LAG** 取得上一輛車的相關資料。</span><span class="sxs-lookup"><span data-stu-id="efc07-399">You can also use **LAG** to get data about the previous car.</span></span>

## <a name="query-example-detect-the-duration-between-events"></a><span data-ttu-id="efc07-400">查詢範例：偵測事件與事件之間的持續時間</span><span class="sxs-lookup"><span data-stu-id="efc07-400">Query example: Detect the duration between events</span></span>
<span data-ttu-id="efc07-401">**描述**：尋找指定事件的持續時間。</span><span class="sxs-lookup"><span data-stu-id="efc07-401">**Description**: Find the duration of a given event.</span></span> <span data-ttu-id="efc07-402">例如，指定某一網頁點選流，以判斷在某一功能上花費的時間。</span><span class="sxs-lookup"><span data-stu-id="efc07-402">For example, given a web clickstream, determine the time spent on a feature.</span></span>

<span data-ttu-id="efc07-403">**輸入**：</span><span class="sxs-lookup"><span data-stu-id="efc07-403">**Input**:</span></span>  

| <span data-ttu-id="efc07-404">User</span><span class="sxs-lookup"><span data-stu-id="efc07-404">User</span></span> | <span data-ttu-id="efc07-405">功能</span><span class="sxs-lookup"><span data-stu-id="efc07-405">Feature</span></span> | <span data-ttu-id="efc07-406">Event</span><span class="sxs-lookup"><span data-stu-id="efc07-406">Event</span></span> | <span data-ttu-id="efc07-407">時間</span><span class="sxs-lookup"><span data-stu-id="efc07-407">Time</span></span> |
| --- | --- | --- | --- |
| user@location.com |<span data-ttu-id="efc07-408">RightMenu</span><span class="sxs-lookup"><span data-stu-id="efc07-408">RightMenu</span></span> |<span data-ttu-id="efc07-409">Start</span><span class="sxs-lookup"><span data-stu-id="efc07-409">Start</span></span> |<span data-ttu-id="efc07-410">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-410">2015-01-01T00:00:01.0000000Z</span></span> |
| user@location.com |<span data-ttu-id="efc07-411">RightMenu</span><span class="sxs-lookup"><span data-stu-id="efc07-411">RightMenu</span></span> |<span data-ttu-id="efc07-412">End</span><span class="sxs-lookup"><span data-stu-id="efc07-412">End</span></span> |<span data-ttu-id="efc07-413">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-413">2015-01-01T00:00:08.0000000Z</span></span> |

<span data-ttu-id="efc07-414">**輸出**：</span><span class="sxs-lookup"><span data-stu-id="efc07-414">**Output**:</span></span>  

| <span data-ttu-id="efc07-415">User</span><span class="sxs-lookup"><span data-stu-id="efc07-415">User</span></span> | <span data-ttu-id="efc07-416">功能</span><span class="sxs-lookup"><span data-stu-id="efc07-416">Feature</span></span> | <span data-ttu-id="efc07-417">Duration</span><span class="sxs-lookup"><span data-stu-id="efc07-417">Duration</span></span> |
| --- | --- | --- |
| user@location.com |<span data-ttu-id="efc07-418">RightMenu</span><span class="sxs-lookup"><span data-stu-id="efc07-418">RightMenu</span></span> |<span data-ttu-id="efc07-419">7</span><span class="sxs-lookup"><span data-stu-id="efc07-419">7</span></span> |

<span data-ttu-id="efc07-420">**解決方案**：</span><span class="sxs-lookup"><span data-stu-id="efc07-420">**Solution**:</span></span>

````
    SELECT
        [user], feature, DATEDIFF(second, LAST(Time) OVER (PARTITION BY [user], feature LIMIT DURATION(hour, 1) WHEN Event = 'start'), Time) as duration
    FROM input TIMESTAMP BY Time
    WHERE
        Event = 'end'
````

<span data-ttu-id="efc07-421">**說明**：當事件類型為 **Start** 時，使用 **LAST** 函式取出最後一個 **TIME** 值。</span><span class="sxs-lookup"><span data-stu-id="efc07-421">**Explanation**: Use the **LAST** function to retrieve the last **TIME** value when the event type was **Start**.</span></span> <span data-ttu-id="efc07-422">**LAST** 函式使用 **PARTITION BY [user]** 來表達會為個別使用者分別計算結果。</span><span class="sxs-lookup"><span data-stu-id="efc07-422">The **LAST** function uses **PARTITION BY [user]** to indicate that the result is computed per unique user.</span></span> <span data-ttu-id="efc07-423">查詢的 **Start** 與 **Stop** 事件之間時間差的上限為 1 小時，但該值可以在必要時變更 **(LIMIT DURATION(hour, 1)**。</span><span class="sxs-lookup"><span data-stu-id="efc07-423">The query has a 1-hour maximum threshold for the time difference between **Start** and **Stop** events, but is configurable as needed **(LIMIT DURATION(hour, 1)**.</span></span>

## <a name="query-example-detect-the-duration-of-a-condition"></a><span data-ttu-id="efc07-424">查詢範例：偵測某個情況的持續時間</span><span class="sxs-lookup"><span data-stu-id="efc07-424">Query example: Detect the duration of a condition</span></span>
<span data-ttu-id="efc07-425">**描述**：找出某個情況的持續時間。</span><span class="sxs-lookup"><span data-stu-id="efc07-425">**Description**: Find out how long a condition occurred.</span></span>
<span data-ttu-id="efc07-426">例如，假設有個錯誤導致所有車輛的重量不正確 (超過 20,000 磅)，</span><span class="sxs-lookup"><span data-stu-id="efc07-426">For example, suppose that a bug resulted in all cars having an incorrect weight (above 20,000 pounds).</span></span> <span data-ttu-id="efc07-427">而我們想要計算該錯誤的持續時間。</span><span class="sxs-lookup"><span data-stu-id="efc07-427">We want to compute the duration of the bug.</span></span>

<span data-ttu-id="efc07-428">**輸入**：</span><span class="sxs-lookup"><span data-stu-id="efc07-428">**Input**:</span></span>

| <span data-ttu-id="efc07-429">Make</span><span class="sxs-lookup"><span data-stu-id="efc07-429">Make</span></span> | <span data-ttu-id="efc07-430">時間</span><span class="sxs-lookup"><span data-stu-id="efc07-430">Time</span></span> | <span data-ttu-id="efc07-431">Weight</span><span class="sxs-lookup"><span data-stu-id="efc07-431">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="efc07-432">Honda</span><span class="sxs-lookup"><span data-stu-id="efc07-432">Honda</span></span> |<span data-ttu-id="efc07-433">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-433">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="efc07-434">2000</span><span class="sxs-lookup"><span data-stu-id="efc07-434">2000</span></span> |
| <span data-ttu-id="efc07-435">Toyota</span><span class="sxs-lookup"><span data-stu-id="efc07-435">Toyota</span></span> |<span data-ttu-id="efc07-436">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-436">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="efc07-437">25000</span><span class="sxs-lookup"><span data-stu-id="efc07-437">25000</span></span> |
| <span data-ttu-id="efc07-438">Honda</span><span class="sxs-lookup"><span data-stu-id="efc07-438">Honda</span></span> |<span data-ttu-id="efc07-439">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-439">2015-01-01T00:00:03.0000000Z</span></span> |<span data-ttu-id="efc07-440">26000</span><span class="sxs-lookup"><span data-stu-id="efc07-440">26000</span></span> |
| <span data-ttu-id="efc07-441">Toyota</span><span class="sxs-lookup"><span data-stu-id="efc07-441">Toyota</span></span> |<span data-ttu-id="efc07-442">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-442">2015-01-01T00:00:04.0000000Z</span></span> |<span data-ttu-id="efc07-443">25000</span><span class="sxs-lookup"><span data-stu-id="efc07-443">25000</span></span> |
| <span data-ttu-id="efc07-444">Honda</span><span class="sxs-lookup"><span data-stu-id="efc07-444">Honda</span></span> |<span data-ttu-id="efc07-445">2015-01-01T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-445">2015-01-01T00:00:05.0000000Z</span></span> |<span data-ttu-id="efc07-446">26000</span><span class="sxs-lookup"><span data-stu-id="efc07-446">26000</span></span> |
| <span data-ttu-id="efc07-447">Toyota</span><span class="sxs-lookup"><span data-stu-id="efc07-447">Toyota</span></span> |<span data-ttu-id="efc07-448">2015-01-01T00:00:06.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-448">2015-01-01T00:00:06.0000000Z</span></span> |<span data-ttu-id="efc07-449">25000</span><span class="sxs-lookup"><span data-stu-id="efc07-449">25000</span></span> |
| <span data-ttu-id="efc07-450">Honda</span><span class="sxs-lookup"><span data-stu-id="efc07-450">Honda</span></span> |<span data-ttu-id="efc07-451">2015-01-01T00:00:07.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-451">2015-01-01T00:00:07.0000000Z</span></span> |<span data-ttu-id="efc07-452">26000</span><span class="sxs-lookup"><span data-stu-id="efc07-452">26000</span></span> |
| <span data-ttu-id="efc07-453">Toyota</span><span class="sxs-lookup"><span data-stu-id="efc07-453">Toyota</span></span> |<span data-ttu-id="efc07-454">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-454">2015-01-01T00:00:08.0000000Z</span></span> |<span data-ttu-id="efc07-455">2000</span><span class="sxs-lookup"><span data-stu-id="efc07-455">2000</span></span> |

<span data-ttu-id="efc07-456">**輸出**：</span><span class="sxs-lookup"><span data-stu-id="efc07-456">**Output**:</span></span>

| <span data-ttu-id="efc07-457">StartFault</span><span class="sxs-lookup"><span data-stu-id="efc07-457">StartFault</span></span> | <span data-ttu-id="efc07-458">EndFault</span><span class="sxs-lookup"><span data-stu-id="efc07-458">EndFault</span></span> |
| --- | --- |
| <span data-ttu-id="efc07-459">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-459">2015-01-01T00:00:02.000Z</span></span> |<span data-ttu-id="efc07-460">2015-01-01T00:00:07.000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-460">2015-01-01T00:00:07.000Z</span></span> |

<span data-ttu-id="efc07-461">**解決方案**：</span><span class="sxs-lookup"><span data-stu-id="efc07-461">**Solution**:</span></span>

````
    WITH SelectPreviousEvent AS
    (
    SELECT
    *,
        LAG([time]) OVER (LIMIT DURATION(hour, 24)) as previousTime,
        LAG([weight]) OVER (LIMIT DURATION(hour, 24)) as previousWeight
    FROM input TIMESTAMP BY [time]
    )

    SELECT 
        LAG(time) OVER (LIMIT DURATION(hour, 24) WHEN previousWeight < 20000 ) [StartFault],
        previousTime [EndFault]
    FROM SelectPreviousEvent
    WHERE
        [weight] < 20000
        AND previousWeight > 20000
````

<span data-ttu-id="efc07-462">**說明**：使用 **LAG** 來檢視 24 小時內的輸入資料流，並尋找其中的 **StartFault** 和 **StopFault** 被 weight < 20000 合併的執行個體。</span><span class="sxs-lookup"><span data-stu-id="efc07-462">**Explanation**: Use **LAG** to view the input stream for 24 hours and look for instances where **StartFault** and **StopFault** are spanned by the weight < 20000.</span></span>

## <a name="query-example-fill-missing-values"></a><span data-ttu-id="efc07-463">查詢範例：填入遺漏值</span><span class="sxs-lookup"><span data-stu-id="efc07-463">Query example: Fill missing values</span></span>
<span data-ttu-id="efc07-464">**描述**：對於有遺漏值的事件串流，以固定間隔產生事件串流。</span><span class="sxs-lookup"><span data-stu-id="efc07-464">**Description**: For the stream of events that have missing values, produce a stream of events with regular intervals.</span></span>
<span data-ttu-id="efc07-465">例如，每隔 5 秒產生事件，報告最近所見的資料點。</span><span class="sxs-lookup"><span data-stu-id="efc07-465">For example, generate an event every 5 seconds that reports the most recently seen data point.</span></span>

<span data-ttu-id="efc07-466">**輸入**：</span><span class="sxs-lookup"><span data-stu-id="efc07-466">**Input**:</span></span>

| <span data-ttu-id="efc07-467">t</span><span class="sxs-lookup"><span data-stu-id="efc07-467">t</span></span> | <span data-ttu-id="efc07-468">value</span><span class="sxs-lookup"><span data-stu-id="efc07-468">value</span></span> |
| --- | --- |
| <span data-ttu-id="efc07-469">"2014-01-01T06:01:00"</span><span class="sxs-lookup"><span data-stu-id="efc07-469">"2014-01-01T06:01:00"</span></span> |<span data-ttu-id="efc07-470">1</span><span class="sxs-lookup"><span data-stu-id="efc07-470">1</span></span> |
| <span data-ttu-id="efc07-471">"2014-01-01T06:01:05"</span><span class="sxs-lookup"><span data-stu-id="efc07-471">"2014-01-01T06:01:05"</span></span> |<span data-ttu-id="efc07-472">2</span><span class="sxs-lookup"><span data-stu-id="efc07-472">2</span></span> |
| <span data-ttu-id="efc07-473">"2014-01-01T06:01:10"</span><span class="sxs-lookup"><span data-stu-id="efc07-473">"2014-01-01T06:01:10"</span></span> |<span data-ttu-id="efc07-474">3</span><span class="sxs-lookup"><span data-stu-id="efc07-474">3</span></span> |
| <span data-ttu-id="efc07-475">"2014-01-01T06:01:15"</span><span class="sxs-lookup"><span data-stu-id="efc07-475">"2014-01-01T06:01:15"</span></span> |<span data-ttu-id="efc07-476">4</span><span class="sxs-lookup"><span data-stu-id="efc07-476">4</span></span> |
| <span data-ttu-id="efc07-477">"2014-01-01T06:01:30"</span><span class="sxs-lookup"><span data-stu-id="efc07-477">"2014-01-01T06:01:30"</span></span> |<span data-ttu-id="efc07-478">5</span><span class="sxs-lookup"><span data-stu-id="efc07-478">5</span></span> |
| <span data-ttu-id="efc07-479">"2014-01-01T06:01:35"</span><span class="sxs-lookup"><span data-stu-id="efc07-479">"2014-01-01T06:01:35"</span></span> |<span data-ttu-id="efc07-480">6</span><span class="sxs-lookup"><span data-stu-id="efc07-480">6</span></span> |

<span data-ttu-id="efc07-481">**輸出 (前 10 個資料列)**：</span><span class="sxs-lookup"><span data-stu-id="efc07-481">**Output (first 10 rows)**:</span></span>

| <span data-ttu-id="efc07-482">windowend</span><span class="sxs-lookup"><span data-stu-id="efc07-482">windowend</span></span> | <span data-ttu-id="efc07-483">lastevent.t</span><span class="sxs-lookup"><span data-stu-id="efc07-483">lastevent.t</span></span> | <span data-ttu-id="efc07-484">lastevent.value</span><span class="sxs-lookup"><span data-stu-id="efc07-484">lastevent.value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="efc07-485">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-485">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="efc07-486">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-486">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="efc07-487">1</span><span class="sxs-lookup"><span data-stu-id="efc07-487">1</span></span> |
| <span data-ttu-id="efc07-488">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-488">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="efc07-489">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-489">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="efc07-490">2</span><span class="sxs-lookup"><span data-stu-id="efc07-490">2</span></span> |
| <span data-ttu-id="efc07-491">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-491">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="efc07-492">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-492">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="efc07-493">3</span><span class="sxs-lookup"><span data-stu-id="efc07-493">3</span></span> |
| <span data-ttu-id="efc07-494">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-494">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="efc07-495">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-495">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="efc07-496">4</span><span class="sxs-lookup"><span data-stu-id="efc07-496">4</span></span> |
| <span data-ttu-id="efc07-497">2014-01-01T14:01:20.000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-497">2014-01-01T14:01:20.000Z</span></span> |<span data-ttu-id="efc07-498">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-498">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="efc07-499">4</span><span class="sxs-lookup"><span data-stu-id="efc07-499">4</span></span> |
| <span data-ttu-id="efc07-500">2014-01-01T14:01:25.000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-500">2014-01-01T14:01:25.000Z</span></span> |<span data-ttu-id="efc07-501">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-501">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="efc07-502">4</span><span class="sxs-lookup"><span data-stu-id="efc07-502">4</span></span> |
| <span data-ttu-id="efc07-503">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-503">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="efc07-504">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-504">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="efc07-505">5</span><span class="sxs-lookup"><span data-stu-id="efc07-505">5</span></span> |
| <span data-ttu-id="efc07-506">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-506">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="efc07-507">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-507">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="efc07-508">6</span><span class="sxs-lookup"><span data-stu-id="efc07-508">6</span></span> |
| <span data-ttu-id="efc07-509">2014-01-01T14:01:40.000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-509">2014-01-01T14:01:40.000Z</span></span> |<span data-ttu-id="efc07-510">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-510">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="efc07-511">6</span><span class="sxs-lookup"><span data-stu-id="efc07-511">6</span></span> |
| <span data-ttu-id="efc07-512">2014-01-01T14:01:45.000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-512">2014-01-01T14:01:45.000Z</span></span> |<span data-ttu-id="efc07-513">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="efc07-513">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="efc07-514">6</span><span class="sxs-lookup"><span data-stu-id="efc07-514">6</span></span> |

<span data-ttu-id="efc07-515">**解決方案**：</span><span class="sxs-lookup"><span data-stu-id="efc07-515">**Solution**:</span></span>

    SELECT
        System.Timestamp AS windowEnd,
        TopOne() OVER (ORDER BY t DESC) AS lastEvent
    FROM
        input TIMESTAMP BY t
    GROUP BY HOPPINGWINDOW(second, 300, 5)


<span data-ttu-id="efc07-516">**說明**：此查詢會每隔 5 秒產生事件，並且會輸出之前收到的最後一個事件。</span><span class="sxs-lookup"><span data-stu-id="efc07-516">**Explanation**: This query generates events every 5 seconds and outputs the last event that was received previously.</span></span> <span data-ttu-id="efc07-517">[跳動視窗](https://msdn.microsoft.com/library/dn835041.aspx "跳動視窗 - Azure 串流分析")持續時間會決定查詢回溯到多久之前以找出最新的事件 (在此範例中為 300 秒)。</span><span class="sxs-lookup"><span data-stu-id="efc07-517">The [Hopping window](https://msdn.microsoft.com/library/dn835041.aspx "Hopping window--Azure Stream Analytics") duration determines how far back the query looks to find the latest event (300 seconds in this example).</span></span>

## <a name="get-help"></a><span data-ttu-id="efc07-518">取得說明</span><span class="sxs-lookup"><span data-stu-id="efc07-518">Get help</span></span>
<span data-ttu-id="efc07-519">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。</span><span class="sxs-lookup"><span data-stu-id="efc07-519">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="efc07-520">後續步驟</span><span class="sxs-lookup"><span data-stu-id="efc07-520">Next steps</span></span>
* [<span data-ttu-id="efc07-521">Azure Stream Analytics 介紹</span><span class="sxs-lookup"><span data-stu-id="efc07-521">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="efc07-522">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="efc07-522">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="efc07-523">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="efc07-523">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="efc07-524">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="efc07-524">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="efc07-525">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="efc07-525">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

