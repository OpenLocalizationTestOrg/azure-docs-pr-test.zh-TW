---
title: "使用者定義函數的資料流分析 JavaScript aaaAzure |Microsoft 文件"
description: "使用 JavaScript 使用者定義函式來執行進階查詢技術"
keywords: "javascript, 使用者定義函式, udf"
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 28eeb8f6437c23989e8887687b950361fed4414c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-javascript-user-defined-functions"></a><span data-ttu-id="32bfd-104">Azure 串流分析 JavaScript 使用者定義函式</span><span class="sxs-lookup"><span data-stu-id="32bfd-104">Azure Stream Analytics JavaScript user-defined functions</span></span>
<span data-ttu-id="32bfd-105">Azure 串流分析支援以 JavaScript 撰寫的使用者定義函式。</span><span class="sxs-lookup"><span data-stu-id="32bfd-105">Azure Stream Analytics supports user-defined functions written in JavaScript.</span></span> <span data-ttu-id="32bfd-106">使用豐富的 hello**字串**， **RegExp**，**數學**，**陣列**，和**日期**方法，提供 JavaScript，複雜資料轉換與串流分析工作變得更容易 toocreate。</span><span class="sxs-lookup"><span data-stu-id="32bfd-106">With hello rich set of **String**, **RegExp**, **Math**, **Array**, and **Date** methods that JavaScript provides, complex data transformations with Stream Analytics jobs become easier toocreate.</span></span>

## <a name="javascript-user-defined-functions"></a><span data-ttu-id="32bfd-107">JavaScript 使用者定義函式</span><span class="sxs-lookup"><span data-stu-id="32bfd-107">JavaScript user-defined functions</span></span>
<span data-ttu-id="32bfd-108">JavaScript 使用者定義的函式支援無狀態且只做為計算用途的純量函式，而且不需要外部連線能力。</span><span class="sxs-lookup"><span data-stu-id="32bfd-108">JavaScript user-defined functions support stateless, compute-only scalar functions that do not require external connectivity.</span></span> <span data-ttu-id="32bfd-109">hello 傳回函式的值只能是純量 （單一） 值。</span><span class="sxs-lookup"><span data-stu-id="32bfd-109">hello return value of a function can only be a scalar (single) value.</span></span> <span data-ttu-id="32bfd-110">加入 JavaScript 使用者定義函數 tooa 作業之後，您可以在任何地方在 hello 查詢中，內建的純量函式中使用 hello 函式。</span><span class="sxs-lookup"><span data-stu-id="32bfd-110">After you add a JavaScript user-defined function tooa job, you can use hello function anywhere in hello query, like a built-in scalar function.</span></span>

<span data-ttu-id="32bfd-111">從以下的一些案例可以看出 JavaScript 使用者定義函式很實用：</span><span class="sxs-lookup"><span data-stu-id="32bfd-111">Here are some scenarios where you might find JavaScript user-defined functions useful:</span></span>
* <span data-ttu-id="32bfd-112">剖析及操作具有規則運算式函式的字串，例如：**Regexp_Replace()** 和 **Regexp_Extract()**</span><span class="sxs-lookup"><span data-stu-id="32bfd-112">Parsing and manipulating strings that have regular expression functions, for example, **Regexp_Replace()** and **Regexp_Extract()**</span></span>
* <span data-ttu-id="32bfd-113">解碼和編碼資料，例如：從二進位轉換成十六進位</span><span class="sxs-lookup"><span data-stu-id="32bfd-113">Decoding and encoding data, for example, binary-to-hex conversion</span></span>
* <span data-ttu-id="32bfd-114">使用 JavaScript **Math** 函式做數學運算</span><span class="sxs-lookup"><span data-stu-id="32bfd-114">Performing mathematic computations with JavaScript **Math** functions</span></span>
* <span data-ttu-id="32bfd-115">執行陣列作業，例如，排序、連結、尋找及填入</span><span class="sxs-lookup"><span data-stu-id="32bfd-115">Performing array operations like sort, join, find, and fill</span></span>

