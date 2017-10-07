---
title: "aaaInduce 混亂中 Service Fabric 叢集 |Microsoft 文件"
description: "使用錯誤資料隱碼以及叢集分析服務 Api toomanage Chaos hello 叢集中。"
services: service-fabric
documentationcenter: .net
author: motanv
manager: anmola
editor: motanv
ms.assetid: 2bd13443-3478-4382-9a5a-1f6c6b32bfc9
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: motanv
ms.openlocfilehash: 7e87cae22645fc4ba52e258471d8f3a4ffdb1cce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="induce-controlled-chaos-in-service-fabric-clusters"></a>在 Service Fabric 叢集中引發受控制的混亂
雲端基礎結構之類的大型分散式系統本身並不可靠。 Azure Service Fabric 可讓開發人員 toowrite 可靠分散式的服務不可靠的基礎結構之上。 toowrite 健全的分散式的服務不可靠的基礎結構之上，開發人員需要其服務 toobe 無法 tootest hello 穩定性 hello 基礎不可靠的基礎結構正在進行複雜的狀態轉換時到期 toofaults。

hello[錯誤插入和叢集分析服務](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview)(也稱為 hello 錯誤 Analysis Service) 可讓開發人員 hello tooinduce 錯誤 tootest 其服務。 這些目標模擬錯誤，例如[重新啟動資料分割](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps)，可協助執行 hello 最常見的狀態轉換。 但針對性模擬錯誤會因為定義而有偏差，因此可能會遺漏只會出現在難以預測、冗長且複雜的狀態轉換順序中的問題。 如需無偏差測試，您可以使用混亂。

Chaos 模擬交錯，按定期錯誤 （依正常程序和不正常） hello 叢集在一段很長的時間。 一旦設定 Chaos hello 速率與 hello 類錯誤，您可以透過產生錯誤 hello 叢集中，並在您服務中的 C# 或 Powershell API toostart 啟動混亂。 您可以設定 Chaos toorun 之後 Chaos 會自動停止，在指定的時間範圍 （例如，對於一小時後），或您可以呼叫 StopChaos API （C# 或 Powershell） toostop 它在任何時間。

> [!NOTE]
> 其目前的格式，Chaos 產生唯一安全的錯誤，這表示，hello 沒有的外部錯誤的情況下遺失仲裁、 或資料遺失絕不會發生。
>

Chaos 執行時，它會產生不同的事件擷取 hello hello hello 當時執行狀態。 例如，ExecutingFaultsEvent 包含所有 Chaos 決定 tooexecute 該反覆項目中的 hello 錯誤。 ValidationFailedEvent 包含 hello hello 叢集驗證期間找不到驗證失敗 （健康情況或穩定性問題） 的 hello 詳細資料。 您可以叫用混亂回合 hello GetChaosReport API （C# 或 Powershell） tooget hello 的報表。 這些事件保存在[可靠的字典](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections)中，其中有由兩個組態決定的截斷原則：MaxStoredChaosEventCount (預設值為 25000) 及 StoredActionCleanupIntervalInSeconds (預設值為 3600)。 每個*StoredActionCleanupIntervalInSeconds* Chaos 檢查和所有但 hello 最近*MaxStoredChaosEventCount*事件，會清除從 hello 可靠的字典。

## <a name="faults-induced-in-chaos"></a>混亂中引發的錯誤
Chaos 跨 hello 整個 Service Fabric 叢集會產生錯誤，並將壓縮會出現在月或年，到幾個小時的錯誤。 hello 組合的交錯錯誤與 hello 高錯誤的速率尋找極端案例，否則可能會遺漏。 此練習中混亂的引導 tooa 顯著改進的 hello 服務的 hello 程式碼品質。

Chaos 引發錯誤從 hello 下列類別：

* 重新啟動節點
* 重新啟動已部署的程式碼封裝
* 移除複本
* 重新啟動複本
* 移動主要複本 (可設定)
* 移動次要複本 (可設定)

