---
title: "啟用 Batch 事件的診斷記錄 - Azure | Microsoft Docs"
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
ms.openlocfilehash: b7bc6fd9921ab0f2374ace33ea5c1ab93a78f860
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="log-events-for-diagnostic-evaluation-and-monitoring-of-batch-solutions"></a><span data-ttu-id="9b555-103">記錄事件以便對 Batch 解決方案進行診斷評估和監視</span><span class="sxs-lookup"><span data-stu-id="9b555-103">Log events for diagnostic evaluation and monitoring of Batch solutions</span></span>

<span data-ttu-id="9b555-104">和許多 Azure 服務一樣，Batch 服務會在資源存留期間發出特定資源的記錄事件。</span><span class="sxs-lookup"><span data-stu-id="9b555-104">As with many Azure services, the Batch service emits log events for certain resources during the lifetime of the resource.</span></span> <span data-ttu-id="9b555-105">您可以啟用 Azure Batch 診斷記錄來記錄資源 (如集區和工作) 的事件，接著使用記錄進行診斷評估和監視。</span><span class="sxs-lookup"><span data-stu-id="9b555-105">You can enable Azure Batch diagnostic logs to record events for resources like pools and tasks, and then use the logs for diagnostic evaluation and monitoring.</span></span> <span data-ttu-id="9b555-106">集區建立、集區刪除、工作開始、工作完成及其他事件等，都會包含在 Batch 診斷記錄中。</span><span class="sxs-lookup"><span data-stu-id="9b555-106">Events like pool create, pool delete, task start, task complete, and others are included in Batch diagnostic logs.</span></span>

