---
title: "使用 SELECT INTO 對 Azure 串流分析查詢進行偵錯 | Microsoft Docs"
description: "在串流分析中使用 SELECT INTO 陳述式對進行中的查詢進行資料取樣"
keywords: 
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: b05222c6d6f4fc2c5b847dd75ff7e29352cd538c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="debug-queries-by-using-select-into-statements"></a><span data-ttu-id="1d5ab-103">使用 SELECT INTO 陳述式對查詢進行偵錯</span><span class="sxs-lookup"><span data-stu-id="1d5ab-103">Debug queries by using SELECT INTO statements</span></span>

<span data-ttu-id="1d5ab-104">在即時的資料處理中，了解資料在查詢進行中所呈現的樣子將會相當有幫助。</span><span class="sxs-lookup"><span data-stu-id="1d5ab-104">In real-time data processing, knowing what the data looks like in the middle of the query can be helpful.</span></span> <span data-ttu-id="1d5ab-105">由於 Azure 串流分析作業的輸入或步驟可以讀取多次，因此您可以寫入額外的 SELECT INTO 陳述式。</span><span class="sxs-lookup"><span data-stu-id="1d5ab-105">Because inputs or steps of an Azure Stream Analytics job can be read multiple times, you can write extra SELECT INTO statements.</span></span> <span data-ttu-id="1d5ab-106">這種方式會將中繼資料輸出到儲存體，讓您可以檢查資料的正確性，就像您對程式進行偵錯時*監看變數*的動作一樣。</span><span class="sxs-lookup"><span data-stu-id="1d5ab-106">Doing so outputs intermediate data into storage and lets you inspect the correctness of the data, just as *watch variables* do when you debug a program.</span></span>

## <a name="use-select-into-to-check-the-data-stream"></a><span data-ttu-id="1d5ab-107">使用 SELECT INTO 檢查資料串流</span><span class="sxs-lookup"><span data-stu-id="1d5ab-107">Use SELECT INTO to check the data stream</span></span>

<span data-ttu-id="1d5ab-108">下列 Azure 串流分析作業中的查詢範例有一個串流輸入、兩個的參考資料輸入和要傳送至 Azure 資料表儲存體的輸出。</span><span class="sxs-lookup"><span data-stu-id="1d5ab-108">The following example query in an Azure Stream Analytics job has one stream input, two reference data inputs, and an output to Azure Table Storage.</span></span> <span data-ttu-id="1d5ab-109">查詢會聯結事件中樞的資料和兩個參考 Blob 以取得名稱和類別資訊︰</span><span class="sxs-lookup"><span data-stu-id="1d5ab-109">The query joins data from the event hub and two reference blobs to get the name and category information:</span></span>

![SELECT INTO 查詢範例](./media/stream-analytics-select-into/stream-analytics-select-into-query1.png)

<span data-ttu-id="1d5ab-111">請注意，雖然作業正在執行，但不會在輸出中產生任何事件。</span><span class="sxs-lookup"><span data-stu-id="1d5ab-111">Note that the job is running, but no events are being produced in the output.</span></span> <span data-ttu-id="1d5ab-112">在 [監視]圖格上 (如此處所示)，您可以看到輸入正在產生資料，但您無法知道哪一個**聯結**步驟會造成所有資料遭到捨棄。</span><span class="sxs-lookup"><span data-stu-id="1d5ab-112">On the **Monitoring** tile, shown here, you can see that the input is producing data, but you don’t know which step of the **JOIN** caused all the events to be dropped.</span></span>

![監視圖格](./media/stream-analytics-select-into/stream-analytics-select-into-monitor.png)
 
<span data-ttu-id="1d5ab-114">在此情況下，您可以新增一些額外的 SELECT INTO 陳述式以「記錄」中繼「聯結」結果及從輸入中讀取的資料。</span><span class="sxs-lookup"><span data-stu-id="1d5ab-114">In this situation, you can add a few extra SELECT INTO statements to “log” the intermediate JOIN results and the data that's read from the input.</span></span>

<span data-ttu-id="1d5ab-115">在此範例中，我們新增了兩個新的「暫存輸出」。</span><span class="sxs-lookup"><span data-stu-id="1d5ab-115">In this example, we've added two new “temporary outputs.”</span></span> <span data-ttu-id="1d5ab-116">這些暫存輸出可以是您喜歡的任何接收體。</span><span class="sxs-lookup"><span data-stu-id="1d5ab-116">They can be any sink you like.</span></span> <span data-ttu-id="1d5ab-117">在這裡我們使用 Azure 儲存體作為範例︰</span><span class="sxs-lookup"><span data-stu-id="1d5ab-117">Here we use Azure Storage as an example:</span></span>

