---
title: "Azure 串流分析的事件順序和延遲處理 | Microsoft Docs"
description: "深入了解串流分析如何處理資料串流中順序錯亂或延遲的事件。"
keywords: "順序錯亂、延遲、事件"
documentationcenter: 
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
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: a48e48c5fc65d0ffbb7c23f426a4b06dcd568821
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-stream-analytics-event-order-handling"></a><span data-ttu-id="bc0b7-104">Azure 串流分析事件的順序處理</span><span class="sxs-lookup"><span data-stu-id="bc0b7-104">Azure Stream Analytics event order handling</span></span>

<span data-ttu-id="bc0b7-105">在事件的暫存資料串流中，每個事件都會進行記錄，其中會包含收到事件的時間。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-105">In a temporal data stream of events, each event is recorded with the time that the event is received.</span></span> <span data-ttu-id="bc0b7-106">有時候，某些情況可能會造成串流收到某些事件的順序與事件送出的順序不同。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-106">Some conditions might cause event streams to occasionally receive some events in a different order than which they were sent.</span></span> <span data-ttu-id="bc0b7-107">簡易的 TCP 重新傳送動作或甚至是傳送裝置與接收事件中樞間的時鐘誤差，都有可能造成此狀況發生。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-107">A simple TCP retransmit, or even a clock skew between the sending device and the receiving event hub might cause this to occur.</span></span> <span data-ttu-id="bc0b7-108">接收的事件串流中也已新增「標點符號」事件，以便在事件未抵達的情況下讓時間繼續前進。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-108">“Punctuation” events also are added to received event streams, to advance the time in the absence of event arrivals.</span></span> <span data-ttu-id="bc0b7-109">例如「3 分鐘後沒出現登入作業請通知我」的情況就需要標點符號事件。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-109">These are needed in scenarios like “Notify me when no logins occur for 3 minutes."</span></span>

<span data-ttu-id="bc0b7-110">未依照順序的輸入串流為以下兩者其中之一：</span><span class="sxs-lookup"><span data-stu-id="bc0b7-110">Input streams that are not in order are either:</span></span>
* <span data-ttu-id="bc0b7-111">已分類 (並因此**延遲**)。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-111">Sorted (and therefore **delayed**).</span></span>
* <span data-ttu-id="bc0b7-112">已由系統調整 (根據使用者指定的原則)。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-112">Adjusted by the system, according to a user-specified policy.</span></span>


## <a name="lateness-tolerance"></a><span data-ttu-id="bc0b7-113">延遲容許</span><span class="sxs-lookup"><span data-stu-id="bc0b7-113">Lateness tolerance</span></span>
<span data-ttu-id="bc0b7-114">串流分析可容許這類情況。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-114">Stream Analytics tolerates these types of scenarios.</span></span> <span data-ttu-id="bc0b7-115">串流分析可處理「順序錯亂」和「延遲」事件。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-115">Stream Analytics has handling for "out-of-order" and "late" events.</span></span> <span data-ttu-id="bc0b7-116">以下是串流分析處理這些事件的方式︰</span><span class="sxs-lookup"><span data-stu-id="bc0b7-116">It handles these events in the following ways:</span></span>

* <span data-ttu-id="bc0b7-117">抵達順序錯亂但在所設定容許範圍內的事件會透過**時間戳記重新排序**。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-117">Events that arrive out of order but within the set tolerance are **reordered by timestamp**.</span></span>
* <span data-ttu-id="bc0b7-118">抵達時間比容許範圍還晚的事件會遭到**捨棄或調整**。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-118">Events that arrive later than tolerance are **dropped or adjusted**.</span></span>
    * <span data-ttu-id="bc0b7-119">**調整**︰調整為看起來是在最低可接受時間抵達。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-119">**Adjusted**: Adjusted to appear to have arrived at the latest acceptable time.</span></span>
    * <span data-ttu-id="bc0b7-120">**捨棄**︰放棄。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-120">**Dropped**: Discarded.</span></span>

![串流分析事件處理](media/stream-analytics-event-handling/stream-analytics-event-handling.png)

## <a name="reduce-the-number-of-out-of-order-events"></a><span data-ttu-id="bc0b7-122">減少順序錯亂的事件數目</span><span class="sxs-lookup"><span data-stu-id="bc0b7-122">Reduce the number of out-of-order events</span></span>

<span data-ttu-id="bc0b7-123">由於串流分析在處理傳入事件時會套用暫存轉換 (例如視窗型彙總或暫存聯結)，因此串流分析會以時間戳記的順序將傳入事件排序。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-123">Because Stream Analytics applies a temporal transformation when it processes incoming events (for example, for windowed aggregates or temporal joins), Stream Analytics sorts incoming events by timestamp order.</span></span>

<span data-ttu-id="bc0b7-124">如果**沒有**使用 timestamp by 關鍵字，就會依預設使用 Azure 事件中樞的事件加入佇列時間。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-124">When the “timestamp by” keyword is **not** used, the Azure Event Hubs event enqueue time is used by default.</span></span> <span data-ttu-id="bc0b7-125">事件中樞可保證事件中樞每個分割區中時間戳記的單調性。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-125">Event Hubs guarantees monotonicity of the timestamp on each partition of the event hub.</span></span> <span data-ttu-id="bc0b7-126">也保證所有分割區的事件將會依時間戳記順序進行合併。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-126">It also guarantees that events from all partitions will be merged in timestamp order.</span></span> <span data-ttu-id="bc0b7-127">這兩個事件中樞保證可確保沒有順序錯亂的事件發生。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-127">These two Event Hubs guarantees ensure no out-of-order events.</span></span>

