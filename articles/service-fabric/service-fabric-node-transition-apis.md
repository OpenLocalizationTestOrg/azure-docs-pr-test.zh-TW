---
title: "啟動和停止叢集節點以測試 Azure 微服務 | Microsoft Docs"
description: "了解如何使用錯誤插入，藉由啟動和停止叢集節點的方式，測試 Service Fabric 應用程式。"
services: service-fabric
documentationcenter: .net
author: LMWF
manager: rsinha
editor: 
ms.assetid: f4e70f6f-cad9-4a3e-9655-009b4db09c6d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/12/2017
ms.author: lemai
ms.openlocfilehash: 850fbc0c74811ec942292da64064dec867cd1b9e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="replacing-the-start-node-and-stop-node-apis-with-the-node-transition-api"></a><span data-ttu-id="9da45-103">以節點轉換 API 取代啟動節點和停止節點 API</span><span class="sxs-lookup"><span data-stu-id="9da45-103">Replacing the Start Node and Stop node APIs with the Node Transition API</span></span>

## <a name="what-do-the-stop-node-and-start-node-apis-do"></a><span data-ttu-id="9da45-104">啟動節點和停止節點 API 有什麼功用？</span><span class="sxs-lookup"><span data-stu-id="9da45-104">What do the Stop Node and Start Node APIs do?</span></span>

<span data-ttu-id="9da45-105">停止節點 API (受管理︰[StopNodeAsync()][stopnode]、PowerShell：[Stop-ServiceFabricNode][stopnodeps]) 會停止 Service Fabric 節點。</span><span class="sxs-lookup"><span data-stu-id="9da45-105">The Stop Node API (managed: [StopNodeAsync()][stopnode], PowerShell: [Stop-ServiceFabricNode][stopnodeps]) stops a Service Fabric node.</span></span>  <span data-ttu-id="9da45-106">Service Fabric 節點是處理序，不是 VM 或機器 – VM 或機器仍將繼續執行。</span><span class="sxs-lookup"><span data-stu-id="9da45-106">A Service Fabric node is process, not a VM or machine – the VM or machine will still be running.</span></span>  <span data-ttu-id="9da45-107">在文件的其餘部分，「節點」是指 Service Fabric 節點。</span><span class="sxs-lookup"><span data-stu-id="9da45-107">For the rest of the document "node" will mean Service Fabric node.</span></span>  <span data-ttu-id="9da45-108">停止節點時是將其放入「停止」狀態，此時節點不是叢集的成員，無法裝載服務，因此就像是個「關閉」的節點。</span><span class="sxs-lookup"><span data-stu-id="9da45-108">Stopping a node puts it into a *stopped* state where it is not a member of the cluster and cannot host services, thus simulating a *down* node.</span></span>  <span data-ttu-id="9da45-109">在將錯誤插入系統以測試應用程式系統時，這非常有用。</span><span class="sxs-lookup"><span data-stu-id="9da45-109">This is useful for injecting faults into the system to test your application.</span></span>  <span data-ttu-id="9da45-110">啟動節點 API (受管理︰ [StartNodeAsync()][startnode]、PowerShell：[Start-ServiceFabricNode][startnodeps]) 會反轉停止節點 API，將節點帶回一般狀態。</span><span class="sxs-lookup"><span data-stu-id="9da45-110">The Start Node API (managed: [StartNodeAsync()][startnode], PowerShell: [Start-ServiceFabricNode][startnodeps]]) reverses the Stop Node API,  which brings the node back to a normal state.</span></span>

## <a name="why-are-we-replacing-these"></a><span data-ttu-id="9da45-111">為什麼要取代它們？</span><span class="sxs-lookup"><span data-stu-id="9da45-111">Why are we replacing these?</span></span>

<span data-ttu-id="9da45-112">如先前所述，「停止」的 Service Fabric 節點是使用停止節點 API 刻意鎖定目標的節點。</span><span class="sxs-lookup"><span data-stu-id="9da45-112">As described earlier, a *stopped* Service Fabric node is a node intentionally targeted using the Stop Node API.</span></span>  <span data-ttu-id="9da45-113">「關閉」節點是基於其他因素 (例如 VM 或機器已關閉) 而關閉的節點。</span><span class="sxs-lookup"><span data-stu-id="9da45-113">A *down* node is a node that is down for any other reason (e.g. the VM or machine is off).</span></span>  <span data-ttu-id="9da45-114">使用停止節點 API 時，系統不會公開資訊，您無法區分「停止」節點和「關閉」節點。</span><span class="sxs-lookup"><span data-stu-id="9da45-114">With the Stop Node API, the system does not expose information to differentiate between *stopped* nodes and *down* nodes.</span></span>

