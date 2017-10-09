---
title: "診斷記錄的批次事件-Azure aaaEnable |Microsoft 文件"
description: "記錄並分析 Azure Batch 帳戶資源 (如集區和工作) 的診斷記錄事件。"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: e14e611d-12cd-4671-91dc-bc506dc853e5
ms.service: batch
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9d03303a3e857e9303f40cc6de5c32b5a51d8f8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="log-events-for-diagnostic-evaluation-and-monitoring-of-batch-solutions"></a><span data-ttu-id="655d9-103">記錄事件以便對 Batch 解決方案進行診斷評估和監視</span><span class="sxs-lookup"><span data-stu-id="655d9-103">Log events for diagnostic evaluation and monitoring of Batch solutions</span></span>

<span data-ttu-id="655d9-104">如同許多 Azure 服務，hello 批次服務會發出某些資源期間 hello hello 資源的存留期的記錄事件。</span><span class="sxs-lookup"><span data-stu-id="655d9-104">As with many Azure services, hello Batch service emits log events for certain resources during hello lifetime of hello resource.</span></span> <span data-ttu-id="655d9-105">您可以啟用 Azure 批次的資源集區和工作，如的診斷記錄檔 toorecord 事件，然後再使用 診斷評估及監視 hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="655d9-105">You can enable Azure Batch diagnostic logs toorecord events for resources like pools and tasks, and then use hello logs for diagnostic evaluation and monitoring.</span></span> <span data-ttu-id="655d9-106">集區建立、集區刪除、工作開始、工作完成及其他事件等，都會包含在 Batch 診斷記錄中。</span><span class="sxs-lookup"><span data-stu-id="655d9-106">Events like pool create, pool delete, task start, task complete, and others are included in Batch diagnostic logs.</span></span>