![新增額外的 SELECT INTO 陳述式](./media/stream-analytics-select-into/stream-analytics-select-into-outputs.png)

<span data-ttu-id="1d5ab-119">然後您可以重新撰寫查詢，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="1d5ab-119">You can then rewrite the query like this:</span></span>

![重新撰寫 SELECT INTO 查詢](./media/stream-analytics-select-into/stream-analytics-select-into-query2.png)

<span data-ttu-id="1d5ab-121">現在請再次啟動作業，並讓它執行幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="1d5ab-121">Now start the job again, and let it run for a few minutes.</span></span> <span data-ttu-id="1d5ab-122">然後使用 Visual Studio Cloud Explorer 查詢 temp1 和 temp2 以產生下列表格︰</span><span class="sxs-lookup"><span data-stu-id="1d5ab-122">Then query temp1 and temp2 with Visual Studio Cloud Explorer to produce the following tables:</span></span>

<span data-ttu-id="1d5ab-123">**temp1 資料表**
![SELECT INTO temp1 資料表](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)</span><span class="sxs-lookup"><span data-stu-id="1d5ab-123">**temp1 table**
![SELECT INTO temp1 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)</span></span>

<span data-ttu-id="1d5ab-124">**temp2 資料表**
![SELECT INTO temp2 資料表](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)</span><span class="sxs-lookup"><span data-stu-id="1d5ab-124">**temp2 table**
![SELECT INTO temp2 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)</span></span>

<span data-ttu-id="1d5ab-125">如您所見，temp1 和 temp2 都有資料，且 temp2 的名稱資料欄已正確地填入。</span><span class="sxs-lookup"><span data-stu-id="1d5ab-125">As you can see, temp1 and temp2 both have data, and the name column is populated correctly in temp2.</span></span> <span data-ttu-id="1d5ab-126">不過，因為輸出中仍沒有資料，可能有些地方出了問題︰</span><span class="sxs-lookup"><span data-stu-id="1d5ab-126">However, because there is still no data in output, something is wrong:</span></span>

![SELECT INTO output1 資料表沒有資料](./media/stream-analytics-select-into/stream-analytics-select-into-out-table-1.png)

<span data-ttu-id="1d5ab-128">藉由資料取樣，您幾乎可以確定問題出自第二個「聯結」。</span><span class="sxs-lookup"><span data-stu-id="1d5ab-128">By sampling the data, you can be almost certain that the issue is with the second JOIN.</span></span> <span data-ttu-id="1d5ab-129">您可以從 Blob 下載參考資料，以及查看下列項目︰</span><span class="sxs-lookup"><span data-stu-id="1d5ab-129">You can download the reference data from the blob and take a look:</span></span>

![SELECT INTO 參考資料表](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-1.png)

<span data-ttu-id="1d5ab-131">如您所見，此參考資料中的 GUID 格式與 temp2 中的 [from] 資料欄格式不同。</span><span class="sxs-lookup"><span data-stu-id="1d5ab-131">As you can see, the format of the GUID in this reference data is different from the format of the [from] column in temp2.</span></span> <span data-ttu-id="1d5ab-132">這就是為什麼資料並未如預期般送達 output1。</span><span class="sxs-lookup"><span data-stu-id="1d5ab-132">That’s why the data didn’t arrive in output1 as expected.</span></span>

<span data-ttu-id="1d5ab-133">您可以修正資料格式並上傳至參考 Blob，然後再試一次︰</span><span class="sxs-lookup"><span data-stu-id="1d5ab-133">You can fix the data format, upload it to reference blob, and try again:</span></span>

![SELECT INTO 暫存資料表](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-2.png)

<span data-ttu-id="1d5ab-135">此時，輸出中的資料已如預期般進行格式化並填入。</span><span class="sxs-lookup"><span data-stu-id="1d5ab-135">This time, the data in the output is formatted and populated as expected.</span></span>

![SELECT INTO 的最終資料表](./media/stream-analytics-select-into/stream-analytics-select-into-final-table.png)


## <a name="get-help"></a><span data-ttu-id="1d5ab-137">取得說明</span><span class="sxs-lookup"><span data-stu-id="1d5ab-137">Get help</span></span>

<span data-ttu-id="1d5ab-138">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。</span><span class="sxs-lookup"><span data-stu-id="1d5ab-138">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d5ab-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1d5ab-139">Next steps</span></span>

* [<span data-ttu-id="1d5ab-140">Azure Stream Analytics 介紹</span><span class="sxs-lookup"><span data-stu-id="1d5ab-140">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="1d5ab-141">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1d5ab-141">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="1d5ab-142">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="1d5ab-142">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="1d5ab-143">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="1d5ab-143">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="1d5ab-144">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="1d5ab-144">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

