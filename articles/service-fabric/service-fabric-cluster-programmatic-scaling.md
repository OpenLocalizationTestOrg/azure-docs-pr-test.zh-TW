---
title: "Azure Service Fabric 程式設計調整 | Microsoft Docs"
description: "以程式設計方式根據自訂觸發程序相應縮小或放大 Azure Service Fabric 叢集"
services: service-fabric
documentationcenter: .net
author: mjrousos
manager: jonjung
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: mikerou
ms.openlocfilehash: 46b0b62f92abbac57bc27bbcdd5821eafedf5519
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="scale-a-service-fabric-cluster-programmatically"></a><span data-ttu-id="842d3-103">以程式設計方式調整 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="842d3-103">Scale a Service Fabric cluster programmatically</span></span> 

<span data-ttu-id="842d3-104">在關於[叢集調整](./service-fabric-cluster-scale-up-down.md)的文件中探討了 Azure Service Fabric 叢集調整的基本概念。</span><span class="sxs-lookup"><span data-stu-id="842d3-104">Fundamentals of scaling a Service Fabric cluster in Azure are covered in documentation on [cluster scaling](./service-fabric-cluster-scale-up-down.md).</span></span> <span data-ttu-id="842d3-105">該文章探討如何以虛擬機器擴展集為基礎來建置 Service Fabric 叢集，以及如何以手動方式或自動調整規則來加以調整。</span><span class="sxs-lookup"><span data-stu-id="842d3-105">That article covers how Service Fabric clusters are built on top of virtual machine scale sets and can be scaled either manually or with auto-scale rules.</span></span> <span data-ttu-id="842d3-106">本文件則探討如何以程式設計方法讓 Azure 調整作業能夠配合更進階的案例。</span><span class="sxs-lookup"><span data-stu-id="842d3-106">This document looks at programmatic methods of coordinating Azure scaling operations for more advanced scenarios.</span></span> 

## <a name="reasons-for-programmatic-scaling"></a><span data-ttu-id="842d3-107">以程式設計方式調整的原因</span><span class="sxs-lookup"><span data-stu-id="842d3-107">Reasons for programmatic scaling</span></span>
<span data-ttu-id="842d3-108">在許多案例中，以手動方式或透過自動調整規則來調整是不錯的解決方案。</span><span class="sxs-lookup"><span data-stu-id="842d3-108">In many scenarios, scaling manually or via auto-scale rules are good solutions.</span></span> <span data-ttu-id="842d3-109">但在其他案例中，可能就不合適。</span><span class="sxs-lookup"><span data-stu-id="842d3-109">In other scenarios, though, they may not be the right fit.</span></span> <span data-ttu-id="842d3-110">這些方法的可能缺點包括︰</span><span class="sxs-lookup"><span data-stu-id="842d3-110">Potential drawbacks to these approaches include:</span></span>

