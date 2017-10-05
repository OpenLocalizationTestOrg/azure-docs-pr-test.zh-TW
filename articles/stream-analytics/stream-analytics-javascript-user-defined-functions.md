---
title: "Azure 串流分析 JavaScript 使用者定義函式 | Microsoft Docs"
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
ms.openlocfilehash: e4a9e6c7078031240c22a51378c0459426b7f626
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-stream-analytics-javascript-user-defined-functions"></a><span data-ttu-id="8fa9a-104">Azure 串流分析 JavaScript 使用者定義函式</span><span class="sxs-lookup"><span data-stu-id="8fa9a-104">Azure Stream Analytics JavaScript user-defined functions</span></span>
<span data-ttu-id="8fa9a-105">Azure 串流分析支援以 JavaScript 撰寫的使用者定義函式。</span><span class="sxs-lookup"><span data-stu-id="8fa9a-105">Azure Stream Analytics supports user-defined functions written in JavaScript.</span></span> <span data-ttu-id="8fa9a-106">JavaScript 提供豐富的 **String**、**RegExp**、**Math**、**Array** 和 **Date** 方法，可讓使用串流分析作業建立複雜的資料轉換變得更容易。</span><span class="sxs-lookup"><span data-stu-id="8fa9a-106">With the rich set of **String**, **RegExp**, **Math**, **Array**, and **Date** methods that JavaScript provides, complex data transformations with Stream Analytics jobs become easier to create.</span></span>

## <a name="javascript-user-defined-functions"></a><span data-ttu-id="8fa9a-107">JavaScript 使用者定義函式</span><span class="sxs-lookup"><span data-stu-id="8fa9a-107">JavaScript user-defined functions</span></span>
<span data-ttu-id="8fa9a-108">JavaScript 使用者定義的函式支援無狀態且只做為計算用途的純量函式，而且不需要外部連線能力。</span><span class="sxs-lookup"><span data-stu-id="8fa9a-108">JavaScript user-defined functions support stateless, compute-only scalar functions that do not require external connectivity.</span></span> <span data-ttu-id="8fa9a-109">函數的傳回值只能是純量 (單一) 值。</span><span class="sxs-lookup"><span data-stu-id="8fa9a-109">The return value of a function can only be a scalar (single) value.</span></span> <span data-ttu-id="8fa9a-110">將 JavaScript 使用者定義函式新增至作業之後，您可以在查詢中的任何位置使用函式，就像是內建的純量函式。</span><span class="sxs-lookup"><span data-stu-id="8fa9a-110">After you add a JavaScript user-defined function to a job, you can use the function anywhere in the query, like a built-in scalar function.</span></span>

<span data-ttu-id="8fa9a-111">從以下的一些案例可以看出 JavaScript 使用者定義函式很實用：</span><span class="sxs-lookup"><span data-stu-id="8fa9a-111">Here are some scenarios where you might find JavaScript user-defined functions useful:</span></span>
* <span data-ttu-id="8fa9a-112">剖析及操作具有規則運算式函式的字串，例如：**Regexp_Replace()** 和 **Regexp_Extract()**</span><span class="sxs-lookup"><span data-stu-id="8fa9a-112">Parsing and manipulating strings that have regular expression functions, for example, **Regexp_Replace()** and **Regexp_Extract()**</span></span>
* <span data-ttu-id="8fa9a-113">解碼和編碼資料，例如：從二進位轉換成十六進位</span><span class="sxs-lookup"><span data-stu-id="8fa9a-113">Decoding and encoding data, for example, binary-to-hex conversion</span></span>
* <span data-ttu-id="8fa9a-114">使用 JavaScript **Math** 函式做數學運算</span><span class="sxs-lookup"><span data-stu-id="8fa9a-114">Performing mathematic computations with JavaScript **Math** functions</span></span>
* <span data-ttu-id="8fa9a-115">執行陣列作業，例如，排序、連結、尋找及填入</span><span class="sxs-lookup"><span data-stu-id="8fa9a-115">Performing array operations like sort, join, find, and fill</span></span>

