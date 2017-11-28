---
title: "服務網狀架構以程式設計方式調整 aaaAzure |Microsoft 文件"
description: "調整 Azure Service Fabric 叢集或以程式設計的方式，根據 toocustom 觸發程序"
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
ms.openlocfilehash: a0c6499b1a143a173006248cf8a15380632637e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-service-fabric-cluster-programmatically"></a><span data-ttu-id="d43f4-103">以程式設計方式調整 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="d43f4-103">Scale a Service Fabric cluster programmatically</span></span> 

<span data-ttu-id="d43f4-104">在關於[叢集調整](./service-fabric-cluster-scale-up-down.md)的文件中探討了 Azure Service Fabric 叢集調整的基本概念。</span><span class="sxs-lookup"><span data-stu-id="d43f4-104">Fundamentals of scaling a Service Fabric cluster in Azure are covered in documentation on [cluster scaling](./service-fabric-cluster-scale-up-down.md).</span></span> <span data-ttu-id="d43f4-105">該文章探討如何以虛擬機器擴展集為基礎來建置 Service Fabric 叢集，以及如何以手動方式或自動調整規則來加以調整。</span><span class="sxs-lookup"><span data-stu-id="d43f4-105">That article covers how Service Fabric clusters are built on top of virtual machine scale sets and can be scaled either manually or with auto-scale rules.</span></span> <span data-ttu-id="d43f4-106">本文件則探討如何以程式設計方法讓 Azure 調整作業能夠配合更進階的案例。</span><span class="sxs-lookup"><span data-stu-id="d43f4-106">This document looks at programmatic methods of coordinating Azure scaling operations for more advanced scenarios.</span></span> 

## <a name="reasons-for-programmatic-scaling"></a><span data-ttu-id="d43f4-107">以程式設計方式調整的原因</span><span class="sxs-lookup"><span data-stu-id="d43f4-107">Reasons for programmatic scaling</span></span>
<span data-ttu-id="d43f4-108">在許多案例中，以手動方式或透過自動調整規則來調整是不錯的解決方案。</span><span class="sxs-lookup"><span data-stu-id="d43f4-108">In many scenarios, scaling manually or via auto-scale rules are good solutions.</span></span> <span data-ttu-id="d43f4-109">在其他情況下，不過，它們可能不是右符合 hello。</span><span class="sxs-lookup"><span data-stu-id="d43f4-109">In other scenarios, though, they may not be hello right fit.</span></span> <span data-ttu-id="d43f4-110">潛在缺點 toothese 方法包括：</span><span class="sxs-lookup"><span data-stu-id="d43f4-110">Potential drawbacks toothese approaches include:</span></span>

- <span data-ttu-id="d43f4-111">手動調整會要求您在 toolog 且明確地調整作業的要求。</span><span class="sxs-lookup"><span data-stu-id="d43f4-111">Manually scaling requires you toolog in and explicitly request scaling operations.</span></span> <span data-ttu-id="d43f4-112">如果調整作業需要經常進行或難以預料會在何時進行，這個方法可能就不是合適的解決方案。</span><span class="sxs-lookup"><span data-stu-id="d43f4-112">If scaling operations are required frequently or at unpredictable times, this approach may not be a good solution.</span></span>
- <span data-ttu-id="d43f4-113">當自動調整規模規則移除虛擬機器規模集的執行個體時，他們不要自動移除該節點的知識相關聯的 hello Service Fabric 叢集除非 hello 節點型別具有銀級或金級持久性層級。</span><span class="sxs-lookup"><span data-stu-id="d43f4-113">When auto-scale rules remove an instance from a virtual machine scale set, they do not automatically remove knowledge of that node from hello associated Service Fabric cluster unless hello node type has a durability level of Silver or Gold.</span></span> <span data-ttu-id="d43f4-114">自動調整規模規則才有作用大規模 hello 設定層級 （而不是在 hello Service Fabric 級），因為自動調整規模規則可以移除 Service Fabric 節點，而不會關閉它們依正常程序。</span><span class="sxs-lookup"><span data-stu-id="d43f4-114">Because auto-scale rules work at hello scale set level (rather than at hello Service Fabric level), auto-scale rules can remove Service Fabric nodes without shutting them down gracefully.</span></span> <span data-ttu-id="d43f4-115">以這種方式粗糙地移除節點，會在相應縮小作業完成後留下「準刪除」的 Service Fabric 節點狀態。</span><span class="sxs-lookup"><span data-stu-id="d43f4-115">This rude node removal will leave 'ghost' Service Fabric node state behind after scale-in operations.</span></span> <span data-ttu-id="d43f4-116">個人 （或服務） 需要 tooperiodically 清除 hello Service Fabric 叢集中移除的節點狀態。</span><span class="sxs-lookup"><span data-stu-id="d43f4-116">An individual (or a service) would need tooperiodically clean up removed node state in hello Service Fabric cluster.</span></span>
  - <span data-ttu-id="d43f4-117">請注意，持久性等級為金級或銀級的節點類型會自動清除已移除的節點。</span><span class="sxs-lookup"><span data-stu-id="d43f4-117">Note that a node type with a durability level of Gold or Silver will automatically clean up removed nodes.</span></span>  
