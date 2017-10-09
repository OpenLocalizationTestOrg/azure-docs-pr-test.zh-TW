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
# <a name="log-events-for-diagnostic-evaluation-and-monitoring-of-batch-solutions"></a>記錄事件以便對 Batch 解決方案進行診斷評估和監視

如同許多 Azure 服務，hello 批次服務會發出某些資源期間 hello hello 資源的存留期的記錄事件。 您可以啟用 Azure 批次的資源集區和工作，如的診斷記錄檔 toorecord 事件，然後再使用 診斷評估及監視 hello 記錄檔。 集區建立、集區刪除、工作開始、工作完成及其他事件等，都會包含在 Batch 診斷記錄中。

> [!NOTE]
> 本文討論 Batch 帳戶資源本身的記錄事件，而非作業和工作輸出資料。 如需儲存 hello 輸出資料，您的工作和工作的詳細資訊，請參閱[保存 Azure 批次作業和工作的輸出](batch-task-output.md)。
> 
> 

## <a name="prerequisites"></a>必要條件
* [Azure Batch 帳戶](batch-account-create-portal.md)
* [Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)
  
  toopersist 批次診斷記錄檔，您必須建立 Azure 將會在其中儲存 hello 記錄檔的 Azure 儲存體帳戶。 當您為您的 Batch 帳戶[啟用診斷記錄](#enable-diagnostic-logging)時，請指定此儲存體帳戶。 hello 您指定當您啟用收集記錄的儲存體帳戶不是 hello 相同為連結的儲存體帳戶參照的 tooin hello[應用程式封裝](batch-application-packages.md)和[工作輸出的持續性](batch-task-output.md)文件。
  
  > [!WARNING]
  > 您是**收費**hello 資料儲存在您的 Azure 儲存體帳戶。 這包括 hello 本文所討論的診斷記錄檔。 在設計您的[記錄保留原則](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)時請牢記這一點。
  > 
  > 

## <a name="enable-diagnostic-logging"></a>啟用診斷記錄
您的 Batch 帳戶預設未啟用診斷記錄。 您必須明確啟用診斷記錄的每個您想要讓 toomonitor 的批次帳戶：

[如何 tooenable 收集診斷記錄檔](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)

我們建議您先閱讀完整 hello[概觀的 Azure 診斷記錄檔](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)文章 toogain 不僅如何 tooenable 記錄，但 hello 登類別了解支援 hello 各種 Azure 服務。 例如，Azure Batch 目前支援一種記錄類別︰**服務記錄檔**。

## <a name="service-logs"></a>服務記錄檔
Azure 批次服務記錄檔包含在 hello 的批次之類的資源集區或工作的存留期 hello Azure 批次服務所發出的事件。 每個批次所發出的事件會儲存在指定的 hello 以 JSON 格式的儲存體帳戶。 比方說，這是範例 hello 主體**集區建立事件**:

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

每個事件主體位於.json 檔案 hello 中的指定 Azure 儲存體帳戶。 如果您想直接 tooaccess hello 的記錄檔，您可能希望 tooreview hello [hello 儲存體帳戶中的診斷記錄檔的結構描述](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account)。

## <a name="service-log-events"></a>服務記錄檔事件
目前，hello 批次服務會發出 hello 下列服務記錄檔事件。 這份清單可能不完整，因為自上次更新此文件後可能已新增額外的事件。

| **服務記錄檔事件** |
| --- |
| [建立集區][pool_create] |
| [開始刪除集區][pool_delete_start] |
| [完成集區刪除][pool_delete_complete] |
| [開始調整集區大小][pool_resize_start] |
| [完成集區大小調整][pool_resize_complete] |
| [開始工作][task_start] |
| [完成工作][task_complete] |
| [工作失敗][task_fail] |

## <a name="next-steps"></a>後續步驟
在 Azure 儲存體帳戶中的加法 toostoring 診斷記錄事件，您也可以送批次服務記錄檔事件 tooan [Azure 事件中心](../event-hubs/event-hubs-what-is-event-hubs.md)，並將它們傳送到太[Azure Log Analytics](../log-analytics/log-analytics-overview.md)。

* [資料流 Azure 診斷記錄檔 tooEvent 集線器](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md)
  
  串流處理批次的診斷事件 toohello 高度可擴充的資料輸入服務，事件中心。 事件中樞每秒可輸入數百萬個事件，您可以使用任何即時分析提供者來轉換和儲存。
* [使用 Log Analytics 分析 Azure 診斷記錄](../log-analytics/log-analytics-azure-storage.md)
  
  傳送您的診斷記錄檔 tooLog 分析，您可以在此分析它們在 hello Operations Management Suite (OMS) 的入口網站，或將它們匯出為 Power BI 或 Excel 中分析。

[pool_create]: https://msdn.microsoft.com/library/azure/mt743615.aspx
[pool_delete_start]: https://msdn.microsoft.com/library/azure/mt743610.aspx
[pool_delete_complete]: https://msdn.microsoft.com/library/azure/mt743618.aspx
[pool_resize_start]: https://msdn.microsoft.com/library/azure/mt743609.aspx
[pool_resize_complete]: https://msdn.microsoft.com/library/azure/mt743608.aspx
[task_start]: https://msdn.microsoft.com/library/azure/mt743616.aspx
[task_complete]: https://msdn.microsoft.com/library/azure/mt743612.aspx
[task_fail]: https://msdn.microsoft.com/library/azure/mt743607.aspx
