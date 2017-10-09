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
# <a name="testability-actions"></a><span data-ttu-id="a89ee-103">Testability 動作</span><span class="sxs-lookup"><span data-stu-id="a89ee-103">Testability actions</span></span>
<span data-ttu-id="a89ee-104">在順序 toosimulate 不可靠的基礎結構，Azure Service Fabric 提供您 hello 開發人員，方式 toosimulate 各種真實世界失敗和狀態轉換。</span><span class="sxs-lookup"><span data-stu-id="a89ee-104">In order toosimulate an unreliable infrastructure, Azure Service Fabric provides you, hello developer, with ways toosimulate various real-world failures and state transitions.</span></span> <span data-ttu-id="a89ee-105">這些方法會以 Testability 動作的形式公開。</span><span class="sxs-lookup"><span data-stu-id="a89ee-105">These are exposed as testability actions.</span></span> <span data-ttu-id="a89ee-106">hello 動作是 hello 會造成特定的錯誤資料隱碼、 狀態轉換或驗證的低階 Api。</span><span class="sxs-lookup"><span data-stu-id="a89ee-106">hello actions are hello low-level APIs that cause a specific fault injection, state transition, or validation.</span></span> <span data-ttu-id="a89ee-107">結合這些動作後，便可以為您的服務撰寫完整的測試案例。</span><span class="sxs-lookup"><span data-stu-id="a89ee-107">By combining these actions, you can write comprehensive test scenarios for your services.</span></span>

<span data-ttu-id="a89ee-108">Service Fabric 會提供由這些動作所組成的一些常見測試案例。</span><span class="sxs-lookup"><span data-stu-id="a89ee-108">Service Fabric provides some common test scenarios composed of these actions.</span></span> <span data-ttu-id="a89ee-109">我們強烈建議您利用這些內建的情況下，謹慎選擇 tootest 常用的狀態轉換以及失敗情況。</span><span class="sxs-lookup"><span data-stu-id="a89ee-109">We highly recommend that you utilize these built-in scenarios, which are carefully chosen tootest common state transitions and failure cases.</span></span> <span data-ttu-id="a89ee-110">不過，動作可以使用的 toocreate 自訂測試案例的情況下，未涵蓋的 hello 內建案例尚未或自訂所量身訂做的應用程式需要 tooadd 涵蓋範圍時。</span><span class="sxs-lookup"><span data-stu-id="a89ee-110">However, actions can be used toocreate custom test scenarios when you want tooadd coverage for scenarios that are not covered by hello built-in scenarios yet or that are custom tailored for your application.</span></span>

<span data-ttu-id="a89ee-111">Hello System.Fabric.dll 組件中找到的 hello 動作的 C# 實作。</span><span class="sxs-lookup"><span data-stu-id="a89ee-111">C# implementations of hello actions are found in hello System.Fabric.dll assembly.</span></span> <span data-ttu-id="a89ee-112">hello Microsoft.ServiceFabric.Powershell.dll 組件中找到 hello 系統網狀架構 PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="a89ee-112">hello System Fabric PowerShell module is found in hello Microsoft.ServiceFabric.Powershell.dll assembly.</span></span> <span data-ttu-id="a89ee-113">Hello ServiceFabric PowerShell 模組執行階段安裝的一部分，是為了方便使用的已安裝的 tooallow。</span><span class="sxs-lookup"><span data-stu-id="a89ee-113">As part of runtime installation, hello ServiceFabric PowerShell module is installed tooallow for ease of use.</span></span>

## <a name="graceful-vs-ungraceful-fault-actions"></a><span data-ttu-id="a89ee-114">非失誤性與失誤性錯誤動作比較</span><span class="sxs-lookup"><span data-stu-id="a89ee-114">Graceful vs. ungraceful fault actions</span></span>
<span data-ttu-id="a89ee-115">Testability 動作分為兩個主要貯體：</span><span class="sxs-lookup"><span data-stu-id="a89ee-115">Testability actions are classified into two major buckets:</span></span>

* <span data-ttu-id="a89ee-116">失誤性錯誤：這些錯誤會模擬失敗案例 (例如機器重新啟動和處理程序當機)。</span><span class="sxs-lookup"><span data-stu-id="a89ee-116">Ungraceful faults: These faults simulate failures like machine restarts and process crashes.</span></span> <span data-ttu-id="a89ee-117">在這類的失敗的情況下，hello 執行內容的程序會突然停止。</span><span class="sxs-lookup"><span data-stu-id="a89ee-117">In such cases of failures, hello execution context of process stops abruptly.</span></span> <span data-ttu-id="a89ee-118">這表示不會清除 hello 狀態的 hello 應用程式重新啟動之前執行。</span><span class="sxs-lookup"><span data-stu-id="a89ee-118">This means no cleanup of hello state can run before hello application starts up again.</span></span>
* <span data-ttu-id="a89ee-119">非失誤性錯誤：這些錯誤會模擬正常動作 (例如由負載平衡觸發的複本移動及卸除)。</span><span class="sxs-lookup"><span data-stu-id="a89ee-119">Graceful faults: These faults simulate graceful actions like replica moves and drops triggered by load balancing.</span></span> <span data-ttu-id="a89ee-120">在這種情況下，hello 服務收到通知，hello 關閉，並可以清除在結束之前的 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="a89ee-120">In such cases, hello service gets a notification of hello close and can clean up hello state before exiting.</span></span>

