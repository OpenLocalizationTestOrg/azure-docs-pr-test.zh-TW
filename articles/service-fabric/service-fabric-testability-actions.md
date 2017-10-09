---
title: "在 Azure microservices aaaSimulate 失敗 |Microsoft 文件"
description: "這篇文章討論關於在 Microsoft Azure Service Fabric 中找到的 hello 可測試性動作。"
services: service-fabric
documentationcenter: .net
author: motanv
manager: timlt
editor: toddabel
ms.assetid: ed53ca5c-4d5e-4b48-93c9-e386f32d8b7a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: motanv;heeldin
ms.openlocfilehash: 5bdda1c0c5a40b243ab956c4791afd52e11c4089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="testability-actions"></a>Testability 動作
在順序 toosimulate 不可靠的基礎結構，Azure Service Fabric 提供您 hello 開發人員，方式 toosimulate 各種真實世界失敗和狀態轉換。 這些方法會以 Testability 動作的形式公開。 hello 動作是 hello 會造成特定的錯誤資料隱碼、 狀態轉換或驗證的低階 Api。 結合這些動作後，便可以為您的服務撰寫完整的測試案例。

Service Fabric 會提供由這些動作所組成的一些常見測試案例。 我們強烈建議您利用這些內建的情況下，謹慎選擇 tootest 常用的狀態轉換以及失敗情況。 不過，動作可以使用的 toocreate 自訂測試案例的情況下，未涵蓋的 hello 內建案例尚未或自訂所量身訂做的應用程式需要 tooadd 涵蓋範圍時。

Hello System.Fabric.dll 組件中找到的 hello 動作的 C# 實作。 hello Microsoft.ServiceFabric.Powershell.dll 組件中找到 hello 系統網狀架構 PowerShell 模組。 Hello ServiceFabric PowerShell 模組執行階段安裝的一部分，是為了方便使用的已安裝的 tooallow。

## <a name="graceful-vs-ungraceful-fault-actions"></a>非失誤性與失誤性錯誤動作比較
Testability 動作分為兩個主要貯體：

* 失誤性錯誤：這些錯誤會模擬失敗案例 (例如機器重新啟動和處理程序當機)。 在這類的失敗的情況下，hello 執行內容的程序會突然停止。 這表示不會清除 hello 狀態的 hello 應用程式重新啟動之前執行。
* 非失誤性錯誤：這些錯誤會模擬正常動作 (例如由負載平衡觸發的複本移動及卸除)。 在這種情況下，hello 服務收到通知，hello 關閉，並可以清除在結束之前的 hello 狀態。

較佳的品質驗證執行 hello 服務和企業工作負載時由引發各種依正常程序與不正常的錯誤。 不正常的錯誤執行其中 hello 服務處理序突然結束 hello 中間的某些工作流程的案例。 此程序一旦 hello 服務複本還原 Service Fabric 測試 hello 復原路徑。 這將有助於測試資料的一致性和是否 hello 服務狀態正確維護在失敗之後。 hello 失敗 （hello 正常失敗） 的其他組測試 hello 服務正確地回應 tooreplicas Service Fabric 移動。 這在 hello RunAsync 方法中測試取消的處理。 hello 服務需要 toocheck hello 取消語彙基元所設定，正確地儲存其狀態，並結束 hello RunAsync 方法。

