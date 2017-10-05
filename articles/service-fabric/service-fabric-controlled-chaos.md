---
title: "在 Service Fabric 叢集中引發混亂 | Microsoft Docs"
description: "使用錯誤注射與叢集分析服務的 API 來管理叢集中的混亂。"
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
ms.openlocfilehash: 3b3b93bc9ec5ecdcfc289e5b62e84de6aa4172ed
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="induce-controlled-chaos-in-service-fabric-clusters"></a><span data-ttu-id="04702-103">在 Service Fabric 叢集中引發受控制的混亂</span><span class="sxs-lookup"><span data-stu-id="04702-103">Induce controlled Chaos in Service Fabric clusters</span></span>
<span data-ttu-id="04702-104">雲端基礎結構之類的大型分散式系統本身並不可靠。</span><span class="sxs-lookup"><span data-stu-id="04702-104">Large-scale distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="04702-105">Azure Service Fabric 可讓開發人員在不可靠的基礎結構之上撰寫可靠的分散式服務。</span><span class="sxs-lookup"><span data-stu-id="04702-105">Azure Service Fabric enables developers to write reliable distributed services on top of an unreliable infrastructure.</span></span> <span data-ttu-id="04702-106">若要在不可靠的基礎結構之上撰寫健全的分散式服務，開發人員需要能夠測試其服務的穩定性，同時不可靠的基礎結構會因錯誤而經歷複雜的狀態轉換。</span><span class="sxs-lookup"><span data-stu-id="04702-106">To write robust distributed services on top of an unreliable infrastructure, developers need to be able to test the stability of their services while the underlying unreliable infrastructure is going through complicated state transitions due to faults.</span></span>

