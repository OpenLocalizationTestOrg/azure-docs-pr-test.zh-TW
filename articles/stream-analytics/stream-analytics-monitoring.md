---
title: "資料流分析作業的監視 aaaUnderstanding |Microsoft 文件"
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
ms.openlocfilehash: 36819025c7b2ddbf4b9694522f1b4820407ca5f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understand-stream-analytics-job-monitoring-and-how-toomonitor-queries"></a><span data-ttu-id="f4c7a-104">了解資料流分析作業的監視和如何 toomonitor 查詢</span><span class="sxs-lookup"><span data-stu-id="f4c7a-104">Understand Stream Analytics job monitoring and how toomonitor queries</span></span>

## <a name="introduction-hello-monitor-page"></a><span data-ttu-id="f4c7a-105">簡介： hello 監視頁面</span><span class="sxs-lookup"><span data-stu-id="f4c7a-105">Introduction: hello monitor page</span></span>
<span data-ttu-id="f4c7a-106">hello 兩者介面，可以使用的 toomonitor 並疑難排解查詢和作業的效能關鍵效能標準的 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="f4c7a-106">hello Azure portal both surface key performance metrics that can be used toomonitor and troubleshoot your query and job performance.</span></span> <span data-ttu-id="f4c7a-107">toosee 這些度量，瀏覽 toohello 資料流分析工作，您有興趣查看的度量，檢視 hello**監視**hello 概觀 頁面上的一節。</span><span class="sxs-lookup"><span data-stu-id="f4c7a-107">toosee these metrics, browse toohello Stream Analytics job you are interested in seeing metrics for and view hello **Monitoring** section on hello Overview page.</span></span>  

![監視連結](./media/stream-analytics-monitoring/02-stream-analytics-monitoring-block.png)

<span data-ttu-id="f4c7a-109">hello 視窗會出現如下所示：</span><span class="sxs-lookup"><span data-stu-id="f4c7a-109">hello window will appear as shown:</span></span>

![監視工作儀表板](./media/stream-analytics-monitoring/01-stream-analytics-monitoring.png)  