<span data-ttu-id="32bfd-116">以下是一些在串流分析中無法使用 JavaScript 使用者定義函式達成的事項：</span><span class="sxs-lookup"><span data-stu-id="32bfd-116">Here are some things that you cannot do with a JavaScript user-defined function in Stream Analytics:</span></span>
* <span data-ttu-id="32bfd-117">呼叫外部 REST 端點，例如，執行反向 IP 查詢或從外部來源提取參考資料</span><span class="sxs-lookup"><span data-stu-id="32bfd-117">Call out external REST endpoints, for example, performing reverse IP lookup or pulling reference data from an external source</span></span>
* <span data-ttu-id="32bfd-118">對輸入/輸出執行自訂事件格式序列化或還原序列化</span><span class="sxs-lookup"><span data-stu-id="32bfd-118">Perform custom event format serialization or deserialization on inputs/outputs</span></span>
* <span data-ttu-id="32bfd-119">建立自訂彙總</span><span class="sxs-lookup"><span data-stu-id="32bfd-119">Create custom aggregates</span></span>

<span data-ttu-id="32bfd-120">雖然函式像**Date.GetDate()**或**Math.random()**不會封鎖在 hello 函式定義中，您應該避免使用它們。</span><span class="sxs-lookup"><span data-stu-id="32bfd-120">Although functions like **Date.GetDate()** or **Math.random()** are not blocked in hello functions definition, you should avoid using them.</span></span> <span data-ttu-id="32bfd-121">這些函式**不**傳回 hello 相同結果每次您呼叫它們，並 hello Azure Stream Analytics 服務不會保留筆記本的函式引動過程，以及傳回結果。</span><span class="sxs-lookup"><span data-stu-id="32bfd-121">These functions **do not** return hello same result every time you call them, and hello Azure Stream Analytics service does not keep a journal of function invocations and returned results.</span></span> <span data-ttu-id="32bfd-122">如果函式會傳回不同的結果上 hello 相同的事件，您或 hello Stream Analytics 服務重新啟動作業時不保證重複性。</span><span class="sxs-lookup"><span data-stu-id="32bfd-122">If a function returns different result on hello same events, repeatability is not guaranteed when a job is restarted by you or by hello Stream Analytics service.</span></span>

## <a name="add-a-javascript-user-defined-function-in-hello-azure-portal"></a><span data-ttu-id="32bfd-123">在 hello Azure 入口網站中加入 JavaScript 使用者定義函式</span><span class="sxs-lookup"><span data-stu-id="32bfd-123">Add a JavaScript user-defined function in hello Azure portal</span></span>
<span data-ttu-id="32bfd-124">toocreate 的簡單 JavaScript 使用者定義函式在為現有的資料流分析工作，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="32bfd-124">toocreate a simple JavaScript user-defined function under an existing Stream Analytics job, do these steps:</span></span>

1.  <span data-ttu-id="32bfd-125">在 hello Azure 入口網站，尋找您的資料流分析工作。</span><span class="sxs-lookup"><span data-stu-id="32bfd-125">In hello Azure portal, find your Stream Analytics job.</span></span>
2.  <span data-ttu-id="32bfd-126">在 [作業拓撲] 下，選取您的函式。</span><span class="sxs-lookup"><span data-stu-id="32bfd-126">Under **JOB TOPOLOGY**, select your function.</span></span> <span data-ttu-id="32bfd-127">空白的函式清單隨即出現。</span><span class="sxs-lookup"><span data-stu-id="32bfd-127">An empty list of functions appears.</span></span>
3.  <span data-ttu-id="32bfd-128">選取新的使用者定義函數，toocreate**新增**。</span><span class="sxs-lookup"><span data-stu-id="32bfd-128">toocreate a new user-defined function, select **Add**.</span></span>
4.  <span data-ttu-id="32bfd-129">在 hello**新函式**刀鋒視窗中，針對**函式類型**，選取**JavaScript**。</span><span class="sxs-lookup"><span data-stu-id="32bfd-129">On hello **New Function** blade, for **Function Type**, select **JavaScript**.</span></span> <span data-ttu-id="32bfd-130">Hello 編輯器中會出現預設函式樣板。</span><span class="sxs-lookup"><span data-stu-id="32bfd-130">A default function template appears in hello editor.</span></span>
5.  <span data-ttu-id="32bfd-131">Hello **UDF 別名**，輸入**hex2Int**，並變更 hello 函式實作，如下所示：</span><span class="sxs-lookup"><span data-stu-id="32bfd-131">For hello **UDF alias**, enter **hex2Int**, and change hello function implementation as follows:</span></span>

    ```
    // Convert Hex value toointeger.
    function main(hexValue) {
        return parseInt(hexValue, 16);
    }
    ```

