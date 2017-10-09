---
title: "監視自動調整規模常見標準 aaaAzure |Microsoft 文件"
description: "了解哪些度量常用於自動調整您的雲端服務、虛擬機器和 Web Apps。"
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 189b2a13-01c8-4aca-afd5-90711903ca59
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/6/2016
ms.author: ancav
ms.openlocfilehash: 372a40d72d7a6c22c5ff854b1460ec8a3b7ed1d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor-autoscaling-common-metrics"></a>Azure 監視器自動調整的常用度量
Azure 監視的自動調整可讓您執行的執行個體 tooscale hello 數目向上或向下根據遙測資料 （度量）。 本文件說明常見的度量，您可能想 toouse。 在 hello Azure 入口網站雲端服務和伺服器陣列而言，您可以選擇由 hello 資源 tooscale hello 公制。 不過，您也可以選擇不同的資源 tooscale 的任何度量。

Azure 監視的自動調整規模太只適用於[虛擬機器擴展集](https://azure.microsoft.com/services/virtual-machine-scale-sets/)，[雲端服務](https://azure.microsoft.com/services/cloud-services/)，和[應用程式服務-Web 應用程式](https://azure.microsoft.com/services/app-service/web/)。 其他 Azure 服務使用不同的調整方法。

## <a name="compute-metrics-for-resource-manager-based-vms"></a>針對以 Resource Manager 為基礎的 VM 來計算度量
根據預設，以 Resource Manager 為基礎的虛擬機器和虛擬機器擴展集會發出基本 (主機層級) 的度量。 此外，當您設定的 Azure VM，以及 VMSS 收集診斷資料，hello Azure 診斷擴充功能也會發出 （通常稱為 「 客體 OS 度量 」） 的客體 OS 效能計數器。  您在自動調整規則中使用所有這些度量。

您可以使用 hello `Get MetricDefinitions` API/PoSH CLI tooview hello 度量可用於 VMSS 資源。

如果您使用 VM 擴展集，而且發現特定度量沒有列出來，可能是您的診斷擴充功能已「停用」它。

如果特定的度量不被取樣或在傳送嗨您想要的頻率，您可以更新 hello 診斷組態。

如果任一上述的情況下為 true，則請檢閱[執行 Windows 的虛擬機器中使用 PowerShell tooenable Azure 診斷](../virtual-machines/windows/ps-extensions-diagnostics.md)有關 PowerShell tooconfigure 和更新您的 Azure VM 診斷延伸模組 tooenable hello 度量。 該文章也包含診斷組態檔的範例。

### <a name="host-metrics-for-resource-manager-based-windows-and-linux-vms"></a>以 Resource Manager 為基礎的 Windows 和 Linux VM 的主機度量
下列主機層級度量的 hello 會發出預設 Azure VM 和 VMSS Windows 和 Linux 的執行個體。 這些度量會描述您的 Azure VM，但會收集從 hello Azure VM 的主機，而不是透過 hello 客體 VM 上安裝代理程式。 您可以在自動調整規則中使用這些度量。

- [以 Resource Manager 為基礎的 Windows 和 Linux VM 的主機度量](monitoring-supported-metrics.md#microsoftcomputevirtualmachines)
- [以 Resource Manager 為基礎的 Windows 和 Linux VM 擴展集的主機度量](monitoring-supported-metrics.md#microsoftcomputevirtualmachinescalesets)

### <a name="guest-os-metrics-resource-manager-based-windows-vms"></a>客體 OS 度量以 Resource Manager 為基礎的 Windows VM
當您在 Azure 中建立 VM 時，診斷會啟用使用 hello 診斷延伸模組。 hello 診斷延伸模組會發出一組取自 hello VM 內的度量。 這表示您可以關閉自動調整依預設不發出的度量。

您可以使用下列命令在 PowerShell 中的 hello 產生 hello 度量的清單。

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

您可以建立 hello 下列度量的警示：

| 度量名稱 | 單位 |
| --- | --- |
| \Processor(_Total)\% Processor Time |百分比 |
| \Processor(_Total)\% Privileged Time |百分比 |
| \Processor(_Total)\% User Time |百分比 |
| \Processor Information(_Total)\Processor Frequency |Count |
| \System\Processes |Count |
| \Process(_Total)\Thread Count |Count |
| \Process(_Total)\Handle Count |Count |
| \Memory\% Committed Bytes In Use |百分比 |
| \Memory\Available Bytes |位元組 |
| \Memory\Committed Bytes |位元組 |
| \Memory\Commit Limit |位元組 |
| \Memory\Pool Paged Bytes |位元組 |
| \Memory\Pool Nonpaged Bytes |位元組 |
| \PhysicalDisk(_Total)\% Disk Time |百分比 |
| \PhysicalDisk(_Total)\% Disk Read Time |百分比 |
| \PhysicalDisk(_Total)\% Disk Write Time |百分比 |
| \PhysicalDisk(_Total)\每秒的磁碟傳輸數 |每秒計數 |
| \PhysicalDisk(_Total)\Disk Reads/sec |每秒計數 |
| \PhysicalDisk(_Total)\Disk Writes/sec |每秒計數 |
| \PhysicalDisk(_Total)\Disk Bytes/sec |每秒位元組 |
| \PhysicalDisk(_Total)\Disk Read Bytes/sec |每秒位元組 |
| \PhysicalDisk(_Total)\Disk Write Bytes/sec |每秒位元組 |
| \PhysicalDisk(_Total)\Avg.磁碟佇列長度 |Count |
| \PhysicalDisk(_Total)\Avg.磁碟讀取佇列長度 |Count |
| \PhysicalDisk(_Total)\Avg.磁碟寫入佇列長度 |Count |
| \LogicalDisk(_Total)\% Free Space |百分比 |
| \LogicalDisk(_Total)\Free Megabytes |Count |

### <a name="guest-os-metrics-linux-vms"></a>客體 OS 度量 Linux VM
當您在 Azure 中建立 VM 時，根據預設會使用診斷擴充來啟用診斷。

您可以使用下列命令在 PowerShell 中的 hello 產生 hello 度量的清單。

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

 您可以建立 hello 下列度量的警示：

| 度量名稱 | 單位 |
| --- | --- |
| \Memory\AvailableMemory |位元組 |
| \Memory\PercentAvailableMemory |百分比 |
| \Memory\UsedMemory |位元組 |
| \Memory\PercentUsedMemory |百分比 |
| \Memory\PercentUsedByCache |百分比 |
| \Memory\PagesPerSec |每秒計數 |
| \Memory\PagesReadPerSec |每秒計數 |
| \Memory\PagesWrittenPerSec |每秒計數 |
| \Memory\AvailableSwap |位元組 |
| \Memory\PercentAvailableSwap |百分比 |
| \Memory\UsedSwap |位元組 |
| \Memory\PercentUsedSwap |百分比 |
| \Processor\PercentIdleTime |百分比 |
| \Processor\PercentUserTime |百分比 |
| \Processor\PercentNiceTime |百分比 |
| \Processor\PercentPrivilegedTime |百分比 |
| \Processor\PercentInterruptTime |百分比 |
| \Processor\PercentDPCTime |百分比 |
| \Processor\PercentProcessorTime |百分比 |
| \Processor\PercentIOWaitTime |百分比 |
| \PhysicalDisk\BytesPerSecond |每秒位元組 |
| \PhysicalDisk\ReadBytesPerSecond |每秒位元組 |
| \PhysicalDisk\WriteBytesPerSecond |每秒位元組 |
| \PhysicalDisk\TransfersPerSecond |每秒計數 |
| \PhysicalDisk\ReadsPerSecond |每秒計數 |
| \PhysicalDisk\WritesPerSecond |每秒計數 |
| \PhysicalDisk\AverageReadTime |秒 |
| \PhysicalDisk\AverageWriteTime |秒 |
| \PhysicalDisk\AverageTransferTime |秒 |
| \PhysicalDisk\AverageDiskQueueLength |Count |
| \NetworkInterface\BytesTransmitted |位元組 |
| \NetworkInterface\BytesReceived |位元組 |
| \NetworkInterface\PacketsTransmitted |Count |
| \NetworkInterface\PacketsReceived |Count |
| \NetworkInterface\BytesTotal |位元組 |
| \NetworkInterface\TotalRxErrors |Count |
| \NetworkInterface\TotalTxErrors |Count |
| \NetworkInterface\TotalCollisions |Count |

## <a name="commonly-used-web-server-farm-metrics"></a>常用的 Web (伺服器陣列) 度量
您也可以執行一般的 web 伺服器度量，例如 hello Http 佇列長度為基礎的自動調整規模。 它的計量名稱是 **HttpQueueLength**。  hello 之後 > 一節列出可用的伺服器陣列 （Web 應用程式） 度量資訊。

### <a name="web-apps-metrics"></a>Web Apps 度量
您可以使用下列命令在 PowerShell 中的 hello 產生一份 hello Web 應用程式的度量。

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

您可以針對這些度量發出警示通知或以其為調整依據。

| 度量名稱 | 單位 |
| --- | --- |
| CpuPercentage |百分比 |
| MemoryPercentage |百分比 |
| DiskQueueLength |Count |
| HttpQueueLength |Count |
| BytesReceived |位元組 |
| BytesSent |位元組 |

## <a name="commonly-used-storage-metrics"></a>常用的儲存體度量
您可以調整的儲存體佇列長度是 hello hello 儲存體佇列中的訊息數目。 儲存體佇列長度是特殊的度量且 hello 臨界值為 hello 訊息，每個執行個體數目。 比方說，如果有兩個執行個體，而且 hello 閾值設定 too100，調整時發生 hello 總 hello 佇列中的訊息數目為 200。 可以是每個執行個體的 100 個訊息、 120 和 80，或任何其他的組合加總 too200 或多個。

設定此設定，在 hello Azure 入口網站中 hello**設定**刀鋒視窗。 針對 VM 規模集，您可以更新 hello 自動調整規模設定中 hello 資源管理員範本 toouse *metricName*為*ApproximateMessageCount*並傳遞 hello 識別碼 hello 儲存體佇列，做為*metricResourceUri*。

例如，以傳統的儲存體帳戶 hello 包含自動調整規模設定 metricTrigger:

```
"metricName": "ApproximateMessageCount",
 "metricNamespace": "",
 "metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.ClassicStorage/storageAccounts/STORAGE_ACCOUNT_NAME/services/queue/queues/QUEUE_NAME"
 ```

（非傳統） 儲存體帳戶，會包含 hello metricTrigger:

```
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.Storage/storageAccounts/STORAGE_ACCOUNT_NAME/services/queue/queues/QUEUE_NAME"
```

## <a name="commonly-used-service-bus-metrics"></a>常用的服務匯流排衡量標準
您可以調整服務匯流排佇列長度是 hello hello 服務匯流排佇列中的訊息數目。 服務匯流排佇列長度是特殊的度量和 hello 臨界值是每個執行個體訊息的 hello 數目。 比方說，如果有兩個執行個體，而且 hello 閾值設定 too100，調整時發生 hello 總 hello 佇列中的訊息數目為 200。 可以是每個執行個體的 100 個訊息、 120 和 80，或任何其他的組合加總 too200 或多個。

針對 VM 規模集，您可以更新 hello 自動調整規模設定中 hello 資源管理員範本 toouse *metricName*為*ApproximateMessageCount*並傳遞 hello 識別碼 hello 儲存體佇列，做為*metricResourceUri*。

```
"metricName": "MessageCount",
 "metricNamespace": "",
"metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.ServiceBus/namespaces/SB_NAMESPACE/queues/QUEUE_NAME"
```

> [!NOTE]
> 服務匯流排的 hello 資源群組概念不存在，但 Azure 資源管理員會建立每個區域的預設資源群組。 hello 資源群組通常是 hello '預設值-ServiceBus-[region]' 格式。 例如，'Default-ServiceBus-EastUS'、'Default-ServiceBus-WestUS'、'Default-ServiceBus-AustraliaEast' 等。
>
>
