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
# <a name="testability-scenarios"></a><span data-ttu-id="95269-103">Testability 案例</span><span class="sxs-lookup"><span data-stu-id="95269-103">Testability scenarios</span></span>
<span data-ttu-id="95269-104">雲端基礎結構之類的大型分散式系統本身並不可靠。</span><span class="sxs-lookup"><span data-stu-id="95269-104">Large distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="95269-105">Azure Service Fabric 提供開發人員 hello 能力 toowrite 服務 toorun 不可靠的基礎結構之上。</span><span class="sxs-lookup"><span data-stu-id="95269-105">Azure Service Fabric gives developers hello ability toowrite services toorun on top of unreliable infrastructures.</span></span> <span data-ttu-id="95269-106">在順序 toowrite 高品質的服務，開發人員需要 toobe 無法 tooinduce 這類不可靠的基礎結構 tootest hello 的穩定性其服務。</span><span class="sxs-lookup"><span data-stu-id="95269-106">In order toowrite high-quality services, developers need toobe able tooinduce such unreliable infrastructure tootest hello stability of their services.</span></span>

<span data-ttu-id="95269-107">hello 錯誤分析服務讓開發人員 hello 能力 tooinduce 錯誤動作 tootest 服務中的失敗 hello 存在。</span><span class="sxs-lookup"><span data-stu-id="95269-107">hello Fault Analysis Service gives developers hello ability tooinduce fault actions tootest services in hello presence of failures.</span></span> <span data-ttu-id="95269-108">但鎖定式模擬錯誤就僅只於此了。</span><span class="sxs-lookup"><span data-stu-id="95269-108">However, targeted simulated faults will get you only so far.</span></span> <span data-ttu-id="95269-109">此外，測試 tootake hello hello 測試案例用於 Service Fabric: chaos 測試和容錯移轉測試。</span><span class="sxs-lookup"><span data-stu-id="95269-109">tootake hello testing further, you can use hello test scenarios in Service Fabric: a chaos test and a failover test.</span></span> <span data-ttu-id="95269-110">這些案例，以模擬連續交錯的錯誤，依正常程序並不正常，整個 hello 叢集一段很長的時間。</span><span class="sxs-lookup"><span data-stu-id="95269-110">These scenarios simulate continuous interleaved faults, both graceful and ungraceful, throughout hello cluster over extended periods of time.</span></span> <span data-ttu-id="95269-111">測試設定之後 hello 速率與類型的錯誤，則可以透過 C# Api 或 PowerShell，toogenerate hello 叢集中的錯誤和您的服務啟動。</span><span class="sxs-lookup"><span data-stu-id="95269-111">Once a test is configured with hello rate and kind of faults, it can be started through either C# APIs or PowerShell, toogenerate faults in hello cluster and your service.</span></span>