<span data-ttu-id="8fa9a-116">以下是一些在串流分析中無法使用 JavaScript 使用者定義函式達成的事項：</span><span class="sxs-lookup"><span data-stu-id="8fa9a-116">Here are some things that you cannot do with a JavaScript user-defined function in Stream Analytics:</span></span>
* <span data-ttu-id="8fa9a-117">呼叫外部 REST 端點，例如，執行反向 IP 查詢或從外部來源提取參考資料</span><span class="sxs-lookup"><span data-stu-id="8fa9a-117">Call out external REST endpoints, for example, performing reverse IP lookup or pulling reference data from an external source</span></span>
* <span data-ttu-id="8fa9a-118">對輸入/輸出執行自訂事件格式序列化或還原序列化</span><span class="sxs-lookup"><span data-stu-id="8fa9a-118">Perform custom event format serialization or deserialization on inputs/outputs</span></span>
* <span data-ttu-id="8fa9a-119">建立自訂彙總</span><span class="sxs-lookup"><span data-stu-id="8fa9a-119">Create custom aggregates</span></span>

<span data-ttu-id="8fa9a-120">雖然沒有在函式定義中封鎖 **Date.GetDate()** 或 **Math.random()** 等函式，您仍應避免使用它們。</span><span class="sxs-lookup"><span data-stu-id="8fa9a-120">Although functions like **Date.GetDate()** or **Math.random()** are not blocked in the functions definition, you should avoid using them.</span></span> <span data-ttu-id="8fa9a-121">這些函式**不會**在每次呼叫時都傳回同樣的結果，且「串流分析」服務不會記錄函式叫用和傳回值的日誌。</span><span class="sxs-lookup"><span data-stu-id="8fa9a-121">These functions **do not** return the same result every time you call them, and the Azure Stream Analytics service does not keep a journal of function invocations and returned results.</span></span> <span data-ttu-id="8fa9a-122">若函式針對同樣事件傳回不同的值，當您或串流分析重新啟動某作業之後，將不保證它具有可重覆性。</span><span class="sxs-lookup"><span data-stu-id="8fa9a-122">If a function returns different result on the same events, repeatability is not guaranteed when a job is restarted by you or by the Stream Analytics service.</span></span>

## <a name="add-a-javascript-user-defined-function-in-the-azure-portal"></a><span data-ttu-id="8fa9a-123">在 Azure 入口網站中新增 JavaScript 使用者定義函式</span><span class="sxs-lookup"><span data-stu-id="8fa9a-123">Add a JavaScript user-defined function in the Azure portal</span></span>
<span data-ttu-id="8fa9a-124">若要在現有串流分析作業下建立簡單的 JavaScript 使用者定義函式，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="8fa9a-124">To create a simple JavaScript user-defined function under an existing Stream Analytics job, do these steps:</span></span>

1.  <span data-ttu-id="8fa9a-125">在 Azure 入口網站中，找出您的串流分析作業。</span><span class="sxs-lookup"><span data-stu-id="8fa9a-125">In the Azure portal, find your Stream Analytics job.</span></span>
2.  <span data-ttu-id="8fa9a-126">在 [作業拓撲] 下，選取您的函式。</span><span class="sxs-lookup"><span data-stu-id="8fa9a-126">Under **JOB TOPOLOGY**, select your function.</span></span> <span data-ttu-id="8fa9a-127">空白的函式清單隨即出現。</span><span class="sxs-lookup"><span data-stu-id="8fa9a-127">An empty list of functions appears.</span></span>
3.  <span data-ttu-id="8fa9a-128">若要建立新的使用者定義函式，請選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="8fa9a-128">To create a new user-defined function, select **Add**.</span></span>
4.  <span data-ttu-id="8fa9a-129">在 [新增函式] 刀鋒視窗中，針對 [函式類型]，選取 [JavaScript]。</span><span class="sxs-lookup"><span data-stu-id="8fa9a-129">On the **New Function** blade, for **Function Type**, select **JavaScript**.</span></span> <span data-ttu-id="8fa9a-130">預設的函式範本會出現在編輯器中。</span><span class="sxs-lookup"><span data-stu-id="8fa9a-130">A default function template appears in the editor.</span></span>
5.  <span data-ttu-id="8fa9a-131">針對 **UDF 別名**，輸入 **hex2Int**，並變更函式實作，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8fa9a-131">For the **UDF alias**, enter **hex2Int**, and change the function implementation as follows:</span></span>

    ```
    // Convert Hex value to integer.
    function main(hexValue) {
        return parseInt(hexValue, 16);
    }
    ```

