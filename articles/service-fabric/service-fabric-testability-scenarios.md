---
title: "針對 Azure 微服務建立混亂與容錯移轉測試 | Microsoft Docs"
description: "使用 Service Fabric 混亂測試和容錯移轉測試案例來引發錯誤並確認服務的可靠性。"
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
ms.openlocfilehash: d06026c750e01ad5825338a78d9af331265f434a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="testability-scenarios"></a><span data-ttu-id="3ef17-103">Testability 案例</span><span class="sxs-lookup"><span data-stu-id="3ef17-103">Testability scenarios</span></span>
<span data-ttu-id="3ef17-104">雲端基礎結構之類的大型分散式系統本身並不可靠。</span><span class="sxs-lookup"><span data-stu-id="3ef17-104">Large distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="3ef17-105">Azure Service Fabric 讓開發人員能夠撰寫可在不可靠的基礎結構上執行的服務。</span><span class="sxs-lookup"><span data-stu-id="3ef17-105">Azure Service Fabric gives developers the ability to write services to run on top of unreliable infrastructures.</span></span> <span data-ttu-id="3ef17-106">為了撰寫高品質的服務，開發人員必須能夠產生這類不可靠的基礎結構，才能測試其服務的穩定性。</span><span class="sxs-lookup"><span data-stu-id="3ef17-106">In order to write high-quality services, developers need to be able to induce such unreliable infrastructure to test the stability of their services.</span></span>

<span data-ttu-id="3ef17-107">「錯誤分析服務」讓開發人員可以引發錯誤動作，藉此以失敗情況測試服務。</span><span class="sxs-lookup"><span data-stu-id="3ef17-107">The Fault Analysis Service gives developers the ability to induce fault actions to test services in the presence of failures.</span></span> <span data-ttu-id="3ef17-108">但鎖定式模擬錯誤就僅只於此了。</span><span class="sxs-lookup"><span data-stu-id="3ef17-108">However, targeted simulated faults will get you only so far.</span></span> <span data-ttu-id="3ef17-109">若要進一步測試，您可以在 Service Fabric 中使用測試案例：混亂測試和容錯移轉測試。</span><span class="sxs-lookup"><span data-stu-id="3ef17-109">To take the testing further, you can use the test scenarios in Service Fabric: a chaos test and a failover test.</span></span> <span data-ttu-id="3ef17-110">這些案例會以很長的時間在整個叢集上模擬連續的交錯錯誤，包括非失誤性和失誤性錯誤。</span><span class="sxs-lookup"><span data-stu-id="3ef17-110">These scenarios simulate continuous interleaved faults, both graceful and ungraceful, throughout the cluster over extended periods of time.</span></span> <span data-ttu-id="3ef17-111">一旦設定測試的比率和錯誤類型後，即可開始透過 C# API 或 PowerShell 在叢集和您的服務中產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="3ef17-111">Once a test is configured with the rate and kind of faults, it can be started through either C# APIs or PowerShell, to generate faults in the cluster and your service.</span></span>

> [!WARNING]
> <span data-ttu-id="3ef17-112">ChaosTestScenario 已被更有彈性、以服務為基礎的混亂取代。</span><span class="sxs-lookup"><span data-stu-id="3ef17-112">ChaosTestScenario is being replaced by a more resilient, service-based Chaos.</span></span> <span data-ttu-id="3ef17-113">請參閱 [控制的混亂](service-fabric-controlled-chaos.md) 了解詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="3ef17-113">Please refer to the new article [Controlled Chaos](service-fabric-controlled-chaos.md) for more details.</span></span>
> 
> 