混亂會多次反覆執行。 每個反覆項目包含錯誤，而 hello 的叢集驗證指定的期間。 您可以設定 hello hello 叢集 toostabilize 和驗證 toosucceed 所花費的時間。 如果失敗位於叢集驗證，Chaos 產生，並保存 ValidationFailedEvent hello UTC 時間戳記與 hello 失敗詳細資料。 例如，請考慮設定 toorun 的三個並行錯誤最多一個小時的混亂的執行個體。 Chaos 產生三個錯誤，並接著會驗證 hello 叢集健全狀況。 它會逐一 hello 上一個步驟，直到它已明確地停止透過 hello StopChaosAsync API 或一小時會傳遞。 如果 hello 叢集會變為狀況不良任何反覆項目中 （也就是它不會不穩定內傳入 MaxClusterStabilizationTimeout hello）、 Chaos 產生 ValidationFailedEvent。 此事件表示發生了錯誤，且可能需要進一步調查。

發生錯誤導致混亂 tooget，您可以使用 GetChaosReport API （powershell 或 C#）。 hello API 取得 hello 的 hello 傳入的接續 token 或 hello 傳入的時間範圍為基礎的 hello Chaos 報表的下一個區段。 您可以指定 hello ContinuationToken tooget hello 下一個區段的 hello Chaos 報表或您可以指定 hello 時間範圍透過 StartTimeUtc 和 EndTimeUtc，但是您無法同時指定 hello ContinuationToken 和 hello 時間範圍中 hello 相同的呼叫。 超過 100 個 Chaos 事件時，hello Chaos 報表就會傳回區段其中一個區段包含不超過 100 個 Chaos 事件。

## <a name="important-configuration-options"></a>重要的組態選項
* **TimeToRun**：混亂在成功完成前的總執行時間。 它已透過 hello StopChaos API 執行 hello TimeToRun 期間之前，您可以停止混亂。

* **MaxClusterStabilizationTimeout**: hello hello 叢集 toobecome 才會產生 ValidationFailedEvent 狀況良好的時間 toowait 數量上限。 它會復原時，這項等候是 tooreduce hello 負載 hello 叢集上。 執行 hello 檢查包括：
  * 如果 hello 叢集健全狀況正常
  * 如果 hello 服務健全狀況正常
  * 如果 hello 目標複本集大小為止 hello 服務磁碟分割
  * 沒有 InBuild 複本存在
* **MaxConcurrentFaults**: hello 的並行會導致每個反覆項目中的錯誤數目上限。 hello hello 編號，更積極混亂且 hello hello 和容錯移轉狀態轉換組合 hello 叢集經歷也是更複雜的 hello。 

> [!NOTE]
> 無論高值*MaxConcurrentFaults*有，Chaos 可保證-hello 沒有的外部錯誤-沒有任何仲裁遺失或資料遺失。
>

* **EnableMoveReplicaFaults**： 啟用或停用造成 hello 主要或次要複本 toomove hello 錯誤。 預設會停用這些錯誤。
* **WaitTimeBetweenIterations**: hello 反覆項目之間的時間 toowait 數量。 也就是說，hello Chaos 會暫停，需要執行的錯誤和具有完成 hello 對應 hello hello 叢集健全狀況驗證一輪之後的時間量。 hello hello 值越高，較低的 hello 是 hello 平均錯誤資料隱碼的速率。
* **WaitTimeBetweenFaults**: hello 單一的反覆項目中的兩個連續錯誤之間的時間 toowait 數量。 hello hello 值越高，、 hello 的較低的 hello 並行 （或 hello 之間重疊） 錯誤。
* **ClusterHealthPolicy**： 叢集健全狀況原則是使用的 toovalidate hello Chaos 反覆項目之間的 hello 叢集健全狀況。 如果發生錯誤 hello 叢集健全狀況，或發生未預期的例外狀況錯誤執行期間，Chaos 會等待 30 分鐘，再 hello 下一個健全狀況檢查的某些時間 toorecuperate tooprovide hello 叢集。
* **內容**：(string, string) 類型索引鍵-值組的集合。 hello 對應可使用的 toorecord hello Chaos 執行資訊。 此類組合不能超過 100 個，且每個字串 (索引鍵或值) 最多為 4095 個字元長。 此對應是由 hello 入門 hello Chaos 執行 toooptionally 存放區 hello 內容的 hello 特定執行的相關設定。

