---
title: "aaaDebug Azure 串流分析查詢使用 SELECT INTO |Microsoft 文件"
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
ms.openlocfilehash: 27e41af1a6ea06b4509d07a3a67087490d0ec1fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="debug-queries-by-using-select-into-statements"></a><span data-ttu-id="04ceb-103">使用 SELECT INTO 陳述式對查詢進行偵錯</span><span class="sxs-lookup"><span data-stu-id="04ceb-103">Debug queries by using SELECT INTO statements</span></span>

<span data-ttu-id="04ceb-104">在即時的資料處理，得知哪些 hello 資料似乎 hello 中間 hello 的查詢可以是很有幫助。</span><span class="sxs-lookup"><span data-stu-id="04ceb-104">In real-time data processing, knowing what hello data looks like in hello middle of hello query can be helpful.</span></span> <span data-ttu-id="04ceb-105">由於 Azure 串流分析作業的輸入或步驟可以讀取多次，因此您可以寫入額外的 SELECT INTO 陳述式。</span><span class="sxs-lookup"><span data-stu-id="04ceb-105">Because inputs or steps of an Azure Stream Analytics job can be read multiple times, you can write extra SELECT INTO statements.</span></span> <span data-ttu-id="04ceb-106">這樣會輸出到儲存體的中繼資料並可讓您檢查 hello 正確性的 hello 資料，就像*監看變數*執行時偵錯程式。</span><span class="sxs-lookup"><span data-stu-id="04ceb-106">Doing so outputs intermediate data into storage and lets you inspect hello correctness of hello data, just as *watch variables* do when you debug a program.</span></span>

## <a name="use-select-into-toocheck-hello-data-stream"></a><span data-ttu-id="04ceb-107">使用 SELECT INTO toocheck hello 資料流</span><span class="sxs-lookup"><span data-stu-id="04ceb-107">Use SELECT INTO toocheck hello data stream</span></span>

<span data-ttu-id="04ceb-108">hello Azure Stream Analytics 工作中的下列範例查詢有一個資料流輸入、 兩個參考資料輸入和輸出 tooAzure 資料表儲存體。</span><span class="sxs-lookup"><span data-stu-id="04ceb-108">hello following example query in an Azure Stream Analytics job has one stream input, two reference data inputs, and an output tooAzure Table Storage.</span></span> <span data-ttu-id="04ceb-109">hello 查詢會聯結來自 hello 事件中樞與兩個參考 blob tooget hello 名稱和類別目錄資訊的資料：</span><span class="sxs-lookup"><span data-stu-id="04ceb-109">hello query joins data from hello event hub and two reference blobs tooget hello name and category information:</span></span>

![SELECT INTO 查詢範例](./media/stream-analytics-select-into/stream-analytics-select-into-query1.png)

<span data-ttu-id="04ceb-111">請注意，執行 hello 工作時，正在 hello 輸出中產生任何事件。</span><span class="sxs-lookup"><span data-stu-id="04ceb-111">Note that hello job is running, but no events are being produced in hello output.</span></span> <span data-ttu-id="04ceb-112">在 hello**監視**磚，在這裡顯示，您可以看到 hello 輸入產生的資料，但是您不知道哪一個步驟中的 hello**聯結**造成所有 hello 事件 toobe 卸除。</span><span class="sxs-lookup"><span data-stu-id="04ceb-112">On hello **Monitoring** tile, shown here, you can see that hello input is producing data, but you don’t know which step of hello **JOIN** caused all hello events toobe dropped.</span></span>

![hello 監視磚](./media/stream-analytics-select-into/stream-analytics-select-into-monitor.png)
 
<span data-ttu-id="04ceb-114">在此情況下，您可以加入幾個額外 SELECT INTO 陳述式太 「 記錄 」 hello 中繼聯結結果和 hello 讀取資料，從輸入 hello。</span><span class="sxs-lookup"><span data-stu-id="04ceb-114">In this situation, you can add a few extra SELECT INTO statements too“log” hello intermediate JOIN results and hello data that's read from hello input.</span></span>

<span data-ttu-id="04ceb-115">在此範例中，我們新增了兩個新的「暫存輸出」。</span><span class="sxs-lookup"><span data-stu-id="04ceb-115">In this example, we've added two new “temporary outputs.”</span></span> <span data-ttu-id="04ceb-116">這些暫存輸出可以是您喜歡的任何接收體。</span><span class="sxs-lookup"><span data-stu-id="04ceb-116">They can be any sink you like.</span></span> <span data-ttu-id="04ceb-117">在這裡我們使用 Azure 儲存體作為範例︰</span><span class="sxs-lookup"><span data-stu-id="04ceb-117">Here we use Azure Storage as an example:</span></span>

![新增額外的 SELECT INTO 陳述式](./media/stream-analytics-select-into/stream-analytics-select-into-outputs.png)