## <a name="chaos-test"></a><span data-ttu-id="3ef17-114">混亂測試</span><span class="sxs-lookup"><span data-stu-id="3ef17-114">Chaos test</span></span>
<span data-ttu-id="3ef17-115">混亂案例會在整個 Service Fabric 叢集中產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="3ef17-115">The chaos scenario generates faults across the entire Service Fabric cluster.</span></span> <span data-ttu-id="3ef17-116">此案例會壓縮錯誤，通常是將幾個月或幾年壓縮到幾小時。</span><span class="sxs-lookup"><span data-stu-id="3ef17-116">The scenario compresses faults generally seen in months or years to a few hours.</span></span> <span data-ttu-id="3ef17-117">交錯錯誤和高錯誤率的組合，可以找到會在其他情形下被遺漏的極端狀況。</span><span class="sxs-lookup"><span data-stu-id="3ef17-117">The combination of interleaved faults with the high fault rate finds corner cases that are otherwise missed.</span></span> <span data-ttu-id="3ef17-118">這會使服務的程式碼品質大幅提升。</span><span class="sxs-lookup"><span data-stu-id="3ef17-118">This leads to a significant improvement in the code quality of the service.</span></span>

### <a name="faults-simulated-in-the-chaos-test"></a><span data-ttu-id="3ef17-119">混亂測試中模擬的錯誤</span><span class="sxs-lookup"><span data-stu-id="3ef17-119">Faults simulated in the chaos test</span></span>
* <span data-ttu-id="3ef17-120">重新啟動節點</span><span class="sxs-lookup"><span data-stu-id="3ef17-120">Restart a node</span></span>
* <span data-ttu-id="3ef17-121">重新啟動已部署的程式碼封裝</span><span class="sxs-lookup"><span data-stu-id="3ef17-121">Restart a deployed code package</span></span>
* <span data-ttu-id="3ef17-122">移除複本</span><span class="sxs-lookup"><span data-stu-id="3ef17-122">Remove a replica</span></span>
* <span data-ttu-id="3ef17-123">重新啟動複本</span><span class="sxs-lookup"><span data-stu-id="3ef17-123">Restart a replica</span></span>
* <span data-ttu-id="3ef17-124">移動主要複本 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="3ef17-124">Move a primary replica (optional)</span></span>
* <span data-ttu-id="3ef17-125">移動次要複本 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="3ef17-125">Move a secondary replica (optional)</span></span>

<span data-ttu-id="3ef17-126">混亂測試會在指定的一段時間中，多次執行反覆的錯誤和叢集驗證。</span><span class="sxs-lookup"><span data-stu-id="3ef17-126">The chaos test runs multiple iterations of faults and cluster validations for the specified period of time.</span></span> <span data-ttu-id="3ef17-127">讓叢集穩定和驗證成功的所需時間也是可設定的。</span><span class="sxs-lookup"><span data-stu-id="3ef17-127">The time spent for the cluster to stabilize and for validation to succeed is also configurable.</span></span> <span data-ttu-id="3ef17-128">當您在叢集驗證中發生一次失敗，案例就會失敗。</span><span class="sxs-lookup"><span data-stu-id="3ef17-128">The scenario fails when you hit a single failure in cluster validation.</span></span>

<span data-ttu-id="3ef17-129">例如，請考慮將測試設為執行 1 小時，且最多 3 個並行錯誤。</span><span class="sxs-lookup"><span data-stu-id="3ef17-129">For example, consider a test set to run for one hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="3ef17-130">測試會引發 3 個錯誤，然後驗證叢集的健康情況。</span><span class="sxs-lookup"><span data-stu-id="3ef17-130">The test will induce three faults, and then validate the cluster health.</span></span> <span data-ttu-id="3ef17-131">上一個步驟的測試會反覆進行，直到叢集變成狀況不佳，或經過了 1 小時為止。</span><span class="sxs-lookup"><span data-stu-id="3ef17-131">The test will iterate through the previous step till the cluster becomes unhealthy or one hour passes.</span></span> <span data-ttu-id="3ef17-132">如果任何反覆運算中的叢集變成狀況不佳，也就是在設定的時間內不穩定，則測試就會失敗並產生例外狀況。</span><span class="sxs-lookup"><span data-stu-id="3ef17-132">If the cluster becomes unhealthy in any iteration, i.e. it does not stabilize within a configured time, the test will fail with an exception.</span></span> <span data-ttu-id="3ef17-133">此例外狀況表示發生了錯誤，且需要進一步調查。</span><span class="sxs-lookup"><span data-stu-id="3ef17-133">This exception indicates that something has gone wrong and needs further investigation.</span></span>