6.  <span data-ttu-id="8fa9a-132">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="8fa9a-132">Select **Save**.</span></span> <span data-ttu-id="8fa9a-133">您的函式會出現在函式的清單中。</span><span class="sxs-lookup"><span data-stu-id="8fa9a-133">Your function appears in the list of functions.</span></span>
7.  <span data-ttu-id="8fa9a-134">選取新的 **hex2Int** 函式，並檢查函式定義。</span><span class="sxs-lookup"><span data-stu-id="8fa9a-134">Select the new **hex2Int** function, and check the function definition.</span></span> <span data-ttu-id="8fa9a-135">所有函式必須在函式別名前端新增 **UDF** 前置詞。</span><span class="sxs-lookup"><span data-stu-id="8fa9a-135">All functions have a **UDF** prefix added to the function alias.</span></span> <span data-ttu-id="8fa9a-136">在串流分析查詢中呼叫函式時，您需要*包含前置詞*。</span><span class="sxs-lookup"><span data-stu-id="8fa9a-136">You need to *include the prefix* when you call the function in your Stream Analytics query.</span></span> <span data-ttu-id="8fa9a-137">在此情況下，您會呼叫 **UDF.hex2Int**。</span><span class="sxs-lookup"><span data-stu-id="8fa9a-137">In this case, you call **UDF.hex2Int**.</span></span>

## <a name="call-a-javascript-user-defined-function-in-a-query"></a><span data-ttu-id="8fa9a-138">在查詢中呼叫 JavaScript 使用者定義函式</span><span class="sxs-lookup"><span data-stu-id="8fa9a-138">Call a JavaScript user-defined function in a query</span></span>

1. <span data-ttu-id="8fa9a-139">在查詢編輯器中，於 [作業拓撲] 下，選取 [查詢]。</span><span class="sxs-lookup"><span data-stu-id="8fa9a-139">In the query editor, under **JOB TOPOLOGY**, select **Query**.</span></span>
2.  <span data-ttu-id="8fa9a-140">編輯您的查詢，然後呼叫使用者定義函式，就像這樣：</span><span class="sxs-lookup"><span data-stu-id="8fa9a-140">Edit your query, and then call the user-defined function, like this:</span></span>

    ```
    SELECT
        time,
        UDF.hex2Int(offset) AS IntOffset
    INTO
        output
    FROM
        InputStream
    ```

3.  <span data-ttu-id="8fa9a-141">若要上傳範例資料檔案，請以滑鼠右鍵按一下作業輸入。</span><span class="sxs-lookup"><span data-stu-id="8fa9a-141">To upload the sample data file, right-click the job input.</span></span>
4.  <span data-ttu-id="8fa9a-142">若要測試您的查詢，請選取 [測試]。</span><span class="sxs-lookup"><span data-stu-id="8fa9a-142">To test your query, select **Test**.</span></span>


## <a name="supported-javascript-objects"></a><span data-ttu-id="8fa9a-143">支援的 JavaScript 物件</span><span class="sxs-lookup"><span data-stu-id="8fa9a-143">Supported JavaScript objects</span></span>
<span data-ttu-id="8fa9a-144">Azure 串流分析 JavaScript 使用者定義函式支援標準的內建 JavaScript 物件。</span><span class="sxs-lookup"><span data-stu-id="8fa9a-144">Azure Stream Analytics JavaScript user-defined functions support standard, built-in JavaScript objects.</span></span> <span data-ttu-id="8fa9a-145">如需這些物件的清單，請參閱[全域物件](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects)。</span><span class="sxs-lookup"><span data-stu-id="8fa9a-145">For a list of these objects, see [Global Objects](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).</span></span>

### <a name="stream-analytics-and-javascript-type-conversion"></a><span data-ttu-id="8fa9a-146">串流分析與 JavaScript 類型轉換</span><span class="sxs-lookup"><span data-stu-id="8fa9a-146">Stream Analytics and JavaScript type conversion</span></span>

<span data-ttu-id="8fa9a-147">串流分析查詢語言與 JavaScript 支援的類型有一些差異。</span><span class="sxs-lookup"><span data-stu-id="8fa9a-147">There are differences in the types that the Stream Analytics query language and JavaScript support.</span></span> <span data-ttu-id="8fa9a-148">此表列出兩者之間的轉換對應：</span><span class="sxs-lookup"><span data-stu-id="8fa9a-148">This table lists the conversion mappings between the two:</span></span>