## <a name="how-toorun-chaos"></a>如何 toorun Chaos

```csharp
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
using System.Fabric;

using System.Diagnostics;
using System.Fabric.Chaos.DataStructures;

class Program
{
    private class ChaosEventComparer : IEqualityComparer<ChaosEvent>
    {
        public bool Equals(ChaosEvent x, ChaosEvent y)
        {
            return x.TimeStampUtc.Equals(y.TimeStampUtc);
        }

        public int GetHashCode(ChaosEvent obj)
        {
            return obj.TimeStampUtc.GetHashCode();
        }
    }

    static void Main(string[] args)
    {
        var clusterConnectionString = "localhost:19000";
        using (var client = new FabricClient(clusterConnectionString))
        {
            var startTimeUtc = DateTime.UtcNow;
            var stabilizationTimeout = TimeSpan.FromSeconds(30.0);
            var timeToRun = TimeSpan.FromMinutes(60.0);
            var maxConcurrentFaults = 3;

            var parameters = new ChaosParameters(
                stabilizationTimeout,
                maxConcurrentFaults,
                true, /* EnableMoveReplicaFault */
                timeToRun);

            try
            {
                client.TestManager.StartChaosAsync(parameters).GetAwaiter().GetResult();
            }
            catch (FabricChaosAlreadyRunningException)
            {
                Console.WriteLine("An instance of Chaos is already running in hello cluster.");
            }

            var filter = new ChaosReportFilter(startTimeUtc, DateTime.MaxValue);

            var eventSet = new HashSet<ChaosEvent>(new ChaosEventComparer());

            while (true)
            {
                var report = client.TestManager.GetChaosReportAsync(filter).GetAwaiter().GetResult();

                foreach (var chaosEvent in report.History)
                {
                    if (eventSet.Add(chaosEvent))
                    {
                        Console.WriteLine(chaosEvent);
                    }
                }

                // When Chaos stops, a StoppedEvent is created.
                // If a StoppedEvent is found, exit hello loop.
                var lastEvent = report.History.LastOrDefault();

                if (lastEvent is StoppedEvent)
                {
                    break;
                }

                Task.Delay(TimeSpan.FromSeconds(1.0)).GetAwaiter().GetResult();
            }
        }
    }
}
```

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

$events = @{}
$now = [System.DateTime]::UtcNow

Start-ServiceFabricChaos -TimeToRunMinute $timeToRun -MaxConcurrentFaults $concurrentFaults -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec

while($true)
{
    $stopped = $false
    $report = Get-ServiceFabricChaosReport -StartTimeUtc $now -EndTimeUtc ([System.DateTime]::MaxValue)

    foreach ($e in $report.History) {

        if(-Not ($events.Contains($e.TimeStampUtc.Ticks)))
        {
            $events.Add($e.TimeStampUtc.Ticks, $e)
            if($e -is [System.Fabric.Chaos.DataStructures.ValidationFailedEvent])
            {
                Write-Host -BackgroundColor White -ForegroundColor Red $e
            }
            else
            {
                if($e -is [System.Fabric.Chaos.DataStructures.StoppedEvent])
                {
                    $stopped = $true
                }

                Write-Host $e
            }
        }
    }

    if($stopped -eq $true)
    {
        break
    }

    Start-Sleep -Seconds 1
}

Stop-ServiceFabricChaos
```
