---
title: "模擬 Azure 微服務中的失敗 | Microsoft Docs"
description: "本文說明關於在 Microsoft Azure Service Fabric 中找到的 Testability 動作。"
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
ms.openlocfilehash: c8ddc7732999ae555323bebaef60aa34c8f2ec17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="testability-actions"></a><span data-ttu-id="87ada-103">Testability 動作</span><span class="sxs-lookup"><span data-stu-id="87ada-103">Testability actions</span></span>
<span data-ttu-id="87ada-104">為了模擬不可靠的基礎結構，Azure Service Fabric 會提供開發人員用於模擬各種真實失敗案例及狀態轉換的方法。</span><span class="sxs-lookup"><span data-stu-id="87ada-104">In order to simulate an unreliable infrastructure, Azure Service Fabric provides you, the developer, with ways to simulate various real-world failures and state transitions.</span></span> <span data-ttu-id="87ada-105">這些方法會以 Testability 動作的形式公開。</span><span class="sxs-lookup"><span data-stu-id="87ada-105">These are exposed as testability actions.</span></span> <span data-ttu-id="87ada-106">這些動作是低階 API，會導致特定錯誤插入、狀態轉換或驗證。</span><span class="sxs-lookup"><span data-stu-id="87ada-106">The actions are the low-level APIs that cause a specific fault injection, state transition, or validation.</span></span> <span data-ttu-id="87ada-107">結合這些動作後，便可以為您的服務撰寫完整的測試案例。</span><span class="sxs-lookup"><span data-stu-id="87ada-107">By combining these actions, you can write comprehensive test scenarios for your services.</span></span>

<span data-ttu-id="87ada-108">Service Fabric 會提供由這些動作所組成的一些常見測試案例。</span><span class="sxs-lookup"><span data-stu-id="87ada-108">Service Fabric provides some common test scenarios composed of these actions.</span></span> <span data-ttu-id="87ada-109">強烈建議您使用這些內建案例，因為它們是經過仔細挑選，可用來測試常見狀態轉換和失敗案例的案例。</span><span class="sxs-lookup"><span data-stu-id="87ada-109">We highly recommend that you utilize these built-in scenarios, which are carefully chosen to test common state transitions and failure cases.</span></span> <span data-ttu-id="87ada-110">不過，若您想要新增案例涵蓋範圍以補足內建案例尚未涵蓋，或並非針對您的應用程式量身打造的案例時，動作就可用來建立自訂測試案例。</span><span class="sxs-lookup"><span data-stu-id="87ada-110">However, actions can be used to create custom test scenarios when you want to add coverage for scenarios that are not covered by the built-in scenarios yet or that are custom tailored for your application.</span></span>

<span data-ttu-id="87ada-111">這些動作的 C# 實作可在 System.Fabric.dll 組件中找到。</span><span class="sxs-lookup"><span data-stu-id="87ada-111">C# implementations of the actions are found in the System.Fabric.dll assembly.</span></span> <span data-ttu-id="87ada-112">System Fabric PowerShell 模組可在 Microsoft.ServiceFabric.Powershell.dll 組件中找到。</span><span class="sxs-lookup"><span data-stu-id="87ada-112">The System Fabric PowerShell module is found in the Microsoft.ServiceFabric.Powershell.dll assembly.</span></span> <span data-ttu-id="87ada-113">ServiceFabric PowerShell 模組會在執行階段安裝過程中安裝，讓您方便使用。</span><span class="sxs-lookup"><span data-stu-id="87ada-113">As part of runtime installation, the ServiceFabric PowerShell module is installed to allow for ease of use.</span></span>

## <a name="graceful-vs-ungraceful-fault-actions"></a><span data-ttu-id="87ada-114">非失誤性與失誤性錯誤動作比較</span><span class="sxs-lookup"><span data-stu-id="87ada-114">Graceful vs. ungraceful fault actions</span></span>
<span data-ttu-id="87ada-115">Testability 動作分為兩個主要貯體：</span><span class="sxs-lookup"><span data-stu-id="87ada-115">Testability actions are classified into two major buckets:</span></span>

* <span data-ttu-id="87ada-116">失誤性錯誤：這些錯誤會模擬失敗案例 (例如機器重新啟動和處理程序當機)。</span><span class="sxs-lookup"><span data-stu-id="87ada-116">Ungraceful faults: These faults simulate failures like machine restarts and process crashes.</span></span> <span data-ttu-id="87ada-117">在這類失敗情況下，處理程序的執行內容會突然停止。</span><span class="sxs-lookup"><span data-stu-id="87ada-117">In such cases of failures, the execution context of process stops abruptly.</span></span> <span data-ttu-id="87ada-118">這表示在應用程式再次啟動前，您都不能執行任何狀態清除作業。</span><span class="sxs-lookup"><span data-stu-id="87ada-118">This means no cleanup of the state can run before the application starts up again.</span></span>
* <span data-ttu-id="87ada-119">非失誤性錯誤：這些錯誤會模擬正常動作 (例如由負載平衡觸發的複本移動及卸除)。</span><span class="sxs-lookup"><span data-stu-id="87ada-119">Graceful faults: These faults simulate graceful actions like replica moves and drops triggered by load balancing.</span></span> <span data-ttu-id="87ada-120">在這類情況下，服務會在結束前取得關閉通知並且清除狀態。</span><span class="sxs-lookup"><span data-stu-id="87ada-120">In such cases, the service gets a notification of the close and can clean up the state before exiting.</span></span>