- <span data-ttu-id="d43f4-118">雖然自動調整規則支援[許多計量](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md)，但這組計量的數量仍然有限。</span><span class="sxs-lookup"><span data-stu-id="d43f4-118">Although there are [many metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) supported by auto-scale rules, it is still a limited set.</span></span> <span data-ttu-id="d43f4-119">如果您的案例所需要的調整是以該組計量所未涵蓋的一些計量為基礎，則自動調整規則可能不是很好的選擇。</span><span class="sxs-lookup"><span data-stu-id="d43f4-119">If your scenario calls for scaling based on some metric not covered in that set, then auto-scale rules may not be a good option.</span></span>

<span data-ttu-id="d43f4-120">根據這些限制，您可能希望 tooimplement 多自訂自動調整的模型。</span><span class="sxs-lookup"><span data-stu-id="d43f4-120">Based on these limitations, you may wish tooimplement more customized automatic scaling models.</span></span> 

## <a name="scaling-apis"></a><span data-ttu-id="d43f4-121">調整 API</span><span class="sxs-lookup"><span data-stu-id="d43f4-121">Scaling APIs</span></span>
<span data-ttu-id="d43f4-122">Azure 應用程式開發介面存在可讓應用程式 tooprogrammatically 工作虛擬機器擴展集與 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="d43f4-122">Azure APIs exist which allow applications tooprogrammatically work with virtual machine scale sets and Service Fabric clusters.</span></span> <span data-ttu-id="d43f4-123">如果現有的自動調整規模選項不適用於您案例，這些 Api 使得可能 tooimplement 自訂縮放邏輯。</span><span class="sxs-lookup"><span data-stu-id="d43f4-123">If existing auto-scale options don't work for your scenario, these APIs make it possible tooimplement custom scaling logic.</span></span> 

<span data-ttu-id="d43f4-124">其中一個方法 tooimplementing '首頁-變' 的自動調整功能是 tooadd 新無狀態服務 toohello Service Fabric 應用程式 toomanage 調整作業。</span><span class="sxs-lookup"><span data-stu-id="d43f4-124">One approach tooimplementing this 'home-made' auto-scaling functionality is tooadd a new stateless service toohello Service Fabric application toomanage scaling operations.</span></span> <span data-ttu-id="d43f4-125">Hello 服務內`RunAsync`方法，觸發程序的一組可以判斷是否需要 （包括檢查參數，例如最大叢集大小和縮放比例 cooldowns） 縮放比例。</span><span class="sxs-lookup"><span data-stu-id="d43f4-125">Within hello service's `RunAsync` method, a set of triggers can determine if scaling is required (including checking parameters such as maximum cluster size and scaling cooldowns).</span></span>   

