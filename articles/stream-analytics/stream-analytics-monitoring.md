---
title: "了解串流分析工作監視 | Microsoft Docs"
description: "了解串流分析工作監視"
keywords: "查詢監視"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5f5cc00f-4a7b-491e-89e1-dbafea46d399
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 13d96807a5591ec88deda19ea73cfedc07078433
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="understand-stream-analytics-job-monitoring-and-how-to-monitor-queries"></a><span data-ttu-id="c5646-104">了解串流分析工作監視功能，以及如何監視查詢</span><span class="sxs-lookup"><span data-stu-id="c5646-104">Understand Stream Analytics job monitoring and how to monitor queries</span></span>

## <a name="introduction-the-monitor-page"></a><span data-ttu-id="c5646-105">簡介：監視頁面</span><span class="sxs-lookup"><span data-stu-id="c5646-105">Introduction: The monitor page</span></span>
<span data-ttu-id="c5646-106">Azure 入口網站會顯示關鍵效能計量，可供您用來監視查詢和工作效能並進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="c5646-106">The Azure portal both surface key performance metrics that can be used to monitor and troubleshoot your query and job performance.</span></span> <span data-ttu-id="c5646-107">若要查看這些計量，請瀏覽至您有興趣查看計量的「串流分析」工作，然後檢視 [概觀] 頁面上的 [監視] 區段。</span><span class="sxs-lookup"><span data-stu-id="c5646-107">To see these metrics, browse to the Stream Analytics job you are interested in seeing metrics for and view the **Monitoring** section on the Overview page.</span></span>  

![監視連結](./media/stream-analytics-monitoring/02-stream-analytics-monitoring-block.png)

<span data-ttu-id="c5646-109">視窗將會出現，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c5646-109">The window will appear as shown:</span></span>

![監視工作儀表板](./media/stream-analytics-monitoring/01-stream-analytics-monitoring.png)  