> [!NOTE]
> <span data-ttu-id="9b555-107">本文討論 Batch 帳戶資源本身的記錄事件，而非作業和工作輸出資料。</span><span class="sxs-lookup"><span data-stu-id="9b555-107">This article discusses logging events for Batch account resources themselves, not job and task output data.</span></span> <span data-ttu-id="9b555-108">如需儲存作業和工作輸出資料的詳細資訊，請參閱[保存 Azure Batch 作業和工作輸出](batch-task-output.md)。</span><span class="sxs-lookup"><span data-stu-id="9b555-108">For details on storing the output data of your jobs and tasks, see [Persist Azure Batch job and task output](batch-task-output.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="9b555-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="9b555-109">Prerequisites</span></span>
* [<span data-ttu-id="9b555-110">Azure Batch 帳戶</span><span class="sxs-lookup"><span data-stu-id="9b555-110">Azure Batch account</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="9b555-111">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="9b555-111">Azure Storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)
  
  <span data-ttu-id="9b555-112">若要保留 Batch 診斷記錄，您必須建立 Azure 將用來儲存記錄的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9b555-112">To persist Batch diagnostic logs, you must create an Azure Storage account where Azure will store the logs.</span></span> <span data-ttu-id="9b555-113">當您為您的 Batch 帳戶[啟用診斷記錄](#enable-diagnostic-logging)時，請指定此儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9b555-113">You specify this Storage account when you [enable diagnostic logging](#enable-diagnostic-logging) for your Batch account.</span></span> <span data-ttu-id="9b555-114">您啟用記錄收集時指定的儲存體帳戶不同於[應用程式封裝](batch-application-packages.md)和[工作輸出持續性](batch-task-output.md)文件中提及的連結儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9b555-114">The Storage account you specify when you enable log collection is not the same as a linked storage account referred to in the [application packages](batch-application-packages.md) and [task output persistence](batch-task-output.md) articles.</span></span>
  
  > [!WARNING]
  > <span data-ttu-id="9b555-115">儲存在您的 Azure 儲存體帳戶中的資料需要**收費**。</span><span class="sxs-lookup"><span data-stu-id="9b555-115">You are **charged** for the data stored in your Azure Storage account.</span></span> <span data-ttu-id="9b555-116">這包括本文討論的診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="9b555-116">This includes the diagnostic logs discussed in this article.</span></span> <span data-ttu-id="9b555-117">在設計您的[記錄保留原則](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)時請牢記這一點。</span><span class="sxs-lookup"><span data-stu-id="9b555-117">Keep this in mind when designing your [log retention policy](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span></span>
  > 
  > 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="9b555-118">啟用診斷記錄</span><span class="sxs-lookup"><span data-stu-id="9b555-118">Enable diagnostic logging</span></span>
<span data-ttu-id="9b555-119">您的 Batch 帳戶預設未啟用診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="9b555-119">Diagnostic logging is not enabled by default for your Batch account.</span></span> <span data-ttu-id="9b555-120">您必須為每個您想要監視的 Batch 帳戶明確啟用診斷記錄︰</span><span class="sxs-lookup"><span data-stu-id="9b555-120">You must explicitly enable diagnostic logging for each Batch account you want to monitor:</span></span>

[<span data-ttu-id="9b555-121">如何啟用診斷記錄的收集</span><span class="sxs-lookup"><span data-stu-id="9b555-121">How to enable collection of Diagnostic Logs</span></span>](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)

<span data-ttu-id="9b555-122">建議您閱讀完整的 [Azure 診斷記錄概觀](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)文件，以了解如何啟用記錄和各種 Azure 服務支援的記錄類別。</span><span class="sxs-lookup"><span data-stu-id="9b555-122">We recommend that you read the full [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article to gain an understanding of not only how to enable logging, but the log categories supported by the various Azure services.</span></span> <span data-ttu-id="9b555-123">例如，Azure Batch 目前支援一種記錄類別︰**服務記錄檔**。</span><span class="sxs-lookup"><span data-stu-id="9b555-123">For example, Azure Batch currently supports one log category: **Service Logs**.</span></span>

## <a name="service-logs"></a><span data-ttu-id="9b555-124">服務記錄檔</span><span class="sxs-lookup"><span data-stu-id="9b555-124">Service Logs</span></span>
<span data-ttu-id="9b555-125">Azure Batch 服務記錄檔包含 Batch 資源 (如集區或工作) 的存留期間，由 Azure Batch 服務發出的事件。</span><span class="sxs-lookup"><span data-stu-id="9b555-125">Azure Batch Service Logs contain events emitted by the Azure Batch service during the lifetime of a Batch resource like a pool or task.</span></span> <span data-ttu-id="9b555-126">Batch 所發出的每個事件會以 JSON 格式儲存在指定的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9b555-126">Each event emitted by Batch is stored in the specified Storage account in JSON format.</span></span> <span data-ttu-id="9b555-127">例如，**集區建立事件**範例的主體為：</span><span class="sxs-lookup"><span data-stu-id="9b555-127">For example, this is the body of a sample **pool create event**:</span></span>

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

<span data-ttu-id="9b555-128">每個事件主體位於指定的 Azure 儲存體帳戶中的 .json 檔案內。</span><span class="sxs-lookup"><span data-stu-id="9b555-128">Each event body resides in a .json file in the specified Azure Storage account.</span></span> <span data-ttu-id="9b555-129">如果您想要直接存取記錄檔，您可能想要檢閱 [儲存體帳戶中的診斷記錄結構描述](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="9b555-129">If you want to access the logs directly, you may wish to review the [schema of Diagnostic Logs in the storage account](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span></span>

## <a name="service-log-events"></a><span data-ttu-id="9b555-130">服務記錄檔事件</span><span class="sxs-lookup"><span data-stu-id="9b555-130">Service Log events</span></span>
<span data-ttu-id="9b555-131">Batch 服務目前會發出下列服務記錄檔事件。</span><span class="sxs-lookup"><span data-stu-id="9b555-131">The Batch service currently emits the following Service Log events.</span></span> <span data-ttu-id="9b555-132">這份清單可能不完整，因為自上次更新此文件後可能已新增額外的事件。</span><span class="sxs-lookup"><span data-stu-id="9b555-132">This list may not be exhaustive, since additional events may have been added since this article was last updated.</span></span>

| <span data-ttu-id="9b555-133">**服務記錄檔事件**</span><span class="sxs-lookup"><span data-stu-id="9b555-133">**Service Log events**</span></span> |
| --- |
| <span data-ttu-id="9b555-134">[建立集區][pool_create]</span><span class="sxs-lookup"><span data-stu-id="9b555-134">[Pool create][pool_create]</span></span> |
| <span data-ttu-id="9b555-135">[開始刪除集區][pool_delete_start]</span><span class="sxs-lookup"><span data-stu-id="9b555-135">[Pool delete start][pool_delete_start]</span></span> |
| <span data-ttu-id="9b555-136">[完成集區刪除][pool_delete_complete]</span><span class="sxs-lookup"><span data-stu-id="9b555-136">[Pool delete complete][pool_delete_complete]</span></span> |
| <span data-ttu-id="9b555-137">[開始調整集區大小][pool_resize_start]</span><span class="sxs-lookup"><span data-stu-id="9b555-137">[Pool resize start][pool_resize_start]</span></span> |
| <span data-ttu-id="9b555-138">[完成集區大小調整][pool_resize_complete]</span><span class="sxs-lookup"><span data-stu-id="9b555-138">[Pool resize complete][pool_resize_complete]</span></span> |
| <span data-ttu-id="9b555-139">[開始工作][task_start]</span><span class="sxs-lookup"><span data-stu-id="9b555-139">[Task start][task_start]</span></span> |
| <span data-ttu-id="9b555-140">[完成工作][task_complete]</span><span class="sxs-lookup"><span data-stu-id="9b555-140">[Task complete][task_complete]</span></span> |
| <span data-ttu-id="9b555-141">[工作失敗][task_fail]</span><span class="sxs-lookup"><span data-stu-id="9b555-141">[Task fail][task_fail]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9b555-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9b555-142">Next steps</span></span>
<span data-ttu-id="9b555-143">除了將診斷記錄事件儲存在 Azure 儲存體帳戶外，您也可以將 Batch 服務記錄檔事件串流處理到 [Azure 事件中樞](../event-hubs/event-hubs-what-is-event-hubs.md)，並傳送至 [Azure Log Analytics](../log-analytics/log-analytics-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="9b555-143">In addition to storing diagnostic log events in an Azure Storage account, you can also stream Batch Service Log events to an [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md), and send them to [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span>

* [<span data-ttu-id="9b555-144">將 Azure 診斷記錄檔串流至事件中樞</span><span class="sxs-lookup"><span data-stu-id="9b555-144">Stream Azure Diagnostic Logs to Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md)
  
  <span data-ttu-id="9b555-145">將 Batch 診斷事件串流處理至高擴充性的資料輸入服務：事件中樞。</span><span class="sxs-lookup"><span data-stu-id="9b555-145">Stream Batch diagnostic events to the highly scalable data ingress service, Event Hubs.</span></span> <span data-ttu-id="9b555-146">事件中樞每秒可輸入數百萬個事件，您可以使用任何即時分析提供者來轉換和儲存。</span><span class="sxs-lookup"><span data-stu-id="9b555-146">Event Hubs can ingest millions of events per second, which you can then transform and store using any real-time analytics provider.</span></span>
* [<span data-ttu-id="9b555-147">使用 Log Analytics 分析 Azure 診斷記錄</span><span class="sxs-lookup"><span data-stu-id="9b555-147">Analyze Azure diagnostic logs using Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
  
  <span data-ttu-id="9b555-148">將您的診斷記錄傳送至 Log Analytics，您可以在 Operations Management Suite (OMS) 入口網站中分析它們，或是匯出它們以在 Power BI 或 Excel 中分析。</span><span class="sxs-lookup"><span data-stu-id="9b555-148">Send your diagnostic logs to Log Analytics where you can analyze them in the Operations Management Suite (OMS) portal, or export them for analysis in Power BI or Excel.</span></span>

[pool_create]: https://msdn.microsoft.com/library/azure/mt743615.aspx
[pool_delete_start]: https://msdn.microsoft.com/library/azure/mt743610.aspx
[pool_delete_complete]: https://msdn.microsoft.com/library/azure/mt743618.aspx
[pool_resize_start]: https://msdn.microsoft.com/library/azure/mt743609.aspx
[pool_resize_complete]: https://msdn.microsoft.com/library/azure/mt743608.aspx
[task_start]: https://msdn.microsoft.com/library/azure/mt743616.aspx
[task_complete]: https://msdn.microsoft.com/library/azure/mt743612.aspx
[task_fail]: https://msdn.microsoft.com/library/azure/mt743607.aspx
