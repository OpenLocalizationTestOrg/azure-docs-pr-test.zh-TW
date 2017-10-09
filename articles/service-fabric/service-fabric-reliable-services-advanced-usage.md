---
title: "可靠的服務使用量 aaaAdvanced |Microsoft 文件"
description: "深入了解 Service Fabric 的 Reliable Services 的進階用法，以在服務中增加彈性。"
services: Service-Fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: masnider
ms.assetid: f2942871-863d-47c3-b14a-7cdad9a742c7
ms.service: Service-Fabric
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: e6d6310a4deae9edcfcd76551e1337f0e39e9e5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-usage-of-hello-reliable-services-programming-model"></a>進階的 hello 可靠服務程式設計模型使用方式
Azure Service Fabric 可簡化撰寫和管理可靠的無狀態與具狀態服務。 本指南示範的可靠服務 toogain 進階使用方式的相關更多控制權和彈性透過您的服務。 此指南先前 tooreading，熟悉[hello 可靠服務程式設計模型](service-fabric-reliable-services-introduction.md)。

可設定狀態與無狀態服務有使用者程式碼的兩個主要進入點：

* `RunAsync(C#) / runAsync(Java)` 是服務程式碼的一般用途進入點。
* `CreateServiceReplicaListeners(C#)` 和 `CreateServiceInstanceListeners(C#) / createServiceInstanceListeners(Java)` 適用於開啟用戶端要求的通訊接聽程式。

對於大部分服務而言，這些兩個進入點已足夠。 在少數情況下，需要更充分掌控服務的命週期時，可以使用其他生命週期事件。

## <a name="stateless-service-instance-lifecycle"></a>無狀態服務執行個體生命週期
無狀態服務的生命週期非常簡單。 無狀態服務只能開啟、關閉或中止。 無狀態服務中的 `RunAsync` 會在服務執行個體開啟時執行，並在服務執行個體關閉或中止時取消。

雖然`RunAsync`應該很足夠中幾乎所有的情況下，hello 開啟時，關閉，並中止事件中無狀態服務也會提供：

* `Task OnOpenAsync(IStatelessServicePartition, CancellationToken) - C# / CompletableFuture<String> onOpenAsync(CancellationToken) - Java`關於使用 toobe hello 無狀態服務執行個體時，會呼叫 OnOpenAsync。 這個階段可以啟動擴充服務的初始化作業。
* `Task OnCloseAsync(CancellationToken) - C# / CompletableFuture onCloseAsync(CancellationToken) - Java`OnCloseAsync 稱為 hello 無狀態服務執行個體即將 toobe 時正常關閉。 發生這個問題正在升級 hello 服務的程式碼、 tooload 平衡，因為正在移動 hello 服務執行個體或偵測到暫時性錯誤。 OnCloseAsync 可以關閉使用的 toosafely 任何資源，停止任何背景處理、 完成儲存外部的狀態，或關閉現有連接。
* `void OnAbort() - C# / void onAbort() - Java`OnAbort 稱為 hello 無狀態服務執行個體被強制關閉時。 這通常稱為 hello 節點上偵測到永久錯誤時，或 Service Fabric 無法可靠地管理 hello 服務執行個體的生命週期到期 toointernal 失敗時。

## <a name="stateful-service-replica-lifecycle"></a>具狀態服務複本生命週期

> [!NOTE]
> Java 中尚未支援具狀態 Reliable Services。
>
>

具狀態服務複本的生命週期比無狀態服務執行個體更為複雜。 此外 tooopen，關閉並終止事件，可設定狀態的服務複本正在進行角色變更，在其存留期間。 當具狀態服務複本變更角色時，hello`OnChangeRoleAsync`觸發事件：

* `Task OnChangeRoleAsync(ReplicaRole, CancellationToken)`OnChangeRoleAsync 稱為 hello 可設定狀態的服務複本變更角色，例如 tooprimary 或次要資料庫時。 主要複本可以寫入狀態 （允許 toocreate 和寫入 tooReliable 集合）。 次要複本則會獲得讀取狀態 (只能從現有的可靠集合讀取)。 可設定狀態的服務中的大多數工作是在 hello 主要複本執行。 次要複本可以執行唯讀驗證、產生報表、資料採礦或其他唯讀作業。

在可設定狀態的服務中，hello 主要複本會具有寫入權限 toostate，並因此通常是 hello 服務執行實際工作時。 hello`RunAsync`執行 hello 可設定狀態的服務複本為主要時，才可設定狀態的服務中的方法。 hello`RunAsync`方法取消當主要複本的角色變更從主要資料庫，以及在 hello 期間關閉，並中止事件。

使用 hello`OnChangeRoleAsync`事件可讓您根據複本角色也如同回應 toorole 變更 tooperform 工作。

可設定狀態的服務並且提供其 hello 相同的四個週期事件為無狀態服務，與 hello 相同的語意，它使用案例：

```csharp
* Task OnOpenAsync(IStatefulServicePartition, CancellationToken)
* Task OnCloseAsync(CancellationToken)
* void OnAbort()
```

## <a name="next-steps"></a>後續步驟
更進階主題相關 tooService 網狀架構，請參閱下列文章 hello:

* [設定具狀態的 Reliable Services](service-fabric-reliable-services-configuration.md)
* [Service Fabric 健康狀態簡介](service-fabric-health-introduction.md)
* [使用系統健康狀態報告進行疑難排解](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [設定服務以 hello Service Fabric 叢集資源管理員](service-fabric-cluster-resource-manager-configure-services.md)