<span data-ttu-id="8fa9a-149">串流分析</span><span class="sxs-lookup"><span data-stu-id="8fa9a-149">Stream Analytics</span></span> | <span data-ttu-id="8fa9a-150">JavaScript</span><span class="sxs-lookup"><span data-stu-id="8fa9a-150">JavaScript</span></span>
--- | ---
<span data-ttu-id="8fa9a-151">bigint</span><span class="sxs-lookup"><span data-stu-id="8fa9a-151">bigint</span></span> | <span data-ttu-id="8fa9a-152">Number (JavaScript 只能準確地表示最高到 2^53 的整數)</span><span class="sxs-lookup"><span data-stu-id="8fa9a-152">Number (JavaScript can only represent integers up to precisely 2^53)</span></span>
<span data-ttu-id="8fa9a-153">DateTime</span><span class="sxs-lookup"><span data-stu-id="8fa9a-153">DateTime</span></span> | <span data-ttu-id="8fa9a-154">Date (JavaScript 只支援毫秒)</span><span class="sxs-lookup"><span data-stu-id="8fa9a-154">Date (JavaScript only supports milliseconds)</span></span>
<span data-ttu-id="8fa9a-155">double</span><span class="sxs-lookup"><span data-stu-id="8fa9a-155">double</span></span> | <span data-ttu-id="8fa9a-156">Number</span><span class="sxs-lookup"><span data-stu-id="8fa9a-156">Number</span></span>
<span data-ttu-id="8fa9a-157">nvarchar(MAX)</span><span class="sxs-lookup"><span data-stu-id="8fa9a-157">nvarchar(MAX)</span></span> | <span data-ttu-id="8fa9a-158">String</span><span class="sxs-lookup"><span data-stu-id="8fa9a-158">String</span></span>
<span data-ttu-id="8fa9a-159">Record</span><span class="sxs-lookup"><span data-stu-id="8fa9a-159">Record</span></span> | <span data-ttu-id="8fa9a-160">Object</span><span class="sxs-lookup"><span data-stu-id="8fa9a-160">Object</span></span>
<span data-ttu-id="8fa9a-161">陣列</span><span class="sxs-lookup"><span data-stu-id="8fa9a-161">Array</span></span> | <span data-ttu-id="8fa9a-162">陣列</span><span class="sxs-lookup"><span data-stu-id="8fa9a-162">Array</span></span>
<span data-ttu-id="8fa9a-163">NULL</span><span class="sxs-lookup"><span data-stu-id="8fa9a-163">NULL</span></span> | <span data-ttu-id="8fa9a-164">Null</span><span class="sxs-lookup"><span data-stu-id="8fa9a-164">Null</span></span>


<span data-ttu-id="8fa9a-165">以下是 JavaScript 至串流分析的轉換：</span><span class="sxs-lookup"><span data-stu-id="8fa9a-165">Here are JavaScript-to-Stream Analytics conversions:</span></span>