<span data-ttu-id="9da45-115">此外，這些 API 傳回的某些錯誤的描述不明確。</span><span class="sxs-lookup"><span data-stu-id="9da45-115">In addition, some errors returned by these APIs are not as descriptive as they could be.</span></span>  <span data-ttu-id="9da45-116">例如，在已經「停止」的節點上叫用停止節點 API 會傳回 *InvalidAddress* 錯誤。</span><span class="sxs-lookup"><span data-stu-id="9da45-116">For example, invoking the Stop Node API on an already *stopped* node will return the error *InvalidAddress*.</span></span>  <span data-ttu-id="9da45-117">這種經驗可以改善。</span><span class="sxs-lookup"><span data-stu-id="9da45-117">This experience could be improved.</span></span>

<span data-ttu-id="9da45-118">此外，節點停止的持續時間是「無限期」，直到 Start Node API 被叫用。</span><span class="sxs-lookup"><span data-stu-id="9da45-118">Also, the duration a node is stopped for is “infinite” until the Start Node API is invoked.</span></span>  <span data-ttu-id="9da45-119">我們發現這可能會造成問題，比較容易出錯。</span><span class="sxs-lookup"><span data-stu-id="9da45-119">We’ve found this can cause problems and may be error-prone.</span></span>  <span data-ttu-id="9da45-120">例如，我們已經看到使用者在節點叫用停止節點 API 之後將它忘得一乾二淨的問題。</span><span class="sxs-lookup"><span data-stu-id="9da45-120">For example, we’ve seen problems where a user invoked the Stop Node API on a node and then forgot about it.</span></span>  <span data-ttu-id="9da45-121">之後，將無從得知它是「關閉」或「停止」節點。</span><span class="sxs-lookup"><span data-stu-id="9da45-121">Later, it was unclear if the node was *down* or *stopped*.</span></span>


## <a name="introducing-the-node-transition-apis"></a><span data-ttu-id="9da45-122">節點轉換 API 簡介</span><span class="sxs-lookup"><span data-stu-id="9da45-122">Introducing the Node Transition APIs</span></span>

<span data-ttu-id="9da45-123">我們已經用一組新的 API 解決上述問題。</span><span class="sxs-lookup"><span data-stu-id="9da45-123">We’ve addressed these issues above in a new set of APIs.</span></span>  <span data-ttu-id="9da45-124">新的節點轉換 API (受管理︰ [StartNodeTransitionAsync()][snt]) 可用來將 Service Fabric 節點轉換為「停止」狀態，或將它從「停止」狀態轉換為一般狀態。</span><span class="sxs-lookup"><span data-stu-id="9da45-124">The new Node Transition API (managed: [StartNodeTransitionAsync()][snt]) may be used to transition a Service Fabric node to a *stopped* state, or to transition it from a *stopped* state to a normal up state.</span></span>  <span data-ttu-id="9da45-125">請注意，此 API 名稱中的 "Start" 不是啟動節點之意。</span><span class="sxs-lookup"><span data-stu-id="9da45-125">Please note that the “Start” in the name of the API does not refer to starting a node.</span></span>  <span data-ttu-id="9da45-126">是指開始系統將執行、會將節點轉換為「停止」或啟動狀態的非同步作業。</span><span class="sxs-lookup"><span data-stu-id="9da45-126">It refers to beginning an asynchronous operation that the system will execute to transition the node to either *stopped* or started state.</span></span>

<span data-ttu-id="9da45-127">**用法**</span><span class="sxs-lookup"><span data-stu-id="9da45-127">**Usage**</span></span>