## <a name="metrics-available-for-stream-analytics"></a><span data-ttu-id="c5646-111">可供串流分析使用的度量</span><span class="sxs-lookup"><span data-stu-id="c5646-111">Metrics available for Stream Analytics</span></span>
| <span data-ttu-id="c5646-112">度量</span><span class="sxs-lookup"><span data-stu-id="c5646-112">Metric</span></span>                 | <span data-ttu-id="c5646-113">定義</span><span class="sxs-lookup"><span data-stu-id="c5646-113">Definition</span></span>                               |
| ---------------------- | ---------------------------------------- |
| <span data-ttu-id="c5646-114">SU % 使用率</span><span class="sxs-lookup"><span data-stu-id="c5646-114">SU % Utilization</span></span>       | <span data-ttu-id="c5646-115">從工作的 [調整] 索引標籤指派給工作的串流處理單元使用率。</span><span class="sxs-lookup"><span data-stu-id="c5646-115">The utilization of the Streaming Unit(s) assigned to a job from the Scale tab of the job.</span></span> <span data-ttu-id="c5646-116">若此指標達到 80% 以上，則代表事件處理作業極有可能延遲或暫停。</span><span class="sxs-lookup"><span data-stu-id="c5646-116">Should this indicator reach 80%, or above, there is high probability that event processing may be delayed or stopped making progress.</span></span> |
| <span data-ttu-id="c5646-117">輸入事件</span><span class="sxs-lookup"><span data-stu-id="c5646-117">Input Events</span></span>           | <span data-ttu-id="c5646-118">「串流分析」工作所接收到的資料量 (以事件數為單位)。</span><span class="sxs-lookup"><span data-stu-id="c5646-118">Amount of data received by the Stream Analytics job, in number of events.</span></span> <span data-ttu-id="c5646-119">這可以用來驗證傳送到輸入來源的事件。</span><span class="sxs-lookup"><span data-stu-id="c5646-119">This can be used to validate that events are being sent to the input source.</span></span> |
| <span data-ttu-id="c5646-120">輸出事件</span><span class="sxs-lookup"><span data-stu-id="c5646-120">Output Events</span></span>          | <span data-ttu-id="c5646-121">「串流分析」工作所傳送的資料量 (以事件數為單位)。</span><span class="sxs-lookup"><span data-stu-id="c5646-121">Amount of data sent by the Stream Analytics job to the output target, in number of events.</span></span> |
| <span data-ttu-id="c5646-122">順序錯亂事件</span><span class="sxs-lookup"><span data-stu-id="c5646-122">Out-of-Order Events</span></span>    | <span data-ttu-id="c5646-123">所收到順序錯亂的事件數目，這些事件會根據事件順序原則，予以捨棄或指定調整後的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="c5646-123">Number of events received out of order that were either dropped or given an adjusted timestamp, based on the Event Ordering Policy.</span></span> <span data-ttu-id="c5646-124">順序錯亂容錯視窗設定的組態可能會造成影響。</span><span class="sxs-lookup"><span data-stu-id="c5646-124">This can be impacted by the configuration of the Out of Order Tolerance Window setting.</span></span> |
| <span data-ttu-id="c5646-125">資料轉換錯誤</span><span class="sxs-lookup"><span data-stu-id="c5646-125">Data Conversion Errors</span></span> | <span data-ttu-id="c5646-126">串流分析工作所造成的錯誤訊息數目。</span><span class="sxs-lookup"><span data-stu-id="c5646-126">Number of data conversion errors incurred by a Stream Analytics job.</span></span> |
| <span data-ttu-id="c5646-127">執行階段錯誤</span><span class="sxs-lookup"><span data-stu-id="c5646-127">Runtime Errors</span></span>         | <span data-ttu-id="c5646-128">在執行「串流分析」工作期間發生的錯誤總數。</span><span class="sxs-lookup"><span data-stu-id="c5646-128">The total number of errors that happen during execution of a Stream Analytics job.</span></span> |
| <span data-ttu-id="c5646-129">延遲輸入事件</span><span class="sxs-lookup"><span data-stu-id="c5646-129">Late Input Events</span></span>      | <span data-ttu-id="c5646-130">從來源延遲抵達的事件數目，這些事件已根據延遲抵達容錯視窗設定的事件順序原則組態卸除或調整其時間戳記。</span><span class="sxs-lookup"><span data-stu-id="c5646-130">Number of events arriving late from the source which have either been dropped or their timestamp has been adjusted, based on the Event Ordering Policy configuration of the Late Arrival Tolerance Window setting.</span></span> |
| <span data-ttu-id="c5646-131">函式要求</span><span class="sxs-lookup"><span data-stu-id="c5646-131">Function Requests</span></span>      | <span data-ttu-id="c5646-132">對 Azure Machine Learning 函式發出的呼叫次數 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="c5646-132">Number of calls to the Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="c5646-133">失敗的函式要求</span><span class="sxs-lookup"><span data-stu-id="c5646-133">Failed Function Requests</span></span> | <span data-ttu-id="c5646-134">失敗的 Azure Machine Learning 函式呼叫次數 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="c5646-134">Number of failed Azure Machine Learning function calls (if present).</span></span> |
| <span data-ttu-id="c5646-135">函式事件</span><span class="sxs-lookup"><span data-stu-id="c5646-135">Function Events</span></span>        | <span data-ttu-id="c5646-136">傳送給 Azure Machine Learning 函式的事件數目 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="c5646-136">Number of events sent to the Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="c5646-137">輸入事件位元組</span><span class="sxs-lookup"><span data-stu-id="c5646-137">Input Event Bytes</span></span>      | <span data-ttu-id="c5646-138">「串流分析」工作所接收到的資料量 (以位元組為單位)。</span><span class="sxs-lookup"><span data-stu-id="c5646-138">Amount of data received by the Stream Analytics job, in bytes.</span></span> <span data-ttu-id="c5646-139">這可以用來驗證傳送到輸入來源的事件。</span><span class="sxs-lookup"><span data-stu-id="c5646-139">This can be used to validate that events are being sent to the input source.</span></span> |


## <a name="customizing-monitoring-in-the-azure-portal"></a><span data-ttu-id="c5646-140">在 Azure 入口網站中自訂監視</span><span class="sxs-lookup"><span data-stu-id="c5646-140">Customizing Monitoring in the Azure portal</span></span>
<span data-ttu-id="c5646-141">您可以在 [編輯圖表] 設定中調整圖表類型、顯示的度量和時間範圍。</span><span class="sxs-lookup"><span data-stu-id="c5646-141">You can adjust the type of chart, metrics shown, and time range in the Edit Chart settings.</span></span> <span data-ttu-id="c5646-142">如需詳細資料，請參閱[如何自訂監視](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md)。</span><span class="sxs-lookup"><span data-stu-id="c5646-142">For details, see [How to Customize Monitoring](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

  ![查詢監視時間圖](./media/stream-analytics-monitoring/08-stream-analytics-monitoring.png)  


## <a name="get-help"></a><span data-ttu-id="c5646-144">取得說明</span><span class="sxs-lookup"><span data-stu-id="c5646-144">Get help</span></span>
<span data-ttu-id="c5646-145">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="c5646-145">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5646-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c5646-146">Next steps</span></span>
* [<span data-ttu-id="c5646-147">Azure Stream Analytics 介紹</span><span class="sxs-lookup"><span data-stu-id="c5646-147">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="c5646-148">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c5646-148">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="c5646-149">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="c5646-149">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="c5646-150">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="c5646-150">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="c5646-151">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="c5646-151">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

