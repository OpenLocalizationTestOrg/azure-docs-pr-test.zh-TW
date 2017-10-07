---
title: "在 Stream Analytics aaaHow toowrite 查詢 |Microsoft 文件"
description: "在串流分析中編寫查詢及查詢資料 | 學習路徑區段。"
keywords: "toowrite 查詢、 查詢的資料、 如何撰寫查詢時，撰寫查詢"
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
ms.openlocfilehash: b943c34f10afd2b21789afbd341c471a5f168729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowrite-queries-in-stream-analytics"></a><span data-ttu-id="da449-104">Toowrite 在 Stream Analytics 中查詢的方式</span><span class="sxs-lookup"><span data-stu-id="da449-104">How toowrite queries in Stream Analytics</span></span>
<span data-ttu-id="da449-105">撰寫資料流處理邏輯，在 Azure Stream Analytics 查詢會實作為 「 常設查詢 」 工作開始的資料到達 hello 作業執行之前所定義。</span><span class="sxs-lookup"><span data-stu-id="da449-105">Writing queries for stream processing logic in Azure Stream Analytics is implemented as a "standing query" that is defined before a job starts and executed on data as it reaches hello job.</span></span> <span data-ttu-id="da449-106">hello 資料轉換是類似 SQL 的查詢語言表達，這是大部分 T-SQL 某些子集新增語言擴充功能，例如[Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx)用 tooexpress 時態語意。</span><span class="sxs-lookup"><span data-stu-id="da449-106">hello data transformation is expressed in a SQL-like query language, which is largely a subset of T-SQL with some added language extensions like [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) used tooexpress temporal semantics.</span></span>

## <a name="writing-queries"></a><span data-ttu-id="da449-107">編寫查詢：</span><span class="sxs-lookup"><span data-stu-id="da449-107">Writing Queries:</span></span>
1. <span data-ttu-id="da449-108">在資料流分析工作 hello Azure 管理入口網站中，按一下**查詢**。</span><span class="sxs-lookup"><span data-stu-id="da449-108">In your Stream Analytics Job in hello Azure Management portal, click **Query**.</span></span>
   
    ![選取查詢](./media/stream-analytics-write-queries/1-stream-analytics-write-queries.png)  
   
    <span data-ttu-id="da449-110">在 hello Azure 入口網站，按一下 **查詢**。</span><span class="sxs-lookup"><span data-stu-id="da449-110">In hello Azure Portal, click **Query**.</span></span>
   
    ![選取查詢預覽](./media/stream-analytics-write-queries/query-preview-portal.png)  
