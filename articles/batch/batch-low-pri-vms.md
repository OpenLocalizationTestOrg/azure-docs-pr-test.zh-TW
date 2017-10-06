---
title: "aaaRun Azure 批次工作負載符合成本效益的低優先順序 Vm （預覽） |Microsoft 文件"
description: "了解 tooprovision 低優先權 Vm tooreduce hello Azure 批次工作負載的成本。"
services: batch
author: mscurrell
manager: timlt
ms.assetid: dc6ba151-1718-468a-b455-2da549225ab2
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.workload: na
ms.date: 07/21/2017
ms.author: markscu
ms.openlocfilehash: 91a5e89a819d05583e6b146932d925e217b4be4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-low-priority-vms-with-batch-preview"></a>使用低優先順序的 VM 搭配 Batch (預覽)

Azure 批次提供批次工作負載的低先後虛擬機器 (Vm) tooreduce hello 的成本。 低優先順序的 VM 能提供大量的計算能力，同時也是經濟實惠的選擇，從而實現新的 Batch 工作負載類型。

低優先順序的 VM 能善用 Azure 中的剩餘容量。 當您指定集區中的低優先順序 VM 時，Azure Batch 就會在有多餘的容量時自動加以使用。

使用低優先權 Vm hello 權衡取捨是使用在 Azure 中沒有多餘的容量時，可能佔用那些 Vm。 基於這個理由，低優先順序的 VM 最適合特定類型的工作負載。 批次和 hello 作業完成時間是有彈性且 hello 工作會分散到多個 Vm 的非同步處理工作負載使用低優先權的 Vm。