- <span data-ttu-id="842d3-111">手動調整需要登入系統，並明確地要求調整作業。</span><span class="sxs-lookup"><span data-stu-id="842d3-111">Manually scaling requires you to log in and explicitly request scaling operations.</span></span> <span data-ttu-id="842d3-112">如果調整作業需要經常進行或難以預料會在何時進行，這個方法可能就不是合適的解決方案。</span><span class="sxs-lookup"><span data-stu-id="842d3-112">If scaling operations are required frequently or at unpredictable times, this approach may not be a good solution.</span></span>
- <span data-ttu-id="842d3-113">自動調整規則在從虛擬機器擴展集內移除執行個體時，並不會自動從相關聯的 Service Fabric 叢集移除對於該節點的認識，除非該節點類型的持久性等級為銀級或金級。</span><span class="sxs-lookup"><span data-stu-id="842d3-113">When auto-scale rules remove an instance from a virtual machine scale set, they do not automatically remove knowledge of that node from the associated Service Fabric cluster unless the node type has a durability level of Silver or Gold.</span></span> <span data-ttu-id="842d3-114">自動調整規則會作用在擴展集層級 (而非 Service Fabric 層級)，所以自動調整規則會直接移除 Service Fabric 節點，而未將其正常關閉。</span><span class="sxs-lookup"><span data-stu-id="842d3-114">Because auto-scale rules work at the scale set level (rather than at the Service Fabric level), auto-scale rules can remove Service Fabric nodes without shutting them down gracefully.</span></span> <span data-ttu-id="842d3-115">以這種方式粗糙地移除節點，會在相應縮小作業完成後留下「準刪除」的 Service Fabric 節點狀態。</span><span class="sxs-lookup"><span data-stu-id="842d3-115">This rude node removal will leave 'ghost' Service Fabric node state behind after scale-in operations.</span></span> <span data-ttu-id="842d3-116">個人 (或服務) 必須定期清除 Service Fabric 叢集中的已移除節點狀態。</span><span class="sxs-lookup"><span data-stu-id="842d3-116">An individual (or a service) would need to periodically clean up removed node state in the Service Fabric cluster.</span></span>
  - <span data-ttu-id="842d3-117">請注意，持久性等級為金級或銀級的節點類型會自動清除已移除的節點。</span><span class="sxs-lookup"><span data-stu-id="842d3-117">Note that a node type with a durability level of Gold or Silver will automatically clean up removed nodes.</span></span>  
- <span data-ttu-id="842d3-118">雖然自動調整規則支援[許多計量](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md)，但這組計量的數量仍然有限。</span><span class="sxs-lookup"><span data-stu-id="842d3-118">Although there are [many metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) supported by auto-scale rules, it is still a limited set.</span></span> <span data-ttu-id="842d3-119">如果您的案例所需要的調整是以該組計量所未涵蓋的一些計量為基礎，則自動調整規則可能不是很好的選擇。</span><span class="sxs-lookup"><span data-stu-id="842d3-119">If your scenario calls for scaling based on some metric not covered in that set, then auto-scale rules may not be a good option.</span></span>

<span data-ttu-id="842d3-120">根據這些限制，您可能會想要實作自訂能力更大的自動調整模型。</span><span class="sxs-lookup"><span data-stu-id="842d3-120">Based on these limitations, you may wish to implement more customized automatic scaling models.</span></span> 

## <a name="scaling-apis"></a><span data-ttu-id="842d3-121">調整 API</span><span class="sxs-lookup"><span data-stu-id="842d3-121">Scaling APIs</span></span>
<span data-ttu-id="842d3-122">Azure API 的存在可讓應用程式以程式設計方式使用虛擬機器擴展集和 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="842d3-122">Azure APIs exist which allow applications to programmatically work with virtual machine scale sets and Service Fabric clusters.</span></span> <span data-ttu-id="842d3-123">如果現有自動調整選項不適用於您的案例，這些 API 可讓您實作自訂調整邏輯。</span><span class="sxs-lookup"><span data-stu-id="842d3-123">If existing auto-scale options don't work for your scenario, these APIs make it possible to implement custom scaling logic.</span></span> 

<span data-ttu-id="842d3-124">若要實作此「自製」自動調整功能，有一個方法是將新的無狀態服務新增至 Service Fabric 應用程式以管理調整作業。</span><span class="sxs-lookup"><span data-stu-id="842d3-124">One approach to implementing this 'home-made' auto-scaling functionality is to add a new stateless service to the Service Fabric application to manage scaling operations.</span></span> <span data-ttu-id="842d3-125">在服務的 `RunAsync` 方法內，有一組觸發程序可以判斷是否需要調整 (包括檢查最大叢集大小和調整冷卻等參數)。</span><span class="sxs-lookup"><span data-stu-id="842d3-125">Within the service's `RunAsync` method, a set of triggers can determine if scaling is required (including checking parameters such as maximum cluster size and scaling cooldowns).</span></span>   