> [!NOTE]
> <span data-ttu-id="655d9-107">本文討論 Batch 帳戶資源本身的記錄事件，而非作業和工作輸出資料。</span><span class="sxs-lookup"><span data-stu-id="655d9-107">This article discusses logging events for Batch account resources themselves, not job and task output data.</span></span> <span data-ttu-id="655d9-108">如需儲存 hello 輸出資料，您的工作和工作的詳細資訊，請參閱[保存 Azure 批次作業和工作的輸出](batch-task-output.md)。</span><span class="sxs-lookup"><span data-stu-id="655d9-108">For details on storing hello output data of your jobs and tasks, see [Persist Azure Batch job and task output](batch-task-output.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="655d9-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="655d9-109">Prerequisites</span></span>
* [<span data-ttu-id="655d9-110">Azure Batch 帳戶</span><span class="sxs-lookup"><span data-stu-id="655d9-110">Azure Batch account</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="655d9-111">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="655d9-111">Azure Storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)
  
  <span data-ttu-id="655d9-112">toopersist 批次診斷記錄檔，您必須建立 Azure 將會在其中儲存 hello 記錄檔的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="655d9-112">toopersist Batch diagnostic logs, you must create an Azure Storage account where Azure will store hello logs.</span></span> <span data-ttu-id="655d9-113">當您為您的 Batch 帳戶[啟用診斷記錄](#enable-diagnostic-logging)時，請指定此儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="655d9-113">You specify this Storage account when you [enable diagnostic logging](#enable-diagnostic-logging) for your Batch account.</span></span> <span data-ttu-id="655d9-114">hello 您指定當您啟用收集記錄的儲存體帳戶不是 hello 相同為連結的儲存體帳戶參照的 tooin hello[應用程式封裝](batch-application-packages.md)和[工作輸出的持續性](batch-task-output.md)文件。</span><span class="sxs-lookup"><span data-stu-id="655d9-114">hello Storage account you specify when you enable log collection is not hello same as a linked storage account referred tooin hello [application packages](batch-application-packages.md) and [task output persistence](batch-task-output.md) articles.</span></span>
  
  > [!WARNING]
  > <span data-ttu-id="655d9-115">您是**收費**hello 資料儲存在您的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="655d9-115">You are **charged** for hello data stored in your Azure Storage account.</span></span> <span data-ttu-id="655d9-116">這包括 hello 本文所討論的診斷記錄檔。</span><span class="sxs-lookup"><span data-stu-id="655d9-116">This includes hello diagnostic logs discussed in this article.</span></span> <span data-ttu-id="655d9-117">在設計您的[記錄保留原則](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)時請牢記這一點。</span><span class="sxs-lookup"><span data-stu-id="655d9-117">Keep this in mind when designing your [log retention policy](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span></span>
  > 
  > 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="655d9-118">啟用診斷記錄</span><span class="sxs-lookup"><span data-stu-id="655d9-118">Enable diagnostic logging</span></span>
<span data-ttu-id="655d9-119">您的 Batch 帳戶預設未啟用診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="655d9-119">Diagnostic logging is not enabled by default for your Batch account.</span></span> <span data-ttu-id="655d9-120">您必須明確啟用診斷記錄的每個您想要讓 toomonitor 的批次帳戶：</span><span class="sxs-lookup"><span data-stu-id="655d9-120">You must explicitly enable diagnostic logging for each Batch account you want toomonitor:</span></span>

[<span data-ttu-id="655d9-121">如何 tooenable 收集診斷記錄檔</span><span class="sxs-lookup"><span data-stu-id="655d9-121">How tooenable collection of Diagnostic Logs</span></span>](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)

<span data-ttu-id="655d9-122">我們建議您先閱讀完整 hello[概觀的 Azure 診斷記錄檔](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)文章 toogain 不僅如何 tooenable 記錄，但 hello 登類別了解支援 hello 各種 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="655d9-122">We recommend that you read hello full [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article toogain an understanding of not only how tooenable logging, but hello log categories supported by hello various Azure services.</span></span> <span data-ttu-id="655d9-123">例如，Azure Batch 目前支援一種記錄類別︰**服務記錄檔**。</span><span class="sxs-lookup"><span data-stu-id="655d9-123">For example, Azure Batch currently supports one log category: **Service Logs**.</span></span>

## <a name="service-logs"></a><span data-ttu-id="655d9-124">服務記錄檔</span><span class="sxs-lookup"><span data-stu-id="655d9-124">Service Logs</span></span>
<span data-ttu-id="655d9-125">Azure 批次服務記錄檔包含在 hello 的批次之類的資源集區或工作的存留期 hello Azure 批次服務所發出的事件。</span><span class="sxs-lookup"><span data-stu-id="655d9-125">Azure Batch Service Logs contain events emitted by hello Azure Batch service during hello lifetime of a Batch resource like a pool or task.</span></span> <span data-ttu-id="655d9-126">每個批次所發出的事件會儲存在指定的 hello 以 JSON 格式的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="655d9-126">Each event emitted by Batch is stored in hello specified Storage account in JSON format.</span></span> <span data-ttu-id="655d9-127">比方說，這是範例 hello 主體**集區建立事件**:</span><span class="sxs-lookup"><span data-stu-id="655d9-127">For example, this is hello body of a sample **pool create event**:</span></span>

```json
{
    "poolId": "myPool1",
    "displayName": "Production Pool",
    "vmSize": "Small",
    "cloudServiceConfiguration": {
        "osFamily": "4",
        "targetOsVersion": "*"
    },
    "networkConfiguration": {
        "subnetId": " "
    },
    "resizeTimeout": "300000",
    "targetDedicatedComputeNodes": 2,
    "maxTasksPerNode": 1,
    "vmFillType": "Spread",
    "enableAutoscale": false,
    "enableInterNodeCommunication": false,
    "isAutoPool": false
}
```

<span data-ttu-id="655d9-128">每個事件主體位於.json 檔案 hello 中的指定 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="655d9-128">Each event body resides in a .json file in hello specified Azure Storage account.</span></span> <span data-ttu-id="655d9-129">如果您想直接 tooaccess hello 的記錄檔，您可能希望 tooreview hello [hello 儲存體帳戶中的診斷記錄檔的結構描述](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="655d9-129">If you want tooaccess hello logs directly, you may wish tooreview hello [schema of Diagnostic Logs in hello storage account](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span></span>

## <a name="service-log-events"></a><span data-ttu-id="655d9-130">服務記錄檔事件</span><span class="sxs-lookup"><span data-stu-id="655d9-130">Service Log events</span></span>
<span data-ttu-id="655d9-131">目前，hello 批次服務會發出 hello 下列服務記錄檔事件。</span><span class="sxs-lookup"><span data-stu-id="655d9-131">hello Batch service currently emits hello following Service Log events.</span></span> <span data-ttu-id="655d9-132">這份清單可能不完整，因為自上次更新此文件後可能已新增額外的事件。</span><span class="sxs-lookup"><span data-stu-id="655d9-132">This list may not be exhaustive, since additional events may have been added since this article was last updated.</span></span>

| <span data-ttu-id="655d9-133">**服務記錄檔事件**</span><span class="sxs-lookup"><span data-stu-id="655d9-133">**Service Log events**</span></span> |
| --- |
| <span data-ttu-id="655d9-134">[建立集區][pool_create]</span><span class="sxs-lookup"><span data-stu-id="655d9-134">[Pool create][pool_create]</span></span> |
| <span data-ttu-id="655d9-135">[開始刪除集區][pool_delete_start]</span><span class="sxs-lookup"><span data-stu-id="655d9-135">[Pool delete start][pool_delete_start]</span></span> |
| <span data-ttu-id="655d9-136">[完成集區刪除][pool_delete_complete]</span><span class="sxs-lookup"><span data-stu-id="655d9-136">[Pool delete complete][pool_delete_complete]</span></span> |
| <span data-ttu-id="655d9-137">[開始調整集區大小][pool_resize_start]</span><span class="sxs-lookup"><span data-stu-id="655d9-137">[Pool resize start][pool_resize_start]</span></span> |
| <span data-ttu-id="655d9-138">[完成集區大小調整][pool_resize_complete]</span><span class="sxs-lookup"><span data-stu-id="655d9-138">[Pool resize complete][pool_resize_complete]</span></span> |
| <span data-ttu-id="655d9-139">[開始工作][task_start]</span><span class="sxs-lookup"><span data-stu-id="655d9-139">[Task start][task_start]</span></span> |
| <span data-ttu-id="655d9-140">[完成工作][task_complete]</span><span class="sxs-lookup"><span data-stu-id="655d9-140">[Task complete][task_complete]</span></span> |
| <span data-ttu-id="655d9-141">[工作失敗][task_fail]</span><span class="sxs-lookup"><span data-stu-id="655d9-141">[Task fail][task_fail]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="655d9-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="655d9-142">Next steps</span></span>
<span data-ttu-id="655d9-143">在 Azure 儲存體帳戶中的加法 toostoring 診斷記錄事件，您也可以送批次服務記錄檔事件 tooan [Azure 事件中心](../event-hubs/event-hubs-what-is-event-hubs.md)，並將它們傳送到太[Azure Log Analytics](../log-analytics/log-analytics-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="655d9-143">In addition toostoring diagnostic log events in an Azure Storage account, you can also stream Batch Service Log events tooan [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md), and send them too[Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span>

* [<span data-ttu-id="655d9-144">資料流 Azure 診斷記錄檔 tooEvent 集線器</span><span class="sxs-lookup"><span data-stu-id="655d9-144">Stream Azure Diagnostic Logs tooEvent Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md)
  
  <span data-ttu-id="655d9-145">串流處理批次的診斷事件 toohello 高度可擴充的資料輸入服務，事件中心。</span><span class="sxs-lookup"><span data-stu-id="655d9-145">Stream Batch diagnostic events toohello highly scalable data ingress service, Event Hubs.</span></span> <span data-ttu-id="655d9-146">事件中樞每秒可輸入數百萬個事件，您可以使用任何即時分析提供者來轉換和儲存。</span><span class="sxs-lookup"><span data-stu-id="655d9-146">Event Hubs can ingest millions of events per second, which you can then transform and store using any real-time analytics provider.</span></span>
* [<span data-ttu-id="655d9-147">使用 Log Analytics 分析 Azure 診斷記錄</span><span class="sxs-lookup"><span data-stu-id="655d9-147">Analyze Azure diagnostic logs using Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
  
  <span data-ttu-id="655d9-148">傳送您的診斷記錄檔 tooLog 分析，您可以在此分析它們在 hello Operations Management Suite (OMS) 的入口網站，或將它們匯出為 Power BI 或 Excel 中分析。</span><span class="sxs-lookup"><span data-stu-id="655d9-148">Send your diagnostic logs tooLog Analytics where you can analyze them in hello Operations Management Suite (OMS) portal, or export them for analysis in Power BI or Excel.</span></span>

[pool_create]: https://msdn.microsoft.com/library/azure/mt743615.aspx
[pool_delete_start]: https://msdn.microsoft.com/library/azure/mt743610.aspx
[pool_delete_complete]: https://msdn.microsoft.com/library/azure/mt743618.aspx
[pool_resize_start]: https://msdn.microsoft.com/library/azure/mt743609.aspx
[pool_resize_complete]: https://msdn.microsoft.com/library/azure/mt743608.aspx
[task_start]: https://msdn.microsoft.com/library/azure/mt743616.aspx
[task_complete]: https://msdn.microsoft.com/library/azure/mt743612.aspx
[task_fail]: https://msdn.microsoft.com/library/azure/mt743607.aspx