<span data-ttu-id="9da45-128">如果節點轉換 API 被呼叫時沒有擲回例外狀況，則系統已接受非同步作業，並將執行它。</span><span class="sxs-lookup"><span data-stu-id="9da45-128">If the Node Transition API does not throw an exception when invoked, then the system has accepted the asynchronous operation, and will execute it.</span></span>  <span data-ttu-id="9da45-129">成功的呼叫並不表示作業完成。</span><span class="sxs-lookup"><span data-stu-id="9da45-129">A successful call does not imply the operation is finished yet.</span></span>  <span data-ttu-id="9da45-130">若要取得作業的目前狀態資訊，請呼叫節點轉換進度 API (受管理︰ [GetNodeTransitionProgressAsync()][gntp])，並搭配此作業叫用節點轉換 API 時使用的 guid。</span><span class="sxs-lookup"><span data-stu-id="9da45-130">To get information about the current state of the operation, call the Node Transition Progress API (managed: [GetNodeTransitionProgressAsync()][gntp]) with the guid used when invoking Node Transition API for this operation.</span></span>  <span data-ttu-id="9da45-131">節點轉換進度 API 會傳回 NodeTransitionProgress 物件。</span><span class="sxs-lookup"><span data-stu-id="9da45-131">The Node Transition Progress API returns an NodeTransitionProgress object.</span></span>  <span data-ttu-id="9da45-132">此物件的 State 屬性會指定作業的目前狀態。</span><span class="sxs-lookup"><span data-stu-id="9da45-132">This object’s State property specifies the current state of the operation.</span></span>  <span data-ttu-id="9da45-133">如果狀態是 "Running"，則作業正在執行。</span><span class="sxs-lookup"><span data-stu-id="9da45-133">If the state is “Running” then the operation is executing.</span></span>  <span data-ttu-id="9da45-134">如果是 "Completed"，則作業完成沒有錯誤。</span><span class="sxs-lookup"><span data-stu-id="9da45-134">If it is Completed, the operation finished without error.</span></span>  <span data-ttu-id="9da45-135">如果是 "Faulted"，則表示執行作業發生問題。</span><span class="sxs-lookup"><span data-stu-id="9da45-135">If it is Faulted, there was a problem executing the operation.</span></span>  <span data-ttu-id="9da45-136">Result 屬性的 Exception 屬性會指出問題為何。</span><span class="sxs-lookup"><span data-stu-id="9da45-136">The Result property’s Exception property will indicate what the issue was.</span></span>  <span data-ttu-id="9da45-137">請參閱 https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate 了解 State 屬性的相關資訊，以及之後的「範例用法」一節中的程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="9da45-137">See https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate for more information about the State property, and the “Sample Usage” section below for code examples.</span></span>


<span data-ttu-id="9da45-138">**區分停止節點和關閉節點** 如果是使用節點轉換 API「停止」 節點，節點查詢的輸出 (受管理：[GetNodeListAsync()][nodequery]、PowerShell：[Get-ServiceFabricNode][nodequeryps]) 將顯示此節點的 IsStopped 屬性值為 true。</span><span class="sxs-lookup"><span data-stu-id="9da45-138">**Differentiating between a stopped node and a down node** If a node is *stopped* using the Node Transition API, the output of a node query (managed: [GetNodeListAsync()][nodequery], PowerShell: [Get-ServiceFabricNode][nodequeryps]) will show that this node has an *IsStopped* property value of true.</span></span>  <span data-ttu-id="9da45-139">請注意，這和 NodeStatus屬性的值 (Down) 不同。</span><span class="sxs-lookup"><span data-stu-id="9da45-139">Note this is different from the value of the *NodeStatus* property, which will say *Down*.</span></span>  <span data-ttu-id="9da45-140">如果 NodeStatus屬性的值為 Down，但 IsStopped 為 false，則節點並非使用節點轉換 API 停止，而是因其他原因而「關閉」。</span><span class="sxs-lookup"><span data-stu-id="9da45-140">If the *NodeStatus* property has a value of *Down*, but *IsStopped* is false, then the node was not stopped using the Node Transition API, and is *Down* due some other reason.</span></span>  <span data-ttu-id="9da45-141">如果 IsStopped屬性為 true，而NodeStatus 屬性為 Down，則是使用節點轉換 API 停止節點。</span><span class="sxs-lookup"><span data-stu-id="9da45-141">If the *IsStopped* property is true, and the *NodeStatus* property is *Down*, then it was stopped using the Node Transition API.</span></span>

