---
title: "針對 Azure 串流分析與事件中樞接收器進行偵錯 | Microsoft Docs"
description: "查詢最佳做法以配置串流分析作業中的事件中樞取用者群組。"
keywords: "事件中樞限制、取用者群組"
services: stream-analytics
documentationcenter: 
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
ms.openlocfilehash: 145981d0b5eff0c574c5012c85f43a6318ba4126
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="debug-azure-stream-analytics-with-event-hub-receivers"></a><span data-ttu-id="ced20-104">針對 Azure 串流分析與事件中樞接收器進行偵錯</span><span class="sxs-lookup"><span data-stu-id="ced20-104">Debug Azure Stream Analytics with event hub receivers</span></span>

<span data-ttu-id="ced20-105">您可以使用 Azure 串流分析中的 Azure 事件中樞，來內嵌或輸出作業的資料。</span><span class="sxs-lookup"><span data-stu-id="ced20-105">You can use Azure Event Hubs in Azure Stream Analytics to ingest or output data from a job.</span></span> <span data-ttu-id="ced20-106">使用事件中樞的最佳做法是使用多個取用者群組，以確保作業延展性。</span><span class="sxs-lookup"><span data-stu-id="ced20-106">A best practice for using Event Hubs is to use multiple consumer groups, to ensure job scalability.</span></span> <span data-ttu-id="ced20-107">其中一個原因是在特定輸入的串流分析作業中，其讀取器數量會影響單一取用者群組中的讀取器數量。</span><span class="sxs-lookup"><span data-stu-id="ced20-107">One reason is that the number of readers in the Stream Analytics job for a specific input affects the number of readers in a single consumer group.</span></span> <span data-ttu-id="ced20-108">接收器精確數量會以擴展拓撲邏輯的內部實作詳細資料為基礎。</span><span class="sxs-lookup"><span data-stu-id="ced20-108">The precise number of receivers is based on internal implementation details for the scale-out topology logic.</span></span> <span data-ttu-id="ced20-109">接收器數量不會向外公開。</span><span class="sxs-lookup"><span data-stu-id="ced20-109">The number of receivers is not exposed externally.</span></span> <span data-ttu-id="ced20-110">讀取器數量可在作業開始時或作業升級期間變更。</span><span class="sxs-lookup"><span data-stu-id="ced20-110">The number of readers can change either at the job start time or during job upgrades.</span></span>

> [!NOTE]
> <span data-ttu-id="ced20-111">如果在作業升級期間變更讀取器數量，暫時性警告會寫入稽核記錄中。</span><span class="sxs-lookup"><span data-stu-id="ced20-111">When the number of readers changes during a job upgrade, transient warnings are written to audit logs.</span></span> <span data-ttu-id="ced20-112">串流分析作業會從這些暫時性問題中自動復原。</span><span class="sxs-lookup"><span data-stu-id="ced20-112">Stream Analytics jobs automatically recover from these transient issues.</span></span>

## <a name="number-of-readers-per-partition-exceeds-event-hubs-limit-of-five"></a><span data-ttu-id="ced20-113">讀取器數量 (每個分割區) 超過事件中樞上限 (5 個)</span><span class="sxs-lookup"><span data-stu-id="ced20-113">Number of readers per partition exceeds Event Hubs limit of five</span></span>

<span data-ttu-id="ced20-114">讀取器數量 (每個分割區) 超過事件中樞上限 (5 個) 的情況如下：</span><span class="sxs-lookup"><span data-stu-id="ced20-114">Scenarios in which the number of readers per partition exceeds the Event Hubs limit of five include the following:</span></span>

* <span data-ttu-id="ced20-115">多個 SELECT 陳述式︰ 如果您使用多個 SELECT 陳述式參照**相同**的事件中樞輸入，則每個 SELECT 陳述式皆會造成新的接收器建立。</span><span class="sxs-lookup"><span data-stu-id="ced20-115">Multiple SELECT statements: If you use multiple SELECT statements that refer to **same** event hub input, each SELECT statement causes a new receiver to be created.</span></span>
* <span data-ttu-id="ced20-116">UNION︰當您使用 UNION 時，就有可能會有多個輸入參照**相同**的事件中樞和取用者群組。</span><span class="sxs-lookup"><span data-stu-id="ced20-116">UNION: When you use a UNION, it's possible to have multiple inputs that refer to the **same** event hub and consumer group.</span></span>
* <span data-ttu-id="ced20-117">SELF JOIN︰當您使用 SELF JOIN 作業時，就可能發生參照**相同**事件中樞多次的情形。</span><span class="sxs-lookup"><span data-stu-id="ced20-117">SELF JOIN: When you use a SELF JOIN operation, it's possible to refer to the **same** event hub multiple times.</span></span>

