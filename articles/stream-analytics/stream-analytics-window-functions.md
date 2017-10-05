---
title: "串流分析時間範圍函式簡介 | Microsoft Docs"
description: "深入了解串流分析中的三個時間範圍函式 (輪轉、跳動、滑動)。"
keywords: "輪轉時間範圍、滑動時間範圍、跳動時間範圍"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0d8d8717-5d23-43f0-b475-af078ab4627d
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 09915ad747153210f655b152355c551046066a88
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-stream-analytics-window-functions"></a><span data-ttu-id="3b0f5-104">串流分析時間範圍函式簡介</span><span class="sxs-lookup"><span data-stu-id="3b0f5-104">Introduction to Stream Analytics Window functions</span></span>
<span data-ttu-id="3b0f5-105">在許多即時資串流案例中，只必須對暫時時間範圍中內含的資料執行作業。</span><span class="sxs-lookup"><span data-stu-id="3b0f5-105">In many real time streaming scenarios, it is necessary to perform operations only on the data contained in temporal windows.</span></span> <span data-ttu-id="3b0f5-106">時間範圍函式的原生支援是 Azure 串流分析的重要功能，可對撰寫複雜串流處理作業中的開發人員產能造成重大影響。</span><span class="sxs-lookup"><span data-stu-id="3b0f5-106">Native support for windowing functions is a key feature of Azure Stream Analytics that moves the needle on developer productivity in authoring complex stream processing jobs.</span></span> <span data-ttu-id="3b0f5-107">串流分析可讓開發人員使用[**輪轉**](https://msdn.microsoft.com/library/dn835055.aspx)、[**跳動**](https://msdn.microsoft.com/library/dn835041.aspx)和[**滑動**](https://msdn.microsoft.com/library/dn835051.aspx)時間範圍對串流資料執行暫時作業。</span><span class="sxs-lookup"><span data-stu-id="3b0f5-107">Stream Analytics enables developers to use [**Tumbling**](https://msdn.microsoft.com/library/dn835055.aspx), [**Hopping**](https://msdn.microsoft.com/library/dn835041.aspx) and [**Sliding**](https://msdn.microsoft.com/library/dn835051.aspx) windows to perform temporal operations on streaming data.</span></span> <span data-ttu-id="3b0f5-108">值得注意的是，所有 [時間範圍](https://msdn.microsoft.com/library/dn835019.aspx) 作業都會在時間範圍 **結束** 時輸出結果。</span><span class="sxs-lookup"><span data-stu-id="3b0f5-108">It is worth noting that all [Window](https://msdn.microsoft.com/library/dn835019.aspx) operations output results at the **end** of the window.</span></span> <span data-ttu-id="3b0f5-109">時間範圍的輸出會是以使用的彙總函式為基礎的單一事件。</span><span class="sxs-lookup"><span data-stu-id="3b0f5-109">The output of the window will be single event based on the aggregate function used.</span></span> <span data-ttu-id="3b0f5-110">此事件會有時間範圍結束的時間戳記，所有時間範圍函式都是以固定長度定義。</span><span class="sxs-lookup"><span data-stu-id="3b0f5-110">The event will have the time stamp of the end of the window and all Window functions are defined with a fixed length.</span></span> <span data-ttu-id="3b0f5-111">最後務必注意，所有時間範圍函式都應使用於 [**GROUP BY**](https://msdn.microsoft.com/library/dn835023.aspx) 子句中。</span><span class="sxs-lookup"><span data-stu-id="3b0f5-111">Lastly it is important to note that all Window functions should be used in a [**GROUP BY**](https://msdn.microsoft.com/library/dn835023.aspx) clause.</span></span>

![串流分析時間範圍函式概念](media/stream-analytics-window-functions/stream-analytics-window-functions-conceptual.png)

## <a name="tumbling-window"></a><span data-ttu-id="3b0f5-113">輪轉時間範圍</span><span class="sxs-lookup"><span data-stu-id="3b0f5-113">Tumbling Window</span></span>
<span data-ttu-id="3b0f5-114">輪轉時間範圍函式用於將資料串流分成不同的時間區段並對其執行函式，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="3b0f5-114">Tumbling window functions are used to segment a data stream into distinct time segments and perform a function against them, such as the example below.</span></span> <span data-ttu-id="3b0f5-115">輪轉時間範圍的主要差異在於它們會重複，不會重疊，而事件不能屬於一個以上的輪轉時間範圍。</span><span class="sxs-lookup"><span data-stu-id="3b0f5-115">The key differentiators of a Tumbling window are that they repeat, do not overlap and an event cannot belong to more than one tumbling window.</span></span>

![串流分析時間範圍函式輪轉簡介](media/stream-analytics-window-functions/stream-analytics-window-functions-tumbling-intro.png)

## <a name="hopping-window"></a><span data-ttu-id="3b0f5-117">跳動時間範圍</span><span class="sxs-lookup"><span data-stu-id="3b0f5-117">Hopping Window</span></span>
<span data-ttu-id="3b0f5-118">跳動時間範圍函式會在一段固定的時間向前跳動。</span><span class="sxs-lookup"><span data-stu-id="3b0f5-118">Hopping window functions hop forward in time by a fixed period.</span></span> <span data-ttu-id="3b0f5-119">簡單將這類函式視為可以重疊的輪轉時間範圍，因此事件可以屬於一個以上的跳動時間範圍結果集。</span><span class="sxs-lookup"><span data-stu-id="3b0f5-119">It may be easy to think of them as Tumbling windows that can overlap, so events can belong to more than one Hopping window result set.</span></span> <span data-ttu-id="3b0f5-120">若要讓跳動時間範圍與輪轉時間範圍一樣，您只要將躍點大小指定成與時間範圍大小相同。</span><span class="sxs-lookup"><span data-stu-id="3b0f5-120">To make a Hopping window the same as a Tumbling window one would simply specify the hop size to be the same as the window size.</span></span> 

![串流分析時間範圍函式跳動簡介](media/stream-analytics-window-functions/stream-analytics-window-functions-hopping-intro.png)

## <a name="sliding-window"></a><span data-ttu-id="3b0f5-122">滑動時間範圍</span><span class="sxs-lookup"><span data-stu-id="3b0f5-122">Sliding Window</span></span>
<span data-ttu-id="3b0f5-123">不同於輪轉或跳動時間範圍，滑動時間範圍函式**只**會在事件發生時產生輸出。</span><span class="sxs-lookup"><span data-stu-id="3b0f5-123">Sliding window functions, unlike Tumbling or Hopping windows, produce an output **only**  when an event occurs.</span></span> <span data-ttu-id="3b0f5-124">每個時間範圍都至少會有一個事件，而且時間範圍會持續依據 € (epsilon) 向前移動。</span><span class="sxs-lookup"><span data-stu-id="3b0f5-124">Every window will have at least one event and the window continuously moves forward by an € (epsilon).</span></span> <span data-ttu-id="3b0f5-125">如同跳動時間範圍，事件可以屬於一個以上的滑動時間範圍。</span><span class="sxs-lookup"><span data-stu-id="3b0f5-125">Like Hopping Windows, events can belong to more than one Sliding Window.</span></span>

![串流分析時間範圍函式滑動簡介](media/stream-analytics-window-functions/stream-analytics-window-functions-sliding-intro.png)

## <a name="getting-help-with-window-functions"></a><span data-ttu-id="3b0f5-127">取得使用時間範圍函式的說明</span><span class="sxs-lookup"><span data-stu-id="3b0f5-127">Getting help with Window functions</span></span>
<span data-ttu-id="3b0f5-128">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="3b0f5-128">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b0f5-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3b0f5-129">Next steps</span></span>
* [<span data-ttu-id="3b0f5-130">Azure Stream Analytics 介紹</span><span class="sxs-lookup"><span data-stu-id="3b0f5-130">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="3b0f5-131">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3b0f5-131">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="3b0f5-132">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="3b0f5-132">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="3b0f5-133">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="3b0f5-133">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="3b0f5-134">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="3b0f5-134">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