<span data-ttu-id="9da45-142">使用節點轉換 API 啟動「停止」節點會將它恢復運作，再次成為叢集的一般成員。</span><span class="sxs-lookup"><span data-stu-id="9da45-142">Starting a *stopped* node using the Node Transition API will return it to function as a normal member of the cluster again.</span></span>  <span data-ttu-id="9da45-143">節點查詢 API 的輸出會顯示IsStopped 是 false，而 NodeStatus 是 Down 以外的值 (例如 Up)。</span><span class="sxs-lookup"><span data-stu-id="9da45-143">The output of the node query API will show *IsStopped* as false, and *NodeStatus* as something that is not Down (e.g. Up).</span></span>


<span data-ttu-id="9da45-144">**有限的持續時間** 使用節點轉換 API停止節點時，其中一個必要參數 stopNodeDurationInSeconds 表示該節點要保持「停止」的時間，單位為秒。</span><span class="sxs-lookup"><span data-stu-id="9da45-144">**Limited Duration** When using the Node Transition API to stop a node, one of the required parameters, *stopNodeDurationInSeconds*, represents the amount of time in seconds to keep the node *stopped*.</span></span>  <span data-ttu-id="9da45-145">這個值必須在允許範圍內，最低 600，最高 14400。</span><span class="sxs-lookup"><span data-stu-id="9da45-145">This value must be in the allowed range, which has a minimum of 600, and a maximum of 14400.</span></span>  <span data-ttu-id="9da45-146">此時間過期之後，節點本身會自動重新啟動到 Up 狀態。</span><span class="sxs-lookup"><span data-stu-id="9da45-146">After this time expires, the node will restart itself into Up state automatically.</span></span>  <span data-ttu-id="9da45-147">請參閱以下範例 1 的範例用法。</span><span class="sxs-lookup"><span data-stu-id="9da45-147">Refer to Sample 1 below for an example of usage.</span></span>

> [!WARNING]
> <span data-ttu-id="9da45-148">避免混用節點轉換 API 和啟動節點、停止節點 API。</span><span class="sxs-lookup"><span data-stu-id="9da45-148">Avoid mixing Node Transition APIs and the Stop Node and Start Node APIs.</span></span>  <span data-ttu-id="9da45-149">建議只使用節點轉換 API。</span><span class="sxs-lookup"><span data-stu-id="9da45-149">The recommendation is to  use the Node Transition API only.</span></span>  <span data-ttu-id="9da45-150">> 如果已經使用停止節點 API 停止節點，則應該先使用啟動節點 API 啟動它，再使用 > 節點轉換 API。</span><span class="sxs-lookup"><span data-stu-id="9da45-150">> If a node has been already been stopped using the Stop Node API, it should be started using the Start Node API first before using the > Node Transition APIs.</span></span>

> [!WARNING]
> <span data-ttu-id="9da45-151">在相同節點上無法平行呼叫多個節點轉換 API。</span><span class="sxs-lookup"><span data-stu-id="9da45-151">Multiple Node Transition APIs calls cannot be made on the same node in parallel.</span></span>  <span data-ttu-id="9da45-152">在這種情況下，節點轉換 API 將   > 擲回 FabricException，其 ErrorCode 屬性的值為 NodeTransitionInProgress。</span><span class="sxs-lookup"><span data-stu-id="9da45-152">In such a situation, the Node Transition API will    > throw a FabricException with an ErrorCode property value of NodeTransitionInProgress.</span></span>  <span data-ttu-id="9da45-153">一旦特定節點的節點轉換  > 已經開始，您應該等到作業到達終止狀態 (Completed、Faulted 或 ForceCancelled)，才開始  > 對同一節點進行新的轉換。</span><span class="sxs-lookup"><span data-stu-id="9da45-153">Once a node transition on a specific node has  > been started, you should wait until the operation reaches a terminal state (Completed, Faulted, or ForceCancelled) before starting a  > new transition on the same node.</span></span>  <span data-ttu-id="9da45-154">允許在不同節點上平行呼叫節點轉換。</span><span class="sxs-lookup"><span data-stu-id="9da45-154">Parallel node transition calls on different nodes are allowed.</span></span>


#### <a name="sample-usage"></a><span data-ttu-id="9da45-155">範例用法</span><span class="sxs-lookup"><span data-stu-id="9da45-155">Sample Usage</span></span>


