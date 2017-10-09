---
title: "在 Stream Analytics 中常見的使用模式的 aaaQuery 範例 |Microsoft 文件"
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
ms.openlocfilehash: c8f7a8ac661eaf0281f4140b02c42141b73040fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="query-examples-for-common-stream-analytics-usage-patterns"></a><span data-ttu-id="693fb-104">一般串流分析使用模式的查詢範例</span><span class="sxs-lookup"><span data-stu-id="693fb-104">Query examples for common Stream Analytics usage patterns</span></span>
## <a name="introduction"></a><span data-ttu-id="693fb-105">簡介</span><span class="sxs-lookup"><span data-stu-id="693fb-105">Introduction</span></span>
<span data-ttu-id="693fb-106">Azure 串流分析的查詢會以類似 SQL 的查詢語言表達。</span><span class="sxs-lookup"><span data-stu-id="693fb-106">Queries in Azure Stream Analytics are expressed in a SQL-like query language.</span></span> <span data-ttu-id="693fb-107">這些查詢會記載於 hello [Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)指南。</span><span class="sxs-lookup"><span data-stu-id="693fb-107">These queries are documented in hello [Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) guide.</span></span> <span data-ttu-id="693fb-108">此文件大綱解決方案 tooseveral 常見的查詢模式，根據的真實世界案例。</span><span class="sxs-lookup"><span data-stu-id="693fb-108">This article outlines solutions tooseveral common query patterns, based on real-world scenarios.</span></span> <span data-ttu-id="693fb-109">進行中工作，並繼續 toobe 以新的模式，持續地更新。</span><span class="sxs-lookup"><span data-stu-id="693fb-109">It is a work in progress and continues toobe updated with new patterns on an ongoing basis.</span></span>

## <a name="query-example-convert-data-types"></a><span data-ttu-id="693fb-110">查詢範例：轉換資料類型</span><span class="sxs-lookup"><span data-stu-id="693fb-110">Query example: Convert data types</span></span>
<span data-ttu-id="693fb-111">**描述**: hello 輸入資料流定義 hello 類型的屬性。</span><span class="sxs-lookup"><span data-stu-id="693fb-111">**Description**: Define hello types of properties on hello input stream.</span></span>
<span data-ttu-id="693fb-112">比方說，hello 汽車權數是 hello 輸入資料流為字串，並且需要 toobe 太轉換**INT** tooperform**總和**它。</span><span class="sxs-lookup"><span data-stu-id="693fb-112">For example, hello car weight is coming on hello input stream as strings and needs toobe converted too**INT** tooperform **SUM** it up.</span></span>

<span data-ttu-id="693fb-113">**輸入**：</span><span class="sxs-lookup"><span data-stu-id="693fb-113">**Input**:</span></span>

| <span data-ttu-id="693fb-114">Make</span><span class="sxs-lookup"><span data-stu-id="693fb-114">Make</span></span> | <span data-ttu-id="693fb-115">時間</span><span class="sxs-lookup"><span data-stu-id="693fb-115">Time</span></span> | <span data-ttu-id="693fb-116">Weight</span><span class="sxs-lookup"><span data-stu-id="693fb-116">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="693fb-117">Honda</span><span class="sxs-lookup"><span data-stu-id="693fb-117">Honda</span></span> |<span data-ttu-id="693fb-118">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-118">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="693fb-119">"1000"</span><span class="sxs-lookup"><span data-stu-id="693fb-119">"1000"</span></span> |
| <span data-ttu-id="693fb-120">Honda</span><span class="sxs-lookup"><span data-stu-id="693fb-120">Honda</span></span> |<span data-ttu-id="693fb-121">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-121">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="693fb-122">"2000"</span><span class="sxs-lookup"><span data-stu-id="693fb-122">"2000"</span></span> |

<span data-ttu-id="693fb-123">**輸出**：</span><span class="sxs-lookup"><span data-stu-id="693fb-123">**Output**:</span></span>

| <span data-ttu-id="693fb-124">Make</span><span class="sxs-lookup"><span data-stu-id="693fb-124">Make</span></span> | <span data-ttu-id="693fb-125">Weight</span><span class="sxs-lookup"><span data-stu-id="693fb-125">Weight</span></span> |
| --- | --- |
| <span data-ttu-id="693fb-126">Honda</span><span class="sxs-lookup"><span data-stu-id="693fb-126">Honda</span></span> |<span data-ttu-id="693fb-127">3000</span><span class="sxs-lookup"><span data-stu-id="693fb-127">3000</span></span> |

<span data-ttu-id="693fb-128">**解決方案**：</span><span class="sxs-lookup"><span data-stu-id="693fb-128">**Solution**:</span></span>

    SELECT
        Make,
        SUM(CAST(Weight AS BIGINT)) AS Weight
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