> [!WARNING]
> <span data-ttu-id="95269-112">ChaosTestScenario 已被更有彈性、以服務為基礎的混亂取代。</span><span class="sxs-lookup"><span data-stu-id="95269-112">ChaosTestScenario is being replaced by a more resilient, service-based Chaos.</span></span> <span data-ttu-id="95269-113">Toohello 新發行項，請參閱[控制 Chaos](service-fabric-controlled-chaos.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="95269-113">Please refer toohello new article [Controlled Chaos](service-fabric-controlled-chaos.md) for more details.</span></span>
> 
> 

## <a name="chaos-test"></a><span data-ttu-id="95269-114">混亂測試</span><span class="sxs-lookup"><span data-stu-id="95269-114">Chaos test</span></span>
<span data-ttu-id="95269-115">hello chaos 案例 hello 整個 Service Fabric 叢集中，會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="95269-115">hello chaos scenario generates faults across hello entire Service Fabric cluster.</span></span> <span data-ttu-id="95269-116">hello 案例壓縮通常月或年 tooa 中看到幾個小時的錯誤。</span><span class="sxs-lookup"><span data-stu-id="95269-116">hello scenario compresses faults generally seen in months or years tooa few hours.</span></span> <span data-ttu-id="95269-117">hello 組合的交錯錯誤與 hello 高錯誤的速率尋找極端案例，否則會遺失。</span><span class="sxs-lookup"><span data-stu-id="95269-117">hello combination of interleaved faults with hello high fault rate finds corner cases that are otherwise missed.</span></span> <span data-ttu-id="95269-118">這將致使 tooa 顯著改進的 hello 服務的 hello 程式碼品質。</span><span class="sxs-lookup"><span data-stu-id="95269-118">This leads tooa significant improvement in hello code quality of hello service.</span></span>

### <a name="faults-simulated-in-hello-chaos-test"></a><span data-ttu-id="95269-119">Hello chaos 測試中模擬的錯誤</span><span class="sxs-lookup"><span data-stu-id="95269-119">Faults simulated in hello chaos test</span></span>
* <span data-ttu-id="95269-120">重新啟動節點</span><span class="sxs-lookup"><span data-stu-id="95269-120">Restart a node</span></span>
* <span data-ttu-id="95269-121">重新啟動已部署的程式碼封裝</span><span class="sxs-lookup"><span data-stu-id="95269-121">Restart a deployed code package</span></span>
* <span data-ttu-id="95269-122">移除複本</span><span class="sxs-lookup"><span data-stu-id="95269-122">Remove a replica</span></span>
* <span data-ttu-id="95269-123">重新啟動複本</span><span class="sxs-lookup"><span data-stu-id="95269-123">Restart a replica</span></span>
* <span data-ttu-id="95269-124">移動主要複本 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="95269-124">Move a primary replica (optional)</span></span>
* <span data-ttu-id="95269-125">移動次要複本 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="95269-125">Move a secondary replica (optional)</span></span>

<span data-ttu-id="95269-126">hello chaos 測試執行錯誤的多個反覆項目，並 hello 的叢集驗證指定的時間。</span><span class="sxs-lookup"><span data-stu-id="95269-126">hello chaos test runs multiple iterations of faults and cluster validations for hello specified period of time.</span></span> <span data-ttu-id="95269-127">也可設定 hello hello 叢集 toostabilize 和驗證 toosucceed 所花費的時間。</span><span class="sxs-lookup"><span data-stu-id="95269-127">hello time spent for hello cluster toostabilize and for validation toosucceed is also configurable.</span></span> <span data-ttu-id="95269-128">當您叫用單一叢集驗證失敗時，就會失敗 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="95269-128">hello scenario fails when you hit a single failure in cluster validation.</span></span>

<span data-ttu-id="95269-129">例如，請考慮測試設定 toorun 一小時，最大值的三個並行錯誤。</span><span class="sxs-lookup"><span data-stu-id="95269-129">For example, consider a test set toorun for one hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="95269-130">hello 測試將會產生三個錯誤，並驗證 hello 叢集健全狀況。</span><span class="sxs-lookup"><span data-stu-id="95269-130">hello test will induce three faults, and then validate hello cluster health.</span></span> <span data-ttu-id="95269-131">hello 測試會逐一 hello 上一個步驟，直到 hello 叢集會變為狀況不良或一小時已通過檢查。</span><span class="sxs-lookup"><span data-stu-id="95269-131">hello test will iterate through hello previous step till hello cluster becomes unhealthy or one hour passes.</span></span> <span data-ttu-id="95269-132">如果 hello 叢集會變成狀況不良任何反覆項目，也就是它不會不穩定的設定時間內，hello 測試將會失敗並發生例外狀況。</span><span class="sxs-lookup"><span data-stu-id="95269-132">If hello cluster becomes unhealthy in any iteration, i.e. it does not stabilize within a configured time, hello test will fail with an exception.</span></span> <span data-ttu-id="95269-133">此例外狀況表示發生了錯誤，且需要進一步調查。</span><span class="sxs-lookup"><span data-stu-id="95269-133">This exception indicates that something has gone wrong and needs further investigation.</span></span>

<span data-ttu-id="95269-134">其目前的格式，hello chaos 測試中的 hello 錯誤產生引擎會產生只有安全的錯誤。</span><span class="sxs-lookup"><span data-stu-id="95269-134">In its current form, hello fault generation engine in hello chaos test induces only safe faults.</span></span> <span data-ttu-id="95269-135">這表示，在外部錯誤 hello 不存在，仲裁或資料遺失永遠不會發生。</span><span class="sxs-lookup"><span data-stu-id="95269-135">This means that in hello absence of external faults, a quorum or data loss will never occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="95269-136">重要的組態選項</span><span class="sxs-lookup"><span data-stu-id="95269-136">Important configuration options</span></span>
* <span data-ttu-id="95269-137">**TimeToRun**： 總時間成功完成前，將執行該 hello 測試。</span><span class="sxs-lookup"><span data-stu-id="95269-137">**TimeToRun**: Total time that hello test will run before finishing with success.</span></span> <span data-ttu-id="95269-138">hello 測試可以稍早完成，就不需驗證失敗。</span><span class="sxs-lookup"><span data-stu-id="95269-138">hello test can finish earlier in lieu of a validation failure.</span></span>
* <span data-ttu-id="95269-139">**MaxClusterStabilizationTimeout**: hello 叢集 toobecome 狀況良好失敗 hello 測試前的時間 toowait 的數量上限。</span><span class="sxs-lookup"><span data-stu-id="95269-139">**MaxClusterStabilizationTimeout**: Maximum amount of time toowait for hello cluster toobecome healthy before failing hello test.</span></span> <span data-ttu-id="95269-140">hello 執行檢查叢集健全狀況是否為 [確定]、 服務健全狀況正常、 hello 目標複本集大小針對達成 hello 服務資料分割，而且沒有任何 InBuild 複本存在。</span><span class="sxs-lookup"><span data-stu-id="95269-140">hello checks performed are whether cluster health is OK, service health is OK, hello target replica set size is achieved for hello service partition, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="95269-141">**MaxConcurrentFaults**：每個反覆運算中引發的最大並行錯誤數。</span><span class="sxs-lookup"><span data-stu-id="95269-141">**MaxConcurrentFaults**: Maximum number of concurrent faults induced in each iteration.</span></span> <span data-ttu-id="95269-142">hello hello 編號，hello 更積極的 hello 測試，因此導致轉換組合和更複雜的容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="95269-142">hello higher hello number, hello more aggressive hello test, hence resulting in more complex failovers and transition combinations.</span></span> <span data-ttu-id="95269-143">hello 測試可保證沒有外部錯誤的情況下將不會有仲裁或資料遺失，不論這項設定很高。</span><span class="sxs-lookup"><span data-stu-id="95269-143">hello test guarantees that in absence of external faults there will not be a quorum or data loss, irrespective of how high this configuration is.</span></span>
* <span data-ttu-id="95269-144">**EnableMoveReplicaFaults**： 啟用或停用 hello 錯誤造成的 hello hello 移動主要或次要複本。</span><span class="sxs-lookup"><span data-stu-id="95269-144">**EnableMoveReplicaFaults**: Enables or disables hello faults that are causing hello move of hello primary or secondary replicas.</span></span> <span data-ttu-id="95269-145">預設會停用這些錯誤。</span><span class="sxs-lookup"><span data-stu-id="95269-145">These faults are disabled by default.</span></span>
* <span data-ttu-id="95269-146">**WaitTimeBetweenIterations**： 錯誤和對應的驗證的重試回合之後，也就是反覆項目之間的時間 toowait 數量。</span><span class="sxs-lookup"><span data-stu-id="95269-146">**WaitTimeBetweenIterations**: Amount of time toowait between iterations, i.e. after a round of faults and corresponding validation.</span></span>

### <a name="how-toorun-hello-chaos-test"></a><span data-ttu-id="95269-147">如何測試 toorun hello chaos</span><span class="sxs-lookup"><span data-stu-id="95269-147">How toorun hello chaos test</span></span>
<span data-ttu-id="95269-148">C# 範例</span><span class="sxs-lookup"><span data-stu-id="95269-148">C# sample</span></span>

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

<span data-ttu-id="95269-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="95269-149">PowerShell</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```


## <a name="failover-test"></a><span data-ttu-id="95269-150">容錯移轉測試</span><span class="sxs-lookup"><span data-stu-id="95269-150">Failover test</span></span>
<span data-ttu-id="95269-151">hello 容錯移轉的測試案例是以特定的服務資料分割為目標的 hello chaos 測試案例的版本。</span><span class="sxs-lookup"><span data-stu-id="95269-151">hello failover test scenario is a version of hello chaos test scenario that targets a specific service partition.</span></span> <span data-ttu-id="95269-152">它會測試特定服務磁碟分割上的 hello 生效的容錯移轉但保留 hello 其他服務不會受到影響。</span><span class="sxs-lookup"><span data-stu-id="95269-152">It tests hello effect of failover on a specific service partition while leaving hello other services unaffected.</span></span> <span data-ttu-id="95269-153">一旦設定之後 hello 目標資料分割資訊與其他參數，它會以使用 C# Api 或 PowerShell toogenerate 錯誤的服務資料分割的用戶端工具執行。</span><span class="sxs-lookup"><span data-stu-id="95269-153">Once it's configured with hello target partition information and other parameters, it runs as a client-side tool that uses either C# APIs or PowerShell toogenerate faults for a service partition.</span></span> <span data-ttu-id="95269-154">hello 案例逐一一連串的模擬的錯誤和服務驗證您的商務邏輯上 hello 端 tooprovide 工作負載執行時。</span><span class="sxs-lookup"><span data-stu-id="95269-154">hello scenario iterates through a sequence of simulated faults and service validation while your business logic runs on hello side tooprovide a workload.</span></span> <span data-ttu-id="95269-155">服務驗證中若有失敗，表示有需要進一步調查的問題。</span><span class="sxs-lookup"><span data-stu-id="95269-155">A failure in service validation indicates an issue that needs further investigation.</span></span>

### <a name="faults-simulated-in-hello-failover-test"></a><span data-ttu-id="95269-156">Hello 容錯移轉的測試中模擬的錯誤</span><span class="sxs-lookup"><span data-stu-id="95269-156">Faults simulated in hello failover test</span></span>
* <span data-ttu-id="95269-157">重新啟動裝載 hello 資料分割的已部署的程式碼封裝</span><span class="sxs-lookup"><span data-stu-id="95269-157">Restart a deployed code package where hello partition is hosted</span></span>
* <span data-ttu-id="95269-158">移除主要/次要複本或無狀態執行個體</span><span class="sxs-lookup"><span data-stu-id="95269-158">Remove a primary/secondary replica or stateless instance</span></span>
* <span data-ttu-id="95269-159">重新啟動主要的次要複本 (如果是保存的服務)</span><span class="sxs-lookup"><span data-stu-id="95269-159">Restart a primary secondary replica (if a persisted service)</span></span>
* <span data-ttu-id="95269-160">移動主要複本</span><span class="sxs-lookup"><span data-stu-id="95269-160">Move a primary replica</span></span>
* <span data-ttu-id="95269-161">移動次要複本</span><span class="sxs-lookup"><span data-stu-id="95269-161">Move a secondary replica</span></span>
* <span data-ttu-id="95269-162">重新啟動 hello 磁碟分割</span><span class="sxs-lookup"><span data-stu-id="95269-162">Restart hello partition</span></span>

<span data-ttu-id="95269-163">hello 容錯移轉測試，產生所選的錯誤，然後執行驗證 hello 服務 tooensure 上其穩定性。</span><span class="sxs-lookup"><span data-stu-id="95269-163">hello failover test induces a chosen fault and then runs validation on hello service tooensure its stability.</span></span> <span data-ttu-id="95269-164">只有其中一個錯誤的時間，相對於 toopossible 在 hello chaos 測試中的多個錯誤，有可能引起 hello 容錯移轉測試。</span><span class="sxs-lookup"><span data-stu-id="95269-164">hello failover test induces only one fault at a time, as opposed toopossible multiple faults in hello chaos test.</span></span> <span data-ttu-id="95269-165">如果 hello 服務資料分割之後每個錯誤不穩定 hello 設定逾時時間內 hello 測試將會失敗。</span><span class="sxs-lookup"><span data-stu-id="95269-165">If hello service partition does not stabilize within hello configured timeout after each fault, hello test fails.</span></span> <span data-ttu-id="95269-166">hello 測試產生安全的錯誤。</span><span class="sxs-lookup"><span data-stu-id="95269-166">hello test induces only safe faults.</span></span> <span data-ttu-id="95269-167">這表示因為沒有外部錯誤，所以不會發生仲裁或資料遺失。</span><span class="sxs-lookup"><span data-stu-id="95269-167">This means that in absence of external failures, a quorum or data loss will not occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="95269-168">重要的組態選項</span><span class="sxs-lookup"><span data-stu-id="95269-168">Important configuration options</span></span>
* <span data-ttu-id="95269-169">**PartitionSelector**： 指定所需目標的 toobe hello 資料分割的選取器物件。</span><span class="sxs-lookup"><span data-stu-id="95269-169">**PartitionSelector**: Selector object that specifies hello partition that needs toobe targeted.</span></span>
* <span data-ttu-id="95269-170">**TimeToRun**: hello 測試將執行的總時間之前完成。</span><span class="sxs-lookup"><span data-stu-id="95269-170">**TimeToRun**: Total time that hello test will run before finishing.</span></span>
* <span data-ttu-id="95269-171">**MaxServiceStabilizationTimeout**: hello 叢集 toobecome 狀況良好失敗 hello 測試前的時間 toowait 的數量上限。</span><span class="sxs-lookup"><span data-stu-id="95269-171">**MaxServiceStabilizationTimeout**: Maximum amount of time toowait for hello cluster toobecome healthy before failing hello test.</span></span> <span data-ttu-id="95269-172">hello 執行檢查服務健全狀況是否為 [確定]，hello 目標複本集大小為止的所有資料分割，而且沒有任何 InBuild 複本存在。</span><span class="sxs-lookup"><span data-stu-id="95269-172">hello checks performed are whether service health is OK, hello target replica set size is achieved for all partitions, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="95269-173">**WaitTimeBetweenFaults**： 每個錯誤和驗證週期之間的時間 toowait 數量。</span><span class="sxs-lookup"><span data-stu-id="95269-173">**WaitTimeBetweenFaults**: Amount of time toowait between every fault and validation cycle.</span></span>

### <a name="how-toorun-hello-failover-test"></a><span data-ttu-id="95269-174">如何測試 toorun hello 容錯移轉</span><span class="sxs-lookup"><span data-stu-id="95269-174">How toorun hello failover test</span></span>
<span data-ttu-id="95269-175">**C#**</span><span class="sxs-lookup"><span data-stu-id="95269-175">**C#**</span></span>

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


<span data-ttu-id="95269-176">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="95269-176">**PowerShell**</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/SampleApp/SampleService"

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindSingleton
```