<span data-ttu-id="9da45-156">**範例 1** - 下列範例會使用節點轉換 API 來停止節點。</span><span class="sxs-lookup"><span data-stu-id="9da45-156">**Sample 1** - The following sample uses the Node Transition API to stop a node.</span></span>

```csharp
        // Helper function to get information about a node
        static Node GetNodeInfo(FabricClient fc, string node)
        {
            NodeList n = null;
            while (n == null)
            {
                n = fc.QueryManager.GetNodeListAsync(node).GetAwaiter().GetResult();
                Task.Delay(TimeSpan.FromSeconds(1)).GetAwaiter();
            };

            return n.FirstOrDefault();
        }

        static async Task WaitForStateAsync(FabricClient fc, Guid operationId, TestCommandProgressState targetState)
        {
            NodeTransitionProgress progress = null;

            do
            {
                bool exceptionObserved = false;
                try
                {
                    progress = await fc.TestManager.GetNodeTransitionProgressAsync(operationId, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                    exceptionObserved = true;
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                    exceptionObserved = true;
                }

                if (!exceptionObserved)
                {
                    Console.WriteLine("Current state of operation '{0}': {1}", operationId, progress.State);

                    if (progress.State == TestCommandProgressState.Faulted)
                    {
                        // Inspect the progress object's Result.Exception.HResult to get the error code.
                        Console.WriteLine("'{0}' failed with: {1}, HResult: {2}", operationId, progress.Result.Exception, progress.Result.Exception.HResult);

                        // ...additional logic as required
                    }

                    if (progress.State == targetState)
                    {
                        Console.WriteLine("Target state '{0}' has been reached", targetState);
                        break;
                    }
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);
            }
            while (true);
        }

        static async Task StopNodeAsync(FabricClient fc, string nodeName, int durationInSeconds)
        {
            // Uses the GetNodeListAsync() API to get information about the target node
            Node n = GetNodeInfo(fc, nodeName);

            // Create a Guid
            Guid guid = Guid.NewGuid();

            // Create a NodeStopDescription object, which will be used as a parameter into StartNodeTransition
            NodeStopDescription description = new NodeStopDescription(guid, n.NodeName, n.NodeInstanceId, durationInSeconds);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with the NodeStopDescription from above, which will stop the target node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    // This is retryable
                }
                catch (FabricTransientException fte)
                {
                    // This is retryable
                }

                // Backoff
                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);
            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hte desired state is reached.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Completed).ConfigureAwait(false);
        }
```

<span data-ttu-id="9da45-157">**範例 2** - 下列範例會啟動「停止」節點。</span><span class="sxs-lookup"><span data-stu-id="9da45-157">**Sample 2** - The following sample starts a *stopped* node.</span></span>  <span data-ttu-id="9da45-158">它會使用第一個範例中的一些協助程式方法。</span><span class="sxs-lookup"><span data-stu-id="9da45-158">It uses some helper methods from the first sample.</span></span>

```csharp
        static async Task StartNodeAsync(FabricClient fc, string nodeName)
        {
            // Uses the GetNodeListAsync() API to get information about the target node
            Node n = GetNodeInfo(fc, nodeName);

            Guid guid = Guid.NewGuid();
            BigInteger nodeInstanceId = n.NodeInstanceId;

            // Create a NodeStartDescription object, which will be used as a parameter into StartNodeTransition
            NodeStartDescription description = new NodeStartDescription(guid, n.NodeName, nodeInstanceId);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with the NodeStartDescription from above, which will start the target stopped node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);

            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hte desired state is reached.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Completed).ConfigureAwait(false);
        }
```

<span data-ttu-id="9da45-159">**範例 3** - 下列範例示範錯誤用法。</span><span class="sxs-lookup"><span data-stu-id="9da45-159">**Sample 3** - The following sample shows incorrect usage.</span></span>  <span data-ttu-id="9da45-160">這種用法不正確，是因為它提供的 stopDurationInSeconds 大於允許的範圍。</span><span class="sxs-lookup"><span data-stu-id="9da45-160">This usage is incorrect because the *stopDurationInSeconds* it provides is greater than the allowed range.</span></span>  <span data-ttu-id="9da45-161">由於 StartNodeTransitionAsync() 將會失敗並發生嚴重錯誤，作業將不被接受，應該不會呼叫進度 API。</span><span class="sxs-lookup"><span data-stu-id="9da45-161">Since StartNodeTransitionAsync() will fail with a fatal error, the operation was not accepted, and the progress API should not be called.</span></span>  <span data-ttu-id="9da45-162">這個範例會使用第一個範例中的一些協助程式方法。</span><span class="sxs-lookup"><span data-stu-id="9da45-162">This sample uses some helper methods from the first sample.</span></span>

