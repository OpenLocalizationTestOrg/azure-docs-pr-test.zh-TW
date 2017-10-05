---
title: "如何在串流分析中編寫查詢 | Microsoft Docs"
description: "在串流分析中編寫查詢及查詢資料 | 學習路徑區段。"
keywords: "如何編寫查詢, 查詢資料, 編寫查詢, 編寫查詢"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0e9cdadd-0ee0-4bee-b65b-4a06fb863c95
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: b44b0658a06761a805708e7fdeba9e3b2cf9d3ab
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-write-queries-in-stream-analytics"></a><span data-ttu-id="8b461-104">如何在串流分析中撰寫查詢</span><span class="sxs-lookup"><span data-stu-id="8b461-104">How to write queries in Stream Analytics</span></span>
<span data-ttu-id="8b461-105">在 Azure 串流分析中編寫串流處理邏輯的查詢會實作為「常設查詢」，它在工作開始前就已經獲得定義，且會在到達工作時針對資料來執行。</span><span class="sxs-lookup"><span data-stu-id="8b461-105">Writing queries for stream processing logic in Azure Stream Analytics is implemented as a "standing query" that is defined before a job starts and executed on data as it reaches the job.</span></span> <span data-ttu-id="8b461-106">資料轉換會以類似 SQL 的查詢語言來表示，大部分是 T-SQL 子集並加入某些語言擴充功能 (例如 [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) ) 來表示時間語意。</span><span class="sxs-lookup"><span data-stu-id="8b461-106">The data transformation is expressed in a SQL-like query language, which is largely a subset of T-SQL with some added language extensions like [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) used to express temporal semantics.</span></span>

## <a name="writing-queries"></a><span data-ttu-id="8b461-107">編寫查詢：</span><span class="sxs-lookup"><span data-stu-id="8b461-107">Writing Queries:</span></span>
1. <span data-ttu-id="8b461-108">在 Azure 管理入口網站的串流分析工作中，按一下 [查詢] 。</span><span class="sxs-lookup"><span data-stu-id="8b461-108">In your Stream Analytics Job in the Azure Management portal, click **Query**.</span></span>
   
    ![選取查詢](./media/stream-analytics-write-queries/1-stream-analytics-write-queries.png)  
   
    <span data-ttu-id="8b461-110">在 Azure 入口網站，按一下 [查詢] 。</span><span class="sxs-lookup"><span data-stu-id="8b461-110">In the Azure Portal, click **Query**.</span></span>
   
    ![選取查詢預覽](./media/stream-analytics-write-queries/query-preview-portal.png)  
2. <span data-ttu-id="8b461-112">新工作有可以協助您入門的查詢範本。</span><span class="sxs-lookup"><span data-stu-id="8b461-112">New jobs have a query template to help get you started.</span></span> <span data-ttu-id="8b461-113">查詢範本會執行「傳遞」查詢，其會將所有欄位從輸入事件投影至輸出中。</span><span class="sxs-lookup"><span data-stu-id="8b461-113">The query template performs a "pass-through" query that projects all fields from input events into the output.</span></span>  
   
   * <span data-ttu-id="8b461-114">如果您已經為工作定義了至少一個輸入和輸出，便可以將預留位置 "[YourOutputAlias]" 和 "[YourInputAlias]" 欄位取代為您想先用的輸入與輸出別名。</span><span class="sxs-lookup"><span data-stu-id="8b461-114">If you have defined at least one input and output for your job, you can replace the placeholder "[YourOutputAlias]" and "[YourInputAlias]" fields with the aliases of the input and output that you wish use first.</span></span> <span data-ttu-id="8b461-115">此外，您仍可在 Azure  傳統入口網站中撰寫並測試您的查詢，而不需在工作中定義輸入及輸出。</span><span class="sxs-lookup"><span data-stu-id="8b461-115">In addition, you can still author and test your query in the Azure Classic Portal without defining inputs and outputs on the job.</span></span>
   * <span data-ttu-id="8b461-116">如果您想要執行比簡單的傳遞更多的處理，您可以編輯查詢定義。</span><span class="sxs-lookup"><span data-stu-id="8b461-116">If you wish to perform more processing than a simple pass-through, you can edit the query definition.</span></span> <span data-ttu-id="8b461-117">若要開始撰寫查詢，請到 [這裡](stream-analytics-stream-analytics-query-patterns.md)看看一些擷取的常見查詢模式。</span><span class="sxs-lookup"><span data-stu-id="8b461-117">To get started with query authoring, take a look at some common query patterns are captured [here](stream-analytics-stream-analytics-query-patterns.md).</span></span>  
   
   ![查詢資料視窗](./media/stream-analytics-write-queries/2-stream-analytics-write-queries.png)  

