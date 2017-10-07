---
title: "服務網狀架構的效能監視的 aaaAzure |Microsoft 文件"
description: "了解用於監視及診斷 Azure Service Fabric 叢集的效能計數器。"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 54d4c62b7250a1f70b0898ba07ae5a37716f4cf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="performance-metrics"></a>效能度量

度量應該是您的叢集收集的 toounderstand hello 效能，以及它所執行的 hello 應用程式。 Service Fabric 叢集，我們建議收集下列效能計數器的 hello。

## <a name="nodes"></a>節點

針對叢集中的 hello 機器，請考慮收集下列效能計數器 hello 每部機器上的負載，並進行適當調整決策的叢集，了解 toobetter hello。

| 計數器類別 | 計數器名稱 |
| --- | --- |
| PhysicalDisk(per Disk) | Avg.磁碟讀取佇列長度 |
| PhysicalDisk(per Disk) | Avg.磁碟寫入佇列長度 |
| PhysicalDisk(per Disk) | Avg.Disk sec/Read |
| PhysicalDisk(per Disk) | Avg.Disk sec/Write |
| PhysicalDisk(per Disk) | Disk Reads/sec  |
| PhysicalDisk(per Disk) | Disk Read Bytes/sec  |
| PhysicalDisk(per Disk) | Disk Writes/sec |
| PhysicalDisk(per Disk) | Disk Write Bytes/sec |
| 記憶體 | 可用的 MB |
| PagingFile | % 使用量 |
| Process(Total) | % Processor Time |
| Process (per service) | % Processor Time |
| Process (per service) | 識別碼處理序 |
| Process (per service) | 私用位元組 |
| Process (per service) | 執行緒計數 |
| Process (per service) | 虛擬位元組 |
| Process (per service) | 工作集 |
| Process (per service) | 工作集 - 私用 |

## <a name="net-applications-and-services"></a>.NET 應用程式與服務

收集下列計數器，如果您要部署.NET services tooyour 叢集 hello。 

| 計數器類別 | 計數器名稱 |
| --- | --- |
| .NET CLR 記憶體 (每一服務) | 處理序識別碼 |
| .NET CLR 記憶體 (每一服務) | 認可的位元組總數 |
| .NET CLR 記憶體 (每一服務) | 保留的位元組總數 |
| .NET CLR 記憶體 (每一服務) | 所有堆積中的位元組數 |
| .NET CLR 記憶體 (每一服務) | 層代 0 集合數 |
| .NET CLR 記憶體 (每一服務) | 層代 1 集合數 |
| .NET CLR 記憶體 (每一服務) | 層代 2 集合數 |
| .NET CLR 記憶體 (每一服務) | 記憶體回收中的時間 % |

### <a name="service-fabrics-custom-performance-counters"></a>Service Fabric 的自訂效能計數器

Service Fabric 可產生大量的自訂效能計數器。 如果您擁有 hello 安裝 SDK 時，您可以應用程式效能監視中 Windows 電腦上看到 hello 完整清單 (開始 > 效能監視器)。 

Hello 應用程式中，您要部署 tooyour 叢集，如果您使用 Reliable Actors，加入從 countes`Service Fabric Actor`和`Service Fabric Actor Method`類別 (請參閱[服務網狀架構可靠執行者診斷](service-fabric-reliable-actors-diagnostics.md))。

如果您使用 Reliable Services，我們同樣提供 `Service Fabric Service` 和 `Service Fabric Service Method` 計數器類別，您應該從這些類別收集計數器。 

如果您使用可靠的集合，我們建議將加入 hello`Avg. Transaction ms/Commit`從 hello `Service Fabric Transactional Replicator` toocollect hello 平均認可延遲，每個交易標準。


## <a name="next-steps"></a>後續步驟

* 深入了解[hello 平台層級的事件產生](service-fabric-diagnostics-event-generation-infra.md)Service Fabric 中
* 透過 [Azure 診斷](service-fabric-diagnostics-event-aggregation-wad.md)收集效能計量