## <a name="solution"></a><span data-ttu-id="ced20-118">方案</span><span class="sxs-lookup"><span data-stu-id="ced20-118">Solution</span></span>

<span data-ttu-id="ced20-119">以下最佳做法可減少讀取器數量 (每個分割區) 超過事件中樞上限 (5 個) 的情況。</span><span class="sxs-lookup"><span data-stu-id="ced20-119">The following best practices can help mitigate scenarios in which the number of readers per partition exceeds the Event Hubs limit of five.</span></span>

### <a name="split-your-query-into-multiple-steps-by-using-a-with-clause"></a><span data-ttu-id="ced20-120">使用 WITH 子句將查詢分割成多個步驟</span><span class="sxs-lookup"><span data-stu-id="ced20-120">Split your query into multiple steps by using a WITH clause</span></span>

<span data-ttu-id="ced20-121">WITH 子句會指定名為結果集的暫存，並且可由查詢中的 FROM 子句加以參照。</span><span class="sxs-lookup"><span data-stu-id="ced20-121">The WITH clause specifies a temporary named result set that can be referenced by a FROM clause in the query.</span></span> <span data-ttu-id="ced20-122">您可以定義單一 SELECT 陳述式執行範圍的 WITH 子句。</span><span class="sxs-lookup"><span data-stu-id="ced20-122">You define the WITH clause in the execution scope of a single SELECT statement.</span></span>

<span data-ttu-id="ced20-123">例如，不要使用此查詢︰</span><span class="sxs-lookup"><span data-stu-id="ced20-123">For example, instead of this query:</span></span>

```
SELECT foo 
INTO output1
FROM inputEventHub

SELECT bar
INTO output2
FROM inputEventHub 
…
```

<span data-ttu-id="ced20-124">使用此查詢︰</span><span class="sxs-lookup"><span data-stu-id="ced20-124">Use this query:</span></span>

```
WITH input (
   SELECT * FROM inputEventHub
) as data

SELECT foo
INTO output1
FROM data

SELECT bar
INTO output2
FROM data
…
```

### <a name="ensure-that-inputs-bind-to-different-consumer-groups"></a><span data-ttu-id="ced20-125">請確定這些輸入會繫結至不同的取用者群組</span><span class="sxs-lookup"><span data-stu-id="ced20-125">Ensure that inputs bind to different consumer groups</span></span>

<span data-ttu-id="ced20-126">如果查詢中有三個以上的輸入與同一個事件中樞取用者群組連線，請建立個別的取用者群組。</span><span class="sxs-lookup"><span data-stu-id="ced20-126">For queries in which three or more inputs are connected to the same Event Hubs consumer group, create separate consumer groups.</span></span> <span data-ttu-id="ced20-127">這需要建立其他串流分析輸入。</span><span class="sxs-lookup"><span data-stu-id="ced20-127">This requires the creation of additional Stream Analytics inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="ced20-128">取得說明</span><span class="sxs-lookup"><span data-stu-id="ced20-128">Get help</span></span>
<span data-ttu-id="ced20-129">如需其他協助，請參閱我們的 [Azure 串流分析論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。</span><span class="sxs-lookup"><span data-stu-id="ced20-129">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ced20-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ced20-130">Next steps</span></span>
* [<span data-ttu-id="ced20-131">串流分析介紹</span><span class="sxs-lookup"><span data-stu-id="ced20-131">Introduction to Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="ced20-132">開始使用串流分析</span><span class="sxs-lookup"><span data-stu-id="ced20-132">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="ced20-133">調整串流分析作業</span><span class="sxs-lookup"><span data-stu-id="ced20-133">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="ced20-134">串流分析查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="ced20-134">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="ced20-135">串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="ced20-135">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