6.  <span data-ttu-id="32bfd-132">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="32bfd-132">Select **Save**.</span></span> <span data-ttu-id="32bfd-133">您的函式會出現在 hello 函式清單。</span><span class="sxs-lookup"><span data-stu-id="32bfd-133">Your function appears in hello list of functions.</span></span>
7.  <span data-ttu-id="32bfd-134">選取新的 hello **hex2Int**函式，並檢查 hello 函式定義。</span><span class="sxs-lookup"><span data-stu-id="32bfd-134">Select hello new **hex2Int** function, and check hello function definition.</span></span> <span data-ttu-id="32bfd-135">所有函式具有**UDF**前置詞加入的 toohello 函式的別名。</span><span class="sxs-lookup"><span data-stu-id="32bfd-135">All functions have a **UDF** prefix added toohello function alias.</span></span> <span data-ttu-id="32bfd-136">您需要*包含 hello 前置詞*當資料流分析查詢中呼叫 hello 函式。</span><span class="sxs-lookup"><span data-stu-id="32bfd-136">You need too*include hello prefix* when you call hello function in your Stream Analytics query.</span></span> <span data-ttu-id="32bfd-137">在此情況下，您會呼叫 **UDF.hex2Int**。</span><span class="sxs-lookup"><span data-stu-id="32bfd-137">In this case, you call **UDF.hex2Int**.</span></span>

## <a name="call-a-javascript-user-defined-function-in-a-query"></a><span data-ttu-id="32bfd-138">在查詢中呼叫 JavaScript 使用者定義函式</span><span class="sxs-lookup"><span data-stu-id="32bfd-138">Call a JavaScript user-defined function in a query</span></span>

1. <span data-ttu-id="32bfd-139">在 [hello 查詢編輯器] 中，在**作業拓撲**，選取**查詢**。</span><span class="sxs-lookup"><span data-stu-id="32bfd-139">In hello query editor, under **JOB TOPOLOGY**, select **Query**.</span></span>
2.  <span data-ttu-id="32bfd-140">編輯您的查詢，並接著呼叫 hello 使用者定義函數，就像這樣：</span><span class="sxs-lookup"><span data-stu-id="32bfd-140">Edit your query, and then call hello user-defined function, like this:</span></span>

    ```
    SELECT
        time,
        UDF.hex2Int(offset) AS IntOffset
    INTO
        output
    FROM
        InputStream
    ```

3.  <span data-ttu-id="32bfd-141">tooupload hello 範例資料檔，以滑鼠右鍵按一下 hello 作業輸入。</span><span class="sxs-lookup"><span data-stu-id="32bfd-141">tooupload hello sample data file, right-click hello job input.</span></span>
4.  <span data-ttu-id="32bfd-142">tootest 您查詢中，選取**測試**。</span><span class="sxs-lookup"><span data-stu-id="32bfd-142">tootest your query, select **Test**.</span></span>


## <a name="supported-javascript-objects"></a><span data-ttu-id="32bfd-143">支援的 JavaScript 物件</span><span class="sxs-lookup"><span data-stu-id="32bfd-143">Supported JavaScript objects</span></span>
<span data-ttu-id="32bfd-144">Azure 串流分析 JavaScript 使用者定義函式支援標準的內建 JavaScript 物件。</span><span class="sxs-lookup"><span data-stu-id="32bfd-144">Azure Stream Analytics JavaScript user-defined functions support standard, built-in JavaScript objects.</span></span> <span data-ttu-id="32bfd-145">如需這些物件的清單，請參閱[全域物件](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects)。</span><span class="sxs-lookup"><span data-stu-id="32bfd-145">For a list of these objects, see [Global Objects](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).</span></span>

### <a name="stream-analytics-and-javascript-type-conversion"></a><span data-ttu-id="32bfd-146">串流分析與 JavaScript 類型轉換</span><span class="sxs-lookup"><span data-stu-id="32bfd-146">Stream Analytics and JavaScript type conversion</span></span>

<span data-ttu-id="32bfd-147">有一些差異在 hello hello 串流分析查詢語言和 JavaScript 支援的型別中。</span><span class="sxs-lookup"><span data-stu-id="32bfd-147">There are differences in hello types that hello Stream Analytics query language and JavaScript support.</span></span> <span data-ttu-id="32bfd-148">下表列出之間兩個 hello hello 轉換對應：</span><span class="sxs-lookup"><span data-stu-id="32bfd-148">This table lists hello conversion mappings between hello two:</span></span>