## <a name="testability-actions-list"></a>Testability 動作清單
| 動作 | 說明 | Managed API | PowerShell Cmdlet | 非失誤性/失誤性錯誤 |
| --- | --- | --- | --- | --- |
| CleanTestState |Hello 叢集發生不正常關機 hello 測試驅動程式會移除所有 hello 測試狀態。 |CleanTestStateAsync |Remove-ServiceFabricTestState |不適用 |
| InvokeDataLoss |會引發資料遺失至服務分割區中。 |InvokeDataLossAsync |Invoke-ServiceFabricPartitionDataLoss |非失誤性 |
| InvokeQuorumLoss |會放置指定狀態服務分割區至仲裁遺失中。 |InvokeQuorumLossAsync |Invoke-ServiceFabricQuorumLoss |非失誤性 |
| 移動主要複本 |移動 hello 指定具狀態服務 toohello 指定的叢集節點的主要複本。 |MovePrimaryAsync |Move-ServiceFabricPrimaryReplica |非失誤性 |
| 移動次要複本 |移動 hello 目前的次要複本的可設定狀態服務 tooa 不同的叢集節點。 |MoveSecondaryAsync |Move-ServiceFabricSecondaryReplica |非失誤性 |
| RemoveReplica |移除叢集中的複本以模擬複本失敗案例。 這將會關閉 hello 複本，並會將它轉換 toorole 'None'、 從 hello 叢集移除它的所有狀態。 |RemoveReplicaAsync |Remove-ServiceFabricReplica |非失誤性 |
| RestartDeployedCodePackage |藉由重新啟動部署在叢集中之節點上的程式碼封裝，模擬程式碼封裝處理程序的失敗案例。 這會中止 hello 程式碼封裝程序，將重新裝載之所有的 hello 使用者服務複本啟動該處理程序。 |RestartDeployedCodePackageAsync |Restart-ServiceFabricDeployedCodePackage |失誤性 |
| RestartNode |藉由重新啟動節點，模擬 Service Fabric 叢集節點的失敗案例。 |RestartNodeAsync |Restart-ServiceFabricNode |失誤性 |
| RestartPartition |藉由重新啟動部分或所有分割區複本，模擬資料中心停機或叢集停機的案例。 |RestartPartitionAsync |Restart-ServiceFabricPartition |非失誤性 |
| RestartReplica |重新啟動叢集中的永續性的複本、 關閉 hello 複本後再重新開啟它，以模擬複本失敗。 |RestartReplicaAsync |Restart-ServiceFabricReplica |非失誤性 |
| StartNode |會啟動叢集中已停止的節點。 |StartNodeAsync |Start-ServiceFabricNode |不適用 |
| StopNode |藉由停止叢集中的節點，模擬節點失敗案例。 StartNode 呼叫之前，將會向下保持 hello 節點。 |StopNodeAsync |Stop-ServiceFabricNode |失誤性 |
| ValidateApplication |Hello 可用性和健全狀況的應用程式，通常由某些錯誤引發 hello 系統內的所有 Service Fabric 服務驗證。 |ValidateApplicationAsync |Test-ServiceFabricApplication |不適用 |
| ValidateService |通常後一些錯誤查到 hello 系統驗證 hello 可用性和健全狀況的 Service Fabric 服務。 |ValidateServiceAsync |Test-ServiceFabricService |不適用 |

## <a name="running-a-testability-action-using-powershell"></a>使用 PowerShell 執行 Testability 動作
本教學課程示範如何使用 PowerShell 的可測試性動作 toorun。 您將學習如何 toorun 針對本機的 （一個方塊） 叢集或 Azure 的叢集的可測試性動作。 Microsoft.Fabric.Powershell.dll-hello Service Fabric PowerShell 模組--會自動安裝時安裝 Microsoft Service Fabric MSI hello。 當您開啟 PowerShell 命令提示字元時，會自動載入 hello 模組。

教學課程區段：