2. <span data-ttu-id="da449-112">新的作業會讓您開始使用查詢範本 toohelp。</span><span class="sxs-lookup"><span data-stu-id="da449-112">New jobs have a query template toohelp get you started.</span></span> <span data-ttu-id="da449-113">hello 查詢範本會執行 「 通過 」 查詢 hello 輸出至該專案中輸入事件的所有欄位。</span><span class="sxs-lookup"><span data-stu-id="da449-113">hello query template performs a "pass-through" query that projects all fields from input events into hello output.</span></span>  
   
   * <span data-ttu-id="da449-114">如果您已經定義至少一個輸入和輸出工作，您可以取代 hello 預留位置"[YourOutputAlias]"和"[YourInputAlias]"欄位的輸入和輸出 [您希望使用先 hello hello 別名。</span><span class="sxs-lookup"><span data-stu-id="da449-114">If you have defined at least one input and output for your job, you can replace hello placeholder "[YourOutputAlias]" and "[YourInputAlias]" fields with hello aliases of hello input and output that you wish use first.</span></span> <span data-ttu-id="da449-115">此外，您仍然可以撰寫，並在 hello Azure 傳統入口網站中測試您的查詢，而不需 hello 工作定義輸入和輸出。</span><span class="sxs-lookup"><span data-stu-id="da449-115">In addition, you can still author and test your query in hello Azure Classic Portal without defining inputs and outputs on hello job.</span></span>
   * <span data-ttu-id="da449-116">如果您想 tooperform 更多的處理，比簡單的傳遞，您可以編輯 hello 查詢定義。</span><span class="sxs-lookup"><span data-stu-id="da449-116">If you wish tooperform more processing than a simple pass-through, you can edit hello query definition.</span></span> <span data-ttu-id="da449-117">撰寫查詢，開始 tooget 看看一些常用的查詢擷取模式[這裡](stream-analytics-stream-analytics-query-patterns.md)。</span><span class="sxs-lookup"><span data-stu-id="da449-117">tooget started with query authoring, take a look at some common query patterns are captured [here](stream-analytics-stream-analytics-query-patterns.md).</span></span>  
   
   ![查詢資料視窗](./media/stream-analytics-write-queries/2-stream-analytics-write-queries.png)  

## <a name="toovalidate-query-data-is-working"></a><span data-ttu-id="da449-119">正在 toovalidate 查詢資料：</span><span class="sxs-lookup"><span data-stu-id="da449-119">toovalidate query data is working:</span></span>
<span data-ttu-id="da449-120">您可以測試您的查詢行為如預期般 hello 瀏覽器中執行一或多個本機 JSON 檔案包含測試資料。</span><span class="sxs-lookup"><span data-stu-id="da449-120">You can test that your query behaves as expected by running it in hello browser over one or more local JSON files containing test data.</span></span> <span data-ttu-id="da449-121">這不會啟動 hello 作業，或是有任何的計費影響。</span><span class="sxs-lookup"><span data-stu-id="da449-121">This will not start hello job or have any billing implications.</span></span>

> [!NOTE]
> <span data-ttu-id="da449-122">目前瀏覽器中查詢不支援測試 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="da449-122">Currently in-browser query testing is not supported in hello Azure Portal.</span></span>  
> 
> 

1. <span data-ttu-id="da449-123">請確定 hello （否則 hello [測試] 按鈕將會停用） 的查詢中沒有任何錯誤，然後按一下hello [測試] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="da449-123">Make sure that there are no errors in hello query (otherwise hello Test button will be disabled) and then click hello Test button.</span></span>  
   
   ![查詢資料測試](./media/stream-analytics-write-queries/3-stream-analytics-write-queries.png)  
2. <span data-ttu-id="da449-125">您將會針對每個 hello 輸入 hello 查詢中參考的提示的 toospecify 檔案。</span><span class="sxs-lookup"><span data-stu-id="da449-125">You will be prompted toospecify files for each of hello inputs referenced in hello query.</span></span> <span data-ttu-id="da449-126">在此範例中，hello 範本查詢就會維持為是，因此 hello 對話方塊會提示輸入名為"yourinputalias"。</span><span class="sxs-lookup"><span data-stu-id="da449-126">In this example, hello template query is left as-is, so hello dialog is prompting for an input named "yourinputalias".</span></span>  
   
   ![輪詢資料查詢](./media/stream-analytics-write-queries/4-stream-analytics-write-queries.png)  
3. <span data-ttu-id="da449-128">瀏覽 tooa 測試檔案。</span><span class="sxs-lookup"><span data-stu-id="da449-128">Browse tooa test file.</span></span> <span data-ttu-id="da449-129">會提供數個範例檔案[github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) ，您也可以從您自己的資料資料流輸入 hello hello 輸入 索引標籤上的範例資料函式透過擷取資料範例。</span><span class="sxs-lookup"><span data-stu-id="da449-129">Several sample files are available on [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) and you can also retrieve sample data from your own data stream inputs via hello Sample Data function on hello inputs tab.</span></span>  
   
   ![查詢輸入](./media/stream-analytics-write-queries/5-stream-analytics-write-queries.png)  
4. <span data-ttu-id="da449-131">在關閉之後 hello 對話方塊，您的查詢將會執行 hello 測試資料，您會看到在 hello hello [查詢] 頁面底部的 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="da449-131">After closing hello dialog, your query will be run over hello test data and you will see hello results at hello bottom of hello Query page.</span></span>  
   
   ![查詢摘要](./media/stream-analytics-write-queries/6-stream-analytics-write-queries.png)  

## <a name="get-help"></a><span data-ttu-id="da449-133">取得說明</span><span class="sxs-lookup"><span data-stu-id="da449-133">Get help</span></span>
<span data-ttu-id="da449-134">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="da449-134">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="da449-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="da449-135">Next steps</span></span>
* [<span data-ttu-id="da449-136">簡介 tooAzure 資料流分析</span><span class="sxs-lookup"><span data-stu-id="da449-136">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="da449-137">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="da449-137">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="da449-138">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="da449-138">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="da449-139">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="da449-139">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="da449-140">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="da449-140">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