<span data-ttu-id="87ada-121">為了提供更好的品質驗證，請在引發各種非失誤性及失誤性錯誤時，執行服務及商務工作負載。</span><span class="sxs-lookup"><span data-stu-id="87ada-121">For better quality validation, run the service and business workload while inducing various graceful and ungraceful faults.</span></span> <span data-ttu-id="87ada-122">失誤性錯誤會模擬服務處理程序在部分工作流程中突然結束的案例。</span><span class="sxs-lookup"><span data-stu-id="87ada-122">Ungraceful faults exercise scenarios where the service process abruptly exits in the middle of some workflow.</span></span> <span data-ttu-id="87ada-123">當服務複本由 Service Fabric 還原時，便會測試復原路徑。</span><span class="sxs-lookup"><span data-stu-id="87ada-123">This tests  the recovery path once the service replica is restored by Service Fabric.</span></span> <span data-ttu-id="87ada-124">這有助於測試資料的一致性，以及服務狀態在失敗之後是否已正確維護。</span><span class="sxs-lookup"><span data-stu-id="87ada-124">This will help test data consistency and whether the service state is maintained correctly after failures.</span></span> <span data-ttu-id="87ada-125">其他錯誤集 (非失誤性錯誤) 會測試由 Service Fabric 移動的複本是否正確反應。</span><span class="sxs-lookup"><span data-stu-id="87ada-125">The other set of failures (the graceful failures) test that the service correctly reacts to replicas being moved around by Service Fabric.</span></span> <span data-ttu-id="87ada-126">這會測試 RunAsync 方法中的取消處理作業。</span><span class="sxs-lookup"><span data-stu-id="87ada-126">This tests handling of cancellation in the RunAsync method.</span></span> <span data-ttu-id="87ada-127">該服務必須檢查已設定的取消語彙基元、正確地儲存其狀態，並結束 RunAsync 方法。</span><span class="sxs-lookup"><span data-stu-id="87ada-127">The service needs to check for the cancellation token being set, correctly save its state, and exit the RunAsync method.</span></span>