<span data-ttu-id="d43f4-126">hello 用於虛擬機器規模集互動的應用程式開發介面 (這兩個 toocheck hello 目前虛擬機器執行個體數目和 toomodify 它) 為 hello [fluent 應用程式開發的 Azure 管理計算文件庫](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/)。</span><span class="sxs-lookup"><span data-stu-id="d43f4-126">hello API used for virtual machine scale set interactions (both toocheck hello current number of virtual machine instances and toomodify it) is hello [fluent Azure Management Compute library](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/).</span></span> <span data-ttu-id="d43f4-127">hello fluent 應用程式開發的計算程式庫提供方便使用 API 與虛擬機器擴展集互動。</span><span class="sxs-lookup"><span data-stu-id="d43f4-127">hello fluent compute library provides an easy-to-use API for interacting with virtual machine scale sets.</span></span>

<span data-ttu-id="d43f4-128">toointeract hello Service Fabric 叢集本身，以使用[System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient)。</span><span class="sxs-lookup"><span data-stu-id="d43f4-128">toointeract with hello Service Fabric cluster itself, use [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span></span>

<span data-ttu-id="d43f4-129">當然，hello 調整程式碼不需要當做服務 toorun hello 叢集 toobe 縮放中。</span><span class="sxs-lookup"><span data-stu-id="d43f4-129">Of course, hello scaling code doesn't need toorun as a service in hello cluster toobe scaled.</span></span> <span data-ttu-id="d43f4-130">同時`IAzure`和`FabricClient`可以 tootheir 相關聯的 Azure 資源從遠端連線，因此 hello 擴充服務可以輕鬆地是主控台應用程式或從外部 hello Service Fabric 應用程式執行的 Windows 服務。</span><span class="sxs-lookup"><span data-stu-id="d43f4-130">Both `IAzure` and `FabricClient` can connect tootheir associated Azure resources remotely, so hello scaling service could easily be a console application or Windows service running from outside hello Service Fabric application.</span></span> 

## <a name="credential-management"></a><span data-ttu-id="d43f4-131">認證管理</span><span class="sxs-lookup"><span data-stu-id="d43f4-131">Credential management</span></span>
<span data-ttu-id="d43f4-132">撰寫服務 toohandle 縮放比例的一項挑戰是 hello 服務必須能夠 tooaccess 不使用互動式登入虛擬機器小數位數設定資源。</span><span class="sxs-lookup"><span data-stu-id="d43f4-132">One challenge of writing a service toohandle scaling is that hello service must be able tooaccess virtual machine scale set resources without an interactive login.</span></span> <span data-ttu-id="d43f4-133">存取 hello Service Fabric 叢集如果很容易 hello 擴充服務正在修改自己的 Service Fabric 應用程式，但認證需要的 tooaccess hello 規模集。</span><span class="sxs-lookup"><span data-stu-id="d43f4-133">Accessing hello Service Fabric cluster is easy if hello scaling service is modifying its own Service Fabric application, but credentials are needed tooaccess hello scale set.</span></span> <span data-ttu-id="d43f4-134">您可以使用在 toolog，[服務主體](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure)建立 hello [Azure CLI 2.0](https://github.com/azure/azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="d43f4-134">toolog in, you can use a [service principal](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) created with hello [Azure CLI 2.0](https://github.com/azure/azure-cli).</span></span>

<span data-ttu-id="d43f4-135">可以建立服務主體以 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d43f4-135">A service principal can be created with hello following steps:</span></span>

1. <span data-ttu-id="d43f4-136">登入 Azure CLI toohello (`az login`) 具有存取 toohello 虛擬機器規模的使用者設定</span><span class="sxs-lookup"><span data-stu-id="d43f4-136">Log in toohello Azure CLI (`az login`) as a user with access toohello virtual machine scale set</span></span>
2. <span data-ttu-id="d43f4-137">建立 hello 服務主體`az ad sp create-for-rbac`</span><span class="sxs-lookup"><span data-stu-id="d43f4-137">Create hello service principal with `az ad sp create-for-rbac`</span></span>
    1. <span data-ttu-id="d43f4-138">請記下 hello appId （他處呼叫 '用戶端 ID'）、 名稱、 密碼及租用戶，以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="d43f4-138">Make note of hello appId (called 'client ID' elsewhere), name, password, and tenant for later use.</span></span>
    2. <span data-ttu-id="d43f4-139">您還需要訂用帳戶識別碼，若要檢視此識別碼，請使用 `az account list`</span><span class="sxs-lookup"><span data-stu-id="d43f4-139">You will also need your subscription ID, which can be viewed with `az account list`</span></span>

<span data-ttu-id="d43f4-140">hello fluent 應用程式開發的計算程式庫可以使用登入這些認證，如下所示 (請注意核心 fluent 應用程式開發的 Azure 型別想`IAzure`位於 hello [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/)封裝):</span><span class="sxs-lookup"><span data-stu-id="d43f4-140">hello fluent compute library can log in using these credentials as follows (note that core fluent Azure types like `IAzure` are in hello [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) package):</span></span>

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
    ServiceEventSource.Current.ServiceMessage(Context, "ERROR: Failed toologin tooAzure");
}
```

<span data-ttu-id="d43f4-141">登入之後，可以透過 `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity` 來查詢擴展集的執行個體計數。</span><span class="sxs-lookup"><span data-stu-id="d43f4-141">Once logged in, scale set instance count can be queried via `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span></span>

## <a name="scaling-out"></a><span data-ttu-id="d43f4-142">相應放大</span><span class="sxs-lookup"><span data-stu-id="d43f4-142">Scaling out</span></span>
<span data-ttu-id="d43f4-143">使用 hello fluent 應用程式開發 Azure 計算 SDK，可加入執行個體 toohello 虛擬機器擴展集與少數呼叫-</span><span class="sxs-lookup"><span data-stu-id="d43f4-143">Using hello fluent Azure compute SDK, instances can be added toohello virtual machine scale set with just a few calls -</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);
var newCapacity = (int)Math.Min(MaximumNodeCount, scaleSet.Capacity + 1);
scaleSet.Update().WithCapacity(newCapacity).Apply(); 
``` 

<span data-ttu-id="d43f4-144">或者，也可以使用 PowerShell Cmdlet 來管理虛擬機器擴展集大小。</span><span class="sxs-lookup"><span data-stu-id="d43f4-144">Alternatively, virtual machine scale set size can also be managed with PowerShell cmdlets.</span></span> <span data-ttu-id="d43f4-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss)可以擷取 hello 虛擬機器規模集物件。</span><span class="sxs-lookup"><span data-stu-id="d43f4-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss) can retrieve hello virtual machine scale set object.</span></span> <span data-ttu-id="d43f4-146">hello 目前的容量會儲存在 hello`.sku.capacity`屬性。</span><span class="sxs-lookup"><span data-stu-id="d43f4-146">hello current capacity will be stored in hello `.sku.capacity` property.</span></span> <span data-ttu-id="d43f4-147">Hello 虛擬機器擴展集在 Azure 中變更 hello 容量 toohello 所需的值之後，可以更新以 hello [ `Update-AzureRmVmss` ](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss)命令。</span><span class="sxs-lookup"><span data-stu-id="d43f4-147">After changing hello capacity toohello desired value, hello virtual machine scale set in Azure can be updated with hello [`Update-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) command.</span></span>