<span data-ttu-id="04702-107">[錯誤插入與叢集分析服務](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (亦稱為「錯誤分析服務」) 讓開發人員能夠引發錯誤來測試其服務。</span><span class="sxs-lookup"><span data-stu-id="04702-107">The [Fault Injection and Cluster Analysis Service](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (also known as the Fault Analysis Service) gives developers the ability to induce faults to test their services.</span></span> <span data-ttu-id="04702-108">這些針對性模擬錯誤，例如[重新啟動分割區](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps)，可幫助您練習最常見的狀態轉換。</span><span class="sxs-lookup"><span data-stu-id="04702-108">These targeted simulated faults, like [restarting a partition](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), can help exercise the most common state transitions.</span></span> <span data-ttu-id="04702-109">但針對性模擬錯誤會因為定義而有偏差，因此可能會遺漏只會出現在難以預測、冗長且複雜的狀態轉換順序中的問題。</span><span class="sxs-lookup"><span data-stu-id="04702-109">However targeted simulated faults are biased by definition and thus may miss bugs that show up only in hard-to-predict, long and complicated sequence of state transitions.</span></span> <span data-ttu-id="04702-110">如需無偏差測試，您可以使用混亂。</span><span class="sxs-lookup"><span data-stu-id="04702-110">For an unbiased testing, you can use Chaos.</span></span>

<span data-ttu-id="04702-111">混亂會以很長的時間在整個叢集上模擬定期、交錯的錯誤 (包括非失誤性和失誤性錯誤)。</span><span class="sxs-lookup"><span data-stu-id="04702-111">Chaos simulates periodic, interleaved faults (both graceful and ungraceful) throughout the cluster over extended periods of time.</span></span> <span data-ttu-id="04702-112">設定混亂的比率和錯誤類型後，即可透過 C# 或 Powershell API 啟動混亂，以開始在叢集和您的服務中產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="04702-112">Once you have configured Chaos with the rate and the kind of faults, you can start Chaos through C# or Powershell API to start generating faults in the cluster and in your services.</span></span> <span data-ttu-id="04702-113">您可以設定混亂會執行一段指定的時間 (例如 1 小時)、在哪個混亂自動停止後執行，或隨時呼叫 StopChaos API (C# 或 Powershell) 來停止它。</span><span class="sxs-lookup"><span data-stu-id="04702-113">You can configure Chaos to run for a specified time period (for example, for one hour), after which Chaos stops automatically, or you can call StopChaos API (C# or Powershell) to stop it at any time.</span></span>

> [!NOTE]
> <span data-ttu-id="04702-114">目前來說，混亂只會引發安全的錯誤，這表示如果沒有外部錯誤，絕不會發生仲裁遺失或資料遺失。</span><span class="sxs-lookup"><span data-stu-id="04702-114">In its current form, Chaos induces only safe faults, which implies that in the absence of external faults a quorum loss, or data loss never occurs.</span></span>
>

<span data-ttu-id="04702-115">混亂執行時，會產生不同事件來擷取目前執行的狀態。</span><span class="sxs-lookup"><span data-stu-id="04702-115">While Chaos is running, it produces different events that capture the state of the run at the moment.</span></span> <span data-ttu-id="04702-116">例如，ExecutingFaultsEvent 包含混亂已決定正在該反覆運算中執行的所有錯誤。</span><span class="sxs-lookup"><span data-stu-id="04702-116">For example, an ExecutingFaultsEvent contains all the faults that Chaos has decided to execute in that iteration.</span></span> <span data-ttu-id="04702-117">ValidationFailedEvent 包含在驗證叢集期間所發現驗證失敗 (健康情況或穩定性問題) 的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="04702-117">A ValidationFailedEvent contains the details of a validation failure (health or stability issues) that was found during the validation of the cluster.</span></span> <span data-ttu-id="04702-118">您可以叫用 GetChaosReport API (C# 或 Powershell) 以取得混亂執行的報告。</span><span class="sxs-lookup"><span data-stu-id="04702-118">You can invoke the GetChaosReport API (C# or Powershell) to get the report of Chaos runs.</span></span> <span data-ttu-id="04702-119">這些事件保存在[可靠的字典](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections)中，其中有由兩個組態決定的截斷原則：MaxStoredChaosEventCount (預設值為 25000) 及 StoredActionCleanupIntervalInSeconds (預設值為 3600)。</span><span class="sxs-lookup"><span data-stu-id="04702-119">These events get persisted in a [reliable dictionary](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), which has a truncation policy dictated by two configurations: **MaxStoredChaosEventCount** (default value is 25000) and **StoredActionCleanupIntervalInSeconds** (default value is 3600).</span></span> <span data-ttu-id="04702-120">每個 StoredActionCleanupIntervalInSeconds 混亂檢查及最新 MaxStoredChaosEventCount 事件以外的所有事件皆會自可靠字典中清除。</span><span class="sxs-lookup"><span data-stu-id="04702-120">Every *StoredActionCleanupIntervalInSeconds* Chaos checks and all but the most recent *MaxStoredChaosEventCount* events, are purged from the reliable dictionary.</span></span>

## <a name="faults-induced-in-chaos"></a><span data-ttu-id="04702-121">混亂中引發的錯誤</span><span class="sxs-lookup"><span data-stu-id="04702-121">Faults induced in Chaos</span></span>
<span data-ttu-id="04702-122">混亂會在整個 Service Fabric 叢集中產生錯誤，並將在幾個月或幾年內看到的錯誤壓縮成幾小時。</span><span class="sxs-lookup"><span data-stu-id="04702-122">Chaos generates faults across the entire Service Fabric cluster and compresses faults that are seen in months or years into a few hours.</span></span> <span data-ttu-id="04702-123">交錯錯誤和高錯誤率的組合，會尋找可能會在其他情形下遺漏的極端狀況。</span><span class="sxs-lookup"><span data-stu-id="04702-123">The combination of interleaved faults with the high fault rate finds corner cases that may otherwise be missed.</span></span> <span data-ttu-id="04702-124">這個混亂練習可以大幅提升服務的程式碼品質。</span><span class="sxs-lookup"><span data-stu-id="04702-124">This exercise of Chaos leads to a significant improvement in the code quality of the service.</span></span>

<span data-ttu-id="04702-125">混亂會引發下列類別的錯誤︰</span><span class="sxs-lookup"><span data-stu-id="04702-125">Chaos induces faults from the following categories:</span></span>

* <span data-ttu-id="04702-126">重新啟動節點</span><span class="sxs-lookup"><span data-stu-id="04702-126">Restart a node</span></span>
* <span data-ttu-id="04702-127">重新啟動已部署的程式碼封裝</span><span class="sxs-lookup"><span data-stu-id="04702-127">Restart a deployed code package</span></span>
* <span data-ttu-id="04702-128">移除複本</span><span class="sxs-lookup"><span data-stu-id="04702-128">Remove a replica</span></span>
* <span data-ttu-id="04702-129">重新啟動複本</span><span class="sxs-lookup"><span data-stu-id="04702-129">Restart a replica</span></span>
* <span data-ttu-id="04702-130">移動主要複本 (可設定)</span><span class="sxs-lookup"><span data-stu-id="04702-130">Move a primary replica (configurable)</span></span>
* <span data-ttu-id="04702-131">移動次要複本 (可設定)</span><span class="sxs-lookup"><span data-stu-id="04702-131">Move a secondary replica (configurable)</span></span>

<span data-ttu-id="04702-132">混亂會多次反覆執行。</span><span class="sxs-lookup"><span data-stu-id="04702-132">Chaos runs in multiple iterations.</span></span> <span data-ttu-id="04702-133">每次反覆運算都包含指定期間的錯誤和叢集驗證。</span><span class="sxs-lookup"><span data-stu-id="04702-133">Each iteration consists of faults and cluster validation for the specified period.</span></span> <span data-ttu-id="04702-134">您可以設定讓叢集穩定和驗證成功的所需時間。</span><span class="sxs-lookup"><span data-stu-id="04702-134">You can configure the time spent for the cluster to stabilize and for validation to succeed.</span></span> <span data-ttu-id="04702-135">如果在叢集驗證中發現失敗，則混亂會產生並保留一個 ValidationFailedEvent，包含 UTC 時間戳記與失敗詳細資料。</span><span class="sxs-lookup"><span data-stu-id="04702-135">If a failure is found in cluster validation, Chaos generates and persists a ValidationFailedEvent with the UTC timestamp and the failure details.</span></span> <span data-ttu-id="04702-136">例如，考慮一個設為執行 1 小時且最多有 3 個並行錯誤的混亂執行個體。</span><span class="sxs-lookup"><span data-stu-id="04702-136">For example, consider an instance of Chaos that is set to run for an hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="04702-137">混亂會引發三個錯誤，然後驗證叢集健康狀態。</span><span class="sxs-lookup"><span data-stu-id="04702-137">Chaos induces three faults, and then validates the cluster health.</span></span> <span data-ttu-id="04702-138">它會重複執行上一個步驟，直到透過 StopChaosAsync API 或經過一小時後就會明確停止。</span><span class="sxs-lookup"><span data-stu-id="04702-138">It iterates through the previous step until it is explicitly stopped through the StopChaosAsync API or one-hour passes.</span></span> <span data-ttu-id="04702-139">如果任何反覆運算中的叢集變成健康情況不佳 (也就是在傳入的 MaxClusterStabilizationTimeout 內不穩定)，則混亂會產生 ValidationFailedEvent。</span><span class="sxs-lookup"><span data-stu-id="04702-139">If the cluster becomes unhealthy in any iteration (that is, it does not stabilize within the passed-in MaxClusterStabilizationTimeout), Chaos generates a ValidationFailedEvent.</span></span> <span data-ttu-id="04702-140">此事件表示發生了錯誤，且可能需要進一步調查。</span><span class="sxs-lookup"><span data-stu-id="04702-140">This event indicates that something has gone wrong and might need further investigation.</span></span>

<span data-ttu-id="04702-141">若要取得混亂引發的錯誤，您可以使用 GetChaosReport API (powershell 或 C#)。</span><span class="sxs-lookup"><span data-stu-id="04702-141">To get which faults Chaos induced, you can use GetChaosReport API (powershell or C#).</span></span> <span data-ttu-id="04702-142">API 會根據傳入接續權杖或傳入的時間範圍取得混亂報告的下個區段。</span><span class="sxs-lookup"><span data-stu-id="04702-142">The API gets the next segment of the Chaos report based on the passed-in continuation token or the passed-in time-range.</span></span> <span data-ttu-id="04702-143">您可以指定 ContinuationToken 取得混亂報告的下個區段，或者您可以透過 StartTimeUtc 與 EndTimeUtc 指定時間範圍，但您無法在同一個呼叫中同時指定 ContinuationToken 與時間範圍。</span><span class="sxs-lookup"><span data-stu-id="04702-143">You can either specify the ContinuationToken to get the next segment of the Chaos report or you can specify the time-range through StartTimeUtc and EndTimeUtc, but you cannot specify both the ContinuationToken and the time-range in the same call.</span></span> <span data-ttu-id="04702-144">當混亂事件超過 100 個時，系統會分區段傳回混亂報告，每個區段中包含的混亂事件不超過 100 個。</span><span class="sxs-lookup"><span data-stu-id="04702-144">When there are more than 100 Chaos events, the Chaos report is returned in segments where a segment contains no more than 100 Chaos events.</span></span>

## <a name="important-configuration-options"></a><span data-ttu-id="04702-145">重要的組態選項</span><span class="sxs-lookup"><span data-stu-id="04702-145">Important configuration options</span></span>
* <span data-ttu-id="04702-146">**TimeToRun**：混亂在成功完成前的總執行時間。</span><span class="sxs-lookup"><span data-stu-id="04702-146">**TimeToRun**: Total time that Chaos runs before it finishes with success.</span></span> <span data-ttu-id="04702-147">您可以在混亂執行 TimeToRun 這段時間之前透過 StopChaos API 停止混亂。</span><span class="sxs-lookup"><span data-stu-id="04702-147">You can stop Chaos before it has run for the TimeToRun period through the StopChaos API.</span></span>

* <span data-ttu-id="04702-148">**MaxClusterStabilizationTimeout**：在產生 ValidationFailedEvent 前等候叢集健康情況變為良好的時間上限。</span><span class="sxs-lookup"><span data-stu-id="04702-148">**MaxClusterStabilizationTimeout**: The maximum amount of time to wait for the cluster to become healthy before producing a ValidationFailedEvent.</span></span> <span data-ttu-id="04702-149">這段等候時間是為了減少叢集在復原時所承擔的負載。</span><span class="sxs-lookup"><span data-stu-id="04702-149">This wait is to reduce the load on the cluster while it is recovering.</span></span> <span data-ttu-id="04702-150">執行的檢查為：</span><span class="sxs-lookup"><span data-stu-id="04702-150">The checks performed are:</span></span>
  * <span data-ttu-id="04702-151">叢集健康狀態是否正常</span><span class="sxs-lookup"><span data-stu-id="04702-151">If the cluster health is OK</span></span>
  * <span data-ttu-id="04702-152">服務健康狀態是否正常</span><span class="sxs-lookup"><span data-stu-id="04702-152">If the service health is OK</span></span>
  * <span data-ttu-id="04702-153">服務分割區是否達到目標複本集大小</span><span class="sxs-lookup"><span data-stu-id="04702-153">If the target replica set size is achieved for the service partition</span></span>
  * <span data-ttu-id="04702-154">沒有 InBuild 複本存在</span><span class="sxs-lookup"><span data-stu-id="04702-154">That no InBuild replicas exist</span></span>
* <span data-ttu-id="04702-155">**MaxConcurrentFaults**：每個反覆運算中引發的最大並行錯誤數。</span><span class="sxs-lookup"><span data-stu-id="04702-155">**MaxConcurrentFaults**: The maximum number of concurrent faults that are induced in each iteration.</span></span> <span data-ttu-id="04702-156">數字愈大，混亂愈積極，叢集經歷的容錯移轉與狀態轉換也更複雜。</span><span class="sxs-lookup"><span data-stu-id="04702-156">The higher the number, the more aggressive Chaos is and the failovers and the state transition combinations that the cluster goes through are also more complex.</span></span> 

> [!NOTE]
> <span data-ttu-id="04702-157">無論 *MaxConcurrentFaults* 值多大，混亂都能保證在缺少外部錯誤的狀況下，不會有仲裁遺失或資料遺失。</span><span class="sxs-lookup"><span data-stu-id="04702-157">Regardless how high a value *MaxConcurrentFaults* has, Chaos guarantees - in the absence of external faults - there is no quorum loss or data loss.</span></span>
>

* <span data-ttu-id="04702-158">**EnableMoveReplicaFaults**：啟用或停用造成主要或次要複本移動的錯誤。</span><span class="sxs-lookup"><span data-stu-id="04702-158">**EnableMoveReplicaFaults**: Enables or disables the faults that cause the primary or secondary replicas to move.</span></span> <span data-ttu-id="04702-159">預設會停用這些錯誤。</span><span class="sxs-lookup"><span data-stu-id="04702-159">These faults are disabled by default.</span></span>
* <span data-ttu-id="04702-160">**WaitTimeBetweenIterations**︰反覆運算之間要等候的時間量。</span><span class="sxs-lookup"><span data-stu-id="04702-160">**WaitTimeBetweenIterations**: The amount of time to wait between iterations.</span></span> <span data-ttu-id="04702-161">亦即，在已執行一輪的錯誤且已完成對應的叢集健康情況驗證後，混亂將暫停的時間。</span><span class="sxs-lookup"><span data-stu-id="04702-161">That is, the amount of time Chaos will pause after having executed a round of faults and having finished the corresponding validation of the health of the cluster.</span></span> <span data-ttu-id="04702-162">值愈大，平均錯誤插入率愈低。</span><span class="sxs-lookup"><span data-stu-id="04702-162">The higher the value, the lower is the average fault injection rate.</span></span>
* <span data-ttu-id="04702-163">**WaitTimeBetweenFaults**︰單一反覆運算中兩個連續錯誤之間的等候時間長度。</span><span class="sxs-lookup"><span data-stu-id="04702-163">**WaitTimeBetweenFaults**: The amount of time to wait between two consecutive faults in a single iteration.</span></span> <span data-ttu-id="04702-164">值愈大，錯誤的並行程度 (或錯誤之間的重疊度) 愈低。</span><span class="sxs-lookup"><span data-stu-id="04702-164">The higher the value, the lower the concurrency of (or the overlap between) faults.</span></span>
* <span data-ttu-id="04702-165">**ClusterHealthPolicy**︰叢集健康情況原則用於驗證混亂反覆運算之間的叢集健康情況。</span><span class="sxs-lookup"><span data-stu-id="04702-165">**ClusterHealthPolicy**: Cluster health policy is used to validate the health of the cluster in between Chaos iterations.</span></span> <span data-ttu-id="04702-166">如果叢集健康情況發生錯誤，或如果在錯誤執行期間發生未預期的例外狀況，則混亂會先等待 30 分鐘，再執行下一個健康情況檢查，讓叢集有時間復原。</span><span class="sxs-lookup"><span data-stu-id="04702-166">If the cluster health is in error or if an unexpected exception happens during fault execution, Chaos will wait for 30 minutes before the next health-check - to provide the cluster with some time to recuperate.</span></span>
* <span data-ttu-id="04702-167">**內容**：(string, string) 類型索引鍵-值組的集合。</span><span class="sxs-lookup"><span data-stu-id="04702-167">**Context**: A collection of (string, string) type key-value pairs.</span></span> <span data-ttu-id="04702-168">此對應可用於記錄混亂執行的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="04702-168">The map can be used to record information about the Chaos run.</span></span> <span data-ttu-id="04702-169">此類組合不能超過 100 個，且每個字串 (索引鍵或值) 最多為 4095 個字元長。</span><span class="sxs-lookup"><span data-stu-id="04702-169">There cannot be more than 100 such pairs and each string (key or value) can be at most 4095 characters long.</span></span> <span data-ttu-id="04702-170">此對應由混亂執行的起始者設定，以選擇性地儲存特定執行的相關內容。</span><span class="sxs-lookup"><span data-stu-id="04702-170">This map is set by the starter of the Chaos run to optionally store the context about the specific run.</span></span>

## <a name="how-to-run-chaos"></a><span data-ttu-id="04702-171">如何執行混亂</span><span class="sxs-lookup"><span data-stu-id="04702-171">How to run Chaos</span></span>

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
                Console.WriteLine("An instance of Chaos is already running in the cluster.");
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
                // If a StoppedEvent is found, exit the loop.
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
