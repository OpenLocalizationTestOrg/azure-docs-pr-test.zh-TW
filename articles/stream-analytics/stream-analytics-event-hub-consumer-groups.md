---
title: "使用事件中樞接收者 aaaDebug Azure Stream Analytics |Microsoft 文件"
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
ms.openlocfilehash: 89821e6273151de43b5e42d907e547c939e24824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="debug-azure-stream-analytics-with-event-hub-receivers"></a><span data-ttu-id="6f0f1-104">針對 Azure 串流分析與事件中樞接收器進行偵錯</span><span class="sxs-lookup"><span data-stu-id="6f0f1-104">Debug Azure Stream Analytics with event hub receivers</span></span>

<span data-ttu-id="6f0f1-105">Azure Stream Analytics tooingest 或輸出資料從作業中，您可以使用 Azure 事件中心。</span><span class="sxs-lookup"><span data-stu-id="6f0f1-105">You can use Azure Event Hubs in Azure Stream Analytics tooingest or output data from a job.</span></span> <span data-ttu-id="6f0f1-106">使用事件中心的最佳作法是 toouse 多個取用者群組、 tooensure 作業延展性。</span><span class="sxs-lookup"><span data-stu-id="6f0f1-106">A best practice for using Event Hubs is toouse multiple consumer groups, tooensure job scalability.</span></span> <span data-ttu-id="6f0f1-107">其中一個原因是特定的輸入的 hello Stream Analytics 工作中的讀取器的 hello 數目會影響單一取用者群組中的讀取器的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="6f0f1-107">One reason is that hello number of readers in hello Stream Analytics job for a specific input affects hello number of readers in a single consumer group.</span></span> <span data-ttu-id="6f0f1-108">hello 精確接收者數目根據 hello 向外延展拓撲邏輯的內部實作詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6f0f1-108">hello precise number of receivers is based on internal implementation details for hello scale-out topology logic.</span></span> <span data-ttu-id="6f0f1-109">hello 接收者數目不會從外部公開。</span><span class="sxs-lookup"><span data-stu-id="6f0f1-109">hello number of receivers is not exposed externally.</span></span> <span data-ttu-id="6f0f1-110">在 hello 工作開始時間，或是在升級作業期間，可以變更 hello 讀取器數目。</span><span class="sxs-lookup"><span data-stu-id="6f0f1-110">hello number of readers can change either at hello job start time or during job upgrades.</span></span>

> [!NOTE]
> <span data-ttu-id="6f0f1-111">當作業在升級期間，變更 hello 讀取器數目時，暫時性的警告會寫入 tooaudit 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="6f0f1-111">When hello number of readers changes during a job upgrade, transient warnings are written tooaudit logs.</span></span> <span data-ttu-id="6f0f1-112">串流分析作業會從這些暫時性問題中自動復原。</span><span class="sxs-lookup"><span data-stu-id="6f0f1-112">Stream Analytics jobs automatically recover from these transient issues.</span></span>

## <a name="number-of-readers-per-partition-exceeds-event-hubs-limit-of-five"></a><span data-ttu-id="6f0f1-113">讀取器數量 (每個分割區) 超過事件中樞上限 (5 個)</span><span class="sxs-lookup"><span data-stu-id="6f0f1-113">Number of readers per partition exceeds Event Hubs limit of five</span></span>

<span data-ttu-id="6f0f1-114">案例中的 hello 的每個資料分割的讀取器數目超過五個 hello 事件中心限制 hello 如下：</span><span class="sxs-lookup"><span data-stu-id="6f0f1-114">Scenarios in which hello number of readers per partition exceeds hello Event Hubs limit of five include hello following:</span></span>

* <span data-ttu-id="6f0f1-115">多個 SELECT 陳述式： 如果您使用多個 SELECT 陳述式，請參閱太**相同**事件中樞輸入，每個 SELECT 陳述式會建立新的接收者 toobe。</span><span class="sxs-lookup"><span data-stu-id="6f0f1-115">Multiple SELECT statements: If you use multiple SELECT statements that refer too**same** event hub input, each SELECT statement causes a new receiver toobe created.</span></span>
* <span data-ttu-id="6f0f1-116">等位： 當您使用等位時，很可能 toohave 參考 toohello 的多個輸入**相同**事件中樞取用者群組。</span><span class="sxs-lookup"><span data-stu-id="6f0f1-116">UNION: When you use a UNION, it's possible toohave multiple inputs that refer toohello **same** event hub and consumer group.</span></span>
* <span data-ttu-id="6f0f1-117">自我聯結： 當您使用自我聯結作業時，就可能 toorefer toohello**相同**事件中心多次。</span><span class="sxs-lookup"><span data-stu-id="6f0f1-117">SELF JOIN: When you use a SELF JOIN operation, it's possible toorefer toohello **same** event hub multiple times.</span></span>