## <a name="testability-actions-list"></a><span data-ttu-id="87ada-128">Testability 動作清單</span><span class="sxs-lookup"><span data-stu-id="87ada-128">Testability actions list</span></span>
| <span data-ttu-id="87ada-129">動作</span><span class="sxs-lookup"><span data-stu-id="87ada-129">Action</span></span> | <span data-ttu-id="87ada-130">說明</span><span class="sxs-lookup"><span data-stu-id="87ada-130">Description</span></span> | <span data-ttu-id="87ada-131">Managed API</span><span class="sxs-lookup"><span data-stu-id="87ada-131">Managed API</span></span> | <span data-ttu-id="87ada-132">PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="87ada-132">PowerShell cmdlet</span></span> | <span data-ttu-id="87ada-133">非失誤性/失誤性錯誤</span><span class="sxs-lookup"><span data-stu-id="87ada-133">Graceful/ungraceful faults</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="87ada-134">CleanTestState</span><span class="sxs-lookup"><span data-stu-id="87ada-134">CleanTestState</span></span> |<span data-ttu-id="87ada-135">會移除叢集的所有測試狀態，以防止測試驅動程式不正確關閉。</span><span class="sxs-lookup"><span data-stu-id="87ada-135">Removes all the test state from the cluster in case of a bad shutdown of the test driver.</span></span> |<span data-ttu-id="87ada-136">CleanTestStateAsync</span><span class="sxs-lookup"><span data-stu-id="87ada-136">CleanTestStateAsync</span></span> |<span data-ttu-id="87ada-137">Remove-ServiceFabricTestState</span><span class="sxs-lookup"><span data-stu-id="87ada-137">Remove-ServiceFabricTestState</span></span> |<span data-ttu-id="87ada-138">不適用</span><span class="sxs-lookup"><span data-stu-id="87ada-138">Not applicable</span></span> |
| <span data-ttu-id="87ada-139">InvokeDataLoss</span><span class="sxs-lookup"><span data-stu-id="87ada-139">InvokeDataLoss</span></span> |<span data-ttu-id="87ada-140">會引發資料遺失至服務分割區中。</span><span class="sxs-lookup"><span data-stu-id="87ada-140">Induces data loss into a service partition.</span></span> |<span data-ttu-id="87ada-141">InvokeDataLossAsync</span><span class="sxs-lookup"><span data-stu-id="87ada-141">InvokeDataLossAsync</span></span> |<span data-ttu-id="87ada-142">Invoke-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="87ada-142">Invoke-ServiceFabricPartitionDataLoss</span></span> |<span data-ttu-id="87ada-143">非失誤性</span><span class="sxs-lookup"><span data-stu-id="87ada-143">Graceful</span></span> |
| <span data-ttu-id="87ada-144">InvokeQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="87ada-144">InvokeQuorumLoss</span></span> |<span data-ttu-id="87ada-145">會放置指定狀態服務分割區至仲裁遺失中。</span><span class="sxs-lookup"><span data-stu-id="87ada-145">Puts a given stateful service partition into quorum loss.</span></span> |<span data-ttu-id="87ada-146">InvokeQuorumLossAsync</span><span class="sxs-lookup"><span data-stu-id="87ada-146">InvokeQuorumLossAsync</span></span> |<span data-ttu-id="87ada-147">Invoke-ServiceFabricQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="87ada-147">Invoke-ServiceFabricQuorumLoss</span></span> |<span data-ttu-id="87ada-148">非失誤性</span><span class="sxs-lookup"><span data-stu-id="87ada-148">Graceful</span></span> |
| <span data-ttu-id="87ada-149">移動主要複本</span><span class="sxs-lookup"><span data-stu-id="87ada-149">Move Primary</span></span> |<span data-ttu-id="87ada-150">將指定的狀態服務主要複本移動至指定的叢集節點。</span><span class="sxs-lookup"><span data-stu-id="87ada-150">Moves the specified primary replica of a stateful service to the specified cluster node.</span></span> |<span data-ttu-id="87ada-151">MovePrimaryAsync</span><span class="sxs-lookup"><span data-stu-id="87ada-151">MovePrimaryAsync</span></span> |<span data-ttu-id="87ada-152">Move-ServiceFabricPrimaryReplica</span><span class="sxs-lookup"><span data-stu-id="87ada-152">Move-ServiceFabricPrimaryReplica</span></span> |<span data-ttu-id="87ada-153">非失誤性</span><span class="sxs-lookup"><span data-stu-id="87ada-153">Graceful</span></span> |
| <span data-ttu-id="87ada-154">移動次要複本</span><span class="sxs-lookup"><span data-stu-id="87ada-154">Move Secondary</span></span> |<span data-ttu-id="87ada-155">將目前的服務狀態次要複本移動至不同的叢集節點。</span><span class="sxs-lookup"><span data-stu-id="87ada-155">Moves the current secondary replica of a stateful service to a different cluster node.</span></span> |<span data-ttu-id="87ada-156">MoveSecondaryAsync</span><span class="sxs-lookup"><span data-stu-id="87ada-156">MoveSecondaryAsync</span></span> |<span data-ttu-id="87ada-157">Move-ServiceFabricSecondaryReplica</span><span class="sxs-lookup"><span data-stu-id="87ada-157">Move-ServiceFabricSecondaryReplica</span></span> |<span data-ttu-id="87ada-158">非失誤性</span><span class="sxs-lookup"><span data-stu-id="87ada-158">Graceful</span></span> |
| <span data-ttu-id="87ada-159">RemoveReplica</span><span class="sxs-lookup"><span data-stu-id="87ada-159">RemoveReplica</span></span> |<span data-ttu-id="87ada-160">移除叢集中的複本以模擬複本失敗案例。</span><span class="sxs-lookup"><span data-stu-id="87ada-160">Simulates a replica failure by removing a replica from a cluster.</span></span> <span data-ttu-id="87ada-161">這將會關閉複本，並將其轉換為 'None' 角色，進而移除其在叢集中的所有狀態。</span><span class="sxs-lookup"><span data-stu-id="87ada-161">This will close the replica and will transition it to role 'None', removing all of its state from the cluster.</span></span> |<span data-ttu-id="87ada-162">RemoveReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="87ada-162">RemoveReplicaAsync</span></span> |<span data-ttu-id="87ada-163">Remove-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="87ada-163">Remove-ServiceFabricReplica</span></span> |<span data-ttu-id="87ada-164">非失誤性</span><span class="sxs-lookup"><span data-stu-id="87ada-164">Graceful</span></span> |
| <span data-ttu-id="87ada-165">RestartDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="87ada-165">RestartDeployedCodePackage</span></span> |<span data-ttu-id="87ada-166">藉由重新啟動部署在叢集中之節點上的程式碼封裝，模擬程式碼封裝處理程序的失敗案例。</span><span class="sxs-lookup"><span data-stu-id="87ada-166">Simulates a code package process failure by restarting a code package deployed on a node in a cluster.</span></span> <span data-ttu-id="87ada-167">這會中止程式碼封裝處理程序 (會重新啟動所有由其代管的使用者服務複本)。</span><span class="sxs-lookup"><span data-stu-id="87ada-167">This aborts the code package process, which will restart all the user service replicas hosted in that process.</span></span> |<span data-ttu-id="87ada-168">RestartDeployedCodePackageAsync</span><span class="sxs-lookup"><span data-stu-id="87ada-168">RestartDeployedCodePackageAsync</span></span> |<span data-ttu-id="87ada-169">Restart-ServiceFabricDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="87ada-169">Restart-ServiceFabricDeployedCodePackage</span></span> |<span data-ttu-id="87ada-170">失誤性</span><span class="sxs-lookup"><span data-stu-id="87ada-170">Ungraceful</span></span> |
| <span data-ttu-id="87ada-171">RestartNode</span><span class="sxs-lookup"><span data-stu-id="87ada-171">RestartNode</span></span> |<span data-ttu-id="87ada-172">藉由重新啟動節點，模擬 Service Fabric 叢集節點的失敗案例。</span><span class="sxs-lookup"><span data-stu-id="87ada-172">Simulates a Service Fabric cluster node failure by restarting a node.</span></span> |<span data-ttu-id="87ada-173">RestartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="87ada-173">RestartNodeAsync</span></span> |<span data-ttu-id="87ada-174">Restart-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="87ada-174">Restart-ServiceFabricNode</span></span> |<span data-ttu-id="87ada-175">失誤性</span><span class="sxs-lookup"><span data-stu-id="87ada-175">Ungraceful</span></span> |
| <span data-ttu-id="87ada-176">RestartPartition</span><span class="sxs-lookup"><span data-stu-id="87ada-176">RestartPartition</span></span> |<span data-ttu-id="87ada-177">藉由重新啟動部分或所有分割區複本，模擬資料中心停機或叢集停機的案例。</span><span class="sxs-lookup"><span data-stu-id="87ada-177">Simulates a datacenter blackout or cluster blackout scenario by restarting some or all replicas of a partition.</span></span> |<span data-ttu-id="87ada-178">RestartPartitionAsync</span><span class="sxs-lookup"><span data-stu-id="87ada-178">RestartPartitionAsync</span></span> |<span data-ttu-id="87ada-179">Restart-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="87ada-179">Restart-ServiceFabricPartition</span></span> |<span data-ttu-id="87ada-180">非失誤性</span><span class="sxs-lookup"><span data-stu-id="87ada-180">Graceful</span></span> |
| <span data-ttu-id="87ada-181">RestartReplica</span><span class="sxs-lookup"><span data-stu-id="87ada-181">RestartReplica</span></span> |<span data-ttu-id="87ada-182">藉由重新啟動保存在叢集中的複本、關閉該複本再重新開啟的方式，模擬複本失敗案例。</span><span class="sxs-lookup"><span data-stu-id="87ada-182">Simulates a replica failure by restarting a persisted replica in a cluster, closing the replica and then reopening it.</span></span> |<span data-ttu-id="87ada-183">RestartReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="87ada-183">RestartReplicaAsync</span></span> |<span data-ttu-id="87ada-184">Restart-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="87ada-184">Restart-ServiceFabricReplica</span></span> |<span data-ttu-id="87ada-185">非失誤性</span><span class="sxs-lookup"><span data-stu-id="87ada-185">Graceful</span></span> |
| <span data-ttu-id="87ada-186">StartNode</span><span class="sxs-lookup"><span data-stu-id="87ada-186">StartNode</span></span> |<span data-ttu-id="87ada-187">會啟動叢集中已停止的節點。</span><span class="sxs-lookup"><span data-stu-id="87ada-187">Starts a node in a cluster that is already stopped.</span></span> |<span data-ttu-id="87ada-188">StartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="87ada-188">StartNodeAsync</span></span> |<span data-ttu-id="87ada-189">Start-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="87ada-189">Start-ServiceFabricNode</span></span> |<span data-ttu-id="87ada-190">不適用</span><span class="sxs-lookup"><span data-stu-id="87ada-190">Not applicable</span></span> |
| <span data-ttu-id="87ada-191">StopNode</span><span class="sxs-lookup"><span data-stu-id="87ada-191">StopNode</span></span> |<span data-ttu-id="87ada-192">藉由停止叢集中的節點，模擬節點失敗案例。</span><span class="sxs-lookup"><span data-stu-id="87ada-192">Simulates a node failure by stopping a node in a cluster.</span></span> <span data-ttu-id="87ada-193">在呼叫 StartNode 前，節點會維持關閉。</span><span class="sxs-lookup"><span data-stu-id="87ada-193">The node will stay down until StartNode is called.</span></span> |<span data-ttu-id="87ada-194">StopNodeAsync</span><span class="sxs-lookup"><span data-stu-id="87ada-194">StopNodeAsync</span></span> |<span data-ttu-id="87ada-195">Stop-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="87ada-195">Stop-ServiceFabricNode</span></span> |<span data-ttu-id="87ada-196">失誤性</span><span class="sxs-lookup"><span data-stu-id="87ada-196">Ungraceful</span></span> |
| <span data-ttu-id="87ada-197">ValidateApplication</span><span class="sxs-lookup"><span data-stu-id="87ada-197">ValidateApplication</span></span> |<span data-ttu-id="87ada-198">會驗證應用程式中所有 Service Fabric 服務的可用性和健康情況 (通常在引發部分錯誤至系統後)。</span><span class="sxs-lookup"><span data-stu-id="87ada-198">Validates the availability and health of all Service Fabric services within an application, usually after inducing some fault into the system.</span></span> |<span data-ttu-id="87ada-199">ValidateApplicationAsync</span><span class="sxs-lookup"><span data-stu-id="87ada-199">ValidateApplicationAsync</span></span> |<span data-ttu-id="87ada-200">Test-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="87ada-200">Test-ServiceFabricApplication</span></span> |<span data-ttu-id="87ada-201">不適用</span><span class="sxs-lookup"><span data-stu-id="87ada-201">Not applicable</span></span> |
| <span data-ttu-id="87ada-202">ValidateService</span><span class="sxs-lookup"><span data-stu-id="87ada-202">ValidateService</span></span> |<span data-ttu-id="87ada-203">會驗證 Service Fabric 服務的可用性和健康情況 (通常在引發部分錯誤至系統後)。</span><span class="sxs-lookup"><span data-stu-id="87ada-203">Validates the availability and health of a Service Fabric service, usually after inducing some fault into the system.</span></span> |<span data-ttu-id="87ada-204">ValidateServiceAsync</span><span class="sxs-lookup"><span data-stu-id="87ada-204">ValidateServiceAsync</span></span> |<span data-ttu-id="87ada-205">Test-ServiceFabricService</span><span class="sxs-lookup"><span data-stu-id="87ada-205">Test-ServiceFabricService</span></span> |<span data-ttu-id="87ada-206">不適用</span><span class="sxs-lookup"><span data-stu-id="87ada-206">Not applicable</span></span> |