<span data-ttu-id="d43f4-148">時以手動方式加入的節點，將規模調整集合執行個體應該是所有的所需的 toostart 包含新的 Service Fabric 節點由於 hello 規模調整集合範本延伸 tooautomatically 加入新的執行個體 toohello Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="d43f4-148">As when adding a node manually, adding a scale set instance should be all that's needed toostart a new Service Fabric node since hello scale set template includes extensions tooautomatically join new instances toohello Service Fabric cluster.</span></span> 

## <a name="scaling-in"></a><span data-ttu-id="d43f4-149">相應縮小</span><span class="sxs-lookup"><span data-stu-id="d43f4-149">Scaling in</span></span>

<span data-ttu-id="d43f4-150">中的縮放比例是類似 tooscaling 出。hello 實際上會變更的實際虛擬機器規模集 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="d43f4-150">Scaling in is similar tooscaling out. hello actual virtual machine scale set changes are practically hello same.</span></span> <span data-ttu-id="d43f4-151">但就如先前所討論的，Service Fabric 只會自動清除持久性為金級或銀級的已移除節點。</span><span class="sxs-lookup"><span data-stu-id="d43f4-151">But, as was discussed previously, Service Fabric only automatically cleans up removed nodes with a durability of Gold or Silver.</span></span> <span data-ttu-id="d43f4-152">因此，您也可以在 hello 銅級持久性小數位數的情況下，它是以 hello Service Fabric 需要 toointeract 叢集下移除 hello 節點 toobe tooshut 然後 tooremove 其狀態。</span><span class="sxs-lookup"><span data-stu-id="d43f4-152">So, in hello Bronze-durability scale-in case, it's necessary toointeract with hello Service Fabric cluster tooshut down hello node toobe removed and then tooremove its state.</span></span>