<span data-ttu-id="32bfd-149">串流分析</span><span class="sxs-lookup"><span data-stu-id="32bfd-149">Stream Analytics</span></span> | <span data-ttu-id="32bfd-150">JavaScript</span><span class="sxs-lookup"><span data-stu-id="32bfd-150">JavaScript</span></span>
--- | ---
<span data-ttu-id="32bfd-151">bigint</span><span class="sxs-lookup"><span data-stu-id="32bfd-151">bigint</span></span> | <span data-ttu-id="32bfd-152">數字 (JavaScript 只能表示整數向上 tooprecisely 2 ^53)</span><span class="sxs-lookup"><span data-stu-id="32bfd-152">Number (JavaScript can only represent integers up tooprecisely 2^53)</span></span>
<span data-ttu-id="32bfd-153">DateTime</span><span class="sxs-lookup"><span data-stu-id="32bfd-153">DateTime</span></span> | <span data-ttu-id="32bfd-154">Date (JavaScript 只支援毫秒)</span><span class="sxs-lookup"><span data-stu-id="32bfd-154">Date (JavaScript only supports milliseconds)</span></span>
<span data-ttu-id="32bfd-155">double</span><span class="sxs-lookup"><span data-stu-id="32bfd-155">double</span></span> | <span data-ttu-id="32bfd-156">Number</span><span class="sxs-lookup"><span data-stu-id="32bfd-156">Number</span></span>
<span data-ttu-id="32bfd-157">nvarchar(MAX)</span><span class="sxs-lookup"><span data-stu-id="32bfd-157">nvarchar(MAX)</span></span> | <span data-ttu-id="32bfd-158">String</span><span class="sxs-lookup"><span data-stu-id="32bfd-158">String</span></span>
<span data-ttu-id="32bfd-159">Record</span><span class="sxs-lookup"><span data-stu-id="32bfd-159">Record</span></span> | <span data-ttu-id="32bfd-160">Object</span><span class="sxs-lookup"><span data-stu-id="32bfd-160">Object</span></span>
<span data-ttu-id="32bfd-161">陣列</span><span class="sxs-lookup"><span data-stu-id="32bfd-161">Array</span></span> | <span data-ttu-id="32bfd-162">陣列</span><span class="sxs-lookup"><span data-stu-id="32bfd-162">Array</span></span>
<span data-ttu-id="32bfd-163">NULL</span><span class="sxs-lookup"><span data-stu-id="32bfd-163">NULL</span></span> | <span data-ttu-id="32bfd-164">Null</span><span class="sxs-lookup"><span data-stu-id="32bfd-164">Null</span></span>


<span data-ttu-id="32bfd-165">以下是 JavaScript 至串流分析的轉換：</span><span class="sxs-lookup"><span data-stu-id="32bfd-165">Here are JavaScript-to-Stream Analytics conversions:</span></span>