<span data-ttu-id="a89ee-121">較佳的品質驗證執行 hello 服務和企業工作負載時由引發各種依正常程序與不正常的錯誤。</span><span class="sxs-lookup"><span data-stu-id="a89ee-121">For better quality validation, run hello service and business workload while inducing various graceful and ungraceful faults.</span></span> <span data-ttu-id="a89ee-122">不正常的錯誤執行其中 hello 服務處理序突然結束 hello 中間的某些工作流程的案例。</span><span class="sxs-lookup"><span data-stu-id="a89ee-122">Ungraceful faults exercise scenarios where hello service process abruptly exits in hello middle of some workflow.</span></span> <span data-ttu-id="a89ee-123">此程序一旦 hello 服務複本還原 Service Fabric 測試 hello 復原路徑。</span><span class="sxs-lookup"><span data-stu-id="a89ee-123">This tests  hello recovery path once hello service replica is restored by Service Fabric.</span></span> <span data-ttu-id="a89ee-124">這將有助於測試資料的一致性和是否 hello 服務狀態正確維護在失敗之後。</span><span class="sxs-lookup"><span data-stu-id="a89ee-124">This will help test data consistency and whether hello service state is maintained correctly after failures.</span></span> <span data-ttu-id="a89ee-125">hello 失敗 （hello 正常失敗） 的其他組測試 hello 服務正確地回應 tooreplicas Service Fabric 移動。</span><span class="sxs-lookup"><span data-stu-id="a89ee-125">hello other set of failures (hello graceful failures) test that hello service correctly reacts tooreplicas being moved around by Service Fabric.</span></span> <span data-ttu-id="a89ee-126">這在 hello RunAsync 方法中測試取消的處理。</span><span class="sxs-lookup"><span data-stu-id="a89ee-126">This tests handling of cancellation in hello RunAsync method.</span></span> <span data-ttu-id="a89ee-127">hello 服務需要 toocheck hello 取消語彙基元所設定，正確地儲存其狀態，並結束 hello RunAsync 方法。</span><span class="sxs-lookup"><span data-stu-id="a89ee-127">hello service needs toocheck for hello cancellation token being set, correctly save its state, and exit hello RunAsync method.</span></span>