<span data-ttu-id="3ef17-134">以目前的形式來看，混亂測試的錯誤產生引擎只會引發安全的錯誤。</span><span class="sxs-lookup"><span data-stu-id="3ef17-134">In its current form, the fault generation engine in the chaos test induces only safe faults.</span></span> <span data-ttu-id="3ef17-135">這表示因為沒有外部錯誤，所以永遠不會發生仲裁或資料遺失。</span><span class="sxs-lookup"><span data-stu-id="3ef17-135">This means that in the absence of external faults, a quorum or data loss will never occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="3ef17-136">重要的組態選項</span><span class="sxs-lookup"><span data-stu-id="3ef17-136">Important configuration options</span></span>
* <span data-ttu-id="3ef17-137">**TimeToRun**：測試在成功完成前的總執行時間。</span><span class="sxs-lookup"><span data-stu-id="3ef17-137">**TimeToRun**: Total time that the test will run before finishing with success.</span></span> <span data-ttu-id="3ef17-138">測試可以提前完成，而不必等驗證失敗。</span><span class="sxs-lookup"><span data-stu-id="3ef17-138">The test can finish earlier in lieu of a validation failure.</span></span>
* <span data-ttu-id="3ef17-139">**MaxClusterStabilizationTimeout**：測試失敗前，等候叢集變成狀況良好的時間上限。</span><span class="sxs-lookup"><span data-stu-id="3ef17-139">**MaxClusterStabilizationTimeout**: Maximum amount of time to wait for the cluster to become healthy before failing the test.</span></span> <span data-ttu-id="3ef17-140">執行的檢查會查看叢集健康情況或服務健康情況是否正常、服務分割區是否達到目標複本的設定大小，以及是否沒有 InBuild 複本。</span><span class="sxs-lookup"><span data-stu-id="3ef17-140">The checks performed are whether cluster health is OK, service health is OK, the target replica set size is achieved for the service partition, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="3ef17-141">**MaxConcurrentFaults**：每個反覆運算中引發的最大並行錯誤數。</span><span class="sxs-lookup"><span data-stu-id="3ef17-141">**MaxConcurrentFaults**: Maximum number of concurrent faults induced in each iteration.</span></span> <span data-ttu-id="3ef17-142">數量越大，測試會越積極，因此導致更複雜的容錯移轉和轉換組合。</span><span class="sxs-lookup"><span data-stu-id="3ef17-142">The higher the number, the more aggressive the test, hence resulting in more complex failovers and transition combinations.</span></span> <span data-ttu-id="3ef17-143">無論此組態的數量多高，測試都能保證缺少外部錯誤時，就不會發生仲裁或資料遺失。</span><span class="sxs-lookup"><span data-stu-id="3ef17-143">The test guarantees that in absence of external faults there will not be a quorum or data loss, irrespective of how high this configuration is.</span></span>
* <span data-ttu-id="3ef17-144">**EnableMoveReplicaFaults**：啟用或停用造成主要或次要複本移動的錯誤。</span><span class="sxs-lookup"><span data-stu-id="3ef17-144">**EnableMoveReplicaFaults**: Enables or disables the faults that are causing the move of the primary or secondary replicas.</span></span> <span data-ttu-id="3ef17-145">預設會停用這些錯誤。</span><span class="sxs-lookup"><span data-stu-id="3ef17-145">These faults are disabled by default.</span></span>
* <span data-ttu-id="3ef17-146">**WaitTimeBetweenIterations**：反覆運算之間的等待時間長度，也就是在一輪的錯誤與對應的驗證後等待下一輪。</span><span class="sxs-lookup"><span data-stu-id="3ef17-146">**WaitTimeBetweenIterations**: Amount of time to wait between iterations, i.e. after a round of faults and corresponding validation.</span></span>