<span data-ttu-id="693fb-129">**說明**： 使用**轉換**陳述式中 hello**加權**欄位 toospecify 其資料類型。</span><span class="sxs-lookup"><span data-stu-id="693fb-129">**Explanation**: Use a **CAST** statement in hello **Weight** field toospecify its data type.</span></span> <span data-ttu-id="693fb-130">請參閱支援的資料類型中的 hello 清單[資料類型 (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx)。</span><span class="sxs-lookup"><span data-stu-id="693fb-130">See hello list of supported data types in [Data types (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span></span>

## <a name="query-example-use-likenot-like-toodo-pattern-matching"></a><span data-ttu-id="693fb-131">查詢範例： 使用類似/Not like toodo 模式比對</span><span class="sxs-lookup"><span data-stu-id="693fb-131">Query example: Use Like/Not like toodo pattern matching</span></span>
<span data-ttu-id="693fb-132">**描述**： 檢查 hello 事件的欄位值是否符合特定模式。</span><span class="sxs-lookup"><span data-stu-id="693fb-132">**Description**: Check that a field value on hello event matches a certain pattern.</span></span>
<span data-ttu-id="693fb-133">例如，檢查 hello 結果傳回授權盤子與起始或結束與 9。</span><span class="sxs-lookup"><span data-stu-id="693fb-133">For example, check that hello result returns license plates that start with A and end with 9.</span></span>

<span data-ttu-id="693fb-134">**輸入**：</span><span class="sxs-lookup"><span data-stu-id="693fb-134">**Input**:</span></span>

| <span data-ttu-id="693fb-135">Make</span><span class="sxs-lookup"><span data-stu-id="693fb-135">Make</span></span> | <span data-ttu-id="693fb-136">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="693fb-136">LicensePlate</span></span> | <span data-ttu-id="693fb-137">時間</span><span class="sxs-lookup"><span data-stu-id="693fb-137">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="693fb-138">Honda</span><span class="sxs-lookup"><span data-stu-id="693fb-138">Honda</span></span> |<span data-ttu-id="693fb-139">ABC-123</span><span class="sxs-lookup"><span data-stu-id="693fb-139">ABC-123</span></span> |<span data-ttu-id="693fb-140">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-140">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="693fb-141">Toyota</span><span class="sxs-lookup"><span data-stu-id="693fb-141">Toyota</span></span> |<span data-ttu-id="693fb-142">AAA-999</span><span class="sxs-lookup"><span data-stu-id="693fb-142">AAA-999</span></span> |<span data-ttu-id="693fb-143">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-143">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="693fb-144">Nissan</span><span class="sxs-lookup"><span data-stu-id="693fb-144">Nissan</span></span> |<span data-ttu-id="693fb-145">ABC-369</span><span class="sxs-lookup"><span data-stu-id="693fb-145">ABC-369</span></span> |<span data-ttu-id="693fb-146">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-146">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="693fb-147">**輸出**：</span><span class="sxs-lookup"><span data-stu-id="693fb-147">**Output**:</span></span>

| <span data-ttu-id="693fb-148">Make</span><span class="sxs-lookup"><span data-stu-id="693fb-148">Make</span></span> | <span data-ttu-id="693fb-149">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="693fb-149">LicensePlate</span></span> | <span data-ttu-id="693fb-150">時間</span><span class="sxs-lookup"><span data-stu-id="693fb-150">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="693fb-151">Toyota</span><span class="sxs-lookup"><span data-stu-id="693fb-151">Toyota</span></span> |<span data-ttu-id="693fb-152">AAA-999</span><span class="sxs-lookup"><span data-stu-id="693fb-152">AAA-999</span></span> |<span data-ttu-id="693fb-153">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-153">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="693fb-154">Nissan</span><span class="sxs-lookup"><span data-stu-id="693fb-154">Nissan</span></span> |<span data-ttu-id="693fb-155">ABC-369</span><span class="sxs-lookup"><span data-stu-id="693fb-155">ABC-369</span></span> |<span data-ttu-id="693fb-156">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-156">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="693fb-157">**解決方案**：</span><span class="sxs-lookup"><span data-stu-id="693fb-157">**Solution**:</span></span>

    SELECT
        *
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LicensePlate LIKE 'A%9'

<span data-ttu-id="693fb-158">**說明**： 使用 hello**像**陳述式 toocheck hello **LicensePlate**欄位值。</span><span class="sxs-lookup"><span data-stu-id="693fb-158">**Explanation**: Use hello **LIKE** statement toocheck hello **LicensePlate** field value.</span></span> <span data-ttu-id="693fb-159">開頭應該為 A，接著是長度為零或更多字元的字串，並以 9 結尾。</span><span class="sxs-lookup"><span data-stu-id="693fb-159">It should start with an A, then have any string of zero or more characters, and then end with a 9.</span></span> 

## <a name="query-example-specify-logic-for-different-casesvalues-case-statements"></a><span data-ttu-id="693fb-160">查詢範例：為不同的案例/值指定邏輯 (CASE 陳述式)</span><span class="sxs-lookup"><span data-stu-id="693fb-160">Query example: Specify logic for different cases/values (CASE statements)</span></span>
<span data-ttu-id="693fb-161">**描述**：根據特定準則，提供不同的欄位計算方式。</span><span class="sxs-lookup"><span data-stu-id="693fb-161">**Description**: Provide a different computation for a field, based on a particular criterion.</span></span>
<span data-ttu-id="693fb-162">例如，提供與特殊案例 1 多少汽車的 hello 相同進行傳遞的字串描述。</span><span class="sxs-lookup"><span data-stu-id="693fb-162">For example, provide a string description for how many cars of hello same make passed, with a special case for 1.</span></span>

<span data-ttu-id="693fb-163">**輸入**：</span><span class="sxs-lookup"><span data-stu-id="693fb-163">**Input**:</span></span>

| <span data-ttu-id="693fb-164">Make</span><span class="sxs-lookup"><span data-stu-id="693fb-164">Make</span></span> | <span data-ttu-id="693fb-165">時間</span><span class="sxs-lookup"><span data-stu-id="693fb-165">Time</span></span> |
| --- | --- |
| <span data-ttu-id="693fb-166">Honda</span><span class="sxs-lookup"><span data-stu-id="693fb-166">Honda</span></span> |<span data-ttu-id="693fb-167">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-167">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="693fb-168">Toyota</span><span class="sxs-lookup"><span data-stu-id="693fb-168">Toyota</span></span> |<span data-ttu-id="693fb-169">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-169">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="693fb-170">Toyota</span><span class="sxs-lookup"><span data-stu-id="693fb-170">Toyota</span></span> |<span data-ttu-id="693fb-171">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-171">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="693fb-172">**輸出**：</span><span class="sxs-lookup"><span data-stu-id="693fb-172">**Output**:</span></span>

| <span data-ttu-id="693fb-173">CarsPassed</span><span class="sxs-lookup"><span data-stu-id="693fb-173">CarsPassed</span></span> | <span data-ttu-id="693fb-174">時間</span><span class="sxs-lookup"><span data-stu-id="693fb-174">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="693fb-175">1 Honda</span><span class="sxs-lookup"><span data-stu-id="693fb-175">1 Honda</span></span> |<span data-ttu-id="693fb-176">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-176">2015-01-01T00:00:10.0000000Z</span></span> |
| <span data-ttu-id="693fb-177">2 Toyotas</span><span class="sxs-lookup"><span data-stu-id="693fb-177">2 Toyotas</span></span> |<span data-ttu-id="693fb-178">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-178">2015-01-01T00:00:10.0000000Z</span></span> |

<span data-ttu-id="693fb-179">**解決方案**：</span><span class="sxs-lookup"><span data-stu-id="693fb-179">**Solution**:</span></span>

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

<span data-ttu-id="693fb-180">**說明**: hello**案例**子句可讓我們 tooprovide 不同的計算，根據一些條件 （在此案例中的 hello 彙總視窗中的 hello 汽車 hello 計數）。</span><span class="sxs-lookup"><span data-stu-id="693fb-180">**Explanation**: hello **CASE** clause allows us tooprovide a different computation, based on some criteria (in our case, hello count of hello cars in hello aggregate window).</span></span>

## <a name="query-example-send-data-toomultiple-outputs"></a><span data-ttu-id="693fb-181">查詢範例： 傳送資料 toomultiple 輸出</span><span class="sxs-lookup"><span data-stu-id="693fb-181">Query example: Send data toomultiple outputs</span></span>
<span data-ttu-id="693fb-182">**描述**： 傳送資料 toomultiple 輸出一項工作的目標。</span><span class="sxs-lookup"><span data-stu-id="693fb-182">**Description**: Send data toomultiple output targets from a single job.</span></span>
<span data-ttu-id="693fb-183">例如，分析臨界值為基礎的警示資料和封存所有事件 tooblob 存放裝置。</span><span class="sxs-lookup"><span data-stu-id="693fb-183">For example, analyze data for a threshold-based alert and archive all events tooblob storage.</span></span>

<span data-ttu-id="693fb-184">**輸入**：</span><span class="sxs-lookup"><span data-stu-id="693fb-184">**Input**:</span></span>

| <span data-ttu-id="693fb-185">Make</span><span class="sxs-lookup"><span data-stu-id="693fb-185">Make</span></span> | <span data-ttu-id="693fb-186">時間</span><span class="sxs-lookup"><span data-stu-id="693fb-186">Time</span></span> |
| --- | --- |
| <span data-ttu-id="693fb-187">Honda</span><span class="sxs-lookup"><span data-stu-id="693fb-187">Honda</span></span> |<span data-ttu-id="693fb-188">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-188">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="693fb-189">Honda</span><span class="sxs-lookup"><span data-stu-id="693fb-189">Honda</span></span> |<span data-ttu-id="693fb-190">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-190">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="693fb-191">Toyota</span><span class="sxs-lookup"><span data-stu-id="693fb-191">Toyota</span></span> |<span data-ttu-id="693fb-192">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-192">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="693fb-193">Toyota</span><span class="sxs-lookup"><span data-stu-id="693fb-193">Toyota</span></span> |<span data-ttu-id="693fb-194">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-194">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="693fb-195">Toyota</span><span class="sxs-lookup"><span data-stu-id="693fb-195">Toyota</span></span> |<span data-ttu-id="693fb-196">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-196">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="693fb-197">**Output1**：</span><span class="sxs-lookup"><span data-stu-id="693fb-197">**Output1**:</span></span>

| <span data-ttu-id="693fb-198">Make</span><span class="sxs-lookup"><span data-stu-id="693fb-198">Make</span></span> | <span data-ttu-id="693fb-199">時間</span><span class="sxs-lookup"><span data-stu-id="693fb-199">Time</span></span> |
| --- | --- |
| <span data-ttu-id="693fb-200">Honda</span><span class="sxs-lookup"><span data-stu-id="693fb-200">Honda</span></span> |<span data-ttu-id="693fb-201">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-201">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="693fb-202">Honda</span><span class="sxs-lookup"><span data-stu-id="693fb-202">Honda</span></span> |<span data-ttu-id="693fb-203">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-203">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="693fb-204">Toyota</span><span class="sxs-lookup"><span data-stu-id="693fb-204">Toyota</span></span> |<span data-ttu-id="693fb-205">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-205">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="693fb-206">Toyota</span><span class="sxs-lookup"><span data-stu-id="693fb-206">Toyota</span></span> |<span data-ttu-id="693fb-207">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-207">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="693fb-208">Toyota</span><span class="sxs-lookup"><span data-stu-id="693fb-208">Toyota</span></span> |<span data-ttu-id="693fb-209">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-209">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="693fb-210">**Output2**：</span><span class="sxs-lookup"><span data-stu-id="693fb-210">**Output2**:</span></span>

| <span data-ttu-id="693fb-211">Make</span><span class="sxs-lookup"><span data-stu-id="693fb-211">Make</span></span> | <span data-ttu-id="693fb-212">時間</span><span class="sxs-lookup"><span data-stu-id="693fb-212">Time</span></span> | <span data-ttu-id="693fb-213">Count</span><span class="sxs-lookup"><span data-stu-id="693fb-213">Count</span></span> |
| --- | --- | --- |
| <span data-ttu-id="693fb-214">Toyota</span><span class="sxs-lookup"><span data-stu-id="693fb-214">Toyota</span></span> |<span data-ttu-id="693fb-215">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-215">2015-01-01T00:00:10.0000000Z</span></span> |<span data-ttu-id="693fb-216">3</span><span class="sxs-lookup"><span data-stu-id="693fb-216">3</span></span> |

<span data-ttu-id="693fb-217">**解決方案**：</span><span class="sxs-lookup"><span data-stu-id="693fb-217">**Solution**:</span></span>

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

<span data-ttu-id="693fb-218">**說明**: hello **INTO**子句會告知串流分析會輸出 toowrite hello 資料 toofrom 的 hello 這個陳述式。</span><span class="sxs-lookup"><span data-stu-id="693fb-218">**Explanation**: hello **INTO** clause tells Stream Analytics which of hello outputs toowrite hello data toofrom this statement.</span></span>
<span data-ttu-id="693fb-219">hello 第一個查詢是 hello 我們所收到的資料，我們名為 tooan 輸出傳遞**ArchiveOutput**。</span><span class="sxs-lookup"><span data-stu-id="693fb-219">hello first query is a pass-through of hello data we received tooan output that we named **ArchiveOutput**.</span></span>
<span data-ttu-id="693fb-220">hello 第二個查詢執行一些簡單的彙總並篩選，和它傳送嗨結果 tooa 下游警示系統。</span><span class="sxs-lookup"><span data-stu-id="693fb-220">hello second query does some simple aggregation and filtering, and it sends hello results tooa downstream alerting system.</span></span>

<span data-ttu-id="693fb-221">請注意，您也可以重複使用的 hello 通用資料表運算式 (Cte) 的 hello 結果 (例如**WITH**陳述式) 中多個輸出的陳述式。</span><span class="sxs-lookup"><span data-stu-id="693fb-221">Note that you can also reuse hello results of hello common table expressions (CTEs) (such as **WITH** statements) in multiple output statements.</span></span> <span data-ttu-id="693fb-222">此選項已 hello 開啟較少的讀取器 toohello 輸入的來源的好處。</span><span class="sxs-lookup"><span data-stu-id="693fb-222">This option has hello added benefit of opening fewer readers toohello input source.</span></span>
<span data-ttu-id="693fb-223">例如：</span><span class="sxs-lookup"><span data-stu-id="693fb-223">For example:</span></span> 

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

## <a name="query-example-count-unique-values"></a><span data-ttu-id="693fb-224">查詢範例：計算唯一值</span><span class="sxs-lookup"><span data-stu-id="693fb-224">Query example: Count unique values</span></span>
<span data-ttu-id="693fb-225">**描述**: hello 計數的 hello 的時間間隔內的資料流中出現的唯一欄位值。</span><span class="sxs-lookup"><span data-stu-id="693fb-225">**Description**: Count hello number of unique field values that appear in hello stream within a time window.</span></span>
<span data-ttu-id="693fb-226">例如，多少唯一可讓您的傳遞 2 第二個視窗中的 hello 收費亭的車輛嗎？</span><span class="sxs-lookup"><span data-stu-id="693fb-226">For example, how many unique makes of cars passed through hello toll booth in a 2-second window?</span></span>

<span data-ttu-id="693fb-227">**輸入**：</span><span class="sxs-lookup"><span data-stu-id="693fb-227">**Input**:</span></span>

| <span data-ttu-id="693fb-228">Make</span><span class="sxs-lookup"><span data-stu-id="693fb-228">Make</span></span> | <span data-ttu-id="693fb-229">時間</span><span class="sxs-lookup"><span data-stu-id="693fb-229">Time</span></span> |
| --- | --- |
| <span data-ttu-id="693fb-230">Honda</span><span class="sxs-lookup"><span data-stu-id="693fb-230">Honda</span></span> |<span data-ttu-id="693fb-231">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-231">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="693fb-232">Honda</span><span class="sxs-lookup"><span data-stu-id="693fb-232">Honda</span></span> |<span data-ttu-id="693fb-233">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-233">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="693fb-234">Toyota</span><span class="sxs-lookup"><span data-stu-id="693fb-234">Toyota</span></span> |<span data-ttu-id="693fb-235">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-235">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="693fb-236">Toyota</span><span class="sxs-lookup"><span data-stu-id="693fb-236">Toyota</span></span> |<span data-ttu-id="693fb-237">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-237">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="693fb-238">Toyota</span><span class="sxs-lookup"><span data-stu-id="693fb-238">Toyota</span></span> |<span data-ttu-id="693fb-239">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-239">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="693fb-240">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="693fb-240">**Output:**</span></span>

| <span data-ttu-id="693fb-241">Count</span><span class="sxs-lookup"><span data-stu-id="693fb-241">Count</span></span> | <span data-ttu-id="693fb-242">時間</span><span class="sxs-lookup"><span data-stu-id="693fb-242">Time</span></span> |
| --- | --- |
| <span data-ttu-id="693fb-243">2</span><span class="sxs-lookup"><span data-stu-id="693fb-243">2</span></span> |<span data-ttu-id="693fb-244">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-244">2015-01-01T00:00:02.000Z</span></span> |
| <span data-ttu-id="693fb-245">1</span><span class="sxs-lookup"><span data-stu-id="693fb-245">1</span></span> |<span data-ttu-id="693fb-246">2015-01-01T00:00:04.000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-246">2015-01-01T00:00:04.000Z</span></span> |

<span data-ttu-id="693fb-247">**解決方案：**</span><span class="sxs-lookup"><span data-stu-id="693fb-247">**Solution:**</span></span>

````
SELECT
     COUNT(DISTINCT Make) AS CountMake,
     System.TIMESTAMP AS TIME
FROM Input TIMESTAMP BY TIME
GROUP BY 
     TumblingWindow(second, 2)
````


<span data-ttu-id="693fb-248">**說明：**
**計數 （相異請）**傳回 hello hello 中相異值數目**進行**的時間間隔內的資料行。</span><span class="sxs-lookup"><span data-stu-id="693fb-248">**Explanation:**
**COUNT(DISTINCT Make)** returns hello number of distinct values in hello **Make** column within a time window.</span></span>

## <a name="query-example-determine-if-a-value-has-changed"></a><span data-ttu-id="693fb-249">查詢範例：判斷值是否已變更</span><span class="sxs-lookup"><span data-stu-id="693fb-249">Query example: Determine if a value has changed</span></span>
<span data-ttu-id="693fb-250">**描述**： 查看先前的值 toodetermine 是否不同於 hello 目前值。</span><span class="sxs-lookup"><span data-stu-id="693fb-250">**Description**: Look at a previous value toodetermine if it is different than hello current value.</span></span>
<span data-ttu-id="693fb-251">比方說，位於相同讓 hello 目前汽車 hello 付費道路 hello hello 先前汽車嗎？</span><span class="sxs-lookup"><span data-stu-id="693fb-251">For example, is hello previous car on hello toll road hello same make as hello current car?</span></span>

<span data-ttu-id="693fb-252">**輸入**：</span><span class="sxs-lookup"><span data-stu-id="693fb-252">**Input**:</span></span>

| <span data-ttu-id="693fb-253">Make</span><span class="sxs-lookup"><span data-stu-id="693fb-253">Make</span></span> | <span data-ttu-id="693fb-254">時間</span><span class="sxs-lookup"><span data-stu-id="693fb-254">Time</span></span> |
| --- | --- |
| <span data-ttu-id="693fb-255">Honda</span><span class="sxs-lookup"><span data-stu-id="693fb-255">Honda</span></span> |<span data-ttu-id="693fb-256">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-256">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="693fb-257">Toyota</span><span class="sxs-lookup"><span data-stu-id="693fb-257">Toyota</span></span> |<span data-ttu-id="693fb-258">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-258">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="693fb-259">**輸出**：</span><span class="sxs-lookup"><span data-stu-id="693fb-259">**Output**:</span></span>

| <span data-ttu-id="693fb-260">Make</span><span class="sxs-lookup"><span data-stu-id="693fb-260">Make</span></span> | <span data-ttu-id="693fb-261">時間</span><span class="sxs-lookup"><span data-stu-id="693fb-261">Time</span></span> |
| --- | --- |
| <span data-ttu-id="693fb-262">Toyota</span><span class="sxs-lookup"><span data-stu-id="693fb-262">Toyota</span></span> |<span data-ttu-id="693fb-263">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-263">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="693fb-264">**解決方案**：</span><span class="sxs-lookup"><span data-stu-id="693fb-264">**Solution**:</span></span>

    SELECT
        Make,
        Time
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(minute, 1)) <> Make

<span data-ttu-id="693fb-265">**說明**： 使用**延隔**toopeek hello 到輸入資料流的回一個事件，並取得 hello**進行**值。</span><span class="sxs-lookup"><span data-stu-id="693fb-265">**Explanation**: Use **LAG** toopeek into hello input stream one event back and get hello **Make** value.</span></span> <span data-ttu-id="693fb-266">然後比較 toohello**進行**值 hello 目前事件和輸出 hello 事件上，如果不相同。</span><span class="sxs-lookup"><span data-stu-id="693fb-266">Then compare it toohello **Make** value on hello current event and output hello event if they are different.</span></span>

## <a name="query-example-find-hello-first-event-in-a-window"></a><span data-ttu-id="693fb-267">查詢範例： 尋找 hello 中的第一個事件視窗</span><span class="sxs-lookup"><span data-stu-id="693fb-267">Query example: Find hello first event in a window</span></span>
<span data-ttu-id="693fb-268">**描述**： 每隔 10 分鐘的間隔中尋找 hello 第一個汽車。</span><span class="sxs-lookup"><span data-stu-id="693fb-268">**Description**: Find hello first car in every 10-minute interval.</span></span>

<span data-ttu-id="693fb-269">**輸入**：</span><span class="sxs-lookup"><span data-stu-id="693fb-269">**Input**:</span></span>

| <span data-ttu-id="693fb-270">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="693fb-270">LicensePlate</span></span> | <span data-ttu-id="693fb-271">Make</span><span class="sxs-lookup"><span data-stu-id="693fb-271">Make</span></span> | <span data-ttu-id="693fb-272">時間</span><span class="sxs-lookup"><span data-stu-id="693fb-272">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="693fb-273">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="693fb-273">DXE 5291</span></span> |<span data-ttu-id="693fb-274">Honda</span><span class="sxs-lookup"><span data-stu-id="693fb-274">Honda</span></span> |<span data-ttu-id="693fb-275">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-275">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="693fb-276">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="693fb-276">YZK 5704</span></span> |<span data-ttu-id="693fb-277">Ford</span><span class="sxs-lookup"><span data-stu-id="693fb-277">Ford</span></span> |<span data-ttu-id="693fb-278">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-278">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="693fb-279">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="693fb-279">RMV 8282</span></span> |<span data-ttu-id="693fb-280">Honda</span><span class="sxs-lookup"><span data-stu-id="693fb-280">Honda</span></span> |<span data-ttu-id="693fb-281">2015-07-27T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-281">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="693fb-282">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="693fb-282">YHN 6970</span></span> |<span data-ttu-id="693fb-283">Toyota</span><span class="sxs-lookup"><span data-stu-id="693fb-283">Toyota</span></span> |<span data-ttu-id="693fb-284">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-284">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="693fb-285">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="693fb-285">VFE 1616</span></span> |<span data-ttu-id="693fb-286">Toyota</span><span class="sxs-lookup"><span data-stu-id="693fb-286">Toyota</span></span> |<span data-ttu-id="693fb-287">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-287">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="693fb-288">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="693fb-288">QYF 9358</span></span> |<span data-ttu-id="693fb-289">Honda</span><span class="sxs-lookup"><span data-stu-id="693fb-289">Honda</span></span> |<span data-ttu-id="693fb-290">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-290">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="693fb-291">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="693fb-291">MDR 6128</span></span> |<span data-ttu-id="693fb-292">BMW</span><span class="sxs-lookup"><span data-stu-id="693fb-292">BMW</span></span> |<span data-ttu-id="693fb-293">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-293">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="693fb-294">**輸出**：</span><span class="sxs-lookup"><span data-stu-id="693fb-294">**Output**:</span></span>

| <span data-ttu-id="693fb-295">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="693fb-295">LicensePlate</span></span> | <span data-ttu-id="693fb-296">Make</span><span class="sxs-lookup"><span data-stu-id="693fb-296">Make</span></span> | <span data-ttu-id="693fb-297">時間</span><span class="sxs-lookup"><span data-stu-id="693fb-297">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="693fb-298">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="693fb-298">DXE 5291</span></span> |<span data-ttu-id="693fb-299">Honda</span><span class="sxs-lookup"><span data-stu-id="693fb-299">Honda</span></span> |<span data-ttu-id="693fb-300">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-300">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="693fb-301">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="693fb-301">QYF 9358</span></span> |<span data-ttu-id="693fb-302">Honda</span><span class="sxs-lookup"><span data-stu-id="693fb-302">Honda</span></span> |<span data-ttu-id="693fb-303">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-303">2015-07-27T00:12:02.0000000Z</span></span> |

<span data-ttu-id="693fb-304">**解決方案**：</span><span class="sxs-lookup"><span data-stu-id="693fb-304">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) = 1

<span data-ttu-id="693fb-305">現在我們變更 hello 問題，並尋找 hello 第一個汽車的特定把每隔 10 分鐘的間隔中。</span><span class="sxs-lookup"><span data-stu-id="693fb-305">Now let’s change hello problem and find hello first car of a particular make in every 10-minute interval.</span></span>

| <span data-ttu-id="693fb-306">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="693fb-306">LicensePlate</span></span> | <span data-ttu-id="693fb-307">Make</span><span class="sxs-lookup"><span data-stu-id="693fb-307">Make</span></span> | <span data-ttu-id="693fb-308">時間</span><span class="sxs-lookup"><span data-stu-id="693fb-308">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="693fb-309">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="693fb-309">DXE 5291</span></span> |<span data-ttu-id="693fb-310">Honda</span><span class="sxs-lookup"><span data-stu-id="693fb-310">Honda</span></span> |<span data-ttu-id="693fb-311">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-311">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="693fb-312">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="693fb-312">YZK 5704</span></span> |<span data-ttu-id="693fb-313">Ford</span><span class="sxs-lookup"><span data-stu-id="693fb-313">Ford</span></span> |<span data-ttu-id="693fb-314">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-314">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="693fb-315">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="693fb-315">YHN 6970</span></span> |<span data-ttu-id="693fb-316">Toyota</span><span class="sxs-lookup"><span data-stu-id="693fb-316">Toyota</span></span> |<span data-ttu-id="693fb-317">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-317">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="693fb-318">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="693fb-318">QYF 9358</span></span> |<span data-ttu-id="693fb-319">Honda</span><span class="sxs-lookup"><span data-stu-id="693fb-319">Honda</span></span> |<span data-ttu-id="693fb-320">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-320">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="693fb-321">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="693fb-321">MDR 6128</span></span> |<span data-ttu-id="693fb-322">BMW</span><span class="sxs-lookup"><span data-stu-id="693fb-322">BMW</span></span> |<span data-ttu-id="693fb-323">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-323">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="693fb-324">**解決方案**：</span><span class="sxs-lookup"><span data-stu-id="693fb-324">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) OVER (PARTITION BY Make) = 1

## <a name="query-example-find-hello-last-event-in-a-window"></a><span data-ttu-id="693fb-325">查詢範例： 尋找 hello 中的最後一個事件視窗</span><span class="sxs-lookup"><span data-stu-id="693fb-325">Query example: Find hello last event in a window</span></span>
<span data-ttu-id="693fb-326">**描述**： 每隔 10 分鐘的間隔中尋找 hello 最後一個汽車。</span><span class="sxs-lookup"><span data-stu-id="693fb-326">**Description**: Find hello last car in every 10-minute interval.</span></span>

<span data-ttu-id="693fb-327">**輸入**：</span><span class="sxs-lookup"><span data-stu-id="693fb-327">**Input**:</span></span>

| <span data-ttu-id="693fb-328">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="693fb-328">LicensePlate</span></span> | <span data-ttu-id="693fb-329">Make</span><span class="sxs-lookup"><span data-stu-id="693fb-329">Make</span></span> | <span data-ttu-id="693fb-330">時間</span><span class="sxs-lookup"><span data-stu-id="693fb-330">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="693fb-331">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="693fb-331">DXE 5291</span></span> |<span data-ttu-id="693fb-332">Honda</span><span class="sxs-lookup"><span data-stu-id="693fb-332">Honda</span></span> |<span data-ttu-id="693fb-333">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-333">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="693fb-334">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="693fb-334">YZK 5704</span></span> |<span data-ttu-id="693fb-335">Ford</span><span class="sxs-lookup"><span data-stu-id="693fb-335">Ford</span></span> |<span data-ttu-id="693fb-336">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-336">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="693fb-337">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="693fb-337">RMV 8282</span></span> |<span data-ttu-id="693fb-338">Honda</span><span class="sxs-lookup"><span data-stu-id="693fb-338">Honda</span></span> |<span data-ttu-id="693fb-339">2015-07-27T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-339">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="693fb-340">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="693fb-340">YHN 6970</span></span> |<span data-ttu-id="693fb-341">Toyota</span><span class="sxs-lookup"><span data-stu-id="693fb-341">Toyota</span></span> |<span data-ttu-id="693fb-342">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-342">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="693fb-343">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="693fb-343">VFE 1616</span></span> |<span data-ttu-id="693fb-344">Toyota</span><span class="sxs-lookup"><span data-stu-id="693fb-344">Toyota</span></span> |<span data-ttu-id="693fb-345">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-345">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="693fb-346">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="693fb-346">QYF 9358</span></span> |<span data-ttu-id="693fb-347">Honda</span><span class="sxs-lookup"><span data-stu-id="693fb-347">Honda</span></span> |<span data-ttu-id="693fb-348">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-348">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="693fb-349">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="693fb-349">MDR 6128</span></span> |<span data-ttu-id="693fb-350">BMW</span><span class="sxs-lookup"><span data-stu-id="693fb-350">BMW</span></span> |<span data-ttu-id="693fb-351">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-351">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="693fb-352">**輸出**：</span><span class="sxs-lookup"><span data-stu-id="693fb-352">**Output**:</span></span>

| <span data-ttu-id="693fb-353">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="693fb-353">LicensePlate</span></span> | <span data-ttu-id="693fb-354">Make</span><span class="sxs-lookup"><span data-stu-id="693fb-354">Make</span></span> | <span data-ttu-id="693fb-355">時間</span><span class="sxs-lookup"><span data-stu-id="693fb-355">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="693fb-356">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="693fb-356">VFE 1616</span></span> |<span data-ttu-id="693fb-357">Toyota</span><span class="sxs-lookup"><span data-stu-id="693fb-357">Toyota</span></span> |<span data-ttu-id="693fb-358">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-358">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="693fb-359">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="693fb-359">MDR 6128</span></span> |<span data-ttu-id="693fb-360">BMW</span><span class="sxs-lookup"><span data-stu-id="693fb-360">BMW</span></span> |<span data-ttu-id="693fb-361">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-361">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="693fb-362">**解決方案**：</span><span class="sxs-lookup"><span data-stu-id="693fb-362">**Solution**:</span></span>

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

<span data-ttu-id="693fb-363">**說明**: hello 查詢中有兩個步驟。</span><span class="sxs-lookup"><span data-stu-id="693fb-363">**Explanation**: There are two steps in hello query.</span></span> <span data-ttu-id="693fb-364">hello 第一次一個尋找 hello 時間戳記最新 windows 10 分鐘中。</span><span class="sxs-lookup"><span data-stu-id="693fb-364">hello first one finds hello latest time stamp in 10-minute windows.</span></span> <span data-ttu-id="693fb-365">第二個步驟聯結 hello hello hello 與 hello 原始資料流 toofind hello 符合事件 hello 最後一個時間戳記之各個視窗中的第一個查詢的結果。</span><span class="sxs-lookup"><span data-stu-id="693fb-365">hello second step joins hello results of hello first query with hello original stream toofind hello events that match hello last time stamps in each window.</span></span> 

## <a name="query-example-detect-hello-absence-of-events"></a><span data-ttu-id="693fb-366">查詢範例： 偵測 hello 沒有事件</span><span class="sxs-lookup"><span data-stu-id="693fb-366">Query example: Detect hello absence of events</span></span>
<span data-ttu-id="693fb-367">**描述**：檢查串流中是否沒有和特定準則相符的值。</span><span class="sxs-lookup"><span data-stu-id="693fb-367">**Description**: Check that a stream has no value that matches a certain criterion.</span></span>
<span data-ttu-id="693fb-368">比方說，從相同進行的 hello 2 連續汽車輸入 hello 付費道路 hello 內最後 90 秒嗎？</span><span class="sxs-lookup"><span data-stu-id="693fb-368">For example, have 2 consecutive cars from hello same make entered hello toll road within hello last 90 seconds?</span></span>

<span data-ttu-id="693fb-369">**輸入**：</span><span class="sxs-lookup"><span data-stu-id="693fb-369">**Input**:</span></span>

| <span data-ttu-id="693fb-370">Make</span><span class="sxs-lookup"><span data-stu-id="693fb-370">Make</span></span> | <span data-ttu-id="693fb-371">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="693fb-371">LicensePlate</span></span> | <span data-ttu-id="693fb-372">時間</span><span class="sxs-lookup"><span data-stu-id="693fb-372">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="693fb-373">Honda</span><span class="sxs-lookup"><span data-stu-id="693fb-373">Honda</span></span> |<span data-ttu-id="693fb-374">ABC-123</span><span class="sxs-lookup"><span data-stu-id="693fb-374">ABC-123</span></span> |<span data-ttu-id="693fb-375">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-375">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="693fb-376">Honda</span><span class="sxs-lookup"><span data-stu-id="693fb-376">Honda</span></span> |<span data-ttu-id="693fb-377">AAA-999</span><span class="sxs-lookup"><span data-stu-id="693fb-377">AAA-999</span></span> |<span data-ttu-id="693fb-378">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-378">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="693fb-379">Toyota</span><span class="sxs-lookup"><span data-stu-id="693fb-379">Toyota</span></span> |<span data-ttu-id="693fb-380">DEF-987</span><span class="sxs-lookup"><span data-stu-id="693fb-380">DEF-987</span></span> |<span data-ttu-id="693fb-381">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-381">2015-01-01T00:00:03.0000000Z</span></span> |
| <span data-ttu-id="693fb-382">Honda</span><span class="sxs-lookup"><span data-stu-id="693fb-382">Honda</span></span> |<span data-ttu-id="693fb-383">GHI-345</span><span class="sxs-lookup"><span data-stu-id="693fb-383">GHI-345</span></span> |<span data-ttu-id="693fb-384">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-384">2015-01-01T00:00:04.0000000Z</span></span> |

<span data-ttu-id="693fb-385">**輸出**：</span><span class="sxs-lookup"><span data-stu-id="693fb-385">**Output**:</span></span>

| <span data-ttu-id="693fb-386">Make</span><span class="sxs-lookup"><span data-stu-id="693fb-386">Make</span></span> | <span data-ttu-id="693fb-387">時間</span><span class="sxs-lookup"><span data-stu-id="693fb-387">Time</span></span> | <span data-ttu-id="693fb-388">CurrentCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="693fb-388">CurrentCarLicensePlate</span></span> | <span data-ttu-id="693fb-389">FirstCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="693fb-389">FirstCarLicensePlate</span></span> | <span data-ttu-id="693fb-390">FirstCarTime</span><span class="sxs-lookup"><span data-stu-id="693fb-390">FirstCarTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="693fb-391">Honda</span><span class="sxs-lookup"><span data-stu-id="693fb-391">Honda</span></span> |<span data-ttu-id="693fb-392">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-392">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="693fb-393">AAA-999</span><span class="sxs-lookup"><span data-stu-id="693fb-393">AAA-999</span></span> |<span data-ttu-id="693fb-394">ABC-123</span><span class="sxs-lookup"><span data-stu-id="693fb-394">ABC-123</span></span> |<span data-ttu-id="693fb-395">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-395">2015-01-01T00:00:01.0000000Z</span></span> |

<span data-ttu-id="693fb-396">**解決方案**：</span><span class="sxs-lookup"><span data-stu-id="693fb-396">**Solution**:</span></span>

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

<span data-ttu-id="693fb-397">**說明**： 使用**延隔**toopeek hello 到輸入資料流的回一個事件，並取得 hello**進行**值。</span><span class="sxs-lookup"><span data-stu-id="693fb-397">**Explanation**: Use **LAG** toopeek into hello input stream one event back and get hello **Make** value.</span></span> <span data-ttu-id="693fb-398">它比較 toohello**進行**hello 目前事件，然後輸出 hello 事件如果它們是 hello 相同的值。</span><span class="sxs-lookup"><span data-stu-id="693fb-398">Compare it toohello **MAKE** value in hello current event, and then output hello event if they are hello same.</span></span> <span data-ttu-id="693fb-399">您也可以使用**延隔**tooget hello 先前汽車相關的資料。</span><span class="sxs-lookup"><span data-stu-id="693fb-399">You can also use **LAG** tooget data about hello previous car.</span></span>

## <a name="query-example-detect-hello-duration-between-events"></a><span data-ttu-id="693fb-400">查詢範例： 偵測 hello 事件之間的持續期間</span><span class="sxs-lookup"><span data-stu-id="693fb-400">Query example: Detect hello duration between events</span></span>
<span data-ttu-id="693fb-401">**描述**： 尋找 hello 的給定事件的持續時間。</span><span class="sxs-lookup"><span data-stu-id="693fb-401">**Description**: Find hello duration of a given event.</span></span> <span data-ttu-id="693fb-402">例如，給定網站的點選流，判斷 hello 時間花在功能上。</span><span class="sxs-lookup"><span data-stu-id="693fb-402">For example, given a web clickstream, determine hello time spent on a feature.</span></span>

<span data-ttu-id="693fb-403">**輸入**：</span><span class="sxs-lookup"><span data-stu-id="693fb-403">**Input**:</span></span>  

| <span data-ttu-id="693fb-404">User</span><span class="sxs-lookup"><span data-stu-id="693fb-404">User</span></span> | <span data-ttu-id="693fb-405">功能</span><span class="sxs-lookup"><span data-stu-id="693fb-405">Feature</span></span> | <span data-ttu-id="693fb-406">Event</span><span class="sxs-lookup"><span data-stu-id="693fb-406">Event</span></span> | <span data-ttu-id="693fb-407">時間</span><span class="sxs-lookup"><span data-stu-id="693fb-407">Time</span></span> |
| --- | --- | --- | --- |
| user@location.com |<span data-ttu-id="693fb-408">RightMenu</span><span class="sxs-lookup"><span data-stu-id="693fb-408">RightMenu</span></span> |<span data-ttu-id="693fb-409">Start</span><span class="sxs-lookup"><span data-stu-id="693fb-409">Start</span></span> |<span data-ttu-id="693fb-410">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-410">2015-01-01T00:00:01.0000000Z</span></span> |
| user@location.com |<span data-ttu-id="693fb-411">RightMenu</span><span class="sxs-lookup"><span data-stu-id="693fb-411">RightMenu</span></span> |<span data-ttu-id="693fb-412">End</span><span class="sxs-lookup"><span data-stu-id="693fb-412">End</span></span> |<span data-ttu-id="693fb-413">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-413">2015-01-01T00:00:08.0000000Z</span></span> |

<span data-ttu-id="693fb-414">**輸出**：</span><span class="sxs-lookup"><span data-stu-id="693fb-414">**Output**:</span></span>  

| <span data-ttu-id="693fb-415">User</span><span class="sxs-lookup"><span data-stu-id="693fb-415">User</span></span> | <span data-ttu-id="693fb-416">功能</span><span class="sxs-lookup"><span data-stu-id="693fb-416">Feature</span></span> | <span data-ttu-id="693fb-417">Duration</span><span class="sxs-lookup"><span data-stu-id="693fb-417">Duration</span></span> |
| --- | --- | --- |
| user@location.com |<span data-ttu-id="693fb-418">RightMenu</span><span class="sxs-lookup"><span data-stu-id="693fb-418">RightMenu</span></span> |<span data-ttu-id="693fb-419">7</span><span class="sxs-lookup"><span data-stu-id="693fb-419">7</span></span> |

<span data-ttu-id="693fb-420">**解決方案**：</span><span class="sxs-lookup"><span data-stu-id="693fb-420">**Solution**:</span></span>

````
    SELECT
        [user], feature, DATEDIFF(second, LAST(Time) OVER (PARTITION BY [user], feature LIMIT DURATION(hour, 1) WHEN Event = 'start'), Time) as duration
    FROM input TIMESTAMP BY Time
    WHERE
        Event = 'end'
````

<span data-ttu-id="693fb-421">**說明**： 使用 hello**最後**函式 tooretrieve hello**時間**值 hello 事件類型時**啟動**。</span><span class="sxs-lookup"><span data-stu-id="693fb-421">**Explanation**: Use hello **LAST** function tooretrieve hello last **TIME** value when hello event type was **Start**.</span></span> <span data-ttu-id="693fb-422">hello**最後**函式使用**PARTITION BY [使用者]** hello 結果的 tooindicate 計算每個唯一的使用者。</span><span class="sxs-lookup"><span data-stu-id="693fb-422">hello **LAST** function uses **PARTITION BY [user]** tooindicate that hello result is computed per unique user.</span></span> <span data-ttu-id="693fb-423">hello 查詢具有 1 小時 hello 之間的時間差異的最大閾值**啟動**和**停止**事件，但是您視需要**(限制 DURATION(hour, 1)**。</span><span class="sxs-lookup"><span data-stu-id="693fb-423">hello query has a 1-hour maximum threshold for hello time difference between **Start** and **Stop** events, but is configurable as needed **(LIMIT DURATION(hour, 1)**.</span></span>

## <a name="query-example-detect-hello-duration-of-a-condition"></a><span data-ttu-id="693fb-424">查詢範例： 偵測條件的 hello 持續時間</span><span class="sxs-lookup"><span data-stu-id="693fb-424">Query example: Detect hello duration of a condition</span></span>
<span data-ttu-id="693fb-425">**描述**：找出某個情況的持續時間。</span><span class="sxs-lookup"><span data-stu-id="693fb-425">**Description**: Find out how long a condition occurred.</span></span>
<span data-ttu-id="693fb-426">例如，假設有個錯誤導致所有車輛的重量不正確 (超過 20,000 磅)，</span><span class="sxs-lookup"><span data-stu-id="693fb-426">For example, suppose that a bug resulted in all cars having an incorrect weight (above 20,000 pounds).</span></span> <span data-ttu-id="693fb-427">我們想要 hello bug toocompute hello 持續的時間。</span><span class="sxs-lookup"><span data-stu-id="693fb-427">We want toocompute hello duration of hello bug.</span></span>

<span data-ttu-id="693fb-428">**輸入**：</span><span class="sxs-lookup"><span data-stu-id="693fb-428">**Input**:</span></span>

| <span data-ttu-id="693fb-429">Make</span><span class="sxs-lookup"><span data-stu-id="693fb-429">Make</span></span> | <span data-ttu-id="693fb-430">時間</span><span class="sxs-lookup"><span data-stu-id="693fb-430">Time</span></span> | <span data-ttu-id="693fb-431">Weight</span><span class="sxs-lookup"><span data-stu-id="693fb-431">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="693fb-432">Honda</span><span class="sxs-lookup"><span data-stu-id="693fb-432">Honda</span></span> |<span data-ttu-id="693fb-433">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-433">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="693fb-434">2000</span><span class="sxs-lookup"><span data-stu-id="693fb-434">2000</span></span> |
| <span data-ttu-id="693fb-435">Toyota</span><span class="sxs-lookup"><span data-stu-id="693fb-435">Toyota</span></span> |<span data-ttu-id="693fb-436">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-436">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="693fb-437">25000</span><span class="sxs-lookup"><span data-stu-id="693fb-437">25000</span></span> |
| <span data-ttu-id="693fb-438">Honda</span><span class="sxs-lookup"><span data-stu-id="693fb-438">Honda</span></span> |<span data-ttu-id="693fb-439">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-439">2015-01-01T00:00:03.0000000Z</span></span> |<span data-ttu-id="693fb-440">26000</span><span class="sxs-lookup"><span data-stu-id="693fb-440">26000</span></span> |
| <span data-ttu-id="693fb-441">Toyota</span><span class="sxs-lookup"><span data-stu-id="693fb-441">Toyota</span></span> |<span data-ttu-id="693fb-442">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-442">2015-01-01T00:00:04.0000000Z</span></span> |<span data-ttu-id="693fb-443">25000</span><span class="sxs-lookup"><span data-stu-id="693fb-443">25000</span></span> |
| <span data-ttu-id="693fb-444">Honda</span><span class="sxs-lookup"><span data-stu-id="693fb-444">Honda</span></span> |<span data-ttu-id="693fb-445">2015-01-01T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-445">2015-01-01T00:00:05.0000000Z</span></span> |<span data-ttu-id="693fb-446">26000</span><span class="sxs-lookup"><span data-stu-id="693fb-446">26000</span></span> |
| <span data-ttu-id="693fb-447">Toyota</span><span class="sxs-lookup"><span data-stu-id="693fb-447">Toyota</span></span> |<span data-ttu-id="693fb-448">2015-01-01T00:00:06.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-448">2015-01-01T00:00:06.0000000Z</span></span> |<span data-ttu-id="693fb-449">25000</span><span class="sxs-lookup"><span data-stu-id="693fb-449">25000</span></span> |
| <span data-ttu-id="693fb-450">Honda</span><span class="sxs-lookup"><span data-stu-id="693fb-450">Honda</span></span> |<span data-ttu-id="693fb-451">2015-01-01T00:00:07.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-451">2015-01-01T00:00:07.0000000Z</span></span> |<span data-ttu-id="693fb-452">26000</span><span class="sxs-lookup"><span data-stu-id="693fb-452">26000</span></span> |
| <span data-ttu-id="693fb-453">Toyota</span><span class="sxs-lookup"><span data-stu-id="693fb-453">Toyota</span></span> |<span data-ttu-id="693fb-454">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-454">2015-01-01T00:00:08.0000000Z</span></span> |<span data-ttu-id="693fb-455">2000</span><span class="sxs-lookup"><span data-stu-id="693fb-455">2000</span></span> |

<span data-ttu-id="693fb-456">**輸出**：</span><span class="sxs-lookup"><span data-stu-id="693fb-456">**Output**:</span></span>

| <span data-ttu-id="693fb-457">StartFault</span><span class="sxs-lookup"><span data-stu-id="693fb-457">StartFault</span></span> | <span data-ttu-id="693fb-458">EndFault</span><span class="sxs-lookup"><span data-stu-id="693fb-458">EndFault</span></span> |
| --- | --- |
| <span data-ttu-id="693fb-459">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-459">2015-01-01T00:00:02.000Z</span></span> |<span data-ttu-id="693fb-460">2015-01-01T00:00:07.000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-460">2015-01-01T00:00:07.000Z</span></span> |

<span data-ttu-id="693fb-461">**解決方案**：</span><span class="sxs-lookup"><span data-stu-id="693fb-461">**Solution**:</span></span>

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

<span data-ttu-id="693fb-462">**說明**： 使用**延隔**24 小時的 tooview hello 輸入資料流並尋找執行個體**StartFault**和**StopFault**合併的 hello加權 < 20000。</span><span class="sxs-lookup"><span data-stu-id="693fb-462">**Explanation**: Use **LAG** tooview hello input stream for 24 hours and look for instances where **StartFault** and **StopFault** are spanned by hello weight < 20000.</span></span>

## <a name="query-example-fill-missing-values"></a><span data-ttu-id="693fb-463">查詢範例：填入遺漏值</span><span class="sxs-lookup"><span data-stu-id="693fb-463">Query example: Fill missing values</span></span>
<span data-ttu-id="693fb-464">**描述**: hello 資料流有遺漏值的事件，會產生以固定間隔事件資料流。</span><span class="sxs-lookup"><span data-stu-id="693fb-464">**Description**: For hello stream of events that have missing values, produce a stream of events with regular intervals.</span></span>
<span data-ttu-id="693fb-465">例如，產生報告的事件每隔 5 秒，最常出現的 hello 資料點。</span><span class="sxs-lookup"><span data-stu-id="693fb-465">For example, generate an event every 5 seconds that reports hello most recently seen data point.</span></span>

<span data-ttu-id="693fb-466">**輸入**：</span><span class="sxs-lookup"><span data-stu-id="693fb-466">**Input**:</span></span>

| <span data-ttu-id="693fb-467">t</span><span class="sxs-lookup"><span data-stu-id="693fb-467">t</span></span> | <span data-ttu-id="693fb-468">value</span><span class="sxs-lookup"><span data-stu-id="693fb-468">value</span></span> |
| --- | --- |
| <span data-ttu-id="693fb-469">"2014-01-01T06:01:00"</span><span class="sxs-lookup"><span data-stu-id="693fb-469">"2014-01-01T06:01:00"</span></span> |<span data-ttu-id="693fb-470">1</span><span class="sxs-lookup"><span data-stu-id="693fb-470">1</span></span> |
| <span data-ttu-id="693fb-471">"2014-01-01T06:01:05"</span><span class="sxs-lookup"><span data-stu-id="693fb-471">"2014-01-01T06:01:05"</span></span> |<span data-ttu-id="693fb-472">2</span><span class="sxs-lookup"><span data-stu-id="693fb-472">2</span></span> |
| <span data-ttu-id="693fb-473">"2014-01-01T06:01:10"</span><span class="sxs-lookup"><span data-stu-id="693fb-473">"2014-01-01T06:01:10"</span></span> |<span data-ttu-id="693fb-474">3</span><span class="sxs-lookup"><span data-stu-id="693fb-474">3</span></span> |
| <span data-ttu-id="693fb-475">"2014-01-01T06:01:15"</span><span class="sxs-lookup"><span data-stu-id="693fb-475">"2014-01-01T06:01:15"</span></span> |<span data-ttu-id="693fb-476">4</span><span class="sxs-lookup"><span data-stu-id="693fb-476">4</span></span> |
| <span data-ttu-id="693fb-477">"2014-01-01T06:01:30"</span><span class="sxs-lookup"><span data-stu-id="693fb-477">"2014-01-01T06:01:30"</span></span> |<span data-ttu-id="693fb-478">5</span><span class="sxs-lookup"><span data-stu-id="693fb-478">5</span></span> |
| <span data-ttu-id="693fb-479">"2014-01-01T06:01:35"</span><span class="sxs-lookup"><span data-stu-id="693fb-479">"2014-01-01T06:01:35"</span></span> |<span data-ttu-id="693fb-480">6</span><span class="sxs-lookup"><span data-stu-id="693fb-480">6</span></span> |

<span data-ttu-id="693fb-481">**輸出 (前 10 個資料列)**：</span><span class="sxs-lookup"><span data-stu-id="693fb-481">**Output (first 10 rows)**:</span></span>

| <span data-ttu-id="693fb-482">windowend</span><span class="sxs-lookup"><span data-stu-id="693fb-482">windowend</span></span> | <span data-ttu-id="693fb-483">lastevent.t</span><span class="sxs-lookup"><span data-stu-id="693fb-483">lastevent.t</span></span> | <span data-ttu-id="693fb-484">lastevent.value</span><span class="sxs-lookup"><span data-stu-id="693fb-484">lastevent.value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="693fb-485">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-485">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="693fb-486">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-486">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="693fb-487">1</span><span class="sxs-lookup"><span data-stu-id="693fb-487">1</span></span> |
| <span data-ttu-id="693fb-488">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-488">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="693fb-489">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-489">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="693fb-490">2</span><span class="sxs-lookup"><span data-stu-id="693fb-490">2</span></span> |
| <span data-ttu-id="693fb-491">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-491">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="693fb-492">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-492">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="693fb-493">3</span><span class="sxs-lookup"><span data-stu-id="693fb-493">3</span></span> |
| <span data-ttu-id="693fb-494">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-494">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="693fb-495">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-495">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="693fb-496">4</span><span class="sxs-lookup"><span data-stu-id="693fb-496">4</span></span> |
| <span data-ttu-id="693fb-497">2014-01-01T14:01:20.000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-497">2014-01-01T14:01:20.000Z</span></span> |<span data-ttu-id="693fb-498">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-498">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="693fb-499">4</span><span class="sxs-lookup"><span data-stu-id="693fb-499">4</span></span> |
| <span data-ttu-id="693fb-500">2014-01-01T14:01:25.000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-500">2014-01-01T14:01:25.000Z</span></span> |<span data-ttu-id="693fb-501">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-501">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="693fb-502">4</span><span class="sxs-lookup"><span data-stu-id="693fb-502">4</span></span> |
| <span data-ttu-id="693fb-503">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-503">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="693fb-504">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-504">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="693fb-505">5</span><span class="sxs-lookup"><span data-stu-id="693fb-505">5</span></span> |
| <span data-ttu-id="693fb-506">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-506">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="693fb-507">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-507">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="693fb-508">6</span><span class="sxs-lookup"><span data-stu-id="693fb-508">6</span></span> |
| <span data-ttu-id="693fb-509">2014-01-01T14:01:40.000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-509">2014-01-01T14:01:40.000Z</span></span> |<span data-ttu-id="693fb-510">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-510">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="693fb-511">6</span><span class="sxs-lookup"><span data-stu-id="693fb-511">6</span></span> |
| <span data-ttu-id="693fb-512">2014-01-01T14:01:45.000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-512">2014-01-01T14:01:45.000Z</span></span> |<span data-ttu-id="693fb-513">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="693fb-513">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="693fb-514">6</span><span class="sxs-lookup"><span data-stu-id="693fb-514">6</span></span> |

<span data-ttu-id="693fb-515">**解決方案**：</span><span class="sxs-lookup"><span data-stu-id="693fb-515">**Solution**:</span></span>

    SELECT
        System.Timestamp AS windowEnd,
        TopOne() OVER (ORDER BY t DESC) AS lastEvent
    FROM
        input TIMESTAMP BY t
    GROUP BY HOPPINGWINDOW(second, 300, 5)


<span data-ttu-id="693fb-516">**說明**： 此查詢會產生事件每隔 5 秒，並輸出 hello 先前接收的最後一個事件。</span><span class="sxs-lookup"><span data-stu-id="693fb-516">**Explanation**: This query generates events every 5 seconds and outputs hello last event that was received previously.</span></span> <span data-ttu-id="693fb-517">hello [Hopping 視窗](https://msdn.microsoft.com/library/dn835041.aspx "Hopping 視窗-Azure Stream Analytics")持續時間會決定多久後 hello 查詢會尋找 toofind hello 最新事件 （在此範例中的 300 秒）。</span><span class="sxs-lookup"><span data-stu-id="693fb-517">hello [Hopping window](https://msdn.microsoft.com/library/dn835041.aspx "Hopping window--Azure Stream Analytics") duration determines how far back hello query looks toofind hello latest event (300 seconds in this example).</span></span>

## <a name="get-help"></a><span data-ttu-id="693fb-518">取得說明</span><span class="sxs-lookup"><span data-stu-id="693fb-518">Get help</span></span>
<span data-ttu-id="693fb-519">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。</span><span class="sxs-lookup"><span data-stu-id="693fb-519">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="693fb-520">後續步驟</span><span class="sxs-lookup"><span data-stu-id="693fb-520">Next steps</span></span>
* [<span data-ttu-id="693fb-521">簡介 tooAzure 資料流分析</span><span class="sxs-lookup"><span data-stu-id="693fb-521">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="693fb-522">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="693fb-522">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="693fb-523">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="693fb-523">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="693fb-524">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="693fb-524">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="693fb-525">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="693fb-525">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