低優先順序 VM 的成本遠低於專用 VM。 如需定價詳細資料，請參閱 [Batch 定價](https://azure.microsoft.com/pricing/details/batch/)。

低優先順序 Vm 的其他討論，請參閱 hello 部落格文章公告：[批次計算花費少量 hello 價格](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/)。

> [!IMPORTANT]
> 低優先順序的 VM 目前在預覽中，僅適用於 Batch 中執行的工作負載。 
>
>

## <a name="use-cases-for-low-priority-vms"></a>低優先順序 VM 的使用案例

提供的低優先順序 Vm hello 特性，哪些工作負載可以和無法使用它們？ 一般情況下，批次處理工作負載就很適合，因為作業會區分成許多平行的工作，或是會將許多作業相應放大並分散於許多 VM。

-   在 Azure 的適當作業中的多餘容量 toomaximize 使用可以向外擴充。

-   偶爾 Vm 可能無法使用，或將會優先，會導致減少的容量，工作以及可能會導致 tootask 中斷和重播。 作業必須是彈性 hello toorun 花費的時間。

-   如果工作較長的作業受到中斷，可能就會影響較大。 如果長時間執行工作單位會實作檢查點 toosave 進度時，它們執行，則不中斷的影響會最少。 使用較短的時間執行工作通常 toowork 最適合低優先順序的 vm 為 hello 中斷的影響最少。

-   長時間執行 MPI 工作，利用多個 Vm 不適合的 toouse 低優先順序的 Vm 中當做一個先佔 VM 將會需要再次執行 toobe 可能負責人 toohello 整個作業。

批次處理的一些範例使用案例適合的 toouse 低優先順序的 Vm 為：

-   **開發與測試**︰特別是，如果您正在開發大規模的解決方案，就可實現可觀的成本節省。 所有的測試類型都能有所助益，但大規模的負載測試及迴歸測試都是很棒的用途。

-   **補充隨容量**： 低優先權的 Vm 可以用來補充 regular 專用的 Vm-可用時，工作可以和調整其規模較低的成本因此更快速完成; 時無法使用，hello 基準的專用 Vm 使用。

-   **彈性的工作執行時間**： 如果 hello 計時器工作沒有彈性 toocomplete，則可容許的容量可能會卸除; 不過，以 hello 加法的低優先順序 Vm 作業會經常執行更快速且更低的成本。

批次集區可以設定的 toouse 取決於 hello 彈性的低優先順序 Vm 有幾個方法，工作執行時間：

-   低優先順序的 VM 可以單獨用於集區中，Batch 只會在容量可用時，將任何佔用的容量復原。 這是 hello 最便宜的方式 tooexecute 作業，因為只有低優先順序的 Vm 所使用。

-   低優先順序的 VM 可以用來搭配專用 VM 的固定基準。 hello 固定的數目的專用的 Vm 可確保沒有一律某些容量 tookeep 工作進度。

-   可以有動態混合的專用和低優先順序的 Vm，以便可用時，成本較低的低優先順序 Vm 單獨使用，但 hello 全文價格專用 Vm 擴充規模，必要時，tookeep 容量可用 tookeep hello 作業的下限進度。

## <a name="batch-support-for-low-priority-vms"></a>Batch 支援低優先順序的 VM

Azure 批次提供數項功能，可讓您輕鬆 tooconsume 及受益於低優先權的 Vm:

-   Batch 集區可以同時包含專用 VM 和低優先順序的 VM。 當集區會在建立或變更現有集區，使用 hello 明確的調整大小作業，或使用自動調整規模隨時都可以指定 hello 每種類型的 VM 數目。 作業和工作提交可以維持不變，而且不需要顧慮 hello 集區中的 hello VM 類型。 它也是可能 toohave 集區完全使用低優先權 Vm toorun 作業，但啟動專用 Vm 調整為廉價地如果 hello 容量低於下限臨界值，將執行的作業。

-   批次集區會自動搜尋低優先權 Vm toohello 目標數目。 如果 Vm 被佔用，批次會嘗試 tooreplace hello 遺失容量及傳回 toohello 目標。

-   在工作被中斷的 hello 情況下，會偵測到批次，並將其自動工作 toobe 再次執行重新排入佇列中。

-   低優先順序 VM 具有核心配額，不同於專用 VM 的核心配額。 
    hello 引號的低優先順序的 Vm 是高於專用的 Vm，因為低優先權 Vm 成本也比較低。 如需詳細資訊，請參閱 [Batch 服務配額和限制](batch-quota-limit.md#resource-quotas)。    

> [!NOTE]
> 低優先順序 Vm 目前不支援批次帳戶 hello 集區配置模式下設定的位置太[使用者訂用帳戶](batch-account-create-portal.md#user-subscription-mode)。
>
>

## <a name="create-and-update-pools"></a>建立和更新集區

批次集區可以包含專用和低優先順序的 Vm （也參考的 tooas 計算節點）。 您可以設定專用和低優先順序的 Vm 的運算節點的 hello 目標數目。 hello 目標節點的數目指定 hello 數目要 toohave hello 集區中的 Vm。

比方說，使用 Azure 雲端服務 Vm 和 5 的目標集 toocreate 專用 Vm 和 20 低優先權的 Vm:

```csharp
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: "cspool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard_D2_v2",
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4") // WS 2012 R2
);
```

使用 Azure 虛擬機器 （在此情況下 Linux Vm） 具有 5 個目標集 toocreate 專用 Vm 和 20 低優先權的 Vm:

```csharp
ImageReference imageRef = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "16.04.0-LTS",
    version: "latest");

// Create hello pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration("batch.node.ubuntu 16.04", imageRef);

pool = batchClient.PoolOperations.CreatePool(
    poolId: "vmpool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard\_D2\_v2",
    virtualMachineConfiguration: virtualMachineConfiguration);
```

您可以取得專用和低優先順序的 Vm hello 目前節點的數目：

```csharp
int? numDedicated = pool1.CurrentDedicatedComputeNodes;
int? numLowPri = pool1.CurrentLowPriorityComputeNodes;
```

集區的節點具有屬性 tooindicate hello 節點是否為專用或低優先順序的 VM:

```csharp
bool? isNodeDedicated = poolNode.IsDedicated;
```

當集區中的一個或多個節點被佔用，集區清單節點的作業仍會傳回這些節點、 hello 的目前低優先權的節點數目會維持不變，但這些節點都有其狀態設定 toothe**先佔**狀態。 批次會嘗試 toofind 取代 Vm，而且如果成功的話，hello 節點將會瀏覽**建立**然後**起始**狀態才能成為可供工作執行方式就像是新節點。

## <a name="scale-a-pool-containing-low-priority-vms"></a>調整包含低優先順序 VM 的集區

如同單獨組成專用的 Vm 集區，它是可能 tooscale 集區包含低優先權的 Vm，藉由呼叫 hello 調整方法或使用自動調整規模。

hello 集區調整大小作業採用第二個選擇性參數的值更新**targetLowPriorityNodes**:

```csharp
pool.Resize(targetDedicatedComputeNodes: 0, targetLowPriorityComputeNodes: 25);
```

hello 集區自動調整規模公式支援低優先權 Vm 如下所示：

-   您可以取得或設定 hello hello 服務定義的變數值**$TargetLowPriorityNodes**。

-   您可以取得 hello 服務定義變數的 hello 值**$CurrentLowPriorityNodes**。

-   您可以取得 hello 服務定義變數的 hello 值**$PreemptedNodeCount**。 
    此變數傳回 hello hello 中的節點數目佔用狀態，以及可讓您在相應增加或減少 hello 專用節點數目，而是根據 hello 先佔會無法使用的節點數目。

## <a name="jobs-and-tasks"></a>工作 (Job) 和工作 (Task)

工作與工作需要極少支援低優先權的節點。hello 僅支援如下所示：

-   hello 工作 JobManagerTask 屬性已有新的屬性**AllowLowPriorityNode**。 
    這個屬性為 true 時，可以排定 hello 作業管理員工作專用或低優先順序的節點上。 如果此屬性為 false，hello 作業管理員工作將會只排程的 tooa 專用的節點。

-   [環境變數](batch-compute-node-environment-variables.md)是可用 tooa 工作應用程式，使它可以判斷它是否為低優先順序或專用節點上執行。 hello 環境變數是 AZ_BATCH_NODE_IS_DEDICATED。

## <a name="handling-preemption"></a>處理優先佔用

Vm 偶爾可能會預先清空;當發生這種情況，批次未 hello 遵循：

-   hello 先佔的 Vm 有其狀態也更新**先佔**。
-   如果工作上執行 hello 預先清空節點 Vm，則這些工作會排入佇列並再次執行。
-   有效地刪除 hello VM，這會導致 tooany 資料儲存在本機上 hello 遺失的 VM。
-   hello 集區會持續嘗試 tooreach hello 目標可用的低優先權的節點數目。 找到取代容量時，節點會保留其識別碼，但在可供工作排程使用之前，會先重新初始化，逐步進行**建立**和**啟動**狀態。
-   先佔計數可作為 hello Azure 入口網站中的度量。

## <a name="metrics"></a>度量

新的度量資訊是用於 hello [Azure 入口網站](https://portal.azure.com)低優先權的節點。 這些計量包括：

- 低優先順序節點計數
- 低優先順序核心計數 
- 先占節點計數

tooview hello Azure 入口網站中的度量：

1. 巡覽 tooyour hello 入口網站中的批次帳戶，並檢視您的 Batch 帳戶的 hello 設定。
2. 選取**度量**從 hello**監視**> 一節。
3. 選取您想要的 hello 度量從 hello**可用的度量**清單。

![低優先順序節點的計量](media/batch-low-pri-vms/low-pri-metrics.png)

## <a name="next-steps"></a>後續步驟

* 讀取 hello[批次功能概觀，讓開發人員](batch-api-basics.md)，任何人準備 toouse 批次的重要資訊。 hello 發行項包含許多建置批次應用程式時，可以使用的 API 功能的批次服務資源集區、 節點、 工作和工作和 hello，如需詳細的資訊。
* 深入了解 hello[批次應用程式開發介面和工具](batch-apis-tools.md)可用來建置批次的解決方案。