## <a name="to-validate-query-data-is-working"></a><span data-ttu-id="8b461-119">如何驗證查詢資料在運作中：</span><span class="sxs-lookup"><span data-stu-id="8b461-119">To validate query data is working:</span></span>
<span data-ttu-id="8b461-120">您可以透過在瀏覽器中執行一或多個包含測試資料的本機 JSON 檔案，來測試查詢是否如預期執行。</span><span class="sxs-lookup"><span data-stu-id="8b461-120">You can test that your query behaves as expected by running it in the browser over one or more local JSON files containing test data.</span></span> <span data-ttu-id="8b461-121">這不會開始工作，也不會以任何方式計費。</span><span class="sxs-lookup"><span data-stu-id="8b461-121">This will not start the job or have any billing implications.</span></span>

> [!NOTE]
> <span data-ttu-id="8b461-122">Azure 入口網站目前不支援瀏覽器內查詢測試。</span><span class="sxs-lookup"><span data-stu-id="8b461-122">Currently in-browser query testing is not supported in the Azure Portal.</span></span>  
> 
> 

1. <span data-ttu-id="8b461-123">請確定查詢中沒有任何錯誤 (否則 [測試] 按鈕將會停用) 然後按一下 [測試] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8b461-123">Make sure that there are no errors in the query (otherwise the Test button will be disabled) and then click the Test button.</span></span>  
   
   ![查詢資料測試](./media/stream-analytics-write-queries/3-stream-analytics-write-queries.png)  
2. <span data-ttu-id="8b461-125">將會提示您將檔案指定給在查詢中被參考的每個輸入。</span><span class="sxs-lookup"><span data-stu-id="8b461-125">You will be prompted to specify files for each of the inputs referenced in the query.</span></span> <span data-ttu-id="8b461-126">在此範例中，範本查詢將維持現狀，所以對話方塊提示會提示輸入名為 "yourinputalias" 的輸入。</span><span class="sxs-lookup"><span data-stu-id="8b461-126">In this example, the template query is left as-is, so the dialog is prompting for an input named "yourinputalias".</span></span>  
   
   ![輪詢資料查詢](./media/stream-analytics-write-queries/4-stream-analytics-write-queries.png)  
3. <span data-ttu-id="8b461-128">瀏覽至測試檔案。</span><span class="sxs-lookup"><span data-stu-id="8b461-128">Browse to a test file.</span></span> <span data-ttu-id="8b461-129">[GitHub](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) 上有幾個範例檔案，而您也可以透過輸入索引標籤上的範例資料函式，從您自己的資料流輸入來擷取範例資料。</span><span class="sxs-lookup"><span data-stu-id="8b461-129">Several sample files are available on [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) and you can also retrieve sample data from your own data stream inputs via the Sample Data function on the inputs tab.</span></span>  
   
   ![查詢輸入](./media/stream-analytics-write-queries/5-stream-analytics-write-queries.png)  
4. <span data-ttu-id="8b461-131">關閉對話方塊之後，將會針對測試資料執行查詢，而您可在 [查詢] 頁面底部查看結果。</span><span class="sxs-lookup"><span data-stu-id="8b461-131">After closing the dialog, your query will be run over the test data and you will see the results at the bottom of the Query page.</span></span>  
   
   ![查詢摘要](./media/stream-analytics-write-queries/6-stream-analytics-write-queries.png)  

## <a name="get-help"></a><span data-ttu-id="8b461-133">取得說明</span><span class="sxs-lookup"><span data-stu-id="8b461-133">Get help</span></span>
<span data-ttu-id="8b461-134">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="8b461-134">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b461-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8b461-135">Next steps</span></span>
* [<span data-ttu-id="8b461-136">Azure Stream Analytics 介紹</span><span class="sxs-lookup"><span data-stu-id="8b461-136">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="8b461-137">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8b461-137">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="8b461-138">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="8b461-138">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="8b461-139">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="8b461-139">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="8b461-140">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="8b461-140">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