<span data-ttu-id="04ceb-119">然後，您可以重新撰寫 hello 查詢如下：</span><span class="sxs-lookup"><span data-stu-id="04ceb-119">You can then rewrite hello query like this:</span></span>

![重新撰寫 SELECT INTO 查詢](./media/stream-analytics-select-into/stream-analytics-select-into-query2.png)

<span data-ttu-id="04ceb-121">現在 hello 作業重新啟動，並讓它在幾分鐘後執行。</span><span class="sxs-lookup"><span data-stu-id="04ceb-121">Now start hello job again, and let it run for a few minutes.</span></span> <span data-ttu-id="04ceb-122">然後，請查詢 temp1 和 temp2 以 Visual Studio Cloud Explorer tooproduce hello 下列資料表：</span><span class="sxs-lookup"><span data-stu-id="04ceb-122">Then query temp1 and temp2 with Visual Studio Cloud Explorer tooproduce hello following tables:</span></span>

<span data-ttu-id="04ceb-123">**temp1 資料表**
![SELECT INTO temp1 資料表](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)</span><span class="sxs-lookup"><span data-stu-id="04ceb-123">**temp1 table**
![SELECT INTO temp1 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)</span></span>

<span data-ttu-id="04ceb-124">**temp2 資料表**
![SELECT INTO temp2 資料表](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)</span><span class="sxs-lookup"><span data-stu-id="04ceb-124">**temp2 table**
![SELECT INTO temp2 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)</span></span>

<span data-ttu-id="04ceb-125">如您所見，temp1 和 temp2 都有資料，並 hello 名稱資料行都已填妥正確 temp2。</span><span class="sxs-lookup"><span data-stu-id="04ceb-125">As you can see, temp1 and temp2 both have data, and hello name column is populated correctly in temp2.</span></span> <span data-ttu-id="04ceb-126">不過，因為輸出中仍沒有資料，可能有些地方出了問題︰</span><span class="sxs-lookup"><span data-stu-id="04ceb-126">However, because there is still no data in output, something is wrong:</span></span>

![SELECT INTO output1 資料表沒有資料](./media/stream-analytics-select-into/stream-analytics-select-into-out-table-1.png)

<span data-ttu-id="04ceb-128">根據取樣 hello 資料，您可以是幾乎可以肯定 hello 問題是以 hello 聯結的第二個。</span><span class="sxs-lookup"><span data-stu-id="04ceb-128">By sampling hello data, you can be almost certain that hello issue is with hello second JOIN.</span></span> <span data-ttu-id="04ceb-129">您可以下載 hello blob hello 參考資料，並請參閱：</span><span class="sxs-lookup"><span data-stu-id="04ceb-129">You can download hello reference data from hello blob and take a look:</span></span>

![SELECT INTO 參考資料表](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-1.png)

<span data-ttu-id="04ceb-131">如您所見，hello 這個參考資料中的 hello GUID 格式會與不同的 [從] 資料行中 temp2 hello hello 格式。</span><span class="sxs-lookup"><span data-stu-id="04ceb-131">As you can see, hello format of hello GUID in this reference data is different from hello format of hello [from] column in temp2.</span></span> <span data-ttu-id="04ceb-132">這就是為什麼 hello 資料未到達 output1 如預期般。</span><span class="sxs-lookup"><span data-stu-id="04ceb-132">That’s why hello data didn’t arrive in output1 as expected.</span></span>

<span data-ttu-id="04ceb-133">您可以修正 hello 資料格式、 將它上傳 tooreference blob，並再試一次：</span><span class="sxs-lookup"><span data-stu-id="04ceb-133">You can fix hello data format, upload it tooreference blob, and try again:</span></span>

![SELECT INTO 暫存資料表](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-2.png)

<span data-ttu-id="04ceb-135">這次 hello hello 輸出中的資料是格式化，並且如預期般填入。</span><span class="sxs-lookup"><span data-stu-id="04ceb-135">This time, hello data in hello output is formatted and populated as expected.</span></span>

![SELECT INTO 的最終資料表](./media/stream-analytics-select-into/stream-analytics-select-into-final-table.png)


## <a name="get-help"></a><span data-ttu-id="04ceb-137">取得說明</span><span class="sxs-lookup"><span data-stu-id="04ceb-137">Get help</span></span>

<span data-ttu-id="04ceb-138">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。</span><span class="sxs-lookup"><span data-stu-id="04ceb-138">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="04ceb-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="04ceb-139">Next steps</span></span>

* [<span data-ttu-id="04ceb-140">簡介 tooAzure 資料流分析</span><span class="sxs-lookup"><span data-stu-id="04ceb-140">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="04ceb-141">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="04ceb-141">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="04ceb-142">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="04ceb-142">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="04ceb-143">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="04ceb-143">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="04ceb-144">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="04ceb-144">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