## <a name="running-a-testability-action-using-powershell"></a><span data-ttu-id="87ada-207">使用 PowerShell 執行 Testability 動作</span><span class="sxs-lookup"><span data-stu-id="87ada-207">Running a testability action using PowerShell</span></span>
<span data-ttu-id="87ada-208">本教學課程會示範如何使用 PowerShell 執行 Testability 動作。</span><span class="sxs-lookup"><span data-stu-id="87ada-208">This tutorial shows you how to run a testability action by using PowerShell.</span></span> <span data-ttu-id="87ada-209">您將學習如何針對本機 (一整體) 叢集或 Azure 叢集，執行 Testability 動作。</span><span class="sxs-lookup"><span data-stu-id="87ada-209">You will learn how to run a testability action against a local (one-box) cluster or an Azure cluster.</span></span> <span data-ttu-id="87ada-210">當您安裝 Microsoft Service Fabric MSI 時，Microsoft.Fabric.Powershell.dll (Service Fabric PowerShell 模組) 就會自動安裝。</span><span class="sxs-lookup"><span data-stu-id="87ada-210">Microsoft.Fabric.Powershell.dll--the Service Fabric PowerShell module--is installed automatically when you install the Microsoft Service Fabric MSI.</span></span> <span data-ttu-id="87ada-211">當您開啟 PowerShell 提示字元時，此模組就會自動載入。</span><span class="sxs-lookup"><span data-stu-id="87ada-211">The module is loaded automatically when you open a PowerShell prompt.</span></span>