## <a name="testability-actions-list"></a><span data-ttu-id="a89ee-128">Testability 動作清單</span><span class="sxs-lookup"><span data-stu-id="a89ee-128">Testability actions list</span></span>
| <span data-ttu-id="a89ee-129">動作</span><span class="sxs-lookup"><span data-stu-id="a89ee-129">Action</span></span> | <span data-ttu-id="a89ee-130">說明</span><span class="sxs-lookup"><span data-stu-id="a89ee-130">Description</span></span> | <span data-ttu-id="a89ee-131">Managed API</span><span class="sxs-lookup"><span data-stu-id="a89ee-131">Managed API</span></span> | <span data-ttu-id="a89ee-132">PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="a89ee-132">PowerShell cmdlet</span></span> | <span data-ttu-id="a89ee-133">非失誤性/失誤性錯誤</span><span class="sxs-lookup"><span data-stu-id="a89ee-133">Graceful/ungraceful faults</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="a89ee-134">CleanTestState</span><span class="sxs-lookup"><span data-stu-id="a89ee-134">CleanTestState</span></span> |<span data-ttu-id="a89ee-135">Hello 叢集發生不正常關機 hello 測試驅動程式會移除所有 hello 測試狀態。</span><span class="sxs-lookup"><span data-stu-id="a89ee-135">Removes all hello test state from hello cluster in case of a bad shutdown of hello test driver.</span></span> |<span data-ttu-id="a89ee-136">CleanTestStateAsync</span><span class="sxs-lookup"><span data-stu-id="a89ee-136">CleanTestStateAsync</span></span> |<span data-ttu-id="a89ee-137">Remove-ServiceFabricTestState</span><span class="sxs-lookup"><span data-stu-id="a89ee-137">Remove-ServiceFabricTestState</span></span> |<span data-ttu-id="a89ee-138">不適用</span><span class="sxs-lookup"><span data-stu-id="a89ee-138">Not applicable</span></span> |
| <span data-ttu-id="a89ee-139">InvokeDataLoss</span><span class="sxs-lookup"><span data-stu-id="a89ee-139">InvokeDataLoss</span></span> |<span data-ttu-id="a89ee-140">會引發資料遺失至服務分割區中。</span><span class="sxs-lookup"><span data-stu-id="a89ee-140">Induces data loss into a service partition.</span></span> |<span data-ttu-id="a89ee-141">InvokeDataLossAsync</span><span class="sxs-lookup"><span data-stu-id="a89ee-141">InvokeDataLossAsync</span></span> |<span data-ttu-id="a89ee-142">Invoke-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="a89ee-142">Invoke-ServiceFabricPartitionDataLoss</span></span> |<span data-ttu-id="a89ee-143">非失誤性</span><span class="sxs-lookup"><span data-stu-id="a89ee-143">Graceful</span></span> |
| <span data-ttu-id="a89ee-144">InvokeQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="a89ee-144">InvokeQuorumLoss</span></span> |<span data-ttu-id="a89ee-145">會放置指定狀態服務分割區至仲裁遺失中。</span><span class="sxs-lookup"><span data-stu-id="a89ee-145">Puts a given stateful service partition into quorum loss.</span></span> |<span data-ttu-id="a89ee-146">InvokeQuorumLossAsync</span><span class="sxs-lookup"><span data-stu-id="a89ee-146">InvokeQuorumLossAsync</span></span> |<span data-ttu-id="a89ee-147">Invoke-ServiceFabricQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="a89ee-147">Invoke-ServiceFabricQuorumLoss</span></span> |<span data-ttu-id="a89ee-148">非失誤性</span><span class="sxs-lookup"><span data-stu-id="a89ee-148">Graceful</span></span> |
| <span data-ttu-id="a89ee-149">移動主要複本</span><span class="sxs-lookup"><span data-stu-id="a89ee-149">Move Primary</span></span> |<span data-ttu-id="a89ee-150">移動 hello 指定具狀態服務 toohello 指定的叢集節點的主要複本。</span><span class="sxs-lookup"><span data-stu-id="a89ee-150">Moves hello specified primary replica of a stateful service toohello specified cluster node.</span></span> |<span data-ttu-id="a89ee-151">MovePrimaryAsync</span><span class="sxs-lookup"><span data-stu-id="a89ee-151">MovePrimaryAsync</span></span> |<span data-ttu-id="a89ee-152">Move-ServiceFabricPrimaryReplica</span><span class="sxs-lookup"><span data-stu-id="a89ee-152">Move-ServiceFabricPrimaryReplica</span></span> |<span data-ttu-id="a89ee-153">非失誤性</span><span class="sxs-lookup"><span data-stu-id="a89ee-153">Graceful</span></span> |
| <span data-ttu-id="a89ee-154">移動次要複本</span><span class="sxs-lookup"><span data-stu-id="a89ee-154">Move Secondary</span></span> |<span data-ttu-id="a89ee-155">移動 hello 目前的次要複本的可設定狀態服務 tooa 不同的叢集節點。</span><span class="sxs-lookup"><span data-stu-id="a89ee-155">Moves hello current secondary replica of a stateful service tooa different cluster node.</span></span> |<span data-ttu-id="a89ee-156">MoveSecondaryAsync</span><span class="sxs-lookup"><span data-stu-id="a89ee-156">MoveSecondaryAsync</span></span> |<span data-ttu-id="a89ee-157">Move-ServiceFabricSecondaryReplica</span><span class="sxs-lookup"><span data-stu-id="a89ee-157">Move-ServiceFabricSecondaryReplica</span></span> |<span data-ttu-id="a89ee-158">非失誤性</span><span class="sxs-lookup"><span data-stu-id="a89ee-158">Graceful</span></span> |
| <span data-ttu-id="a89ee-159">RemoveReplica</span><span class="sxs-lookup"><span data-stu-id="a89ee-159">RemoveReplica</span></span> |<span data-ttu-id="a89ee-160">移除叢集中的複本以模擬複本失敗案例。</span><span class="sxs-lookup"><span data-stu-id="a89ee-160">Simulates a replica failure by removing a replica from a cluster.</span></span> <span data-ttu-id="a89ee-161">這將會關閉 hello 複本，並會將它轉換 toorole 'None'、 從 hello 叢集移除它的所有狀態。</span><span class="sxs-lookup"><span data-stu-id="a89ee-161">This will close hello replica and will transition it toorole 'None', removing all of its state from hello cluster.</span></span> |<span data-ttu-id="a89ee-162">RemoveReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="a89ee-162">RemoveReplicaAsync</span></span> |<span data-ttu-id="a89ee-163">Remove-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="a89ee-163">Remove-ServiceFabricReplica</span></span> |<span data-ttu-id="a89ee-164">非失誤性</span><span class="sxs-lookup"><span data-stu-id="a89ee-164">Graceful</span></span> |
| <span data-ttu-id="a89ee-165">RestartDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="a89ee-165">RestartDeployedCodePackage</span></span> |<span data-ttu-id="a89ee-166">藉由重新啟動部署在叢集中之節點上的程式碼封裝，模擬程式碼封裝處理程序的失敗案例。</span><span class="sxs-lookup"><span data-stu-id="a89ee-166">Simulates a code package process failure by restarting a code package deployed on a node in a cluster.</span></span> <span data-ttu-id="a89ee-167">這會中止 hello 程式碼封裝程序，將重新裝載之所有的 hello 使用者服務複本啟動該處理程序。</span><span class="sxs-lookup"><span data-stu-id="a89ee-167">This aborts hello code package process, which will restart all hello user service replicas hosted in that process.</span></span> |<span data-ttu-id="a89ee-168">RestartDeployedCodePackageAsync</span><span class="sxs-lookup"><span data-stu-id="a89ee-168">RestartDeployedCodePackageAsync</span></span> |<span data-ttu-id="a89ee-169">Restart-ServiceFabricDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="a89ee-169">Restart-ServiceFabricDeployedCodePackage</span></span> |<span data-ttu-id="a89ee-170">失誤性</span><span class="sxs-lookup"><span data-stu-id="a89ee-170">Ungraceful</span></span> |
| <span data-ttu-id="a89ee-171">RestartNode</span><span class="sxs-lookup"><span data-stu-id="a89ee-171">RestartNode</span></span> |<span data-ttu-id="a89ee-172">藉由重新啟動節點，模擬 Service Fabric 叢集節點的失敗案例。</span><span class="sxs-lookup"><span data-stu-id="a89ee-172">Simulates a Service Fabric cluster node failure by restarting a node.</span></span> |<span data-ttu-id="a89ee-173">RestartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="a89ee-173">RestartNodeAsync</span></span> |<span data-ttu-id="a89ee-174">Restart-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="a89ee-174">Restart-ServiceFabricNode</span></span> |<span data-ttu-id="a89ee-175">失誤性</span><span class="sxs-lookup"><span data-stu-id="a89ee-175">Ungraceful</span></span> |
| <span data-ttu-id="a89ee-176">RestartPartition</span><span class="sxs-lookup"><span data-stu-id="a89ee-176">RestartPartition</span></span> |<span data-ttu-id="a89ee-177">藉由重新啟動部分或所有分割區複本，模擬資料中心停機或叢集停機的案例。</span><span class="sxs-lookup"><span data-stu-id="a89ee-177">Simulates a datacenter blackout or cluster blackout scenario by restarting some or all replicas of a partition.</span></span> |<span data-ttu-id="a89ee-178">RestartPartitionAsync</span><span class="sxs-lookup"><span data-stu-id="a89ee-178">RestartPartitionAsync</span></span> |<span data-ttu-id="a89ee-179">Restart-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="a89ee-179">Restart-ServiceFabricPartition</span></span> |<span data-ttu-id="a89ee-180">非失誤性</span><span class="sxs-lookup"><span data-stu-id="a89ee-180">Graceful</span></span> |
| <span data-ttu-id="a89ee-181">RestartReplica</span><span class="sxs-lookup"><span data-stu-id="a89ee-181">RestartReplica</span></span> |<span data-ttu-id="a89ee-182">重新啟動叢集中的永續性的複本、 關閉 hello 複本後再重新開啟它，以模擬複本失敗。</span><span class="sxs-lookup"><span data-stu-id="a89ee-182">Simulates a replica failure by restarting a persisted replica in a cluster, closing hello replica and then reopening it.</span></span> |<span data-ttu-id="a89ee-183">RestartReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="a89ee-183">RestartReplicaAsync</span></span> |<span data-ttu-id="a89ee-184">Restart-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="a89ee-184">Restart-ServiceFabricReplica</span></span> |<span data-ttu-id="a89ee-185">非失誤性</span><span class="sxs-lookup"><span data-stu-id="a89ee-185">Graceful</span></span> |
| <span data-ttu-id="a89ee-186">StartNode</span><span class="sxs-lookup"><span data-stu-id="a89ee-186">StartNode</span></span> |<span data-ttu-id="a89ee-187">會啟動叢集中已停止的節點。</span><span class="sxs-lookup"><span data-stu-id="a89ee-187">Starts a node in a cluster that is already stopped.</span></span> |<span data-ttu-id="a89ee-188">StartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="a89ee-188">StartNodeAsync</span></span> |<span data-ttu-id="a89ee-189">Start-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="a89ee-189">Start-ServiceFabricNode</span></span> |<span data-ttu-id="a89ee-190">不適用</span><span class="sxs-lookup"><span data-stu-id="a89ee-190">Not applicable</span></span> |
| <span data-ttu-id="a89ee-191">StopNode</span><span class="sxs-lookup"><span data-stu-id="a89ee-191">StopNode</span></span> |<span data-ttu-id="a89ee-192">藉由停止叢集中的節點，模擬節點失敗案例。</span><span class="sxs-lookup"><span data-stu-id="a89ee-192">Simulates a node failure by stopping a node in a cluster.</span></span> <span data-ttu-id="a89ee-193">StartNode 呼叫之前，將會向下保持 hello 節點。</span><span class="sxs-lookup"><span data-stu-id="a89ee-193">hello node will stay down until StartNode is called.</span></span> |<span data-ttu-id="a89ee-194">StopNodeAsync</span><span class="sxs-lookup"><span data-stu-id="a89ee-194">StopNodeAsync</span></span> |<span data-ttu-id="a89ee-195">Stop-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="a89ee-195">Stop-ServiceFabricNode</span></span> |<span data-ttu-id="a89ee-196">失誤性</span><span class="sxs-lookup"><span data-stu-id="a89ee-196">Ungraceful</span></span> |
| <span data-ttu-id="a89ee-197">ValidateApplication</span><span class="sxs-lookup"><span data-stu-id="a89ee-197">ValidateApplication</span></span> |<span data-ttu-id="a89ee-198">Hello 可用性和健全狀況的應用程式，通常由某些錯誤引發 hello 系統內的所有 Service Fabric 服務驗證。</span><span class="sxs-lookup"><span data-stu-id="a89ee-198">Validates hello availability and health of all Service Fabric services within an application, usually after inducing some fault into hello system.</span></span> |<span data-ttu-id="a89ee-199">ValidateApplicationAsync</span><span class="sxs-lookup"><span data-stu-id="a89ee-199">ValidateApplicationAsync</span></span> |<span data-ttu-id="a89ee-200">Test-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="a89ee-200">Test-ServiceFabricApplication</span></span> |<span data-ttu-id="a89ee-201">不適用</span><span class="sxs-lookup"><span data-stu-id="a89ee-201">Not applicable</span></span> |
| <span data-ttu-id="a89ee-202">ValidateService</span><span class="sxs-lookup"><span data-stu-id="a89ee-202">ValidateService</span></span> |<span data-ttu-id="a89ee-203">通常後一些錯誤查到 hello 系統驗證 hello 可用性和健全狀況的 Service Fabric 服務。</span><span class="sxs-lookup"><span data-stu-id="a89ee-203">Validates hello availability and health of a Service Fabric service, usually after inducing some fault into hello system.</span></span> |<span data-ttu-id="a89ee-204">ValidateServiceAsync</span><span class="sxs-lookup"><span data-stu-id="a89ee-204">ValidateServiceAsync</span></span> |<span data-ttu-id="a89ee-205">Test-ServiceFabricService</span><span class="sxs-lookup"><span data-stu-id="a89ee-205">Test-ServiceFabricService</span></span> |<span data-ttu-id="a89ee-206">不適用</span><span class="sxs-lookup"><span data-stu-id="a89ee-206">Not applicable</span></span> |

