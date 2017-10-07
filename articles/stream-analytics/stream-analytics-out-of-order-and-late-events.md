---
title: "aaaHandling 事件順序和使用 Azure Stream Analytics lateness |Microsoft 文件"
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
ms.openlocfilehash: 87c028662fbafbf4f72f57f215d017f65bb649f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-event-order-handling"></a><span data-ttu-id="d184b-104">Azure 串流分析事件的順序處理</span><span class="sxs-lookup"><span data-stu-id="d184b-104">Azure Stream Analytics event order handling</span></span>

<span data-ttu-id="d184b-105">在暫存資料流的事件，每個事件會記錄與 hello 時間收到 hello 事件。</span><span class="sxs-lookup"><span data-stu-id="d184b-105">In a temporal data stream of events, each event is recorded with hello time that hello event is received.</span></span> <span data-ttu-id="d184b-106">某些條件可能會導致 toooccasionally 接收的事件資料流某些事件比用其傳送順序不同。</span><span class="sxs-lookup"><span data-stu-id="d184b-106">Some conditions might cause event streams toooccasionally receive some events in a different order than which they were sent.</span></span> <span data-ttu-id="d184b-107">簡單的 TCP 重新傳輸，或甚至 hello 傳送裝置和 hello 接收事件中心之間的時鐘誤差可能會導致此 toooccur。</span><span class="sxs-lookup"><span data-stu-id="d184b-107">A simple TCP retransmit, or even a clock skew between hello sending device and hello receiving event hub might cause this toooccur.</span></span> <span data-ttu-id="d184b-108">「 對稱 」 事件也會加入 tooreceived 事件資料流，在事件抵達的 hello 缺乏 tooadvance hello 時間。</span><span class="sxs-lookup"><span data-stu-id="d184b-108">“Punctuation” events also are added tooreceived event streams, tooadvance hello time in hello absence of event arrivals.</span></span> <span data-ttu-id="d184b-109">例如「3 分鐘後沒出現登入作業請通知我」的情況就需要標點符號事件。</span><span class="sxs-lookup"><span data-stu-id="d184b-109">These are needed in scenarios like “Notify me when no logins occur for 3 minutes."</span></span>

<span data-ttu-id="d184b-110">未依照順序的輸入串流為以下兩者其中之一：</span><span class="sxs-lookup"><span data-stu-id="d184b-110">Input streams that are not in order are either:</span></span>
* <span data-ttu-id="d184b-111">已分類 (並因此**延遲**)。</span><span class="sxs-lookup"><span data-stu-id="d184b-111">Sorted (and therefore **delayed**).</span></span>
* <span data-ttu-id="d184b-112">調整 hello 系統中，根據 tooa 使用者指定的原則。</span><span class="sxs-lookup"><span data-stu-id="d184b-112">Adjusted by hello system, according tooa user-specified policy.</span></span>


## <a name="lateness-tolerance"></a><span data-ttu-id="d184b-113">延遲容許</span><span class="sxs-lookup"><span data-stu-id="d184b-113">Lateness tolerance</span></span>
<span data-ttu-id="d184b-114">串流分析可容許這類情況。</span><span class="sxs-lookup"><span data-stu-id="d184b-114">Stream Analytics tolerates these types of scenarios.</span></span> <span data-ttu-id="d184b-115">串流分析可處理「順序錯亂」和「延遲」事件。</span><span class="sxs-lookup"><span data-stu-id="d184b-115">Stream Analytics has handling for "out-of-order" and "late" events.</span></span> <span data-ttu-id="d184b-116">它會處理這些事件中 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="d184b-116">It handles these events in hello following ways:</span></span>

