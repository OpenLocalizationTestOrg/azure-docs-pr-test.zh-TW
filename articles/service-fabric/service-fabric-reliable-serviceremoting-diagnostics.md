---
title: "aaaAzure ServiceFabric 診斷和監視 |Microsoft 文件"
description: "本文說明 hello hello ServiceRemoting 可靠的服務網狀架構執行階段，例如它所發出的效能計數器的效能監視功能。"
services: service-fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: suchiagicha
ms.assetid: 1c229923-670a-4634-ad59-468ff781ad18
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: suchiagicha
ms.openlocfilehash: 64db9a890bd59a1326e587d14b89c007b71a9059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-performance-monitoring-for-reliable-service-remoting"></a>Reliable Service Remoting 的診斷和效能監視
hello 可靠 ServiceRemoting 執行階段發出[效能計數器](https://msdn.microsoft.com/library/system.diagnostics.performancecounter.aspx)。 這些提供 hello ServiceRemoting 的運作方式的深入剖析，並協助疑難排解與效能監視。


## <a name="performance-counters"></a>效能計數器
hello 可靠 ServiceRemoting 執行階段會定義下列效能計數器分類的 hello:

| 類別 | 說明 |
| --- | --- |
| Service Fabric Service |計數器特定 tooAzure Service Fabric 服務遠端處理，例如，要求所花費的平均時間 tooprocess |
| Service Fabric Service Method |計數器特定 toomethods 藉由 Service Fabric 遠端服務，例如，服務方法會叫用的頻率 |

每個 hello 前面類別有一個或多個計數器。

hello [Windows 效能監視器](https://technet.microsoft.com/library/cc749249.aspx)hello Windows 作業系統中的預設為可用的應用程式可以是使用的 toocollect 和檢視效能計數器資料。 [Azure 診斷](../cloud-services/cloud-services-dotnet-diagnostics.md)是另一個選項來收集效能計數器資料，並將它上傳 tooAzure 資料表。

### <a name="performance-counter-instance-names"></a>效能計數器執行個體名稱
含大量 ServiceRemoting 服務或資料分割的叢集有大量的效能計數器執行個體。 該 hello 效能計數器執行個體相關聯 hello 效能計數器執行個體名稱可協助您識別 hello 特定分割區和服務方法 （如果適用）。

#### <a name="service-fabric-service-category"></a>Service Fabric Service 類別
Hello 分類`Service Fabric Service`，hello 計數器執行個體名稱會出現在 hello 下列格式：

`ServiceFabricPartitionID_ServiceReplicaOrInstanceId_ServiceRuntimeInternalID`

*ServiceFabricPartitionID* hello 的 hello hello 效能計數器執行個體的 Service Fabric 分割區識別碼是與相關聯的字串表示。 hello 分割區識別碼是 GUID，並透過 hello 產生它的字串表示[ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx)使用"D"的格式規範的方法。

*ServiceReplicaOrInstanceId* hello 的 hello hello 效能計數器執行個體的 Service Fabric 複本/執行個體識別碼相關聯的字串表示。

*ServiceRuntimeInternalID* hello hello 供其內部使用的網狀架構服務執行階段所產生的 64 位元整數的字串表示。 這是包含在 hello 效能計數器執行個體名稱的唯一性 tooensure 和避免與其他效能計數器執行個體名稱相衝突。 使用者不應該嘗試 toointerpret hello 效能計數器執行個體名稱的這個部分。

hello 的範例如下的所屬 toohello 計數器的計數器執行個體名稱`Service Fabric Service`類別：

`2740af29-78aa-44bc-a20b-7e60fb783264_635650083799324046_5008379932`

Hello 前面範例中，在`2740af29-78aa-44bc-a20b-7e60fb783264`hello 字串 hello Service Fabric 分割區識別碼，表示`635650083799324046`是複本/執行個體識別碼的字串表示法和`5008379932`hello hello 執行階段的內部產生的 64 位元識別碼使用。

#### <a name="service-fabric-service-method-category"></a>Service Fabric Service Method 類別
Hello 分類`Service Fabric Service Method`，hello 計數器執行個體名稱會出現在 hello 下列格式：

`MethodName_ServiceRuntimeMethodId_ServiceFabricPartitionID_ServiceReplicaOrInstanceId_ServiceRuntimeInternalID`

*MethodName* hello hello hello 效能計數器執行個體的服務方法的名稱是相關聯。 hello hello 方法名稱格式取決於一些邏輯之間取得平衡的 hello 名稱與 hello hello 效能計數器執行個體名稱的長度上限的條件約束，在 Windows 上的 hello 可讀性 hello Fabric 服務執行階段中。

*ServiceRuntimeMethodId* hello hello 供其內部使用的網狀架構服務執行階段所產生的 32 位元整數的字串表示。 這是包含在 hello 效能計數器執行個體名稱的唯一性 tooensure 和避免與其他效能計數器執行個體名稱相衝突。 使用者不應該嘗試 toointerpret hello 效能計數器執行個體名稱的這個部分。

*ServiceFabricPartitionID* hello 的 hello hello 效能計數器執行個體的 Service Fabric 分割區識別碼是與相關聯的字串表示。 hello 分割區識別碼是 GUID，並透過 hello 產生它的字串表示[ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx)使用"D"的格式規範的方法。

*ServiceReplicaOrInstanceId* hello 的 hello hello 效能計數器執行個體的 Service Fabric 複本/執行個體識別碼相關聯的字串表示。

*ServiceRuntimeInternalID* hello hello 供其內部使用的網狀架構服務執行階段所產生的 64 位元整數的字串表示。 這是包含在 hello 效能計數器執行個體名稱的唯一性 tooensure 和避免與其他效能計數器執行個體名稱相衝突。 使用者不應該嘗試 toointerpret hello 效能計數器執行個體名稱的這個部分。

hello 的範例如下的所屬 toohello 計數器的計數器執行個體名稱`Service Fabric Service Method`類別：

`ivoicemailboxservice.leavemessageasync_2_89383d32-e57e-4a9b-a6ad-57c6792aa521_635650083804480486_5008380`

Hello 前面範例中，在`ivoicemailboxservice.leavemessageasync`是 hello 方法名稱、`2`為 32 位元識別碼產生 hello 執行階段的內部使用，hello `89383d32-e57e-4a9b-a6ad-57c6792aa521` hello 字串 hello Service Fabric 分割區識別碼，表示`635650083804480486`為 hello 字串hello Service Fabric 複本/執行個體識別碼表示法和`5008380`hello 64 位元識別碼產生 hello 執行階段的內部使用。

## <a name="list-of-performance-counters"></a>效能計數器的清單
### <a name="service-method-performance-counters"></a>服務方法效能計數器

hello 可靠的服務執行階段會發行下列服務方法的效能計數器相關的 toohello 執行 hello。

| 類別名稱 | 計數器名稱 | 說明 |
| --- | --- | --- |
| Service Fabric Service Method |叫用數目/秒 |Hello 服務方法會叫用每秒的次數 |
| Service Fabric Service Method |每個叫用的平均毫秒數 |採取 tooexecute hello 服務方法，以毫秒為單位的時間 |
| Service Fabric Service Method |擲回的例外狀況數/秒 |次數，hello 服務方法擲回例外狀況秒 |

### <a name="service-request-processing-performance-counters"></a>服務要求處理效能計數器
當用戶端叫用的方法，透過服務 proxy 物件時，則會導致透過 hello 網路 toohello 遠端服務所傳送的要求訊息。 hello 服務處理 hello 要求訊息，並傳送回應後 toohello 用戶端。 hello 可靠 ServiceRemoting 執行階段會發行下列效能計數器相關的 tooservice 要求處理 hello。

| 類別名稱 | 計數器名稱 | 說明 |
| --- | --- | --- |
| Service Fabric Service |# of outstanding requests |在 hello 服務正在處理的要求數目 |
| Service Fabric Service |每個要求的平均毫秒數 |（以毫秒為單位） hello 服務 tooprocess 所要求的花費的時間 |
| Service Fabric Service |要求還原序列化的平均毫秒數 |時間 （以毫秒為單位） 採用的 toodeserialize 服務要求訊息時收到 hello 服務 |
| Service Fabric Service |要求序列化的平均毫秒數 |時間 （以毫秒為單位） 採用的 tooserialize hello 服務回應訊息之前傳送 toohello 用戶端 hello 回應 hello 服務 |

## <a name="next-steps"></a>後續步驟
* [範例程式碼](https://github.com/Azure/servicefabric-samples)
* [PerfView 中的 EventSource 提供者](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)