* [針對一整體叢集執行動作](#run-an-action-against-a-one-box-cluster)
* [針對 Azure 叢集執行動作](#run-an-action-against-an-azure-cluster)

### <a name="run-an-action-against-a-one-box-cluster"></a>針對一整體叢集執行動作
toohello 叢集和系統管理員模式開啟 hello PowerShell 命令提示字元，第一次連接 toorun 針對本機叢集，可測試性動作。 讓我們看看 hello**重新啟動 ServiceFabricNode**動作。

```powershell
Restart-ServiceFabricNode -NodeName Node1 -CompletionMode DoNotVerify
```

這裡 hello 動作**重新啟動 ServiceFabricNode**名為"Node1"的節點上執行。 hello 完成模式指定，它不應該確認 hello 重新啟動節點動作是否實際上是否成功。 為 [驗證] 指定 hello 完成模式會導致 tooverify 是否實際上成功 hello 重新啟動動作。 而不是直接由其名稱指定 hello 節點，您可以如下所示指定它的資料分割索引鍵和 hello 種類的複本，透過：

```powershell
Restart-ServiceFabricNode -ReplicaKindPrimary  -PartitionKindNamed -PartitionKey Partition3 -CompletionMode Verify
```


```powershell
$connection = "localhost:19000"
$nodeName = "Node1"

Connect-ServiceFabricCluster $connection
Restart-ServiceFabricNode -NodeName $nodeName -CompletionMode DoNotVerify
```

**重新啟動 ServiceFabricNode**應該使用的 toorestart 叢集中的 Service Fabric 節點。 這樣會停止 hello Fabric.exe 程序，將會重新啟動所有 hello 系統服務和使用者服務複本的該節點上裝載。 使用此 API tootest 您的服務，有助於發現 bug，沿著 hello 容錯移轉復原路徑。 它會協助模擬 hello 叢集中的節點失敗。

hello 下列螢幕擷取畫面顯示 hello**重新啟動 ServiceFabricNode**動作中的可測試性命令。

![](media/service-fabric-testability-actions/Restart-ServiceFabricNode.png)

hello 第一次輸出的 hello **Get ServiceFabricNode** (hello Service Fabric PowerShell 模組的 cmdlet) 會顯示該 hello 本機叢集具有五個節點： Node.1 tooNode.5。 Hello 可測試性動作 (cmdlet) 之後**重新啟動 ServiceFabricNode** hello 節點上執行名為 Node.4，我們會看到已重設該 hello 節點的執行時間。

### <a name="run-an-action-against-an-azure-cluster"></a>針對 Azure 叢集執行動作
（透過使用 PowerShell） 執行可測試性動作，對 Azure 的叢集是針對本機叢集類似 toorunning hello 動作。 hello 只能差異在於，您才能執行 hello 動作，而不是連接 toohello 本機叢集，您需要 tooconnect toohello Azure 叢集的第一次。

## <a name="running-a-testability-action-using-c35"></a>使用 C&#35; 執行 Testability 動作
toorun 可測試性動作，使用 C#，首先您需要 tooconnect toohello 叢集使用 FabricClient。 然後取得 hello 所需要的參數 toorun hello 動作。 可以使用不同的參數 toorun hello 相同的動作。
查看 hello RestartServiceFabricNode 動作，它是使用 hello 節點資訊 （節點名稱和節點執行個體識別碼） 的其中一種方式 toorun hello 叢集中。

```csharp
RestartNodeAsync(nodeName, nodeInstanceId, completeMode, operationTimeout, CancellationToken.None)
```

參數說明：

* **CompleteMode**指定模式的 hello 不應該確認 hello 重新啟動動作是否實際上是否成功。 為 [驗證] 指定 hello 完成模式會導致 tooverify 是否實際上成功 hello 重新啟動動作。  
* **OperationTimeout**集 hello hello 作業 toofinish 的時間量之前擲回 TimeoutException 例外狀況。
* **CancellationToken**啟用取消暫止呼叫 toobe。

而不是直接由其名稱指定 hello 節點，您可以指定它透過資料分割索引鍵和 hello 類型的複本。

如需詳細資訊，請參閱 [PartitionSelector 和 ReplicaSelector](#partition_replica_selector)。

```csharp
// Add a reference tooSystem.Fabric.Testability.dll and System.Fabric.dll
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Fabric.Testability;
using System.Fabric;
using System.Threading;
using System.Numerics;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");
        string nodeName = "N0040";
        BigInteger nodeInstanceId = 130743013389060139;

        Console.WriteLine("Starting RestartNode test");
        try
        {
            //Restart hello node by using ReplicaSelector
            RestartNodeAsync(clusterConnection, serviceName).Wait();

            //Another way toorestart node is by using nodeName and nodeInstanceId
            RestartNodeAsync(clusterConnection, nodeName, nodeInstanceId).Wait();
        }
        catch (AggregateException exAgg)
        {
            Console.WriteLine("RestartNode did not complete: ");
            foreach (Exception ex in exAgg.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("RestartNode completed.");
        return 0;
    }

    static async Task RestartNodeAsync(string clusterConnection, Uri serviceName)
    {
        PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);
        ReplicaSelector primaryofReplicaSelector = ReplicaSelector.PrimaryOf(randomPartitionSelector);

        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(primaryofReplicaSelector, CompletionMode.Verify);
    }

    static async Task RestartNodeAsync(string clusterConnection, string nodeName, BigInteger nodeInstanceId)
    {
        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(nodeName, nodeInstanceId, CompletionMode.Verify);
    }
}
```

## <a name="partitionselector-and-replicaselector"></a>PartitionSelector 和 ReplicaSelector
### <a name="partitionselector"></a>PartitionSelector
PartitionSelector 是 helper，可測試性中公開，是使用的 tooselect 特定資料分割上的 tooperform 任一 hello 可測試性動作。 如果事先知道 hello 分割區識別碼，它可以是使用的 tooselect 特定分割區。 或者，您可以提供 hello 資料分割索引鍵並 hello 作業將會在內部解析 hello 分割區識別碼。 您也可以選取隨機的資料分割的 hello 選項。

toouse 此協助程式，建立 hello PartitionSelector 物件，並使用其中一種 hello 選取 * 方法選取 hello 資料分割。 然後傳入 hello PartitionSelector 物件 toohello 需要它的 API。 如果不選取任何選項，則預設 tooa 隨機分割區。

```csharp
Uri serviceName = new Uri("fabric:/samples/InMemoryToDoListApp/InMemoryToDoListService");
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
string partitionName = "Partition1";
Int64 partitionKeyUniformInt64 = 1;

// Select a random partition
PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);

// Select a partition based on ID
PartitionSelector partitionSelectorById = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);

// Select a partition based on name
PartitionSelector namedPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionName);

// Select a partition based on partition key
PartitionSelector uniformIntPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionKeyUniformInt64);
```

### <a name="replicaselector"></a>ReplicaSelector
ReplicaSelector 為可測試性中公開協助程式，而且是使用的 toohelp 選取哪些 tooperform 上的複本任一 hello 可測試性動作。 如果事先知道 hello 複本識別碼，它可以是使用的 tooselect 特定複本。 此外，您可以 hello 選擇選取的主要複本或隨機的次要資料庫。 ReplicaSelector 衍生自 PartitionSelector，因此您需要 tooselect 兩者 hello 複本和 hello 想 tooperform hello 可測試性作業的磁碟分割。

toouse 此協助程式，建立 ReplicaSelector 物件，並設定您想要的 hello 方式 tooselect hello 複本和 hello 磁碟分割。 您可以將它傳遞至 hello 需要它的 API。 如果不選取任何選項，則預設 tooa 隨機複本和隨機分割區。

```csharp
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);
long replicaId = 130559876481875498;

// Select a random replica
ReplicaSelector randomReplicaSelector = ReplicaSelector.RandomOf(partitionSelector);

// Select hello primary replica
ReplicaSelector primaryReplicaSelector = ReplicaSelector.PrimaryOf(partitionSelector);

// Select hello replica by ID
ReplicaSelector replicaByIdSelector = ReplicaSelector.ReplicaIdOf(partitionSelector, replicaId);

// Select a random secondary replica
ReplicaSelector secondaryReplicaSelector = ReplicaSelector.RandomSecondaryOf(partitionSelector);
```

## <a name="next-steps"></a>後續步驟
* [Testability 案例](service-fabric-testability-scenarios.md)
* 如何 tootest 您的服務
  * [模擬服務工作負載期間的失敗案例](service-fabric-testability-workload-tests.md)
  * [服務對服務間通訊的失敗案例](service-fabric-testability-scenarios-service-communication.md)