<span data-ttu-id="d43f4-153">準備 hello 節點關機包括找出 hello 節點 toobe 移除 （hello 最近加入的節點） 並停用它。</span><span class="sxs-lookup"><span data-stu-id="d43f4-153">Preparing hello node for shutdown involves finding hello node toobe removed (hello most recently added node) and deactivating it.</span></span> <span data-ttu-id="d43f4-154">對於非種子節點，可以藉由比較 `NodeInstanceId` 來找到較新的節點。</span><span class="sxs-lookup"><span data-stu-id="d43f4-154">For non-seed nodes, newer nodes can be found by comparing `NodeInstanceId`.</span></span> 

```C#
using (var client = new FabricClient())
{
    var mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync())
        .Where(n => n.NodeType.Equals(NodeTypeToScale, StringComparison.OrdinalIgnoreCase))
        .Where(n => n.NodeStatus == System.Fabric.Query.NodeStatus.Up)
        .OrderByDescending(n => n.NodeInstanceId)
        .FirstOrDefault();
```

<span data-ttu-id="d43f4-155">請注意，*種子*節點看上去不 tooalways 遵循 hello 慣例，會先移除更大的執行個體識別碼。</span><span class="sxs-lookup"><span data-stu-id="d43f4-155">Be aware that *seed* nodes don't seem tooalways follow hello convention that greater instance IDs are removed first.</span></span>

<span data-ttu-id="d43f4-156">一旦找到 hello 節點 toobe 移除，可以停用和移除使用 hello 相同`FabricClient`執行個體和 hello`IAzure`從先前的執行個體。</span><span class="sxs-lookup"><span data-stu-id="d43f4-156">Once hello node toobe removed is found, it can be deactivated and removed using hello same `FabricClient` instance and hello `IAzure` instance from earlier.</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);

// Remove hello node from hello Service Fabric cluster
ServiceEventSource.Current.ServiceMessage(Context, $"Disabling node {mostRecentLiveNode.NodeName}");
await client.ClusterManager.DeactivateNodeAsync(mostRecentLiveNode.NodeName, NodeDeactivationIntent.RemoveNode);

// Wait (up tooa timeout) for hello node toogracefully shutdown
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

<span data-ttu-id="d43f4-157">與相應放大規模時相同，如果偏好使用指令碼處理方法，在這裡也可以使用修改虛擬機器擴展集容量的 PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d43f4-157">As with scaling out, PowerShell cmdlets for modifying virtual machine scale set capacity can also be used here if a scripting approach is preferable.</span></span> <span data-ttu-id="d43f4-158">一旦移除 hello 虛擬機器執行個體時，就可以移除 Service Fabric 節點狀態。</span><span class="sxs-lookup"><span data-stu-id="d43f4-158">Once hello virtual machine instance is removed, Service Fabric node state can be removed.</span></span>