## <a name="metrics-available-for-stream-analytics"></a><span data-ttu-id="f4c7a-111">可供串流分析使用的度量</span><span class="sxs-lookup"><span data-stu-id="f4c7a-111">Metrics available for Stream Analytics</span></span>
| <span data-ttu-id="f4c7a-112">度量</span><span class="sxs-lookup"><span data-stu-id="f4c7a-112">Metric</span></span>                 | <span data-ttu-id="f4c7a-113">定義</span><span class="sxs-lookup"><span data-stu-id="f4c7a-113">Definition</span></span>                               |
| ---------------------- | ---------------------------------------- |
| <span data-ttu-id="f4c7a-114">SU % 使用率</span><span class="sxs-lookup"><span data-stu-id="f4c7a-114">SU % Utilization</span></span>       | <span data-ttu-id="f4c7a-115">hello hello 使用量串流處理單元指派 tooa 作業 hello hello 工作的 [調整] 索引標籤中。</span><span class="sxs-lookup"><span data-stu-id="f4c7a-115">hello utilization of hello Streaming Unit(s) assigned tooa job from hello Scale tab of hello job.</span></span> <span data-ttu-id="f4c7a-116">若此指標達到 80% 以上，則代表事件處理作業極有可能延遲或暫停。</span><span class="sxs-lookup"><span data-stu-id="f4c7a-116">Should this indicator reach 80%, or above, there is high probability that event processing may be delayed or stopped making progress.</span></span> |
| <span data-ttu-id="f4c7a-117">輸入事件</span><span class="sxs-lookup"><span data-stu-id="f4c7a-117">Input Events</span></span>           | <span data-ttu-id="f4c7a-118">收到 hello 資料流分析作業中的事件數目的資料量。</span><span class="sxs-lookup"><span data-stu-id="f4c7a-118">Amount of data received by hello Stream Analytics job, in number of events.</span></span> <span data-ttu-id="f4c7a-119">這可以是使用的 toovalidate 事件會被傳送 toohello 輸入的來源。</span><span class="sxs-lookup"><span data-stu-id="f4c7a-119">This can be used toovalidate that events are being sent toohello input source.</span></span> |
| <span data-ttu-id="f4c7a-120">輸出事件</span><span class="sxs-lookup"><span data-stu-id="f4c7a-120">Output Events</span></span>          | <span data-ttu-id="f4c7a-121">傳送 hello 資料流分析作業 toohello 輸出目標中的事件數目的資料量。</span><span class="sxs-lookup"><span data-stu-id="f4c7a-121">Amount of data sent by hello Stream Analytics job toohello output target, in number of events.</span></span> |
| <span data-ttu-id="f4c7a-122">順序錯亂事件</span><span class="sxs-lookup"><span data-stu-id="f4c7a-122">Out-of-Order Events</span></span>    | <span data-ttu-id="f4c7a-123">從卸除或調整時間戳記，根據 hello 事件排序原則的順序接收的事件數目。</span><span class="sxs-lookup"><span data-stu-id="f4c7a-123">Number of events received out of order that were either dropped or given an adjusted timestamp, based on hello Event Ordering Policy.</span></span> <span data-ttu-id="f4c7a-124">這可能會影響 hello 設定 hello 次序不對的容錯時間設定。</span><span class="sxs-lookup"><span data-stu-id="f4c7a-124">This can be impacted by hello configuration of hello Out of Order Tolerance Window setting.</span></span> |
| <span data-ttu-id="f4c7a-125">資料轉換錯誤</span><span class="sxs-lookup"><span data-stu-id="f4c7a-125">Data Conversion Errors</span></span> | <span data-ttu-id="f4c7a-126">串流分析工作所造成的錯誤訊息數目。</span><span class="sxs-lookup"><span data-stu-id="f4c7a-126">Number of data conversion errors incurred by a Stream Analytics job.</span></span> |
| <span data-ttu-id="f4c7a-127">執行階段錯誤</span><span class="sxs-lookup"><span data-stu-id="f4c7a-127">Runtime Errors</span></span>         | <span data-ttu-id="f4c7a-128">hello 的資料流分析作業執行時，就可能發生的錯誤總數。</span><span class="sxs-lookup"><span data-stu-id="f4c7a-128">hello total number of errors that happen during execution of a Stream Analytics job.</span></span> |
| <span data-ttu-id="f4c7a-129">延遲輸入事件</span><span class="sxs-lookup"><span data-stu-id="f4c7a-129">Late Input Events</span></span>      | <span data-ttu-id="f4c7a-130">這是已卸除的 hello 來源或依時間戳記晚抵達的事件數目已經被自動調整，hello 事件順序的原則設定的設定。 hello 晚抵達容錯時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="f4c7a-130">Number of events arriving late from hello source which have either been dropped or their timestamp has been adjusted, based on hello Event Ordering Policy configuration of hello Late Arrival Tolerance Window setting.</span></span> |
| <span data-ttu-id="f4c7a-131">函式要求</span><span class="sxs-lookup"><span data-stu-id="f4c7a-131">Function Requests</span></span>      | <span data-ttu-id="f4c7a-132">呼叫 toohello Azure Machine Learning 函式 （如果有的話） 的數目。</span><span class="sxs-lookup"><span data-stu-id="f4c7a-132">Number of calls toohello Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="f4c7a-133">失敗的函式要求</span><span class="sxs-lookup"><span data-stu-id="f4c7a-133">Failed Function Requests</span></span> | <span data-ttu-id="f4c7a-134">失敗的 Azure Machine Learning 函式呼叫次數 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="f4c7a-134">Number of failed Azure Machine Learning function calls (if present).</span></span> |
| <span data-ttu-id="f4c7a-135">函式事件</span><span class="sxs-lookup"><span data-stu-id="f4c7a-135">Function Events</span></span>        | <span data-ttu-id="f4c7a-136">（如果有的話） 傳送 toohello Azure Machine Learning 函式的事件數目。</span><span class="sxs-lookup"><span data-stu-id="f4c7a-136">Number of events sent toohello Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="f4c7a-137">輸入事件位元組</span><span class="sxs-lookup"><span data-stu-id="f4c7a-137">Input Event Bytes</span></span>      | <span data-ttu-id="f4c7a-138">收到 hello 資料流分析工作，以位元組為單位的資料量。</span><span class="sxs-lookup"><span data-stu-id="f4c7a-138">Amount of data received by hello Stream Analytics job, in bytes.</span></span> <span data-ttu-id="f4c7a-139">這可以是使用的 toovalidate 事件會被傳送 toohello 輸入的來源。</span><span class="sxs-lookup"><span data-stu-id="f4c7a-139">This can be used toovalidate that events are being sent toohello input source.</span></span> |


## <a name="customizing-monitoring-in-hello-azure-portal"></a><span data-ttu-id="f4c7a-140">在 hello Azure 入口網站中自訂監視</span><span class="sxs-lookup"><span data-stu-id="f4c7a-140">Customizing Monitoring in hello Azure portal</span></span>
<span data-ttu-id="f4c7a-141">您可以調整圖表所示，度量 hello 類型和時間 hello 編輯圖表設定中的範圍。</span><span class="sxs-lookup"><span data-stu-id="f4c7a-141">You can adjust hello type of chart, metrics shown, and time range in hello Edit Chart settings.</span></span> <span data-ttu-id="f4c7a-142">如需詳細資訊，請參閱[如何 tooCustomize 監視](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md)。</span><span class="sxs-lookup"><span data-stu-id="f4c7a-142">For details, see [How tooCustomize Monitoring](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

  ![查詢監視時間圖](./media/stream-analytics-monitoring/08-stream-analytics-monitoring.png)  


## <a name="get-help"></a><span data-ttu-id="f4c7a-144">取得說明</span><span class="sxs-lookup"><span data-stu-id="f4c7a-144">Get help</span></span>
<span data-ttu-id="f4c7a-145">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="f4c7a-145">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4c7a-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f4c7a-146">Next steps</span></span>
* [<span data-ttu-id="f4c7a-147">簡介 tooAzure 資料流分析</span><span class="sxs-lookup"><span data-stu-id="f4c7a-147">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="f4c7a-148">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f4c7a-148">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="f4c7a-149">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="f4c7a-149">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="f4c7a-150">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="f4c7a-150">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="f4c7a-151">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="f4c7a-151">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

