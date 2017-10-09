---
title: "aaaCreate chaos 和容錯移轉測試 Azure microservices |Microsoft 文件"
description: "使用 hello Service Fabric chaos 測試和容錯移轉時，測試案例 tooinduce 錯誤，並確認您的服務的 hello 可靠性。"
services: service-fabric
documentationcenter: .net
author: motanv
manager: rsinha
editor: toddabel
ms.assetid: 8eee7e89-404a-4605-8f00-7e4d4fb17553
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: motanv
ms.openlocfilehash: 1cac4f9e0e4a6c8416d5220d1537b5110decd1f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="testability-scenarios"></a>Testability 案例
雲端基礎結構之類的大型分散式系統本身並不可靠。 Azure Service Fabric 提供開發人員 hello 能力 toowrite 服務 toorun 不可靠的基礎結構之上。 在順序 toowrite 高品質的服務，開發人員需要 toobe 無法 tooinduce 這類不可靠的基礎結構 tootest hello 的穩定性其服務。

hello 錯誤分析服務讓開發人員 hello 能力 tooinduce 錯誤動作 tootest 服務中的失敗 hello 存在。 但鎖定式模擬錯誤就僅只於此了。 此外，測試 tootake hello hello 測試案例用於 Service Fabric: chaos 測試和容錯移轉測試。 這些案例，以模擬連續交錯的錯誤，依正常程序並不正常，整個 hello 叢集一段很長的時間。 測試設定之後 hello 速率與類型的錯誤，則可以透過 C# Api 或 PowerShell，toogenerate hello 叢集中的錯誤和您的服務啟動。

> [!WARNING]
> ChaosTestScenario 已被更有彈性、以服務為基礎的混亂取代。 Toohello 新發行項，請參閱[控制 Chaos](service-fabric-controlled-chaos.md)如需詳細資訊。
> 
> 

## <a name="chaos-test"></a>混亂測試
hello chaos 案例 hello 整個 Service Fabric 叢集中，會產生錯誤。 hello 案例壓縮通常月或年 tooa 中看到幾個小時的錯誤。 hello 組合的交錯錯誤與 hello 高錯誤的速率尋找極端案例，否則會遺失。 這將致使 tooa 顯著改進的 hello 服務的 hello 程式碼品質。

### <a name="faults-simulated-in-hello-chaos-test"></a>Hello chaos 測試中模擬的錯誤
* 重新啟動節點
* 重新啟動已部署的程式碼封裝
* 移除複本
* 重新啟動複本
* 移動主要複本 (選擇性)
* 移動次要複本 (選擇性)

hello chaos 測試執行錯誤的多個反覆項目，並 hello 的叢集驗證指定的時間。 也可設定 hello hello 叢集 toostabilize 和驗證 toosucceed 所花費的時間。 當您叫用單一叢集驗證失敗時，就會失敗 hello 案例。

例如，請考慮測試設定 toorun 一小時，最大值的三個並行錯誤。 hello 測試將會產生三個錯誤，並驗證 hello 叢集健全狀況。 hello 測試會逐一 hello 上一個步驟，直到 hello 叢集會變為狀況不良或一小時已通過檢查。 如果 hello 叢集會變成狀況不良任何反覆項目，也就是它不會不穩定的設定時間內，hello 測試將會失敗並發生例外狀況。 此例外狀況表示發生了錯誤，且需要進一步調查。

其目前的格式，hello chaos 測試中的 hello 錯誤產生引擎會產生只有安全的錯誤。 這表示，在外部錯誤 hello 不存在，仲裁或資料遺失永遠不會發生。

### <a name="important-configuration-options"></a>重要的組態選項
* **TimeToRun**： 總時間成功完成前，將執行該 hello 測試。 hello 測試可以稍早完成，就不需驗證失敗。
* **MaxClusterStabilizationTimeout**: hello 叢集 toobecome 狀況良好失敗 hello 測試前的時間 toowait 的數量上限。 hello 執行檢查叢集健全狀況是否為 [確定]、 服務健全狀況正常、 hello 目標複本集大小針對達成 hello 服務資料分割，而且沒有任何 InBuild 複本存在。
* **MaxConcurrentFaults**：每個反覆運算中引發的最大並行錯誤數。 hello hello 編號，hello 更積極的 hello 測試，因此導致轉換組合和更複雜的容錯移轉。 hello 測試可保證沒有外部錯誤的情況下將不會有仲裁或資料遺失，不論這項設定很高。
* **EnableMoveReplicaFaults**： 啟用或停用 hello 錯誤造成的 hello hello 移動主要或次要複本。 預設會停用這些錯誤。
* **WaitTimeBetweenIterations**： 錯誤和對應的驗證的重試回合之後，也就是反覆項目之間的時間 toowait 數量。

### <a name="how-toorun-hello-chaos-test"></a>如何測試 toorun hello chaos
C# 範例