```csharp
        static async Task StopNodeWithOutOfRangeDurationAsync(FabricClient fc, string nodeName)
        {
            Node n = GetNodeInfo(fc, nodeName);

            Guid guid = Guid.NewGuid();

            // Use an out of range value for stopDurationInSeconds to demonstrate error
            NodeStopDescription description = new NodeStopDescription(guid, n.NodeName, n.NodeInstanceId, 99999);

            try
            {
                await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
            }

            catch (FabricException e)
            {
                Console.WriteLine("Caught {0}", e);
                Console.WriteLine("ErrorCode {0}", e.ErrorCode);
                // Output:
                // Caught System.Fabric.FabricException: System.Runtime.InteropServices.COMException (-2147017629)
                // StopDurationInSeconds is out of range ---> System.Runtime.InteropServices.COMException: Exception from HRESULT: 0x80071C63
                // << Parts of exception omitted>>
                //
                // ErrorCode InvalidDuration
            }
        }
```

<span data-ttu-id="9da45-163">**範例 4** - 下列範例示範當節點轉換 API 所起始的作業被接受，但在稍後執行失敗時，節點轉換進度 API 傳回的錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="9da45-163">**Sample 4** - The following sample shows the error information that will be returned from the Node Transition Progress API when the operation initiated by the Node Transition API is accepted, but fails later while executing.</span></span>  <span data-ttu-id="9da45-164">在此狀況中，失敗是因為節點轉換 API 嘗試啟動不存在的節點。</span><span class="sxs-lookup"><span data-stu-id="9da45-164">In the case, it fails because the Node Transition API attempts to start a node that does not exist.</span></span>  <span data-ttu-id="9da45-165">這個範例會使用第一個範例中的一些協助程式方法。</span><span class="sxs-lookup"><span data-stu-id="9da45-165">This sample uses some helper methods from the first sample.</span></span>

```csharp
        static async Task StartNodeWithNonexistentNodeAsync(FabricClient fc)
        {
            Guid guid = Guid.NewGuid();
            BigInteger nodeInstanceId = 12345;

            // Intentionally use a nonexistent node
            NodeStartDescription description = new NodeStartDescription(guid, "NonexistentNode", nodeInstanceId);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with the NodeStartDescription from above, which will start the target stopped node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);

            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until the desired state is reached.  In this case, it will end up in the Faulted state since the node does not exist.
            // When StartNodeTransitionProgressAsync()'s returned progress object has a State if Faulted, inspect the progress object's Result.Exception.HResult to get the error code.
            // In this case, it will be NodeNotFound.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Faulted).ConfigureAwait(false);
        }
```

[stopnode]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.faultmanagementclient?redirectedfrom=MSDN#System_Fabric_FabricClient_FaultManagementClient_StopNodeAsync_System_String_System_Numerics_BigInteger_System_Fabric_CompletionMode_
[stopnodeps]: https://msdn.microsoft.com/library/mt125982.aspx
[startnode]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.faultmanagementclient?redirectedfrom=MSDN#System_Fabric_FabricClient_FaultManagementClient_StartNodeAsync_System_String_System_Numerics_BigInteger_System_String_System_Int32_System_Fabric_CompletionMode_System_Threading_CancellationToken_
[startnodeps]: https://msdn.microsoft.com/library/mt163520.aspx
[nodequery]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient#System_Fabric_FabricClient_QueryClient_GetNodeListAsync_System_String_
[nodequeryps]: https://docs.microsoft.com/powershell/servicefabric/vlatest/Get-ServiceFabricNode?redirectedfrom=msdn
[snt]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.testmanagementclient#System_Fabric_FabricClient_TestManagementClient_StartNodeTransitionAsync_System_Fabric_Description_NodeTransitionDescription_System_TimeSpan_System_Threading_CancellationToken_
[gntp]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.testmanagementclient#System_Fabric_FabricClient_TestManagementClient_GetNodeTransitionProgressAsync_System_Guid_System_TimeSpan_System_Threading_CancellationToken_