* <span data-ttu-id="d184b-117">事件不按順序抵達，但 hello 內設定容限是**時間戳記來重新排列**。</span><span class="sxs-lookup"><span data-stu-id="d184b-117">Events that arrive out of order but within hello set tolerance are **reordered by timestamp**.</span></span>
* <span data-ttu-id="d184b-118">抵達時間比容許範圍還晚的事件會遭到**捨棄或調整**。</span><span class="sxs-lookup"><span data-stu-id="d184b-118">Events that arrive later than tolerance are **dropped or adjusted**.</span></span>
    * <span data-ttu-id="d184b-119">**調整**： 調整的 tooappear toohave 抵達 hello 最新接受的時間。</span><span class="sxs-lookup"><span data-stu-id="d184b-119">**Adjusted**: Adjusted tooappear toohave arrived at hello latest acceptable time.</span></span>
    * <span data-ttu-id="d184b-120">**捨棄**︰放棄。</span><span class="sxs-lookup"><span data-stu-id="d184b-120">**Dropped**: Discarded.</span></span>

![串流分析事件處理](media/stream-analytics-event-handling/stream-analytics-event-handling.png)

## <a name="reduce-hello-number-of-out-of-order-events"></a><span data-ttu-id="d184b-122">減少 hello 次序不對的事件數目</span><span class="sxs-lookup"><span data-stu-id="d184b-122">Reduce hello number of out-of-order events</span></span>

<span data-ttu-id="d184b-123">由於串流分析在處理傳入事件時會套用暫存轉換 (例如視窗型彙總或暫存聯結)，因此串流分析會以時間戳記的順序將傳入事件排序。</span><span class="sxs-lookup"><span data-stu-id="d184b-123">Because Stream Analytics applies a temporal transformation when it processes incoming events (for example, for windowed aggregates or temporal joins), Stream Analytics sorts incoming events by timestamp order.</span></span>

<span data-ttu-id="d184b-124">當由的 hello"timestamp"關鍵字是**不**hello Azure 事件中心事件加入佇列的時間會使用預設。</span><span class="sxs-lookup"><span data-stu-id="d184b-124">When hello “timestamp by” keyword is **not** used, hello Azure Event Hubs event enqueue time is used by default.</span></span> <span data-ttu-id="d184b-125">事件中心可保證單一性 hello hello 事件中樞的每個磁碟分割上的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="d184b-125">Event Hubs guarantees monotonicity of hello timestamp on each partition of hello event hub.</span></span> <span data-ttu-id="d184b-126">也保證所有分割區的事件將會依時間戳記順序進行合併。</span><span class="sxs-lookup"><span data-stu-id="d184b-126">It also guarantees that events from all partitions will be merged in timestamp order.</span></span> <span data-ttu-id="d184b-127">這兩個事件中樞保證可確保沒有順序錯亂的事件發生。</span><span class="sxs-lookup"><span data-stu-id="d184b-127">These two Event Hubs guarantees ensure no out-of-order events.</span></span>

<span data-ttu-id="d184b-128">有時候，很重要您 toouse hello 寄件者的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="d184b-128">Sometimes, it’s important for you toouse hello sender’s timestamp.</span></span> <span data-ttu-id="d184b-129">在此情況下，從 hello 事件裝載的時間戳記會選擇使用 「 依時間戳記。 」</span><span class="sxs-lookup"><span data-stu-id="d184b-129">In that case, a timestamp from hello event payload is chosen by using “timestamp by.”</span></span> <span data-ttu-id="d184b-130">以下案列會介紹一個或多個事件順序錯誤的情況：</span><span class="sxs-lookup"><span data-stu-id="d184b-130">In these scenarios, one or more sources of event misorder might be introduced:</span></span>

* <span data-ttu-id="d184b-131">事件產生器有時鐘誤差。</span><span class="sxs-lookup"><span data-stu-id="d184b-131">Event producers have clock skews.</span></span> <span data-ttu-id="d184b-132">此狀況常見於不同電腦的產生器，因為電腦的時鐘不同。</span><span class="sxs-lookup"><span data-stu-id="d184b-132">This is common when producers are from different computers, so they have different clocks.</span></span>
* <span data-ttu-id="d184b-133">沒有從 hello 來源 hello 事件 toohello 目的地事件中心的網路延遲。</span><span class="sxs-lookup"><span data-stu-id="d184b-133">There's a network delay from hello source of hello events toohello destination event hub.</span></span>
* <span data-ttu-id="d184b-134">事件中樞分割區之間存在時鐘誤差。</span><span class="sxs-lookup"><span data-stu-id="d184b-134">Clock skews exist between event hub partitions.</span></span> <span data-ttu-id="d184b-135">串流分析第一次從所有事件中樞分割區排序事件時是以事件加入佇列的時間排序。</span><span class="sxs-lookup"><span data-stu-id="d184b-135">Stream Analytics first sorts events from all event hub partitions by event enqueue time.</span></span> <span data-ttu-id="d184b-136">然後，它會檢查 hello 順序的事件資料流。</span><span class="sxs-lookup"><span data-stu-id="d184b-136">Then, it examines hello data stream for misordered events.</span></span>