<span data-ttu-id="32bfd-166">JavaScript</span><span class="sxs-lookup"><span data-stu-id="32bfd-166">JavaScript</span></span> | <span data-ttu-id="32bfd-167">串流分析</span><span class="sxs-lookup"><span data-stu-id="32bfd-167">Stream Analytics</span></span>
--- | ---
<span data-ttu-id="32bfd-168">數字</span><span class="sxs-lookup"><span data-stu-id="32bfd-168">Number</span></span> | <span data-ttu-id="32bfd-169">Bigint （如果 round 和長時間之間 hello 號碼。MinValue，長時間。MaxValue。否則，它是 double）</span><span class="sxs-lookup"><span data-stu-id="32bfd-169">Bigint (if hello number is round and between long.MinValue and long.MaxValue; otherwise, it's double)</span></span>
<span data-ttu-id="32bfd-170">Date</span><span class="sxs-lookup"><span data-stu-id="32bfd-170">Date</span></span> | <span data-ttu-id="32bfd-171">DateTime</span><span class="sxs-lookup"><span data-stu-id="32bfd-171">DateTime</span></span>
<span data-ttu-id="32bfd-172">String</span><span class="sxs-lookup"><span data-stu-id="32bfd-172">String</span></span> | <span data-ttu-id="32bfd-173">nvarchar(MAX)</span><span class="sxs-lookup"><span data-stu-id="32bfd-173">nvarchar(MAX)</span></span>
<span data-ttu-id="32bfd-174">Object</span><span class="sxs-lookup"><span data-stu-id="32bfd-174">Object</span></span> | <span data-ttu-id="32bfd-175">Record</span><span class="sxs-lookup"><span data-stu-id="32bfd-175">Record</span></span>
<span data-ttu-id="32bfd-176">陣列</span><span class="sxs-lookup"><span data-stu-id="32bfd-176">Array</span></span> | <span data-ttu-id="32bfd-177">陣列</span><span class="sxs-lookup"><span data-stu-id="32bfd-177">Array</span></span>
<span data-ttu-id="32bfd-178">Null、Undefined</span><span class="sxs-lookup"><span data-stu-id="32bfd-178">Null, Undefined</span></span> | <span data-ttu-id="32bfd-179">NULL</span><span class="sxs-lookup"><span data-stu-id="32bfd-179">NULL</span></span>
<span data-ttu-id="32bfd-180">任何其他類型 (例如，函式或錯誤)</span><span class="sxs-lookup"><span data-stu-id="32bfd-180">Any other type (for example, a function or error)</span></span> | <span data-ttu-id="32bfd-181">不支援 (產生執行階段錯誤)</span><span class="sxs-lookup"><span data-stu-id="32bfd-181">Not supported (results in runtime error)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="32bfd-182">疑難排解</span><span class="sxs-lookup"><span data-stu-id="32bfd-182">Troubleshooting</span></span>
<span data-ttu-id="32bfd-183">JavaScript 執行階段錯誤會視為嚴重錯誤，並透過 hello 活動記錄檔便會顯示。</span><span class="sxs-lookup"><span data-stu-id="32bfd-183">JavaScript runtime errors are considered fatal, and are surfaced through hello Activity log.</span></span> <span data-ttu-id="32bfd-184">tooretrieve hello 記錄中 hello Azure 入口網站中，移 tooyour 作業並選取**活動記錄檔**。</span><span class="sxs-lookup"><span data-stu-id="32bfd-184">tooretrieve hello log, in hello Azure portal, go tooyour job and select **Activity log**.</span></span>


## <a name="other-javascript-user-defined-function-patterns"></a><span data-ttu-id="32bfd-185">其他 JavaScript 使用者定義函式模式</span><span class="sxs-lookup"><span data-stu-id="32bfd-185">Other JavaScript user-defined function patterns</span></span>

### <a name="write-nested-json-toooutput"></a><span data-ttu-id="32bfd-186">撰寫巢狀的 JSON toooutput</span><span class="sxs-lookup"><span data-stu-id="32bfd-186">Write nested JSON toooutput</span></span>
<span data-ttu-id="32bfd-187">如果您使用做為輸入，輸出資料流分析工作的待處理的處理步驟，而且需要 JSON 格式，您可以撰寫 JSON 字串 toooutput。</span><span class="sxs-lookup"><span data-stu-id="32bfd-187">If you have a follow-up processing step that uses a Stream Analytics job output as input, and it requires a JSON format, you can write a JSON string toooutput.</span></span> <span data-ttu-id="32bfd-188">hello 下一個範例會呼叫 hello **JSON.stringify()** toopack hello 的所有名稱/值組輸入，並再將它們寫入為單一字串中的值輸出函式。</span><span class="sxs-lookup"><span data-stu-id="32bfd-188">hello next example calls hello **JSON.stringify()** function toopack all name/value pairs of hello input, and then write them as a single string value in output.</span></span>

<span data-ttu-id="32bfd-189">**JavaScript 使用者定義函式定義：**</span><span class="sxs-lookup"><span data-stu-id="32bfd-189">**JavaScript user-defined function definition:**</span></span>

```
function main(x) {
return JSON.stringify(x);
}
```

<span data-ttu-id="32bfd-190">**範例查詢︰**</span><span class="sxs-lookup"><span data-stu-id="32bfd-190">**Sample query:**</span></span>
```
SELECT
    DataString,
    DataValue,
    HexValue,
    UDF.json_stringify(input) As InputEvent
INTO
    output
FROM
    input PARTITION BY PARTITIONID
```

## <a name="get-help"></a><span data-ttu-id="32bfd-191">取得說明</span><span class="sxs-lookup"><span data-stu-id="32bfd-191">Get help</span></span>
<span data-ttu-id="32bfd-192">如需其他協助，請參閱我們的 [Azure 串流分析論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。</span><span class="sxs-lookup"><span data-stu-id="32bfd-192">For additional help, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="32bfd-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="32bfd-193">Next steps</span></span>
* [<span data-ttu-id="32bfd-194">簡介 tooAzure 資料流分析</span><span class="sxs-lookup"><span data-stu-id="32bfd-194">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="32bfd-195">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="32bfd-195">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="32bfd-196">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="32bfd-196">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="32bfd-197">Azure 串流分析查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="32bfd-197">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="32bfd-198">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="32bfd-198">Azure Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