<span data-ttu-id="842d3-126">用於虛擬機器擴展集互動 (檢查目前的虛擬機器執行個體數目並加以修改) 的 API 是 [Fluent Azure 管理計算程式庫](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/)。</span><span class="sxs-lookup"><span data-stu-id="842d3-126">The API used for virtual machine scale set interactions (both to check the current number of virtual machine instances and to modify it) is the [fluent Azure Management Compute library](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/).</span></span> <span data-ttu-id="842d3-127">Fluent 計算程式庫可提供方便使用的 API 來與虛擬機器擴展集互動。</span><span class="sxs-lookup"><span data-stu-id="842d3-127">The fluent compute library provides an easy-to-use API for interacting with virtual machine scale sets.</span></span>

<span data-ttu-id="842d3-128">若要與 Service Fabric 叢集本身互動，請使用 [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient)。</span><span class="sxs-lookup"><span data-stu-id="842d3-128">To interact with the Service Fabric cluster itself, use [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span></span>

<span data-ttu-id="842d3-129">當然，調整程式碼不需要以服務的形式在想要調整的叢集中執行。</span><span class="sxs-lookup"><span data-stu-id="842d3-129">Of course, the scaling code doesn't need to run as a service in the cluster to be scaled.</span></span> <span data-ttu-id="842d3-130">`IAzure` 和 `FabricClient` 都能遠端連線到其相關聯的 Azure 資源，因此，調整服務可以輕鬆地成為主控台應用程式或從 Service Fabric 應用程式外部執行的 Windows 服務。</span><span class="sxs-lookup"><span data-stu-id="842d3-130">Both `IAzure` and `FabricClient` can connect to their associated Azure resources remotely, so the scaling service could easily be a console application or Windows service running from outside the Service Fabric application.</span></span> 

## <a name="credential-management"></a><span data-ttu-id="842d3-131">認證管理</span><span class="sxs-lookup"><span data-stu-id="842d3-131">Credential management</span></span>
<span data-ttu-id="842d3-132">撰寫服務來處理調整的其中一項挑戰是，服務必須能夠不經互動式登入程序就存取虛擬機器擴展集資源。</span><span class="sxs-lookup"><span data-stu-id="842d3-132">One challenge of writing a service to handle scaling is that the service must be able to access virtual machine scale set resources without an interactive login.</span></span> <span data-ttu-id="842d3-133">如果調整服務是要修改自己的 Service Fabric 應用程式，存取 Service Fabric 叢集是很容易的事，但需要有認證才能存取擴展集。</span><span class="sxs-lookup"><span data-stu-id="842d3-133">Accessing the Service Fabric cluster is easy if the scaling service is modifying its own Service Fabric application, but credentials are needed to access the scale set.</span></span> <span data-ttu-id="842d3-134">若要登入，您可以使用以 [Azure CLI 2.0](https://github.com/azure/azure-cli) 建立的[服務主體](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure)。</span><span class="sxs-lookup"><span data-stu-id="842d3-134">To log in, you can use a [service principal](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) created with the [Azure CLI 2.0](https://github.com/azure/azure-cli).</span></span>

<span data-ttu-id="842d3-135">您可以透過下列步驟來建立服務主體︰</span><span class="sxs-lookup"><span data-stu-id="842d3-135">A service principal can be created with the following steps:</span></span>

1. <span data-ttu-id="842d3-136">以具有虛擬機器擴展集存取權的使用者身分登入 Azure CLI (`az login`)</span><span class="sxs-lookup"><span data-stu-id="842d3-136">Log in to the Azure CLI (`az login`) as a user with access to the virtual machine scale set</span></span>
2. <span data-ttu-id="842d3-137">使用 `az ad sp create-for-rbac` 建立服務主體</span><span class="sxs-lookup"><span data-stu-id="842d3-137">Create the service principal with `az ad sp create-for-rbac`</span></span>
    1. <span data-ttu-id="842d3-138">記下 appId (在其他地方稱為「用戶端識別碼」)、名稱、密碼及租用戶，以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="842d3-138">Make note of the appId (called 'client ID' elsewhere), name, password, and tenant for later use.</span></span>
    2. <span data-ttu-id="842d3-139">您還需要訂用帳戶識別碼，若要檢視此識別碼，請使用 `az account list`</span><span class="sxs-lookup"><span data-stu-id="842d3-139">You will also need your subscription ID, which can be viewed with `az account list`</span></span>

<span data-ttu-id="842d3-140">Fluent 計算程式庫可以使用這些認證來登入 (請注意，`IAzure` 這類核心 Fluent Azure 類型是在 [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) 套件中)，如下所示：</span><span class="sxs-lookup"><span data-stu-id="842d3-140">The fluent compute library can log in using these credentials as follows (note that core fluent Azure types like `IAzure` are in the [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) package):</span></span>

```C#
var credentials = new AzureCredentials(new ServicePrincipalLoginInformation {
                ClientId = AzureClientId,
                ClientSecret = 
                AzureClientKey }, AzureTenantId, AzureEnvironment.AzureGlobalCloud);
IAzure AzureClient = Azure.Authenticate(credentials).WithSubscription(AzureSubscriptionId);

if (AzureClient?.SubscriptionId == AzureSubscriptionId)
{
    ServiceEventSource.Current.ServiceMessage(Context, "Successfully logged into Azure");
}
else
{
    ServiceEventSource.Current.ServiceMessage(Context, "ERROR: Failed to login to Azure");
}
```

<span data-ttu-id="842d3-141">登入之後，可以透過 `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity` 來查詢擴展集的執行個體計數。</span><span class="sxs-lookup"><span data-stu-id="842d3-141">Once logged in, scale set instance count can be queried via `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span></span>

## <a name="scaling-out"></a><span data-ttu-id="842d3-142">相應放大</span><span class="sxs-lookup"><span data-stu-id="842d3-142">Scaling out</span></span>
<span data-ttu-id="842d3-143">使用 Fluent Azure 計算 SDK 時，只需要幾個呼叫就能將執行個體新增至虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="842d3-143">Using the fluent Azure compute SDK, instances can be added to the virtual machine scale set with just a few calls -</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);
var newCapacity = (int)Math.Min(MaximumNodeCount, scaleSet.Capacity + 1);
scaleSet.Update().WithCapacity(newCapacity).Apply(); 
``` 

<span data-ttu-id="842d3-144">或者，也可以使用 PowerShell Cmdlet 來管理虛擬機器擴展集大小。</span><span class="sxs-lookup"><span data-stu-id="842d3-144">Alternatively, virtual machine scale set size can also be managed with PowerShell cmdlets.</span></span> <span data-ttu-id="842d3-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss) 可以擷取虛擬機器擴展集物件。</span><span class="sxs-lookup"><span data-stu-id="842d3-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss) can retrieve the virtual machine scale set object.</span></span> <span data-ttu-id="842d3-146">目前的容量會儲存在 `.sku.capacity` 屬性中。</span><span class="sxs-lookup"><span data-stu-id="842d3-146">The current capacity will be stored in the `.sku.capacity` property.</span></span> <span data-ttu-id="842d3-147">將容量變更為所需的值之後，便可以使用 [`Update-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) 命令來更新 Azure 中的虛擬機器擴展集。</span><span class="sxs-lookup"><span data-stu-id="842d3-147">After changing the capacity to the desired value, the virtual machine scale set in Azure can be updated with the [`Update-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) command.</span></span>

<span data-ttu-id="842d3-148">和手動新增節點時一樣，若要啟動新的 Service Fabric 節點，您只需要新增擴展集執行個體，因為擴展集範本所含有的擴充功能可自動將新的執行個體加入 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="842d3-148">As when adding a node manually, adding a scale set instance should be all that's needed to start a new Service Fabric node since the scale set template includes extensions to automatically join new instances to the Service Fabric cluster.</span></span> 

## <a name="scaling-in"></a><span data-ttu-id="842d3-149">相應縮小</span><span class="sxs-lookup"><span data-stu-id="842d3-149">Scaling in</span></span>

<span data-ttu-id="842d3-150">相應縮小與相應放大類似。</span><span class="sxs-lookup"><span data-stu-id="842d3-150">Scaling in is similar to scaling out.</span></span> <span data-ttu-id="842d3-151">實際的虛擬機器擴展集變更幾乎完全相同。</span><span class="sxs-lookup"><span data-stu-id="842d3-151">The actual virtual machine scale set changes are practically the same.</span></span> <span data-ttu-id="842d3-152">但就如先前所討論的，Service Fabric 只會自動清除持久性為金級或銀級的已移除節點。</span><span class="sxs-lookup"><span data-stu-id="842d3-152">But, as was discussed previously, Service Fabric only automatically cleans up removed nodes with a durability of Gold or Silver.</span></span> <span data-ttu-id="842d3-153">因此，在銅級持久性的相應縮小案例中，就必須與 Service Fabric 叢集互動，以關閉要移除的節點，然後移除其狀態。</span><span class="sxs-lookup"><span data-stu-id="842d3-153">So, in the Bronze-durability scale-in case, it's necessary to interact with the Service Fabric cluster to shut down the node to be removed and then to remove its state.</span></span>

<span data-ttu-id="842d3-154">關閉節點的準備工作涉及尋找要移除的節點 (最近期新增的節點) 並加以停用。</span><span class="sxs-lookup"><span data-stu-id="842d3-154">Preparing the node for shutdown involves finding the node to be removed (the most recently added node) and deactivating it.</span></span> <span data-ttu-id="842d3-155">對於非種子節點，可以藉由比較 `NodeInstanceId` 來找到較新的節點。</span><span class="sxs-lookup"><span data-stu-id="842d3-155">For non-seed nodes, newer nodes can be found by comparing `NodeInstanceId`.</span></span> 

```C#
using (var client = new FabricClient())
{
    var mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync())
        .Where(n => n.NodeType.Equals(NodeTypeToScale, StringComparison.OrdinalIgnoreCase))
        .Where(n => n.NodeStatus == System.Fabric.Query.NodeStatus.Up)
        .OrderByDescending(n => n.NodeInstanceId)
        .FirstOrDefault();
```

<span data-ttu-id="842d3-156">請注意，種子節點並非一定會遵循較高的執行個體識別碼優先移除的慣例。</span><span class="sxs-lookup"><span data-stu-id="842d3-156">Be aware that *seed* nodes don't seem to always follow the convention that greater instance IDs are removed first.</span></span>

<span data-ttu-id="842d3-157">在找到要移除的節點後，即可使用和稍早相同的 `FabricClient` 執行個體和 `IAzure` 執行個體來加以停用並移除。</span><span class="sxs-lookup"><span data-stu-id="842d3-157">Once the node to be removed is found, it can be deactivated and removed using the same `FabricClient` instance and the `IAzure` instance from earlier.</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);