<span data-ttu-id="d184b-137">Hello 組態索引標籤上，您會看到下列預設值的 hello:</span><span class="sxs-lookup"><span data-stu-id="d184b-137">On hello configuration tab, you see hello following defaults:</span></span>

![串流分析順序錯亂處理](media/stream-analytics-event-handling/stream-analytics-out-of-order-handling.png)

<span data-ttu-id="d184b-139">如果您使用 0 秒做 hello 次序不對容錯時間，您正在判斷提示，所有事件都的順序所有 hello 時間。</span><span class="sxs-lookup"><span data-stu-id="d184b-139">If you use 0 seconds as hello out-of-order tolerance window, you are asserting that all events are in order all hello time.</span></span> <span data-ttu-id="d184b-140">指定 hello 三個來源的順序的事件，也不太可能，這是 true。</span><span class="sxs-lookup"><span data-stu-id="d184b-140">Given hello three sources of misordered events, it’s unlikely that this is true.</span></span> 

<span data-ttu-id="d184b-141">Stream Analytics toocorrect 事件 misorder tooallow，您可以指定非零次序不對容錯時間。</span><span class="sxs-lookup"><span data-stu-id="d184b-141">tooallow Stream Analytics toocorrect an event misorder, you can specify a non-zero out-of-order tolerance window.</span></span> <span data-ttu-id="d184b-142">資料流分析緩衝區事件向上 toothat 視窗，然後再重新排列它們使用 hello 您選擇的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="d184b-142">Stream Analytics buffers events up toothat window, and then reorders them by using hello timestamp you chose.</span></span> <span data-ttu-id="d184b-143">然後，它會套用 hello 暫時轉換。</span><span class="sxs-lookup"><span data-stu-id="d184b-143">It then applies hello temporal transformation.</span></span> <span data-ttu-id="d184b-144">您可以從 3 秒 視窗中，開始，並微調 hello 值 tooreduce hello 事件數目的時間調整。</span><span class="sxs-lookup"><span data-stu-id="d184b-144">You can start with a 3-second window, and tune hello value tooreduce hello number of events that are time-adjusted.</span></span> 

<span data-ttu-id="d184b-145">Hello 緩衝的副作用是，hello 輸出**延遲 hello 相同的時間量**。</span><span class="sxs-lookup"><span data-stu-id="d184b-145">A side effect of hello buffering is that hello output is **delayed by hello same amount of time**.</span></span> <span data-ttu-id="d184b-146">您可以微調 hello 值 tooreduce hello 次序不對的事件數目，並保留 hello 作業延遲更低。</span><span class="sxs-lookup"><span data-stu-id="d184b-146">You can tune hello value tooreduce hello number of out-of-order events, and keep hello job latency low.</span></span>

## <a name="get-help"></a><span data-ttu-id="d184b-147">取得說明</span><span class="sxs-lookup"><span data-stu-id="d184b-147">Get help</span></span>
<span data-ttu-id="d184b-148">如需其他協助，請參閱我們的 [Azure 串流分析論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。</span><span class="sxs-lookup"><span data-stu-id="d184b-148">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d184b-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d184b-149">Next steps</span></span>
* [<span data-ttu-id="d184b-150">簡介 tooStream 分析</span><span class="sxs-lookup"><span data-stu-id="d184b-150">Introduction tooStream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="d184b-151">開始使用串流分析</span><span class="sxs-lookup"><span data-stu-id="d184b-151">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="d184b-152">調整串流分析作業</span><span class="sxs-lookup"><span data-stu-id="d184b-152">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="d184b-153">串流分析查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="d184b-153">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="d184b-154">串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="d184b-154">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)