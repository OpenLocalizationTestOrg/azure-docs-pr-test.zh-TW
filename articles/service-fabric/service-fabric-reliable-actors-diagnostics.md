---
title: "aaaActors 診斷和監視 |Microsoft 文件"
description: "本文說明 hello 診斷和效能監視中 hello 服務網狀架構 Reliable Actors 執行階段，包括 hello 事件和效能計數器，由它發出的功能。"
services: service-fabric
documentationcenter: .net
author: abhishekram
manager: timlt
editor: vturecek
ms.assetid: 1c229923-670a-4634-ad59-468ff781ad18
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: abhisram
ms.openlocfilehash: 5b266d67875722feef5c5be8861bda6d8132a7d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-performance-monitoring-for-reliable-actors"></a>Reliable Actors 的診斷和效能監視
hello Reliable Actors 執行階段發出[EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx)事件和[效能計數器](https://msdn.microsoft.com/library/system.diagnostics.performancecounter.aspx)。 這些提供 hello 執行階段的運作方式的深入剖析，並協助疑難排解與效能監視。

## <a name="eventsource-events"></a>EventSource 事件
hello Reliable Actors 執行階段的 hello EventSource 提供者名稱為 Microsoft-ServiceFabric 位演員。 這個事件來源的事件會出現在 hello[診斷事件](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md#view-service-fabric-system-events-in-visual-studio)hello 行動應用程式時的視窗[在 Visual Studio 中偵錯](service-fabric-debugging-your-application.md)。

工具和技術可協助您收集和/或檢視 EventSource 事件的範例包括[PerfView](http://www.microsoft.com/download/details.aspx?id=28567)， [Azure 診斷](../cloud-services/cloud-services-dotnet-diagnostics.md)，[語意記錄](https://msdn.microsoft.com/library/dn774980.aspx)，和 hello [Microsoft TraceEvent 文件庫](http://www.nuget.org/packages/Microsoft.Diagnostics.Tracing.TraceEvent)。

### <a name="keywords"></a>關鍵字
所有屬於 toohello 可靠的執行者 EventSource 的事件會與一或多個關鍵字相關聯。 這會啟動篩選所選的事件。 下列關鍵字位元的 hello 所定義。

| Bit | 說明 |
| --- | --- |
| 0x1 |摘述 hello hello Fabric 動作項目執行階段作業的重要事件的設定。 |
| 0x2 |說明動作項目方法呼叫的事件集。 如需詳細資訊，請參閱 hello[簡介主題上執行者](service-fabric-reliable-actors-introduction.md)。 |
| 0x4 |一組事件相關的 tooactor 狀態。 如需詳細資訊，請參閱 hello 主題[動作項目狀態管理](service-fabric-reliable-actors-state-management.md)。 |
| 0x8 |事件相關 tooturn 架構中的並行存取 hello 動作項目組。 如需詳細資訊，請參閱 hello 主題[並行](service-fabric-reliable-actors-introduction.md#concurrency)。 |

## <a name="performance-counters"></a>效能計數器
hello Reliable Actors 執行階段定義 hello 下列效能計數器分類。

| 類別 | 說明 |
| --- | --- |
| Service Fabric 動作項目 |計數器特定 tooAzure Service Fabric 動作項目，例如拍攝 toosave 動作項目狀態的時間 |
| Service Fabric 動作項目方法 |計數器特定 toomethods 實作由 Service Fabric 動作項目，例如頻率會叫用動作項目方法 |

每個 hello 上方類別有一個或多個計數器。

hello [Windows 效能監視器](https://technet.microsoft.com/library/cc749249.aspx)hello Windows 作業系統中的預設為可用的應用程式可以是使用的 toocollect 和檢視效能計數器資料。 [Azure 診斷](../cloud-services/cloud-services-dotnet-diagnostics.md)是另一個選項來收集效能計數器資料，並將它上傳 tooAzure 資料表。

### <a name="performance-counter-instance-names"></a>效能計數器執行個體名稱
含大量動作項目服務或動作項目服務資料分割的叢集將有大量的動作項目效能計數器執行個體。 hello 效能計數器執行個體名稱可協助您識別 hello 特定[分割](service-fabric-reliable-actors-platform.md#service-fabric-partition-concepts-for-actors)和動作項目方法 （如果適用） 該 hello 效能計數器執行個體相關聯。

#### <a name="service-fabric-actor-category"></a>Service Fabric 動作項目類別
Hello 分類`Service Fabric Actor`，hello 計數器執行個體名稱會出現在 hello 下列格式：

`ServiceFabricPartitionID_ActorsRuntimeInternalID`

*ServiceFabricPartitionID* hello 的 hello hello 效能計數器執行個體的 Service Fabric 分割區識別碼是與相關聯的字串表示。 hello 分割區識別碼是 GUID，並透過 hello 產生它的字串表示[ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx)使用"D"的格式規範的方法。

*ActorRuntimeInternalID* hello 供其內部使用的 hello Fabric 動作項目執行階段所產生的 64 位元整數的字串表示。 這是包含在 hello 效能計數器執行個體名稱的唯一性 tooensure 和避免與其他效能計數器執行個體名稱相衝突。 使用者不應該嘗試 toointerpret hello 效能計數器執行個體名稱的這個部分。

hello 的範例如下的所屬 toohello 計數器的計數器執行個體名稱`Service Fabric Actor`類別：

`2740af29-78aa-44bc-a20b-7e60fb783264_635650083799324046`

在 hello 上述範例中， `2740af29-78aa-44bc-a20b-7e60fb783264` hello 字串 hello Service Fabric 分割區識別碼，表示和`635650083799324046`hello hello 執行階段的內部產生的 64 位元識別碼使用。

#### <a name="service-fabric-actor-method-category"></a>Service Fabric 動作項目方法類別
Hello 分類`Service Fabric Actor Method`，hello 計數器執行個體名稱會出現在 hello 下列格式：

`MethodName_ActorsRuntimeMethodId_ServiceFabricPartitionID_ActorsRuntimeInternalID`

*MethodName* hello hello 效能計數器執行個體的 hello 執行者方法名稱是相關聯。 hello hello 方法名稱格式取決於一些邏輯之間取得平衡的 hello 名稱與 hello hello 效能計數器執行個體名稱的長度上限的條件約束，在 Windows 上的 hello 可讀性 hello Fabric 動作項目執行階段中。

*ActorsRuntimeMethodId* hello 供其內部使用的 hello Fabric 動作項目執行階段所產生的 32 位元整數的字串表示。 這是包含在 hello 效能計數器執行個體名稱的唯一性 tooensure 和避免與其他效能計數器執行個體名稱相衝突。 使用者不應該嘗試 toointerpret hello 效能計數器執行個體名稱的這個部分。

*ServiceFabricPartitionID* hello 的 hello hello 效能計數器執行個體的 Service Fabric 分割區識別碼是與相關聯的字串表示。 hello 分割區識別碼是 GUID，並透過 hello 產生它的字串表示[ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx)使用"D"的格式規範的方法。

*ActorRuntimeInternalID* hello 供其內部使用的 hello Fabric 動作項目執行階段所產生的 64 位元整數的字串表示。 這是包含在 hello 效能計數器執行個體名稱的唯一性 tooensure 和避免與其他效能計數器執行個體名稱相衝突。 使用者不應該嘗試 toointerpret hello 效能計數器執行個體名稱的這個部分。

hello 的範例如下的所屬 toohello 計數器的計數器執行個體名稱`Service Fabric Actor Method`類別：

`ivoicemailboxactor.leavemessageasync_2_89383d32-e57e-4a9b-a6ad-57c6792aa521_635650083804480486`

在 hello 上述範例中，`ivoicemailboxactor.leavemessageasync`是 hello 方法名稱、`2`為 32 位元識別碼產生 hello 執行階段的內部使用，hello `89383d32-e57e-4a9b-a6ad-57c6792aa521` hello 字串 hello Service Fabric 分割區識別碼，表示和`635650083804480486`hello 64 位元識別碼產生執行階段 hello 內部使用。

## <a name="list-of-events-and-performance-counters"></a>事件與效能計數器清單
### <a name="actor-method-events-and-performance-counters"></a>動作項目方法事件與效能計數器
hello Reliable Actors 執行階段發出下列太相關事件的 hello[執行者方法](service-fabric-reliable-actors-introduction.md)。

| 事件名稱 | 事件識別碼 | Level | 關鍵字 | 說明 |
| --- | --- | --- | --- | --- |
| ActorMethodStart |7 |詳細資訊 |0x2 |動作項目執行階段是關於 tooinvoke 動作項目方法。 |
| ActorMethodStop |8 |詳細資訊 |0x2 |動作項目方法已經完成執行。 也就是說，hello 執行階段非同步呼叫 toohello 執行者方法已傳回，而且 hello hello 執行者方法所傳回的工作已完成。 |
| ActorMethodThrewException |9 |警告 |0x3 |擲回例外狀況 hello 執行動作項目方法期間，在執行階段 hello 非同步呼叫 toohello 執行者方法期間或在 hello hello 工作執行期間 hello 執行者方法所傳回。 這個事件表示某種需要調查 hello 行動程式碼中的失敗。 |

hello Reliable Actors 執行階段會發行下列動作項目方法的效能計數器相關的 toohello 執行 hello。

| 類別名稱 | 計數器名稱 | 說明 |
| --- | --- | --- |
| Service Fabric 動作項目方法 |叫用數目/秒 |Hello 動作項目服務方法會叫用每秒的次數 |
| Service Fabric 動作項目方法 |每個叫用的平均毫秒數 |所花費時間 tooexecute hello 動作項目服務方法以毫秒為單位 |
| Service Fabric 動作項目方法 |擲回的例外狀況數/秒 |次數，hello 動作項目服務方法擲回例外狀況秒 |

### <a name="concurrency-events-and-performance-counters"></a>並行事件與效能計數器
hello Reliable Actors 執行階段發出下列太相關事件的 hello[並行](service-fabric-reliable-actors-introduction.md#concurrency)。

| 事件名稱 | 事件識別碼 | Level | 關鍵字 | 說明 |
| --- | --- | --- | --- | --- |
| ActorMethodCallsWaitingForLock |12 |詳細資訊 |0x8 |此事件會寫入動作項目中的每個新開啟的 hello 開頭。 它包含暫止的動作項目呼叫，正在等候 tooacquire hello 每個動作項目鎖定會強制關閉並行 hello 的數目。 |

hello Reliable Actors 執行階段會發行下列效能計數器相關的 tooconcurrency hello。

| 類別名稱 | 計數器名稱 | 說明 |
| --- | --- | --- |
| Service Fabric 動作項目 |# of actor calls waiting for actor lock |暫止的動作項目呼叫數目等候 tooacquire hello 每個動作項目鎖定會強制關閉基礎的並行存取 |
| Service Fabric 動作項目 |每個 Lock Wait 的平均毫秒數 |會關閉基礎的並行存取強制執行的時間 （以毫秒為單位） 採用的 tooacquire hello 每個動作項目鎖定 |
| Service Fabric 動作項目 |保留動作項目鎖定的平均毫秒數 |哪些 hello 每個動作項目鎖定的時間 （以毫秒為單位） |

### <a name="actor-state-management-events-and-performance-counters"></a>動作項目狀態管理事件與效能計數器
hello Reliable Actors 執行階段發出下列太相關事件的 hello[動作項目狀態管理](service-fabric-reliable-actors-state-management.md)。

| 事件名稱 | 事件識別碼 | Level | 關鍵字 | 說明 |
| --- | --- | --- | --- | --- |
| ActorSaveStateStart |10 |詳細資訊 |0x4 |動作項目執行階段是關於 toosave hello 動作項目狀態。 |
| ActorSaveStateStop |11 |詳細資訊 |0x4 |動作項目執行階段已完成儲存 hello 動作項目狀態。 |

hello Reliable Actors 執行階段會發行 hello 下列效能計數器相關的 tooactor 狀態管理。

| 類別名稱 | 計數器名稱 | 說明 |
| --- | --- | --- |
| Service Fabric 動作項目 |每個儲存狀態作業的平均毫秒數 |時間 toosave 動作項目狀態，以毫秒為單位 |
| Service Fabric 動作項目 |每個載入狀態作業的平均毫秒數 |時間 tooload 動作項目狀態，以毫秒為單位 |

### <a name="events-related-tooactor-replicas"></a>事件相關的 tooactor 複本
hello Reliable Actors 執行階段發出下列太相關事件的 hello[動作項目複本](service-fabric-reliable-actors-platform.md#service-fabric-partition-concepts-for-actors)。

| 事件名稱 | 事件識別碼 | Level | 關鍵字 | 說明 |
| --- | --- | --- | --- | --- |
| ReplicaChangeRoleToPrimary |1 |資訊 |0x1 |動作項目複本變更角色 tooPrimary。 這表示此資料分割的 hello 執行者將會建立在這個複本。 |
| ReplicaChangeRoleFromPrimary |2 |資訊 |0x1 |動作項目複本變更角色 toonon 主要。 這表示，將不會再內這個複本建立 hello 動作項目，這個資料分割。 任何新的要求會不傳遞 tooactors 已經建立這個複本中。 完成任何進行中的要求之後，會終結 hello 執行者。 |

### <a name="actor-activation-and-deactivation-events-and-performance-counters"></a>動作項目啟動與停用事件與效能計數器
hello Reliable Actors 執行階段發出下列太相關事件的 hello[動作項目啟用和停用](service-fabric-reliable-actors-lifecycle.md)。

| 事件名稱 | 事件識別碼 | Level | 關鍵字 | 說明 |
| --- | --- | --- | --- | --- |
| ActorActivated |5 |資訊 |0x1 |動作項目已啟動。 |
| ActorDeactivated |6 |資訊 |0x1 |動作項目已停用。 |

hello Reliable Actors 執行階段發行 hello tooactor 啟用和停用下列效能計數器相關。

| 類別名稱 | 計數器名稱 | 說明 |
| --- | --- | --- |
| Service Fabric 動作項目 |平均 OnActivateAsync 毫秒數 |採取 tooexecute OnActivateAsync 方法，以毫秒為單位的時間 |

### <a name="actor-request-processing-performance-counters"></a>動作項目要求處理效能計數器
當用戶端叫用的方法，透過執行者 proxy 物件時，則會導致透過 hello 網路 toohello 行動服務所傳送的要求訊息。 hello 服務處理 hello 要求訊息，並傳送回應後 toohello 用戶端。 hello Reliable Actors 執行階段會發行下列效能計數器相關的 tooactor 要求處理 hello。

| 類別名稱 | 計數器名稱 | 說明 |
| --- | --- | --- |
| Service Fabric 動作項目 |# of outstanding requests |在 hello 服務正在處理的要求數目 |
| Service Fabric 動作項目 |每個要求的平均毫秒數 |（以毫秒為單位） hello 服務 tooprocess 所要求的花費的時間 |
| Service Fabric 動作項目 |要求還原序列化的平均毫秒數 |時間 （以毫秒為單位） 採用的 toodeserialize 動作項目要求訊息時收到 hello 服務 |
| Service Fabric 動作項目 |要求序列化的平均毫秒數 |時間 （以毫秒為單位） 採用的 tooserialize hello 執行者回應訊息之前傳送 toohello 用戶端 hello 回應 hello 服務 |

## <a name="next-steps"></a>後續步驟
* [Reliable Actors 使用 hello Service Fabric 平台的方式](service-fabric-reliable-actors-platform.md)
* [動作項目 API 參考文件](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [範例程式碼](https://github.com/Azure/servicefabric-samples)
* [PerfView 中的 EventSource 提供者](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)