## <a name="running-a-testability-action-using-powershell"></a><span data-ttu-id="a89ee-207">使用 PowerShell 執行 Testability 動作</span><span class="sxs-lookup"><span data-stu-id="a89ee-207">Running a testability action using PowerShell</span></span>
<span data-ttu-id="a89ee-208">本教學課程示範如何使用 PowerShell 的可測試性動作 toorun。</span><span class="sxs-lookup"><span data-stu-id="a89ee-208">This tutorial shows you how toorun a testability action by using PowerShell.</span></span> <span data-ttu-id="a89ee-209">您將學習如何 toorun 針對本機的 （一個方塊） 叢集或 Azure 的叢集的可測試性動作。</span><span class="sxs-lookup"><span data-stu-id="a89ee-209">You will learn how toorun a testability action against a local (one-box) cluster or an Azure cluster.</span></span> <span data-ttu-id="a89ee-210">Microsoft.Fabric.Powershell.dll-hello Service Fabric PowerShell 模組--會自動安裝時安裝 Microsoft Service Fabric MSI hello。</span><span class="sxs-lookup"><span data-stu-id="a89ee-210">Microsoft.Fabric.Powershell.dll--hello Service Fabric PowerShell module--is installed automatically when you install hello Microsoft Service Fabric MSI.</span></span> <span data-ttu-id="a89ee-211">當您開啟 PowerShell 命令提示字元時，會自動載入 hello 模組。</span><span class="sxs-lookup"><span data-stu-id="a89ee-211">hello module is loaded automatically when you open a PowerShell prompt.</span></span>