<span data-ttu-id="8fa9a-166">JavaScript</span><span class="sxs-lookup"><span data-stu-id="8fa9a-166">JavaScript</span></span> | <span data-ttu-id="8fa9a-167">串流分析</span><span class="sxs-lookup"><span data-stu-id="8fa9a-167">Stream Analytics</span></span>
--- | ---
<span data-ttu-id="8fa9a-168">數字</span><span class="sxs-lookup"><span data-stu-id="8fa9a-168">Number</span></span> | <span data-ttu-id="8fa9a-169">Bigint (若數字為整數且介於 long.MinValue 和 long.MaxValue 之間，否則為 double)</span><span class="sxs-lookup"><span data-stu-id="8fa9a-169">Bigint (if the number is round and between long.MinValue and long.MaxValue; otherwise, it's double)</span></span>
<span data-ttu-id="8fa9a-170">日期</span><span class="sxs-lookup"><span data-stu-id="8fa9a-170">Date</span></span> | <span data-ttu-id="8fa9a-171">DateTime</span><span class="sxs-lookup"><span data-stu-id="8fa9a-171">DateTime</span></span>
<span data-ttu-id="8fa9a-172">String</span><span class="sxs-lookup"><span data-stu-id="8fa9a-172">String</span></span> | <span data-ttu-id="8fa9a-173">nvarchar(MAX)</span><span class="sxs-lookup"><span data-stu-id="8fa9a-173">nvarchar(MAX)</span></span>
<span data-ttu-id="8fa9a-174">Object</span><span class="sxs-lookup"><span data-stu-id="8fa9a-174">Object</span></span> | <span data-ttu-id="8fa9a-175">Record</span><span class="sxs-lookup"><span data-stu-id="8fa9a-175">Record</span></span>
<span data-ttu-id="8fa9a-176">陣列</span><span class="sxs-lookup"><span data-stu-id="8fa9a-176">Array</span></span> | <span data-ttu-id="8fa9a-177">陣列</span><span class="sxs-lookup"><span data-stu-id="8fa9a-177">Array</span></span>
<span data-ttu-id="8fa9a-178">Null、Undefined</span><span class="sxs-lookup"><span data-stu-id="8fa9a-178">Null, Undefined</span></span> | <span data-ttu-id="8fa9a-179">NULL</span><span class="sxs-lookup"><span data-stu-id="8fa9a-179">NULL</span></span>
<span data-ttu-id="8fa9a-180">任何其他類型 (例如，函式或錯誤)</span><span class="sxs-lookup"><span data-stu-id="8fa9a-180">Any other type (for example, a function or error)</span></span> | <span data-ttu-id="8fa9a-181">不支援 (產生執行階段錯誤)</span><span class="sxs-lookup"><span data-stu-id="8fa9a-181">Not supported (results in runtime error)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="8fa9a-182">疑難排解</span><span class="sxs-lookup"><span data-stu-id="8fa9a-182">Troubleshooting</span></span>
<span data-ttu-id="8fa9a-183">JavaScript 執行階段錯誤會被視為嚴重問題，並顯示在活動記錄。</span><span class="sxs-lookup"><span data-stu-id="8fa9a-183">JavaScript runtime errors are considered fatal, and are surfaced through the Activity log.</span></span> <span data-ttu-id="8fa9a-184">若要擷取記錄檔，在 Azure 入口網站中，請移至您的作業並選取 [活動記錄]。</span><span class="sxs-lookup"><span data-stu-id="8fa9a-184">To retrieve the log, in the Azure portal, go to your job and select **Activity log**.</span></span>


## <a name="other-javascript-user-defined-function-patterns"></a><span data-ttu-id="8fa9a-185">其他 JavaScript 使用者定義函式模式</span><span class="sxs-lookup"><span data-stu-id="8fa9a-185">Other JavaScript user-defined function patterns</span></span>

### <a name="write-nested-json-to-output"></a><span data-ttu-id="8fa9a-186">將巢狀 JSON 寫入至輸出</span><span class="sxs-lookup"><span data-stu-id="8fa9a-186">Write nested JSON to output</span></span>
<span data-ttu-id="8fa9a-187">如果您的後續處理步驟使用串流分析作業輸出做為輸入，且其需要 JSON 格式，您可以將 JSON 字串寫入至輸出。</span><span class="sxs-lookup"><span data-stu-id="8fa9a-187">If you have a follow-up processing step that uses a Stream Analytics job output as input, and it requires a JSON format, you can write a JSON string to output.</span></span> <span data-ttu-id="8fa9a-188">以下範例會呼叫 **JSON.stringify()** 函式以包裝所有輸入的名稱/值對，並將它們以單一字串值於輸出中寫入。</span><span class="sxs-lookup"><span data-stu-id="8fa9a-188">The next example calls the **JSON.stringify()** function to pack all name/value pairs of the input, and then write them as a single string value in output.</span></span>

<span data-ttu-id="8fa9a-189">**JavaScript 使用者定義函式定義：**</span><span class="sxs-lookup"><span data-stu-id="8fa9a-189">**JavaScript user-defined function definition:**</span></span>

```
function main(x) {
return JSON.stringify(x);
}
```

<span data-ttu-id="8fa9a-190">**範例查詢︰**</span><span class="sxs-lookup"><span data-stu-id="8fa9a-190">**Sample query:**</span></span>
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

## <a name="get-help"></a><span data-ttu-id="8fa9a-191">取得說明</span><span class="sxs-lookup"><span data-stu-id="8fa9a-191">Get help</span></span>
<span data-ttu-id="8fa9a-192">如需其他協助，請參閱我們的 [Azure 串流分析論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。</span><span class="sxs-lookup"><span data-stu-id="8fa9a-192">For additional help, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8fa9a-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8fa9a-193">Next steps</span></span>
* [<span data-ttu-id="8fa9a-194">Azure Stream Analytics 介紹</span><span class="sxs-lookup"><span data-stu-id="8fa9a-194">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="8fa9a-195">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8fa9a-195">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="8fa9a-196">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="8fa9a-196">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="8fa9a-197">Azure 串流分析查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="8fa9a-197">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="8fa9a-198">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="8fa9a-198">Azure Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