## <a name="solution"></a><span data-ttu-id="6f0f1-118">方案</span><span class="sxs-lookup"><span data-stu-id="6f0f1-118">Solution</span></span>

<span data-ttu-id="6f0f1-119">hello 下列最佳作法可協助減少的案例中的 hello 的每個資料分割的讀取器數目超過五個 hello 事件中心限制。</span><span class="sxs-lookup"><span data-stu-id="6f0f1-119">hello following best practices can help mitigate scenarios in which hello number of readers per partition exceeds hello Event Hubs limit of five.</span></span>

### <a name="split-your-query-into-multiple-steps-by-using-a-with-clause"></a><span data-ttu-id="6f0f1-120">使用 WITH 子句將查詢分割成多個步驟</span><span class="sxs-lookup"><span data-stu-id="6f0f1-120">Split your query into multiple steps by using a WITH clause</span></span>

<span data-ttu-id="6f0f1-121">hello WITH 子句指定可以在 hello 查詢的 FROM 子句中參考的暫存具名的結果集。</span><span class="sxs-lookup"><span data-stu-id="6f0f1-121">hello WITH clause specifies a temporary named result set that can be referenced by a FROM clause in hello query.</span></span> <span data-ttu-id="6f0f1-122">您可以定義 hello WITH 子句 hello 執行範圍中的單一 SELECT 陳述式。</span><span class="sxs-lookup"><span data-stu-id="6f0f1-122">You define hello WITH clause in hello execution scope of a single SELECT statement.</span></span>

<span data-ttu-id="6f0f1-123">例如，不要使用此查詢︰</span><span class="sxs-lookup"><span data-stu-id="6f0f1-123">For example, instead of this query:</span></span>

```
SELECT foo 
INTO output1
FROM inputEventHub

SELECT bar
INTO output2
FROM inputEventHub 
…
```

<span data-ttu-id="6f0f1-124">使用此查詢︰</span><span class="sxs-lookup"><span data-stu-id="6f0f1-124">Use this query:</span></span>

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

### <a name="ensure-that-inputs-bind-toodifferent-consumer-groups"></a><span data-ttu-id="6f0f1-125">請確定輸入繫結 toodifferent 取用者群組</span><span class="sxs-lookup"><span data-stu-id="6f0f1-125">Ensure that inputs bind toodifferent consumer groups</span></span>

<span data-ttu-id="6f0f1-126">查詢中的三個或多個輸入是連接的 toohello 相同事件中心取用者群組中，建立個別取用者群組。</span><span class="sxs-lookup"><span data-stu-id="6f0f1-126">For queries in which three or more inputs are connected toohello same Event Hubs consumer group, create separate consumer groups.</span></span> <span data-ttu-id="6f0f1-127">這需要額外的資料流分析輸入 hello 建立。</span><span class="sxs-lookup"><span data-stu-id="6f0f1-127">This requires hello creation of additional Stream Analytics inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="6f0f1-128">取得說明</span><span class="sxs-lookup"><span data-stu-id="6f0f1-128">Get help</span></span>
<span data-ttu-id="6f0f1-129">如需其他協助，請參閱我們的 [Azure 串流分析論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。</span><span class="sxs-lookup"><span data-stu-id="6f0f1-129">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f0f1-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6f0f1-130">Next steps</span></span>
* [<span data-ttu-id="6f0f1-131">簡介 tooStream 分析</span><span class="sxs-lookup"><span data-stu-id="6f0f1-131">Introduction tooStream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="6f0f1-132">開始使用串流分析</span><span class="sxs-lookup"><span data-stu-id="6f0f1-132">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="6f0f1-133">調整串流分析作業</span><span class="sxs-lookup"><span data-stu-id="6f0f1-133">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="6f0f1-134">串流分析查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="6f0f1-134">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="6f0f1-135">串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="6f0f1-135">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
