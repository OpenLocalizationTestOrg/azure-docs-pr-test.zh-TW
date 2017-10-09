---
title: "aaaIntroduction tooStream 分析視窗函數 |Microsoft 文件"
description: "深入了解在 Stream Analytics 輪轉、 跳動 (滑動） hello 三個視窗函數。"
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
ms.openlocfilehash: 7fc36eb9afb2b28e2791d925d26923145eb38074
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toostream-analytics-window-functions"></a><span data-ttu-id="f439e-104">簡介 tooStream Analytics 視窗函式</span><span class="sxs-lookup"><span data-stu-id="f439e-104">Introduction tooStream Analytics Window functions</span></span>
<span data-ttu-id="f439e-105">在許多即時資料流案例來說，是只在暫時的視窗中所包含的 hello 資料上的必要 tooperform 作業。</span><span class="sxs-lookup"><span data-stu-id="f439e-105">In many real time streaming scenarios, it is necessary tooperform operations only on hello data contained in temporal windows.</span></span> <span data-ttu-id="f439e-106">一項重要功能的 Azure Stream Analytics 將 hello 指針移動上撰寫複雜的資料流處理工作的開發人員生產力視窗化函式的原生支援。</span><span class="sxs-lookup"><span data-stu-id="f439e-106">Native support for windowing functions is a key feature of Azure Stream Analytics that moves hello needle on developer productivity in authoring complex stream processing jobs.</span></span> <span data-ttu-id="f439e-107">資料流分析可讓開發人員 toouse [**輪轉**](https://msdn.microsoft.com/library/dn835055.aspx)， [ **Hopping** ](https://msdn.microsoft.com/library/dn835041.aspx)和[**滑動**](https://msdn.microsoft.com/library/dn835051.aspx) windows tooperform 時態上的作業資料流處理資料。</span><span class="sxs-lookup"><span data-stu-id="f439e-107">Stream Analytics enables developers toouse [**Tumbling**](https://msdn.microsoft.com/library/dn835055.aspx), [**Hopping**](https://msdn.microsoft.com/library/dn835041.aspx) and [**Sliding**](https://msdn.microsoft.com/library/dn835051.aspx) windows tooperform temporal operations on streaming data.</span></span> <span data-ttu-id="f439e-108">值得注意的是，所有[視窗](https://msdn.microsoft.com/library/dn835019.aspx)作業輸出結果在 hello**結束**hello 視窗。</span><span class="sxs-lookup"><span data-stu-id="f439e-108">It is worth noting that all [Window](https://msdn.microsoft.com/library/dn835019.aspx) operations output results at hello **end** of hello window.</span></span> <span data-ttu-id="f439e-109">hello hello 視窗輸出將會根據使用 hello 彙總函式的單一事件。</span><span class="sxs-lookup"><span data-stu-id="f439e-109">hello output of hello window will be single event based on hello aggregate function used.</span></span> <span data-ttu-id="f439e-110">所有的視窗函數定義固定長度與 hello 事件將會有 hello hello hello 視窗結束時間戳記。</span><span class="sxs-lookup"><span data-stu-id="f439e-110">hello event will have hello time stamp of hello end of hello window and all Window functions are defined with a fixed length.</span></span> <span data-ttu-id="f439e-111">它最後會應用於所有的視窗函數的重要 toonote [ **GROUP BY** ](https://msdn.microsoft.com/library/dn835023.aspx)子句。</span><span class="sxs-lookup"><span data-stu-id="f439e-111">Lastly it is important toonote that all Window functions should be used in a [**GROUP BY**](https://msdn.microsoft.com/library/dn835023.aspx) clause.</span></span>

![串流分析時間範圍函式概念](media/stream-analytics-window-functions/stream-analytics-window-functions-conceptual.png)

## <a name="tumbling-window"></a><span data-ttu-id="f439e-113">輪轉時間範圍</span><span class="sxs-lookup"><span data-stu-id="f439e-113">Tumbling Window</span></span>
<span data-ttu-id="f439e-114">輪轉視窗函數會使用的 toosegment 到不同的時間區段的資料流，並執行它們，針對在函式，例如以下 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="f439e-114">Tumbling window functions are used toosegment a data stream into distinct time segments and perform a function against them, such as hello example below.</span></span> <span data-ttu-id="f439e-115">輪轉視窗的 hello 重要的區別因素是，它們重複，沒有重疊，而且事件不能隸屬於一個輪轉視窗 toomore。</span><span class="sxs-lookup"><span data-stu-id="f439e-115">hello key differentiators of a Tumbling window are that they repeat, do not overlap and an event cannot belong toomore than one tumbling window.</span></span>

![串流分析時間範圍函式輪轉簡介](media/stream-analytics-window-functions/stream-analytics-window-functions-tumbling-intro.png)

## <a name="hopping-window"></a><span data-ttu-id="f439e-117">跳動時間範圍</span><span class="sxs-lookup"><span data-stu-id="f439e-117">Hopping Window</span></span>
<span data-ttu-id="f439e-118">跳動時間範圍函式會在一段固定的時間向前跳動。</span><span class="sxs-lookup"><span data-stu-id="f439e-118">Hopping window functions hop forward in time by a fixed period.</span></span> <span data-ttu-id="f439e-119">它可能是簡單 toothink 它們做為可以重疊的輪轉視窗，所以事件可以隸屬 toomore 比 Hopping 視窗結果集。</span><span class="sxs-lookup"><span data-stu-id="f439e-119">It may be easy toothink of them as Tumbling windows that can overlap, so events can belong toomore than one Hopping window result set.</span></span> <span data-ttu-id="f439e-120">toomake Hopping 視窗相同 hello 做為另一個只會指定的輪轉視窗 hello 躍點大小 toobe 相同 hello 與 hello 視窗大小。</span><span class="sxs-lookup"><span data-stu-id="f439e-120">toomake a Hopping window hello same as a Tumbling window one would simply specify hello hop size toobe hello same as hello window size.</span></span> 

![串流分析時間範圍函式跳動簡介](media/stream-analytics-window-functions/stream-analytics-window-functions-hopping-intro.png)

## <a name="sliding-window"></a><span data-ttu-id="f439e-122">滑動時間範圍</span><span class="sxs-lookup"><span data-stu-id="f439e-122">Sliding Window</span></span>
<span data-ttu-id="f439e-123">不同於輪轉或跳動時間範圍，滑動時間範圍函式**只**會在事件發生時產生輸出。</span><span class="sxs-lookup"><span data-stu-id="f439e-123">Sliding window functions, unlike Tumbling or Hopping windows, produce an output **only**  when an event occurs.</span></span> <span data-ttu-id="f439e-124">每個視窗會有一個以上的事件和 hello 視窗持續推進由 € (epsilon)。</span><span class="sxs-lookup"><span data-stu-id="f439e-124">Every window will have at least one event and hello window continuously moves forward by an € (epsilon).</span></span> <span data-ttu-id="f439e-125">跳動視窗，類似事件可隸屬 toomore 超過一個滑動視窗。</span><span class="sxs-lookup"><span data-stu-id="f439e-125">Like Hopping Windows, events can belong toomore than one Sliding Window.</span></span>

![串流分析時間範圍函式滑動簡介](media/stream-analytics-window-functions/stream-analytics-window-functions-sliding-intro.png)

## <a name="getting-help-with-window-functions"></a><span data-ttu-id="f439e-127">取得使用時間範圍函式的說明</span><span class="sxs-lookup"><span data-stu-id="f439e-127">Getting help with Window functions</span></span>
<span data-ttu-id="f439e-128">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="f439e-128">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f439e-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f439e-129">Next steps</span></span>
* [<span data-ttu-id="f439e-130">簡介 tooAzure 資料流分析</span><span class="sxs-lookup"><span data-stu-id="f439e-130">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="f439e-131">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f439e-131">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="f439e-132">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="f439e-132">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="f439e-133">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="f439e-133">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="f439e-134">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="f439e-134">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