<span data-ttu-id="bc0b7-128">有時候，使用傳送者的時間戳記對您來說相當重要。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-128">Sometimes, it’s important for you to use the sender’s timestamp.</span></span> <span data-ttu-id="bc0b7-129">在此情況下將會使用 timestamp by 來選擇事件承載的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-129">In that case, a timestamp from the event payload is chosen by using “timestamp by.”</span></span> <span data-ttu-id="bc0b7-130">以下案列會介紹一個或多個事件順序錯誤的情況：</span><span class="sxs-lookup"><span data-stu-id="bc0b7-130">In these scenarios, one or more sources of event misorder might be introduced:</span></span>

* <span data-ttu-id="bc0b7-131">事件產生器有時鐘誤差。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-131">Event producers have clock skews.</span></span> <span data-ttu-id="bc0b7-132">此狀況常見於不同電腦的產生器，因為電腦的時鐘不同。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-132">This is common when producers are from different computers, so they have different clocks.</span></span>
* <span data-ttu-id="bc0b7-133">從事件來源到目的事件中樞之間的網路發生延遲。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-133">There's a network delay from the source of the events to the destination event hub.</span></span>
* <span data-ttu-id="bc0b7-134">事件中樞分割區之間存在時鐘誤差。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-134">Clock skews exist between event hub partitions.</span></span> <span data-ttu-id="bc0b7-135">串流分析第一次從所有事件中樞分割區排序事件時是以事件加入佇列的時間排序。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-135">Stream Analytics first sorts events from all event hub partitions by event enqueue time.</span></span> <span data-ttu-id="bc0b7-136">因此，資料串流被視為順序錯誤的事件。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-136">Then, it examines the data stream for misordered events.</span></span>

<span data-ttu-id="bc0b7-137">在 [組態] 索引標籤中，您會看到下列預設值︰</span><span class="sxs-lookup"><span data-stu-id="bc0b7-137">On the configuration tab, you see the following defaults:</span></span>

![串流分析順序錯亂處理](media/stream-analytics-event-handling/stream-analytics-out-of-order-handling.png)

<span data-ttu-id="bc0b7-139">如果您將順序錯亂容許範圍設定為 0 秒，則系統會認定您要求所有事件永遠按照順序。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-139">If you use 0 seconds as the out-of-order tolerance window, you are asserting that all events are in order all the time.</span></span> <span data-ttu-id="bc0b7-140">假設是這三種順序錯亂事件來源，則這是不可能實現的事。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-140">Given the three sources of misordered events, it’s unlikely that this is true.</span></span> 

<span data-ttu-id="bc0b7-141">若要允許串流分析修正事件順序錯亂的情況，您可以指定非零值作為順序錯亂的容許範圍。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-141">To allow Stream Analytics to correct an event misorder, you can specify a non-zero out-of-order tolerance window.</span></span> <span data-ttu-id="bc0b7-142">串流分析會讓事件緩衝，直到範圍上限，然後使用您選取的時間戳記重新排序事件。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-142">Stream Analytics buffers events up to that window, and then reorders them by using the timestamp you chose.</span></span> <span data-ttu-id="bc0b7-143">接著套用暫存轉換。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-143">It then applies the temporal transformation.</span></span> <span data-ttu-id="bc0b7-144">您可以從 3 秒鐘的範圍開始，然後調整值以減少遭到調整時間的事件數目。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-144">You can start with a 3-second window, and tune the value to reduce the number of events that are time-adjusted.</span></span> 

<span data-ttu-id="bc0b7-145">緩衝事件的副作用是輸出會有**相同時間的延遲**。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-145">A side effect of the buffering is that the output is **delayed by the same amount of time**.</span></span> <span data-ttu-id="bc0b7-146">您可以調整值以減少順序錯亂的事件數量，然後讓作業保持低延遲。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-146">You can tune the value to reduce the number of out-of-order events, and keep the job latency low.</span></span>

## <a name="get-help"></a><span data-ttu-id="bc0b7-147">取得說明</span><span class="sxs-lookup"><span data-stu-id="bc0b7-147">Get help</span></span>
<span data-ttu-id="bc0b7-148">如需其他協助，請參閱我們的 [Azure 串流分析論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。</span><span class="sxs-lookup"><span data-stu-id="bc0b7-148">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc0b7-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bc0b7-149">Next steps</span></span>
* [<span data-ttu-id="bc0b7-150">串流分析介紹</span><span class="sxs-lookup"><span data-stu-id="bc0b7-150">Introduction to Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="bc0b7-151">開始使用串流分析</span><span class="sxs-lookup"><span data-stu-id="bc0b7-151">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="bc0b7-152">調整串流分析作業</span><span class="sxs-lookup"><span data-stu-id="bc0b7-152">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="bc0b7-153">串流分析查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="bc0b7-153">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="bc0b7-154">串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="bc0b7-154">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)