// Remove the node from the Service Fabric cluster
ServiceEventSource.Current.ServiceMessage(Context, $"Disabling node {mostRecentLiveNode.NodeName}");
await client.ClusterManager.DeactivateNodeAsync(mostRecentLiveNode.NodeName, NodeDeactivationIntent.RemoveNode);

// Wait (up to a timeout) for the node to gracefully shutdown
var timeout = TimeSpan.FromMinutes(5);
var waitStart = DateTime.Now;
while ((mostRecentLiveNode.NodeStatus == System.Fabric.Query.NodeStatus.Up || mostRecentLiveNode.NodeStatus == System.Fabric.Query.NodeStatus.Disabling) &&
        DateTime.Now - waitStart < timeout)
{
    mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync()).FirstOrDefault(n => n.NodeName == mostRecentLiveNode.NodeName);
    await Task.Delay(10 * 1000);
}

// Decrement VMSS capacity
var newCapacity = (int)Math.Max(MinimumNodeCount, scaleSet.Capacity - 1); // Check min count 

scaleSet.Update().WithCapacity(newCapacity).Apply(); 
```

<span data-ttu-id="842d3-158">與相應放大規模時相同，如果偏好使用指令碼處理方法，在這裡也可以使用修改虛擬機器擴展集容量的 PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="842d3-158">As with scaling out, PowerShell cmdlets for modifying virtual machine scale set capacity can also be used here if a scripting approach is preferable.</span></span> <span data-ttu-id="842d3-159">移除虛擬機器執行個體後，就可以移除 Service Fabric 節點狀態。</span><span class="sxs-lookup"><span data-stu-id="842d3-159">Once the virtual machine instance is removed, Service Fabric node state can be removed.</span></span>

```C#
await client.ClusterManager.RemoveNodeStateAsync(mostRecentLiveNode.NodeName);
```

## <a name="potential-drawbacks"></a><span data-ttu-id="842d3-160">可能的缺點</span><span class="sxs-lookup"><span data-stu-id="842d3-160">Potential drawbacks</span></span>

<span data-ttu-id="842d3-161">如前面的程式碼片段所示，建立自己的調整服務就能對應用程式的調整行為握有最高程度的控制力與自訂能力。</span><span class="sxs-lookup"><span data-stu-id="842d3-161">As demonstrated in the preceding code snippets, creating your own scaling service provides the highest degree of control and customizability over your application's scaling behavior.</span></span> <span data-ttu-id="842d3-162">這很適合用於需要精確控制應用程式相應縮小或放大之時機或方式的案例。</span><span class="sxs-lookup"><span data-stu-id="842d3-162">This can be useful for scenarios requiring precise control over when or how an application scales in or out.</span></span> <span data-ttu-id="842d3-163">不過，伴隨此控制能力而來的是程式碼會變得複雜。</span><span class="sxs-lookup"><span data-stu-id="842d3-163">However, this control comes with a tradeoff of code complexity.</span></span> <span data-ttu-id="842d3-164">使用這種方式就表示您必須擁有調整程式碼 (此程式碼很複雜)。</span><span class="sxs-lookup"><span data-stu-id="842d3-164">Using this approach means that you need to own scaling code, which is non-trivial.</span></span>

<span data-ttu-id="842d3-165">處理 Service Fabric 調整的方式取決於您的案例。</span><span class="sxs-lookup"><span data-stu-id="842d3-165">How you should approach Service Fabric scaling depends on your scenario.</span></span> <span data-ttu-id="842d3-166">如果是不常見的調整，以手動方式新增或移除節點的能力或許就綽綽有餘。</span><span class="sxs-lookup"><span data-stu-id="842d3-166">If scaling is uncommon, the ability to add or remove nodes manually is probably sufficient.</span></span> <span data-ttu-id="842d3-167">若是更複雜的案例，能以程式設計方式進行調整的自動調整規則和 SDK 則可提供更強大的替代方案。</span><span class="sxs-lookup"><span data-stu-id="842d3-167">For more complex scenarios, auto-scale rules and SDKs exposing the ability to scale programmatically offer powerful alternatives.</span></span>

## <a name="next-steps"></a><span data-ttu-id="842d3-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="842d3-168">Next steps</span></span>

<span data-ttu-id="842d3-169">若要開始實作您自己的自動調整邏輯，請先熟悉下列概念和實用的 API：</span><span class="sxs-lookup"><span data-stu-id="842d3-169">To get started implementing your own auto-scaling logic, familiarize yourself with the following concepts and useful APIs:</span></span>

- [<span data-ttu-id="842d3-170">以手動方式或透過自動調整規則進行調整</span><span class="sxs-lookup"><span data-stu-id="842d3-170">Scaling manually or with auto-scale rules</span></span>](./service-fabric-cluster-scale-up-down.md)
- <span data-ttu-id="842d3-171">[適用於 .NET 的 Fluent Azure 管理程式庫](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (適用於與 Service Fabric 叢集的基礎虛擬機器擴展集互動)</span><span class="sxs-lookup"><span data-stu-id="842d3-171">[Fluent Azure Management Libraries for .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (useful for interacting with a Service Fabric cluster's underlying virtual machine scale sets)</span></span>
- <span data-ttu-id="842d3-172">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (適用於與 Service Fabric 叢集及其節點互動)</span><span class="sxs-lookup"><span data-stu-id="842d3-172">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (useful for interacting with a Service Fabric cluster and its nodes)</span></span>