```C#
await client.ClusterManager.RemoveNodeStateAsync(mostRecentLiveNode.NodeName);
```

## <a name="potential-drawbacks"></a><span data-ttu-id="d43f4-159">可能的缺點</span><span class="sxs-lookup"><span data-stu-id="d43f4-159">Potential drawbacks</span></span>

<span data-ttu-id="d43f4-160">Hello 前面程式碼片段所示，建立縮放的服務提供 hello 高程度的控制權和自訂您的應用程式上的縮放行為。</span><span class="sxs-lookup"><span data-stu-id="d43f4-160">As demonstrated in hello preceding code snippets, creating your own scaling service provides hello highest degree of control and customizability over your application's scaling behavior.</span></span> <span data-ttu-id="d43f4-161">這很適合用於需要精確控制應用程式相應縮小或放大之時機或方式的案例。不過，伴隨此控制能力而來的是程式碼會變得複雜。</span><span class="sxs-lookup"><span data-stu-id="d43f4-161">This can be useful for scenarios requiring precise control over when or how an application scales in or out. However, this control comes with a tradeoff of code complexity.</span></span> <span data-ttu-id="d43f4-162">使用這種方式表示您需要 tooown 調整為非一般的程式碼。</span><span class="sxs-lookup"><span data-stu-id="d43f4-162">Using this approach means that you need tooown scaling code, which is non-trivial.</span></span>

<span data-ttu-id="d43f4-163">處理 Service Fabric 調整的方式取決於您的案例。</span><span class="sxs-lookup"><span data-stu-id="d43f4-163">How you should approach Service Fabric scaling depends on your scenario.</span></span> <span data-ttu-id="d43f4-164">縮放比例不常見，如果 hello 能力 tooadd 或移除節點，則手動可能足夠。</span><span class="sxs-lookup"><span data-stu-id="d43f4-164">If scaling is uncommon, hello ability tooadd or remove nodes manually is probably sufficient.</span></span> <span data-ttu-id="d43f4-165">更複雜的情況下，自動調整規模規則和以程式設計方式公開 hello 能力 tooscale 的 Sdk 提供功能強大的替代項目。</span><span class="sxs-lookup"><span data-stu-id="d43f4-165">For more complex scenarios, auto-scale rules and SDKs exposing hello ability tooscale programmatically offer powerful alternatives.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d43f4-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d43f4-166">Next steps</span></span>

<span data-ttu-id="d43f4-167">tooget 啟動實作您自己的自動調整的邏輯，會將您自己熟悉 hello 下列概念和有用的 Api:</span><span class="sxs-lookup"><span data-stu-id="d43f4-167">tooget started implementing your own auto-scaling logic, familiarize yourself with hello following concepts and useful APIs:</span></span>

- [<span data-ttu-id="d43f4-168">以手動方式或透過自動調整規則進行調整</span><span class="sxs-lookup"><span data-stu-id="d43f4-168">Scaling manually or with auto-scale rules</span></span>](./service-fabric-cluster-scale-up-down.md)
- <span data-ttu-id="d43f4-169">[適用於 .NET 的 Fluent Azure 管理程式庫](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (適用於與 Service Fabric 叢集的基礎虛擬機器擴展集互動)</span><span class="sxs-lookup"><span data-stu-id="d43f4-169">[Fluent Azure Management Libraries for .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (useful for interacting with a Service Fabric cluster's underlying virtual machine scale sets)</span></span>
- <span data-ttu-id="d43f4-170">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (適用於與 Service Fabric 叢集及其節點互動)</span><span class="sxs-lookup"><span data-stu-id="d43f4-170">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (useful for interacting with a Service Fabric cluster and its nodes)</span></span>