```csharp
using System;
using System.Fabric;
using System.Fabric.Testability.Scenario;
using System.Threading;
using System.Threading.Tasks;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";

        Console.WriteLine("Starting Chaos Test Scenario...");
        try
        {
            RunChaosTestScenarioAsync(clusterConnection).Wait();
        }
        catch (AggregateException ae)
        {
            Console.WriteLine("Chaos Test Scenario did not complete: ");
            foreach (Exception ex in ae.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("Chaos Test Scenario completed.");
        return 0;
    }

    static async Task RunChaosTestScenarioAsync(string clusterConnection)
    {
        TimeSpan maxClusterStabilizationTimeout = TimeSpan.FromSeconds(180);
        uint maxConcurrentFaults = 3;
        bool enableMoveReplicaFaults = true;

        // Create FabricClient with connection and security information here.
        FabricClient fabricClient = new FabricClient(clusterConnection);

        // hello chaos test scenario should run at least 60 minutes or until it fails.
        TimeSpan timeToRun = TimeSpan.FromMinutes(60);
        ChaosTestScenarioParameters scenarioParameters = new ChaosTestScenarioParameters(
          maxClusterStabilizationTimeout,
          maxConcurrentFaults,
          enableMoveReplicaFaults,
          timeToRun);

        // Other related parameters:
        // Pause between two iterations for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenIterations = TimeSpan.FromSeconds(30);
        // Pause between concurrent actions for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenFaults = TimeSpan.FromSeconds(10);

        // Create hello scenario class and execute it asynchronously.
        ChaosTestScenario chaosScenario = new ChaosTestScenario(fabricClient, scenarioParameters);

        try
        {
            await chaosScenario.ExecuteAsync(CancellationToken.None);
        }
        catch (AggregateException ae)
        {
            throw ae.InnerException;
        }
    }
}
```

PowerShell

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```


## <a name="failover-test"></a>容錯移轉測試
hello 容錯移轉的測試案例是以特定的服務資料分割為目標的 hello chaos 測試案例的版本。 它會測試特定服務磁碟分割上的 hello 生效的容錯移轉但保留 hello 其他服務不會受到影響。 一旦設定之後 hello 目標資料分割資訊與其他參數，它會以使用 C# Api 或 PowerShell toogenerate 錯誤的服務資料分割的用戶端工具執行。 hello 案例逐一一連串的模擬的錯誤和服務驗證您的商務邏輯上 hello 端 tooprovide 工作負載執行時。 服務驗證中若有失敗，表示有需要進一步調查的問題。

### <a name="faults-simulated-in-hello-failover-test"></a>Hello 容錯移轉的測試中模擬的錯誤
* 重新啟動裝載 hello 資料分割的已部署的程式碼封裝
* 移除主要/次要複本或無狀態執行個體
* 重新啟動主要的次要複本 (如果是保存的服務)
* 移動主要複本
* 移動次要複本
* 重新啟動 hello 磁碟分割

hello 容錯移轉測試，產生所選的錯誤，然後執行驗證 hello 服務 tooensure 上其穩定性。 只有其中一個錯誤的時間，相對於 toopossible 在 hello chaos 測試中的多個錯誤，有可能引起 hello 容錯移轉測試。 如果 hello 服務資料分割之後每個錯誤不穩定 hello 設定逾時時間內 hello 測試將會失敗。 hello 測試產生安全的錯誤。 這表示因為沒有外部錯誤，所以不會發生仲裁或資料遺失。

### <a name="important-configuration-options"></a>重要的組態選項
* **PartitionSelector**： 指定所需目標的 toobe hello 資料分割的選取器物件。
* **TimeToRun**: hello 測試將執行的總時間之前完成。
* **MaxServiceStabilizationTimeout**: hello 叢集 toobecome 狀況良好失敗 hello 測試前的時間 toowait 的數量上限。 hello 執行檢查服務健全狀況是否為 [確定]，hello 目標複本集大小為止的所有資料分割，而且沒有任何 InBuild 複本存在。
* **WaitTimeBetweenFaults**： 每個錯誤和驗證週期之間的時間 toowait 數量。

### <a name="how-toorun-hello-failover-test"></a>如何測試 toorun hello 容錯移轉
**C#**

```csharp
using System;
using System.Fabric;
using System.Fabric.Testability.Scenario;
using System.Threading;
using System.Threading.Tasks;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");

        Console.WriteLine("Starting Chaos Test Scenario...");
        try
        {
            RunFailoverTestScenarioAsync(clusterConnection, serviceName).Wait();
        }
        catch (AggregateException ae)
        {
            Console.WriteLine("Chaos Test Scenario did not complete: ");
            foreach (Exception ex in ae.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("Chaos Test Scenario completed.");
        return 0;
    }

    static async Task RunFailoverTestScenarioAsync(string clusterConnection, Uri serviceName)
    {
        TimeSpan maxServiceStabilizationTimeout = TimeSpan.FromSeconds(180);
        PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);

        // Create FabricClient with connection and security information here.
        FabricClient fabricClient = new FabricClient(clusterConnection);

        // hello chaos test scenario should run at least 60 minutes or until it fails.
        TimeSpan timeToRun = TimeSpan.FromMinutes(60);
        FailoverTestScenarioParameters scenarioParameters = new FailoverTestScenarioParameters(
          randomPartitionSelector,
          timeToRun,
          maxServiceStabilizationTimeout);

        // Other related parameters:
        // Pause between two iterations for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenIterations = TimeSpan.FromSeconds(30);
        // Pause between concurrent actions for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenFaults = TimeSpan.FromSeconds(10);

        // Create hello scenario class and execute it asynchronously.
        FailoverTestScenario failoverScenario = new FailoverTestScenario(fabricClient, scenarioParameters);

        try
        {
            await failoverScenario.ExecuteAsync(CancellationToken.None);
        }
        catch (AggregateException ae)
        {
            throw ae.InnerException;
        }
    }
}
```


**PowerShell**

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/SampleApp/SampleService"

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindSingleton
```