<span data-ttu-id="a89ee-212">教學課程區段：</span><span class="sxs-lookup"><span data-stu-id="a89ee-212">Tutorial segments:</span></span>

* [<span data-ttu-id="a89ee-213">針對一整體叢集執行動作</span><span class="sxs-lookup"><span data-stu-id="a89ee-213">Run an action against a one-box cluster</span></span>](#run-an-action-against-a-one-box-cluster)
* [<span data-ttu-id="a89ee-214">針對 Azure 叢集執行動作</span><span class="sxs-lookup"><span data-stu-id="a89ee-214">Run an action against an Azure cluster</span></span>](#run-an-action-against-an-azure-cluster)

### <a name="run-an-action-against-a-one-box-cluster"></a><span data-ttu-id="a89ee-215">針對一整體叢集執行動作</span><span class="sxs-lookup"><span data-stu-id="a89ee-215">Run an action against a one-box cluster</span></span>
<span data-ttu-id="a89ee-216">toohello 叢集和系統管理員模式開啟 hello PowerShell 命令提示字元，第一次連接 toorun 針對本機叢集，可測試性動作。</span><span class="sxs-lookup"><span data-stu-id="a89ee-216">toorun a testability action against a local cluster, first connect toohello cluster and open hello PowerShell prompt in administrator mode.</span></span> <span data-ttu-id="a89ee-217">讓我們看看 hello**重新啟動 ServiceFabricNode**動作。</span><span class="sxs-lookup"><span data-stu-id="a89ee-217">Let us look at hello **Restart-ServiceFabricNode** action.</span></span>

```powershell
Restart-ServiceFabricNode -NodeName Node1 -CompletionMode DoNotVerify
```

<span data-ttu-id="a89ee-218">這裡 hello 動作**重新啟動 ServiceFabricNode**名為"Node1"的節點上執行。</span><span class="sxs-lookup"><span data-stu-id="a89ee-218">Here hello action **Restart-ServiceFabricNode** is being run on a node named "Node1".</span></span> <span data-ttu-id="a89ee-219">hello 完成模式指定，它不應該確認 hello 重新啟動節點動作是否實際上是否成功。</span><span class="sxs-lookup"><span data-stu-id="a89ee-219">hello completion mode specifies that it should not verify whether hello restart-node action actually succeeded.</span></span> <span data-ttu-id="a89ee-220">為 [驗證] 指定 hello 完成模式會導致 tooverify 是否實際上成功 hello 重新啟動動作。</span><span class="sxs-lookup"><span data-stu-id="a89ee-220">Specifying hello completion mode as "Verify" will cause it tooverify whether hello restart action actually succeeded.</span></span> <span data-ttu-id="a89ee-221">而不是直接由其名稱指定 hello 節點，您可以如下所示指定它的資料分割索引鍵和 hello 種類的複本，透過：</span><span class="sxs-lookup"><span data-stu-id="a89ee-221">Instead of directly specifying hello node by its name, you can specify it via a partition key and hello kind of replica, as follows:</span></span>

```powershell
Restart-ServiceFabricNode -ReplicaKindPrimary  -PartitionKindNamed -PartitionKey Partition3 -CompletionMode Verify
```


```powershell
$connection = "localhost:19000"
$nodeName = "Node1"

Connect-ServiceFabricCluster $connection
Restart-ServiceFabricNode -NodeName $nodeName -CompletionMode DoNotVerify
```

<span data-ttu-id="a89ee-222">**重新啟動 ServiceFabricNode**應該使用的 toorestart 叢集中的 Service Fabric 節點。</span><span class="sxs-lookup"><span data-stu-id="a89ee-222">**Restart-ServiceFabricNode** should be used toorestart a Service Fabric node in a cluster.</span></span> <span data-ttu-id="a89ee-223">這樣會停止 hello Fabric.exe 程序，將會重新啟動所有 hello 系統服務和使用者服務複本的該節點上裝載。</span><span class="sxs-lookup"><span data-stu-id="a89ee-223">This will stop hello Fabric.exe process, which will restart all of hello system service and user service replicas hosted on that node.</span></span> <span data-ttu-id="a89ee-224">使用此 API tootest 您的服務，有助於發現 bug，沿著 hello 容錯移轉復原路徑。</span><span class="sxs-lookup"><span data-stu-id="a89ee-224">Using this API tootest your service helps uncover bugs along hello failover recovery paths.</span></span> <span data-ttu-id="a89ee-225">它會協助模擬 hello 叢集中的節點失敗。</span><span class="sxs-lookup"><span data-stu-id="a89ee-225">It helps simulate node failures in hello cluster.</span></span>

<span data-ttu-id="a89ee-226">hello 下列螢幕擷取畫面顯示 hello**重新啟動 ServiceFabricNode**動作中的可測試性命令。</span><span class="sxs-lookup"><span data-stu-id="a89ee-226">hello following screenshot shows hello **Restart-ServiceFabricNode** testability command in action.</span></span>

![](media/service-fabric-testability-actions/Restart-ServiceFabricNode.png)

<span data-ttu-id="a89ee-227">hello 第一次輸出的 hello **Get ServiceFabricNode** (hello Service Fabric PowerShell 模組的 cmdlet) 會顯示該 hello 本機叢集具有五個節點： Node.1 tooNode.5。</span><span class="sxs-lookup"><span data-stu-id="a89ee-227">hello output of hello first **Get-ServiceFabricNode** (a cmdlet from hello Service Fabric PowerShell module) shows that hello local cluster has five nodes: Node.1 tooNode.5.</span></span> <span data-ttu-id="a89ee-228">Hello 可測試性動作 (cmdlet) 之後**重新啟動 ServiceFabricNode** hello 節點上執行名為 Node.4，我們會看到已重設該 hello 節點的執行時間。</span><span class="sxs-lookup"><span data-stu-id="a89ee-228">After hello testability action (cmdlet) **Restart-ServiceFabricNode** is executed on hello node, named Node.4, we see that hello node's uptime has been reset.</span></span>

### <a name="run-an-action-against-an-azure-cluster"></a><span data-ttu-id="a89ee-229">針對 Azure 叢集執行動作</span><span class="sxs-lookup"><span data-stu-id="a89ee-229">Run an action against an Azure cluster</span></span>
<span data-ttu-id="a89ee-230">（透過使用 PowerShell） 執行可測試性動作，對 Azure 的叢集是針對本機叢集類似 toorunning hello 動作。</span><span class="sxs-lookup"><span data-stu-id="a89ee-230">Running a testability action (by using PowerShell) against an Azure cluster is similar toorunning hello action against a local cluster.</span></span> <span data-ttu-id="a89ee-231">hello 只能差異在於，您才能執行 hello 動作，而不是連接 toohello 本機叢集，您需要 tooconnect toohello Azure 叢集的第一次。</span><span class="sxs-lookup"><span data-stu-id="a89ee-231">hello only difference is that before you can run hello action, instead of connecting toohello local cluster, you need tooconnect toohello Azure cluster first.</span></span>

## <a name="running-a-testability-action-using-c35"></a><span data-ttu-id="a89ee-232">使用 C&#35; 執行 Testability 動作</span><span class="sxs-lookup"><span data-stu-id="a89ee-232">Running a testability action using C&#35;</span></span>
<span data-ttu-id="a89ee-233">toorun 可測試性動作，使用 C#，首先您需要 tooconnect toohello 叢集使用 FabricClient。</span><span class="sxs-lookup"><span data-stu-id="a89ee-233">toorun a testability action by using C#, first you need tooconnect toohello cluster by using FabricClient.</span></span> <span data-ttu-id="a89ee-234">然後取得 hello 所需要的參數 toorun hello 動作。</span><span class="sxs-lookup"><span data-stu-id="a89ee-234">Then obtain hello parameters needed toorun hello action.</span></span> <span data-ttu-id="a89ee-235">可以使用不同的參數 toorun hello 相同的動作。</span><span class="sxs-lookup"><span data-stu-id="a89ee-235">Different parameters can be used toorun hello same action.</span></span>
<span data-ttu-id="a89ee-236">查看 hello RestartServiceFabricNode 動作，它是使用 hello 節點資訊 （節點名稱和節點執行個體識別碼） 的其中一種方式 toorun hello 叢集中。</span><span class="sxs-lookup"><span data-stu-id="a89ee-236">Looking at hello RestartServiceFabricNode action, one way toorun it is by using hello node information (node name and node instance ID) in hello cluster.</span></span>

```csharp
RestartNodeAsync(nodeName, nodeInstanceId, completeMode, operationTimeout, CancellationToken.None)
```

<span data-ttu-id="a89ee-237">參數說明：</span><span class="sxs-lookup"><span data-stu-id="a89ee-237">Parameter explanation:</span></span>

* <span data-ttu-id="a89ee-238">**CompleteMode**指定模式的 hello 不應該確認 hello 重新啟動動作是否實際上是否成功。</span><span class="sxs-lookup"><span data-stu-id="a89ee-238">**CompleteMode** specifies that hello mode should not verify whether hello restart action actually succeeded.</span></span> <span data-ttu-id="a89ee-239">為 [驗證] 指定 hello 完成模式會導致 tooverify 是否實際上成功 hello 重新啟動動作。</span><span class="sxs-lookup"><span data-stu-id="a89ee-239">Specifying hello completion mode as "Verify" will cause it tooverify whether hello restart action actually succeeded.</span></span>  
* <span data-ttu-id="a89ee-240">**OperationTimeout**集 hello hello 作業 toofinish 的時間量之前擲回 TimeoutException 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="a89ee-240">**OperationTimeout** sets hello amount of time for hello operation toofinish before a TimeoutException exception is thrown.</span></span>
* <span data-ttu-id="a89ee-241">**CancellationToken**啟用取消暫止呼叫 toobe。</span><span class="sxs-lookup"><span data-stu-id="a89ee-241">**CancellationToken** enables a pending call toobe canceled.</span></span>

<span data-ttu-id="a89ee-242">而不是直接由其名稱指定 hello 節點，您可以指定它透過資料分割索引鍵和 hello 類型的複本。</span><span class="sxs-lookup"><span data-stu-id="a89ee-242">Instead of directly specifying hello node by its name, you can specify it via a partition key and hello kind of replica.</span></span>

<span data-ttu-id="a89ee-243">如需詳細資訊，請參閱 [PartitionSelector 和 ReplicaSelector](#partition_replica_selector)。</span><span class="sxs-lookup"><span data-stu-id="a89ee-243">For further information, see [PartitionSelector and ReplicaSelector](#partition_replica_selector).</span></span>

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

## <a name="partitionselector-and-replicaselector"></a><span data-ttu-id="a89ee-244">PartitionSelector 和 ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="a89ee-244">PartitionSelector and ReplicaSelector</span></span>
### <a name="partitionselector"></a><span data-ttu-id="a89ee-245">PartitionSelector</span><span class="sxs-lookup"><span data-stu-id="a89ee-245">PartitionSelector</span></span>
<span data-ttu-id="a89ee-246">PartitionSelector 是 helper，可測試性中公開，是使用的 tooselect 特定資料分割上的 tooperform 任一 hello 可測試性動作。</span><span class="sxs-lookup"><span data-stu-id="a89ee-246">PartitionSelector is a helper exposed in testability and is used tooselect a specific partition on which tooperform any of hello testability actions.</span></span> <span data-ttu-id="a89ee-247">如果事先知道 hello 分割區識別碼，它可以是使用的 tooselect 特定分割區。</span><span class="sxs-lookup"><span data-stu-id="a89ee-247">It can be used tooselect a specific partition if hello partition ID is known beforehand.</span></span> <span data-ttu-id="a89ee-248">或者，您可以提供 hello 資料分割索引鍵並 hello 作業將會在內部解析 hello 分割區識別碼。</span><span class="sxs-lookup"><span data-stu-id="a89ee-248">Or, you can provide hello partition key and hello operation will resolve hello partition ID internally.</span></span> <span data-ttu-id="a89ee-249">您也可以選取隨機的資料分割的 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="a89ee-249">You also have hello option of selecting a random partition.</span></span>

<span data-ttu-id="a89ee-250">toouse 此協助程式，建立 hello PartitionSelector 物件，並使用其中一種 hello 選取 * 方法選取 hello 資料分割。</span><span class="sxs-lookup"><span data-stu-id="a89ee-250">toouse this helper, create hello PartitionSelector object and select hello partition by using one of hello Select* methods.</span></span> <span data-ttu-id="a89ee-251">然後傳入 hello PartitionSelector 物件 toohello 需要它的 API。</span><span class="sxs-lookup"><span data-stu-id="a89ee-251">Then pass in hello PartitionSelector object toohello API that requires it.</span></span> <span data-ttu-id="a89ee-252">如果不選取任何選項，則預設 tooa 隨機分割區。</span><span class="sxs-lookup"><span data-stu-id="a89ee-252">If no option is selected, it defaults tooa random partition.</span></span>

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

### <a name="replicaselector"></a><span data-ttu-id="a89ee-253">ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="a89ee-253">ReplicaSelector</span></span>
<span data-ttu-id="a89ee-254">ReplicaSelector 為可測試性中公開協助程式，而且是使用的 toohelp 選取哪些 tooperform 上的複本任一 hello 可測試性動作。</span><span class="sxs-lookup"><span data-stu-id="a89ee-254">ReplicaSelector is a helper exposed in testability and is used toohelp select a replica on which tooperform any of hello testability actions.</span></span> <span data-ttu-id="a89ee-255">如果事先知道 hello 複本識別碼，它可以是使用的 tooselect 特定複本。</span><span class="sxs-lookup"><span data-stu-id="a89ee-255">It can be used tooselect a specific replica if hello replica ID is known beforehand.</span></span> <span data-ttu-id="a89ee-256">此外，您可以 hello 選擇選取的主要複本或隨機的次要資料庫。</span><span class="sxs-lookup"><span data-stu-id="a89ee-256">In addition, you have hello option of selecting a primary replica or a random secondary.</span></span> <span data-ttu-id="a89ee-257">ReplicaSelector 衍生自 PartitionSelector，因此您需要 tooselect 兩者 hello 複本和 hello 想 tooperform hello 可測試性作業的磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="a89ee-257">ReplicaSelector derives from PartitionSelector, so you need tooselect both hello replica and hello partition on which you wish tooperform hello testability operation.</span></span>

<span data-ttu-id="a89ee-258">toouse 此協助程式，建立 ReplicaSelector 物件，並設定您想要的 hello 方式 tooselect hello 複本和 hello 磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="a89ee-258">toouse this helper, create a ReplicaSelector object and set hello way you want tooselect hello replica and hello partition.</span></span> <span data-ttu-id="a89ee-259">您可以將它傳遞至 hello 需要它的 API。</span><span class="sxs-lookup"><span data-stu-id="a89ee-259">You can then pass it into hello API that requires it.</span></span> <span data-ttu-id="a89ee-260">如果不選取任何選項，則預設 tooa 隨機複本和隨機分割區。</span><span class="sxs-lookup"><span data-stu-id="a89ee-260">If no option is selected, it defaults tooa random replica and random partition.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a89ee-261">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a89ee-261">Next steps</span></span>
* [<span data-ttu-id="a89ee-262">Testability 案例</span><span class="sxs-lookup"><span data-stu-id="a89ee-262">Testability scenarios</span></span>](service-fabric-testability-scenarios.md)
* <span data-ttu-id="a89ee-263">如何 tootest 您的服務</span><span class="sxs-lookup"><span data-stu-id="a89ee-263">How tootest your service</span></span>
  * [<span data-ttu-id="a89ee-264">模擬服務工作負載期間的失敗案例</span><span class="sxs-lookup"><span data-stu-id="a89ee-264">Simulate failures during service workloads</span></span>](service-fabric-testability-workload-tests.md)
  * [<span data-ttu-id="a89ee-265">服務對服務間通訊的失敗案例</span><span class="sxs-lookup"><span data-stu-id="a89ee-265">Service-to-service communication failures</span></span>](service-fabric-testability-scenarios-service-communication.md)