### <a name="how-to-run-the-chaos-test"></a><span data-ttu-id="3ef17-147">如何執行混亂測試</span><span class="sxs-lookup"><span data-stu-id="3ef17-147">How to run the chaos test</span></span>
<span data-ttu-id="3ef17-148">C# 範例</span><span class="sxs-lookup"><span data-stu-id="3ef17-148">C# sample</span></span>

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

        // The chaos test scenario should run at least 60 minutes or until it fails.
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

        // Create the scenario class and execute it asynchronously.
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

<span data-ttu-id="3ef17-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ef17-149">PowerShell</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```


## <a name="failover-test"></a><span data-ttu-id="3ef17-150">容錯移轉測試</span><span class="sxs-lookup"><span data-stu-id="3ef17-150">Failover test</span></span>
<span data-ttu-id="3ef17-151">容錯移轉測試案例是以特定服務分割區為目標的混亂測試案例版本。</span><span class="sxs-lookup"><span data-stu-id="3ef17-151">The failover test scenario is a version of the chaos test scenario that targets a specific service partition.</span></span> <span data-ttu-id="3ef17-152">此測試會測試容錯移轉對特定服務分割區的影響，且其他服務不會受到影響。</span><span class="sxs-lookup"><span data-stu-id="3ef17-152">It tests the effect of failover on a specific service partition while leaving the other services unaffected.</span></span> <span data-ttu-id="3ef17-153">設定了目標分割區資訊和其他參數後，此測試會以用戶端工具的形式執行，並使用 C# API 或 Powershell 來產生服務分割區的錯誤。</span><span class="sxs-lookup"><span data-stu-id="3ef17-153">Once it's configured with the target partition information and other parameters, it runs as a client-side tool that uses either C# APIs or PowerShell to generate faults for a service partition.</span></span> <span data-ttu-id="3ef17-154">案例會在您的商務邏輯執行時，反覆進行一連串模擬的錯誤及服務驗證，同時提供工作負載。</span><span class="sxs-lookup"><span data-stu-id="3ef17-154">The scenario iterates through a sequence of simulated faults and service validation while your business logic runs on the side to provide a workload.</span></span> <span data-ttu-id="3ef17-155">服務驗證中若有失敗，表示有需要進一步調查的問題。</span><span class="sxs-lookup"><span data-stu-id="3ef17-155">A failure in service validation indicates an issue that needs further investigation.</span></span>

### <a name="faults-simulated-in-the-failover-test"></a><span data-ttu-id="3ef17-156">在容錯移轉測試中模擬的錯誤</span><span class="sxs-lookup"><span data-stu-id="3ef17-156">Faults simulated in the failover test</span></span>
* <span data-ttu-id="3ef17-157">重新啟動分割區所在的已部署程式碼封裝</span><span class="sxs-lookup"><span data-stu-id="3ef17-157">Restart a deployed code package where the partition is hosted</span></span>
* <span data-ttu-id="3ef17-158">移除主要/次要複本或無狀態執行個體</span><span class="sxs-lookup"><span data-stu-id="3ef17-158">Remove a primary/secondary replica or stateless instance</span></span>
* <span data-ttu-id="3ef17-159">重新啟動主要的次要複本 (如果是保存的服務)</span><span class="sxs-lookup"><span data-stu-id="3ef17-159">Restart a primary secondary replica (if a persisted service)</span></span>
* <span data-ttu-id="3ef17-160">移動主要複本</span><span class="sxs-lookup"><span data-stu-id="3ef17-160">Move a primary replica</span></span>
* <span data-ttu-id="3ef17-161">移動次要複本</span><span class="sxs-lookup"><span data-stu-id="3ef17-161">Move a secondary replica</span></span>
* <span data-ttu-id="3ef17-162">重新啟動分割區</span><span class="sxs-lookup"><span data-stu-id="3ef17-162">Restart the partition</span></span>

<span data-ttu-id="3ef17-163">容錯移轉測試會引發選定的錯誤，然後在服務上執行驗證，以確保其穩定性。</span><span class="sxs-lookup"><span data-stu-id="3ef17-163">The failover test induces a chosen fault and then runs validation on the service to ensure its stability.</span></span> <span data-ttu-id="3ef17-164">容錯移轉測試一次只會引發一個錯誤，不像混亂測試中可能會有多個錯誤。</span><span class="sxs-lookup"><span data-stu-id="3ef17-164">The failover test induces only one fault at a time, as opposed to possible multiple faults in the chaos test.</span></span> <span data-ttu-id="3ef17-165">如果在每個錯誤後，服務分割區沒有在設定的逾時內變穩定，測試會失敗。</span><span class="sxs-lookup"><span data-stu-id="3ef17-165">If the service partition does not stabilize within the configured timeout after each fault, the test fails.</span></span> <span data-ttu-id="3ef17-166">此測試只會引發安全的錯誤。</span><span class="sxs-lookup"><span data-stu-id="3ef17-166">The test induces only safe faults.</span></span> <span data-ttu-id="3ef17-167">這表示因為沒有外部錯誤，所以不會發生仲裁或資料遺失。</span><span class="sxs-lookup"><span data-stu-id="3ef17-167">This means that in absence of external failures, a quorum or data loss will not occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="3ef17-168">重要的組態選項</span><span class="sxs-lookup"><span data-stu-id="3ef17-168">Important configuration options</span></span>
* <span data-ttu-id="3ef17-169">**PartitionSelector**：指定需要做為目標分割區的選取器物件。</span><span class="sxs-lookup"><span data-stu-id="3ef17-169">**PartitionSelector**: Selector object that specifies the partition that needs to be targeted.</span></span>
* <span data-ttu-id="3ef17-170">**TimeToRun**：測試在完成前的總執行時間。</span><span class="sxs-lookup"><span data-stu-id="3ef17-170">**TimeToRun**: Total time that the test will run before finishing.</span></span>
* <span data-ttu-id="3ef17-171">**MaxServiceStabilizationTimeout**：測試失敗前，等候叢集變成狀況良好的時間上限。</span><span class="sxs-lookup"><span data-stu-id="3ef17-171">**MaxServiceStabilizationTimeout**: Maximum amount of time to wait for the cluster to become healthy before failing the test.</span></span> <span data-ttu-id="3ef17-172">執行的檢查會查看服務健康情況是否正常，或是所有分割區是否達到目標複本的設定大小，以及是否沒有 InBuild 複本。</span><span class="sxs-lookup"><span data-stu-id="3ef17-172">The checks performed are whether service health is OK, the target replica set size is achieved for all partitions, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="3ef17-173">**WaitTimeBetweenFaults**：每個錯誤和驗證的循環之間要等候的時間長度。</span><span class="sxs-lookup"><span data-stu-id="3ef17-173">**WaitTimeBetweenFaults**: Amount of time to wait between every fault and validation cycle.</span></span>

### <a name="how-to-run-the-failover-test"></a><span data-ttu-id="3ef17-174">如何執行容錯移轉測試</span><span class="sxs-lookup"><span data-stu-id="3ef17-174">How to run the failover test</span></span>
<span data-ttu-id="3ef17-175">**C#**</span><span class="sxs-lookup"><span data-stu-id="3ef17-175">**C#**</span></span>

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

        // The chaos test scenario should run at least 60 minutes or until it fails.
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

        // Create the scenario class and execute it asynchronously.
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


<span data-ttu-id="3ef17-176">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="3ef17-176">**PowerShell**</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/SampleApp/SampleService"

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindSingleton
```