<span data-ttu-id="87ada-212">教學課程區段：</span><span class="sxs-lookup"><span data-stu-id="87ada-212">Tutorial segments:</span></span>

* [<span data-ttu-id="87ada-213">針對一整體叢集執行動作</span><span class="sxs-lookup"><span data-stu-id="87ada-213">Run an action against a one-box cluster</span></span>](#run-an-action-against-a-one-box-cluster)
* [<span data-ttu-id="87ada-214">針對 Azure 叢集執行動作</span><span class="sxs-lookup"><span data-stu-id="87ada-214">Run an action against an Azure cluster</span></span>](#run-an-action-against-an-azure-cluster)

### <a name="run-an-action-against-a-one-box-cluster"></a><span data-ttu-id="87ada-215">針對一整體叢集執行動作</span><span class="sxs-lookup"><span data-stu-id="87ada-215">Run an action against a one-box cluster</span></span>
<span data-ttu-id="87ada-216">若要針對本機叢集執行 Testability 動作，請先連接到叢集並在系統管理員模式下開啟 PowerShell 提示字元。</span><span class="sxs-lookup"><span data-stu-id="87ada-216">To run a testability action against a local cluster, first connect to the cluster and open the PowerShell prompt in administrator mode.</span></span> <span data-ttu-id="87ada-217">讓我們來看看 **Restart-ServiceFabricNode** 動作。</span><span class="sxs-lookup"><span data-stu-id="87ada-217">Let us look at the **Restart-ServiceFabricNode** action.</span></span>

```powershell
Restart-ServiceFabricNode -NodeName Node1 -CompletionMode DoNotVerify
```

<span data-ttu-id="87ada-218">這裡的 **Restart-ServiceFabricNode** 動作正在名為 "Node1" 的節點上執行。</span><span class="sxs-lookup"><span data-stu-id="87ada-218">Here the action **Restart-ServiceFabricNode** is being run on a node named "Node1".</span></span> <span data-ttu-id="87ada-219">完成模式會指定該動作不需確認 restart-node 的動作是否確實成功。</span><span class="sxs-lookup"><span data-stu-id="87ada-219">The completion mode specifies that it should not verify whether the restart-node action actually succeeded.</span></span> <span data-ttu-id="87ada-220">指定完成模式為 "Verify" 將會讓其確認重新啟動動作是否確實成功。</span><span class="sxs-lookup"><span data-stu-id="87ada-220">Specifying the completion mode as "Verify" will cause it to verify whether the restart action actually succeeded.</span></span> <span data-ttu-id="87ada-221">您可以透過分割區索引鍵及複本種類指定節點名稱，而不是直接指定其名稱，如下所示：</span><span class="sxs-lookup"><span data-stu-id="87ada-221">Instead of directly specifying the node by its name, you can specify it via a partition key and the kind of replica, as follows:</span></span>

```powershell
Restart-ServiceFabricNode -ReplicaKindPrimary  -PartitionKindNamed -PartitionKey Partition3 -CompletionMode Verify
```


```powershell
$connection = "localhost:19000"
$nodeName = "Node1"

Connect-ServiceFabricCluster $connection
Restart-ServiceFabricNode -NodeName $nodeName -CompletionMode DoNotVerify
```

<span data-ttu-id="87ada-222">**Restart-ServiceFabricNode** 應該用來重新啟動叢集中的 Service Fabric 節點。</span><span class="sxs-lookup"><span data-stu-id="87ada-222">**Restart-ServiceFabricNode** should be used to restart a Service Fabric node in a cluster.</span></span> <span data-ttu-id="87ada-223">這會停止 Fabric.exe 處理程序，此程序會重新啟動該節點代管的所有系統服務和使用者服務複本。</span><span class="sxs-lookup"><span data-stu-id="87ada-223">This will stop the Fabric.exe process, which will restart all of the system service and user service replicas hosted on that node.</span></span> <span data-ttu-id="87ada-224">使用此 API 測試您的服務有助於發現容錯復原路徑中的錯誤。</span><span class="sxs-lookup"><span data-stu-id="87ada-224">Using this API to test your service helps uncover bugs along the failover recovery paths.</span></span> <span data-ttu-id="87ada-225">它可協助模擬叢集中節點的失敗案例。</span><span class="sxs-lookup"><span data-stu-id="87ada-225">It helps simulate node failures in the cluster.</span></span>

<span data-ttu-id="87ada-226">下列螢幕擷取畫面顯示 **Restart-ServiceFabricNode** Testability 命令的實際操作。</span><span class="sxs-lookup"><span data-stu-id="87ada-226">The following screenshot shows the **Restart-ServiceFabricNode** testability command in action.</span></span>

![](media/service-fabric-testability-actions/Restart-ServiceFabricNode.png)

<span data-ttu-id="87ada-227">第一個 **Get-ServiceFabricNode** (Service Fabric PowerShell 模組中的 Cmdlet) 的輸出顯示，本機叢集有五個節點：Node.1 至 Node.5。</span><span class="sxs-lookup"><span data-stu-id="87ada-227">The output of the first **Get-ServiceFabricNode** (a cmdlet from the Service Fabric PowerShell module) shows that the local cluster has five nodes: Node.1 to Node.5.</span></span> <span data-ttu-id="87ada-228">在名為 Node.4 的節點上執行 **Restart-ServiceFabricNode** Testability 動作 (Cmdlet) 之後，我們可以看到節點的運作時間已重設。</span><span class="sxs-lookup"><span data-stu-id="87ada-228">After the testability action (cmdlet) **Restart-ServiceFabricNode** is executed on the node, named Node.4, we see that the node's uptime has been reset.</span></span>

### <a name="run-an-action-against-an-azure-cluster"></a><span data-ttu-id="87ada-229">針對 Azure 叢集執行動作</span><span class="sxs-lookup"><span data-stu-id="87ada-229">Run an action against an Azure cluster</span></span>
<span data-ttu-id="87ada-230">針對 Azure 叢集執行 Testability 動作 (使用 PowerShell)，與針對本機叢集執行該動作的方式類似。</span><span class="sxs-lookup"><span data-stu-id="87ada-230">Running a testability action (by using PowerShell) against an Azure cluster is similar to running the action against a local cluster.</span></span> <span data-ttu-id="87ada-231">唯一的差異在於：執行該動作前，您必須先連接至 Azure 叢集，而非連接至本機叢集。</span><span class="sxs-lookup"><span data-stu-id="87ada-231">The only difference is that before you can run the action, instead of connecting to the local cluster, you need to connect to the Azure cluster first.</span></span>

## <a name="running-a-testability-action-using-c35"></a><span data-ttu-id="87ada-232">使用 C&#35; 執行 Testability 動作</span><span class="sxs-lookup"><span data-stu-id="87ada-232">Running a testability action using C&#35;</span></span>
<span data-ttu-id="87ada-233">若要使用 C# 執行 Testability 動作，您必須先使用 FabricClient 連接至叢集。</span><span class="sxs-lookup"><span data-stu-id="87ada-233">To run a testability action by using C#, first you need to connect to the cluster by using FabricClient.</span></span> <span data-ttu-id="87ada-234">接著，取得執行該動作所需的參數。</span><span class="sxs-lookup"><span data-stu-id="87ada-234">Then obtain the parameters needed to run the action.</span></span> <span data-ttu-id="87ada-235">不同的參數可用來執行相同的動作。</span><span class="sxs-lookup"><span data-stu-id="87ada-235">Different parameters can be used to run the same action.</span></span>
<span data-ttu-id="87ada-236">查看 RestartServiceFabricNode 動作時，您會發現執行該動作的一種方式就是，使用叢集中的節點資訊 (節點名稱和節點執行個體識別碼)。</span><span class="sxs-lookup"><span data-stu-id="87ada-236">Looking at the RestartServiceFabricNode action, one way to run it is by using the node information (node name and node instance ID) in the cluster.</span></span>

```csharp
RestartNodeAsync(nodeName, nodeInstanceId, completeMode, operationTimeout, CancellationToken.None)
```

<span data-ttu-id="87ada-237">參數說明：</span><span class="sxs-lookup"><span data-stu-id="87ada-237">Parameter explanation:</span></span>

* <span data-ttu-id="87ada-238">**CompleteMode** 會指定該模式不需確認重新啟動動作是否確實成功。</span><span class="sxs-lookup"><span data-stu-id="87ada-238">**CompleteMode** specifies that the mode should not verify whether the restart action actually succeeded.</span></span> <span data-ttu-id="87ada-239">指定完成模式為 "Verify" 將會讓其確認重新啟動動作是否確實成功。</span><span class="sxs-lookup"><span data-stu-id="87ada-239">Specifying the completion mode as "Verify" will cause it to verify whether the restart action actually succeeded.</span></span>  
* <span data-ttu-id="87ada-240">**OperationTimeout** 會在擲回 TimeoutException 例外狀況前，設定完成作業所需的時間。</span><span class="sxs-lookup"><span data-stu-id="87ada-240">**OperationTimeout** sets the amount of time for the operation to finish before a TimeoutException exception is thrown.</span></span>
* <span data-ttu-id="87ada-241">**CancellationToken** 可讓擱置中的呼叫取消。</span><span class="sxs-lookup"><span data-stu-id="87ada-241">**CancellationToken** enables a pending call to be canceled.</span></span>

<span data-ttu-id="87ada-242">您可以透過分割區索引鍵及複本種類指定節點名稱，而不是直接指定其名稱。</span><span class="sxs-lookup"><span data-stu-id="87ada-242">Instead of directly specifying the node by its name, you can specify it via a partition key and the kind of replica.</span></span>

<span data-ttu-id="87ada-243">如需詳細資訊，請參閱 [PartitionSelector 和 ReplicaSelector](#partition_replica_selector)。</span><span class="sxs-lookup"><span data-stu-id="87ada-243">For further information, see [PartitionSelector and ReplicaSelector](#partition_replica_selector).</span></span>

```csharp
// Add a reference to System.Fabric.Testability.dll and System.Fabric.dll
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
            //Restart the node by using ReplicaSelector
            RestartNodeAsync(clusterConnection, serviceName).Wait();

            //Another way to restart node is by using nodeName and nodeInstanceId
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

## <a name="partitionselector-and-replicaselector"></a><span data-ttu-id="87ada-244">PartitionSelector 和 ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="87ada-244">PartitionSelector and ReplicaSelector</span></span>
### <a name="partitionselector"></a><span data-ttu-id="87ada-245">PartitionSelector</span><span class="sxs-lookup"><span data-stu-id="87ada-245">PartitionSelector</span></span>
<span data-ttu-id="87ada-246">PartitionSelector 是 Testability 中公開的協助程式，可用來選取特定分割區 (可在其中執行任何 Testability 動作)。</span><span class="sxs-lookup"><span data-stu-id="87ada-246">PartitionSelector is a helper exposed in testability and is used to select a specific partition on which to perform any of the testability actions.</span></span> <span data-ttu-id="87ada-247">如果已事先知道分割區識別碼，就能將其用於選取特定分割區。</span><span class="sxs-lookup"><span data-stu-id="87ada-247">It can be used to select a specific partition if the partition ID is known beforehand.</span></span> <span data-ttu-id="87ada-248">或者，您可以提供分割區索引鍵，作業就會在內部解析分割區識別碼。</span><span class="sxs-lookup"><span data-stu-id="87ada-248">Or, you can provide the partition key and the operation will resolve the partition ID internally.</span></span> <span data-ttu-id="87ada-249">您也可以選擇選取隨機分割區。</span><span class="sxs-lookup"><span data-stu-id="87ada-249">You also have the option of selecting a random partition.</span></span>

<span data-ttu-id="87ada-250">若要使用此協助程式，請建立 PartitionSelector 物件並使用其中一種 Select* 方法來選取分割區。</span><span class="sxs-lookup"><span data-stu-id="87ada-250">To use this helper, create the PartitionSelector object and select the partition by using one of the Select* methods.</span></span> <span data-ttu-id="87ada-251">接著將 PartitionSelector 物件傳遞至有需求的 API。</span><span class="sxs-lookup"><span data-stu-id="87ada-251">Then pass in the PartitionSelector object to the API that requires it.</span></span> <span data-ttu-id="87ada-252">如果不選取任何選項，它會預設為隨機分割區。</span><span class="sxs-lookup"><span data-stu-id="87ada-252">If no option is selected, it defaults to a random partition.</span></span>

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

### <a name="replicaselector"></a><span data-ttu-id="87ada-253">ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="87ada-253">ReplicaSelector</span></span>
<span data-ttu-id="87ada-254">PartitionSelector 是 Testability 中公開的協助程式，可用來協助選取複本 (可在其中執行任何 Testability 動作)。</span><span class="sxs-lookup"><span data-stu-id="87ada-254">ReplicaSelector is a helper exposed in testability and is used to help select a replica on which to perform any of the testability actions.</span></span> <span data-ttu-id="87ada-255">如果已事先知道複本識別碼，就能將其用於選取特定複本。</span><span class="sxs-lookup"><span data-stu-id="87ada-255">It can be used to select a specific replica if the replica ID is known beforehand.</span></span> <span data-ttu-id="87ada-256">此外，您也可以選取主要複本或隨機次要複本。</span><span class="sxs-lookup"><span data-stu-id="87ada-256">In addition, you have the option of selecting a primary replica or a random secondary.</span></span> <span data-ttu-id="87ada-257">ReplicaSelector 衍生自 PartitionSelector，因此您必須同時選取複本和分割區，以便在其中執行您想要的 Testability 作業。</span><span class="sxs-lookup"><span data-stu-id="87ada-257">ReplicaSelector derives from PartitionSelector, so you need to select both the replica and the partition on which you wish to perform the testability operation.</span></span>

<span data-ttu-id="87ada-258">若要使用此協助程式，請建立 ReplicatorSelector 物件，並設定您想選取複本和分割區的方式。</span><span class="sxs-lookup"><span data-stu-id="87ada-258">To use this helper, create a ReplicaSelector object and set the way you want to select the replica and the partition.</span></span> <span data-ttu-id="87ada-259">接著可以將其傳遞至有需求的 API。</span><span class="sxs-lookup"><span data-stu-id="87ada-259">You can then pass it into the API that requires it.</span></span> <span data-ttu-id="87ada-260">如果不選取任何選項，它會預設為隨機複本和隨機分割區。</span><span class="sxs-lookup"><span data-stu-id="87ada-260">If no option is selected, it defaults to a random replica and random partition.</span></span>

```csharp
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);
long replicaId = 130559876481875498;

// Select a random replica
ReplicaSelector randomReplicaSelector = ReplicaSelector.RandomOf(partitionSelector);

// Select the primary replica
ReplicaSelector primaryReplicaSelector = ReplicaSelector.PrimaryOf(partitionSelector);

// Select the replica by ID
ReplicaSelector replicaByIdSelector = ReplicaSelector.ReplicaIdOf(partitionSelector, replicaId);

// Select a random secondary replica
ReplicaSelector secondaryReplicaSelector = ReplicaSelector.RandomSecondaryOf(partitionSelector);
```

## <a name="next-steps"></a><span data-ttu-id="87ada-261">後續步驟</span><span class="sxs-lookup"><span data-stu-id="87ada-261">Next steps</span></span>
* [<span data-ttu-id="87ada-262">Testability 案例</span><span class="sxs-lookup"><span data-stu-id="87ada-262">Testability scenarios</span></span>](service-fabric-testability-scenarios.md)
* <span data-ttu-id="87ada-263">如何測試您的服務</span><span class="sxs-lookup"><span data-stu-id="87ada-263">How to test your service</span></span>
  * [<span data-ttu-id="87ada-264">模擬服務工作負載期間的失敗案例</span><span class="sxs-lookup"><span data-stu-id="87ada-264">Simulate failures during service workloads</span></span>](service-fabric-testability-workload-tests.md)
  * [<span data-ttu-id="87ada-265">服務對服務間通訊的失敗案例</span><span class="sxs-lookup"><span data-stu-id="87ada-265">Service-to-service communication failures</span></span>](service-fabric-testability-scenarios-service-communication.md)

