---
title: "aaaScale Service Fabric 叢集 in 或 out |Microsoft 文件"
description: "縮放 Service Fabric 叢集 in 或 out toomatch 視需要設定每個節點型別/虛擬機器擴展集自動調整規模規則。 新增或移除節點 tooa Service Fabric 叢集"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: aeb76f63-7303-4753-9c64-46146340b83d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/22/2017
ms.author: chackdan
ms.openlocfilehash: 37cfeaf80edc016cf6de017d1c2dc6fbcb8acc2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-service-fabric-cluster-in-or-out-using-auto-scale-rules"></a><span data-ttu-id="dc453-104">使用自動調整規模規則相應縮小或放大 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="dc453-104">Scale a Service Fabric cluster in or out using auto-scale rules</span></span>
<span data-ttu-id="dc453-105">虛擬機器擴展集是 Azure 計算資源，您可以使用 toodeploy 和管理的虛擬機器作為一組的集合。</span><span class="sxs-lookup"><span data-stu-id="dc453-105">Virtual machine scale sets are an Azure compute resource that you can use toodeploy and manage a collection of virtual machines as a set.</span></span> <span data-ttu-id="dc453-106">在 Service Fabric 叢集中定義的每個節點類型都會安裝為不同的虛擬機器擴展集。</span><span class="sxs-lookup"><span data-stu-id="dc453-106">Every node type that is defined in a Service Fabric cluster is set up as a separate Virtual Machine scale set.</span></span> <span data-ttu-id="dc453-107">然後每個節點類型可以獨立相應縮小或放大，可以開啟不同組的連接埠，並可以有不同的容量度量。</span><span class="sxs-lookup"><span data-stu-id="dc453-107">Each node type can then be scaled in or out independently, have different sets of ports open, and can have different capacity metrics.</span></span> <span data-ttu-id="dc453-108">深入了解在 hello [Service Fabric nodetypes](service-fabric-cluster-nodetypes.md)文件。</span><span class="sxs-lookup"><span data-stu-id="dc453-108">Read more about it in hello [Service Fabric nodetypes](service-fabric-cluster-nodetypes.md) document.</span></span> <span data-ttu-id="dc453-109">由於 hello Service Fabric 節點型別，在叢集中的虛擬機器擴展集在 hello 後端進行，您會需要每個節點型別/虛擬機器擴展集 tooset 自動調整規模規則。</span><span class="sxs-lookup"><span data-stu-id="dc453-109">Since hello Service Fabric node types in your cluster are made of Virtual Machine scale sets at hello backend, you need tooset up auto-scale rules for each node type/Virtual Machine scale set.</span></span>

> [!NOTE]
> <span data-ttu-id="dc453-110">您的訂用帳戶必須擁有足夠的核心 tooadd hello 這個叢集所組成的新 Vm。</span><span class="sxs-lookup"><span data-stu-id="dc453-110">Your subscription must have enough cores tooadd hello new VMs that make up this cluster.</span></span> <span data-ttu-id="dc453-111">沒有模型驗證目前，因此您會取得部署階段失敗，如果任何 hello 配額限制會叫用。</span><span class="sxs-lookup"><span data-stu-id="dc453-111">There is no model validation currently, so you get a deployment time failure, if any of hello quota limits are hit.</span></span>
> 
> 

## <a name="choose-hello-node-typevirtual-machine-scale-set-tooscale"></a><span data-ttu-id="dc453-112">選擇 hello 節點型別/虛擬機器擴展集 tooscale</span><span class="sxs-lookup"><span data-stu-id="dc453-112">Choose hello node type/Virtual Machine scale set tooscale</span></span>
<span data-ttu-id="dc453-113">目前，您不使用 hello 入口網站的虛擬機器擴展集無法 toospecify hello 自動調整規模規則，因此讓我們使用 Azure PowerShell （1.0 +） toolist hello 節點型別然後再加入自動調整規模規則 toothem。</span><span class="sxs-lookup"><span data-stu-id="dc453-113">Currently, you are not able toospecify hello auto-scale rules for Virtual Machine scale sets using hello portal, so let us use Azure PowerShell (1.0+) toolist hello node types and then add auto-scale rules toothem.</span></span>

<span data-ttu-id="dc453-114">虛擬機器擴展集的 tooget hello 清單構成您叢集，請執行下列 cmdlet 的 hello:</span><span class="sxs-lookup"><span data-stu-id="dc453-114">tooget hello list of Virtual Machine scale set that make up your cluster, run hello following cmdlets:</span></span>

```powershell
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Compute/VirtualMachineScaleSets

Get-AzureRmVmss -ResourceGroupName <RGname> -VMScaleSetName <Virtual Machine scale set name>
```

## <a name="set-auto-scale-rules-for-hello-node-typevirtual-machine-scale-set"></a><span data-ttu-id="dc453-115">設定自動調整規模規則的 hello 節點型別/虛擬機器規模集</span><span class="sxs-lookup"><span data-stu-id="dc453-115">Set auto-scale rules for hello node type/Virtual Machine scale set</span></span>
<span data-ttu-id="dc453-116">如果您的叢集有多個節點類型，然後重複此作業對於每個節點型別/虛擬機器規模設定的 tooscale （in 或 out）。</span><span class="sxs-lookup"><span data-stu-id="dc453-116">If your cluster has multiple node types, then repeat this for each node types/Virtual Machine scale sets that you want tooscale (in or out).</span></span> <span data-ttu-id="dc453-117">會將節點帳戶 hello 數目，您必須有設定自動調整之前。</span><span class="sxs-lookup"><span data-stu-id="dc453-117">Take into account hello number of nodes that you must have before you set up auto-scaling.</span></span> <span data-ttu-id="dc453-118">您已選擇 hello 可靠性層級有驅動 hello hello 主要節點類型，您必須擁有的節點數目下限。</span><span class="sxs-lookup"><span data-stu-id="dc453-118">hello minimum number of nodes that you must have for hello primary node type is driven by hello reliability level you have chosen.</span></span> <span data-ttu-id="dc453-119">深入了解 [可靠性層級](service-fabric-cluster-capacity.md)。</span><span class="sxs-lookup"><span data-stu-id="dc453-119">Read more about [reliability levels](service-fabric-cluster-capacity.md).</span></span>

> [!NOTE]
> <span data-ttu-id="dc453-120">縮小 hello 主要節點類型 tooless 多於 hello 最小數目進行 hello 叢集不穩定，或將它關機。</span><span class="sxs-lookup"><span data-stu-id="dc453-120">Scaling down hello primary node type tooless than hello minimum number make hello cluster unstable or bring it down.</span></span> <span data-ttu-id="dc453-121">這可能導致資料遺失對於您的應用程式與 hello 系統服務。</span><span class="sxs-lookup"><span data-stu-id="dc453-121">This could result in data loss for your applications and for hello system services.</span></span>
> 
> 

<span data-ttu-id="dc453-122">目前 hello 自動調整規模功能不受到 hello 載入 tooService 網狀架構可能會報告您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="dc453-122">Currently hello auto-scale feature is not driven by hello loads that your applications may be reporting tooService Fabric.</span></span> <span data-ttu-id="dc453-123">因此在此時間 hello 自動調整規模，就是單純地驅動 hello 效能計數器，所發出的每個 hello 虛擬機器規模集執行個體。</span><span class="sxs-lookup"><span data-stu-id="dc453-123">So at this time hello auto-scale you get is purely driven by hello performance counters that are emitted by each of hello Virtual Machine scale set instances.</span></span>  

<span data-ttu-id="dc453-124">請遵循下列指示[總每個虛擬機器擴展集自動調整規模 tooset](../virtual-machine-scale-sets/virtual-machine-scale-sets-autoscale-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="dc453-124">Follow these instructions [tooset up auto-scale for each Virtual Machine scale set](../virtual-machine-scale-sets/virtual-machine-scale-sets-autoscale-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="dc453-125">在向下調整的案例中，除非您的節點型別具有金級 」 或 「 銀級持久性層級，您需要 toocall hello[移除 ServiceFabricNodeState cmdlet](https://msdn.microsoft.com/library/azure/mt125993.aspx) hello 適當的節點名稱。</span><span class="sxs-lookup"><span data-stu-id="dc453-125">In a scale down scenario, unless your node type has a durability level of Gold or Silver you need toocall hello [Remove-ServiceFabricNodeState cmdlet](https://msdn.microsoft.com/library/azure/mt125993.aspx) with hello appropriate node name.</span></span>
> 
> 

## <a name="manually-add-vms-tooa-node-typevirtual-machine-scale-set"></a><span data-ttu-id="dc453-126">手動新增 Vm tooa 節點型別/虛擬機器規模集</span><span class="sxs-lookup"><span data-stu-id="dc453-126">Manually add VMs tooa node type/Virtual Machine scale set</span></span>
<span data-ttu-id="dc453-127">請依照 hello 範例/hello 中指示[快速入門範本庫](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing)toochange hello 數目中每個節點類型的 Vm。</span><span class="sxs-lookup"><span data-stu-id="dc453-127">Follow hello sample/instructions in hello [quick start template gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) toochange hello number of VMs in each Nodetype.</span></span> 

> [!NOTE]
> <span data-ttu-id="dc453-128">新增 Vm 需要時間，所以不要期待 hello 新增 toobe 瞬間完成。</span><span class="sxs-lookup"><span data-stu-id="dc453-128">Adding of VMs takes time, so do not expect hello additions toobe instantaneous.</span></span> <span data-ttu-id="dc453-129">因此也會在時間 tooallow 超過 10 分鐘才能供 hello 複本 hello 的 VM 容量規劃 tooadd 容量/服務執行個體 tooget 放置。</span><span class="sxs-lookup"><span data-stu-id="dc453-129">So plan tooadd capacity well in time, tooallow for over 10 minutes before hello VM capacity is available for hello replicas/ service instances tooget placed.</span></span>
> 
> 

## <a name="manually-remove-vms-from-hello-primary-node-typevirtual-machine-scale-set"></a><span data-ttu-id="dc453-130">手動移除 hello 主要節點類型/虛擬機器規模集的 Vm</span><span class="sxs-lookup"><span data-stu-id="dc453-130">Manually remove VMs from hello primary node type/Virtual Machine scale set</span></span>
> [!NOTE]
> <span data-ttu-id="dc453-131">hello 服務網狀架構系統服務在 hello 主要節點類型，在叢集中執行。</span><span class="sxs-lookup"><span data-stu-id="dc453-131">hello service fabric system services run in hello Primary node type in your cluster.</span></span> <span data-ttu-id="dc453-132">所以應該永遠不會關機或調降 hello 該節點型別中的執行個體數目小於哪些 hello 可靠性層保證。</span><span class="sxs-lookup"><span data-stu-id="dc453-132">So should never shut down or scale down hello number of instances in that node types less than what hello reliability tier warrants.</span></span> <span data-ttu-id="dc453-133">請參閱太[hello 可靠性層級的詳細資訊](service-fabric-cluster-capacity.md)。</span><span class="sxs-lookup"><span data-stu-id="dc453-133">Refer too[hello details on reliability tiers here](service-fabric-cluster-capacity.md).</span></span> 
> 
> 

<span data-ttu-id="dc453-134">您需要 tooexecute hello 下列步驟會一次一個 VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="dc453-134">You need tooexecute hello following steps one VM instance at a time.</span></span> <span data-ttu-id="dc453-135">這可讓 hello 系統服務 （以及您可設定狀態的服務） toobe 正常關閉您要移除 hello VM 執行個體和其他節點上建立的新複本。</span><span class="sxs-lookup"><span data-stu-id="dc453-135">This allows for hello system services (and your stateful services) toobe shut down gracefully on hello VM instance you are removing and new replicas created on other nodes.</span></span>

1. <span data-ttu-id="dc453-136">執行[停用 ServiceFabricNode](https://msdn.microsoft.com/library/mt125852.aspx)與意圖 'RemoveNode' toodisable hello 節點將 tooremove （hello 最大執行個體在該節點類型）。</span><span class="sxs-lookup"><span data-stu-id="dc453-136">Run [Disable-ServiceFabricNode](https://msdn.microsoft.com/library/mt125852.aspx) with intent ‘RemoveNode’ toodisable hello node you’re going tooremove (hello highest instance in that node type).</span></span>
2. <span data-ttu-id="dc453-137">執行[Get ServiceFabricNode](https://msdn.microsoft.com/library/mt125856.aspx) toomake 確定該 hello 節點已確實轉換 toodisabled。</span><span class="sxs-lookup"><span data-stu-id="dc453-137">Run [Get-ServiceFabricNode](https://msdn.microsoft.com/library/mt125856.aspx) toomake sure that hello node has indeed transitioned toodisabled.</span></span> <span data-ttu-id="dc453-138">如果沒有，請等到 hello 節點停用。</span><span class="sxs-lookup"><span data-stu-id="dc453-138">If not, wait until hello node is disabled.</span></span> <span data-ttu-id="dc453-139">您無法加快此步驟的速度。</span><span class="sxs-lookup"><span data-stu-id="dc453-139">You cannot hurry this step.</span></span>
3. <span data-ttu-id="dc453-140">請依照 hello 範例/hello 中指示[快速入門範本庫](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing)toochange hello Vm 數目加一該的 Nodetype。</span><span class="sxs-lookup"><span data-stu-id="dc453-140">Follow hello sample/instructions in hello [quick start template gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) toochange hello number of VMs by one in that Nodetype.</span></span> <span data-ttu-id="dc453-141">移除 hello 執行個體是 hello 最高的 VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="dc453-141">hello instance removed is hello highest VM instance.</span></span> 
4. <span data-ttu-id="dc453-142">重複步驟 1 到 3，如有需要但永遠不會縮小 hello hello 主要節點類型小於需要哪些 hello 可靠性層中的執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="dc453-142">Repeat steps 1 through 3 as needed, but never scale down hello number of instances in hello primary node types less than what hello reliability tier warrants.</span></span> <span data-ttu-id="dc453-143">請參閱太[hello 可靠性層級的詳細資訊](service-fabric-cluster-capacity.md)。</span><span class="sxs-lookup"><span data-stu-id="dc453-143">Refer too[hello details on reliability tiers here](service-fabric-cluster-capacity.md).</span></span> 

## <a name="manually-remove-vms-from-hello-non-primary-node-typevirtual-machine-scale-set"></a><span data-ttu-id="dc453-144">手動移除 hello 非主要節點類型/虛擬機器規模集的 Vm</span><span class="sxs-lookup"><span data-stu-id="dc453-144">Manually remove VMs from hello non-primary node type/Virtual Machine scale set</span></span>
> [!NOTE]
> <span data-ttu-id="dc453-145">可設定狀態的服務，您需要節點 toobe 數目一律 toomaintain 可用性和保留狀態，您的服務。</span><span class="sxs-lookup"><span data-stu-id="dc453-145">For a stateful service, you need a certain number of nodes toobe always up toomaintain availability and preserve state of your service.</span></span> <span data-ttu-id="dc453-146">在 hello 非常小，您需要節點等於 toohello 目標複本集的計數 hello 磁碟分割/服務的 hello 的數目。</span><span class="sxs-lookup"><span data-stu-id="dc453-146">At hello very minimum, you need hello number of nodes equal toohello target replica set count of hello partition/service.</span></span> 
> 
> 

<span data-ttu-id="dc453-147">您需要 hello 執行 hello 遵循步驟一個 VM 執行個體一次。</span><span class="sxs-lookup"><span data-stu-id="dc453-147">You need hello execute hello following steps one VM instance at a time.</span></span> <span data-ttu-id="dc453-148">這可 hello 系統服務 （以及您可設定狀態的服務） toobe 正常關機 hello 上要移除的 VM 執行個體，而且新的複本建立的其他位置。</span><span class="sxs-lookup"><span data-stu-id="dc453-148">This allows for hello system services (and your stateful services) toobe shut down gracefully on hello VM instance you are removing and new replicas created else where.</span></span>

1. <span data-ttu-id="dc453-149">執行[停用 ServiceFabricNode](https://msdn.microsoft.com/library/mt125852.aspx)與意圖 'RemoveNode' toodisable hello 節點將 tooremove （hello 最大執行個體在該節點類型）。</span><span class="sxs-lookup"><span data-stu-id="dc453-149">Run [Disable-ServiceFabricNode](https://msdn.microsoft.com/library/mt125852.aspx) with intent ‘RemoveNode’ toodisable hello node you’re going tooremove (hello highest instance in that node type).</span></span>
2. <span data-ttu-id="dc453-150">執行[Get ServiceFabricNode](https://msdn.microsoft.com/library/mt125856.aspx) toomake 確定該 hello 節點已確實轉換 toodisabled。</span><span class="sxs-lookup"><span data-stu-id="dc453-150">Run [Get-ServiceFabricNode](https://msdn.microsoft.com/library/mt125856.aspx) toomake sure that hello node has indeed transitioned toodisabled.</span></span> <span data-ttu-id="dc453-151">如果不是等到 hello 節點停用。</span><span class="sxs-lookup"><span data-stu-id="dc453-151">If not wait till hello node is disabled.</span></span> <span data-ttu-id="dc453-152">您無法加快此步驟的速度。</span><span class="sxs-lookup"><span data-stu-id="dc453-152">You cannot hurry this step.</span></span>
3. <span data-ttu-id="dc453-153">請依照 hello 範例/hello 中指示[快速入門範本庫](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing)toochange hello Vm 數目加一該的 Nodetype。</span><span class="sxs-lookup"><span data-stu-id="dc453-153">Follow hello sample/instructions in hello [quick start template gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) toochange hello number of VMs by one in that Nodetype.</span></span> <span data-ttu-id="dc453-154">這會立即移除 hello 最高的 VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="dc453-154">This will now remove hello highest VM instance.</span></span> 
4. <span data-ttu-id="dc453-155">重複步驟 1 到 3，如有需要但永遠不會縮小 hello hello 主要節點類型小於需要哪些 hello 可靠性層中的執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="dc453-155">Repeat steps 1 through 3 as needed, but never scale down hello number of instances in hello primary node types less than what hello reliability tier warrants.</span></span> <span data-ttu-id="dc453-156">請參閱太[hello 可靠性層級的詳細資訊](service-fabric-cluster-capacity.md)。</span><span class="sxs-lookup"><span data-stu-id="dc453-156">Refer too[hello details on reliability tiers here](service-fabric-cluster-capacity.md).</span></span>

## <a name="behaviors-you-may-observe-in-service-fabric-explorer"></a><span data-ttu-id="dc453-157">Service Fabric Explorer 可能出現的行為</span><span class="sxs-lookup"><span data-stu-id="dc453-157">Behaviors you may observe in Service Fabric Explorer</span></span>
<span data-ttu-id="dc453-158">當您擴充叢集 hello Service Fabric 總管將會反映 hello 數字的節點 （虛擬機器規模集執行個體） 是 hello 叢集的一部分。</span><span class="sxs-lookup"><span data-stu-id="dc453-158">When you scale up a cluster hello Service Fabric Explorer will reflect hello number of nodes (Virtual Machine scale set instances) that are part of hello cluster.</span></span>  <span data-ttu-id="dc453-159">不過，當您調整叢集清單中，您會看到 hello 移除節點/VM 執行個體顯示在狀況不良狀態，除非您呼叫[移除 ServiceFabricNodeState cmd](https://msdn.microsoft.com/library/mt125993.aspx) hello 適當的節點名稱。</span><span class="sxs-lookup"><span data-stu-id="dc453-159">However, when you scale a cluster down you will see hello removed node/VM instance displayed in an unhealthy state unless you call [Remove-ServiceFabricNodeState cmd](https://msdn.microsoft.com/library/mt125993.aspx) with hello appropriate node name.</span></span>   

<span data-ttu-id="dc453-160">以下是這種行為的 hello 說明。</span><span class="sxs-lookup"><span data-stu-id="dc453-160">Here is hello explanation for this behavior.</span></span>

<span data-ttu-id="dc453-161">hello Service Fabric 總管中所列的節點會反映出 hello Service Fabric 系統服務 (FM 特別) 知道有/有的節點 hello 叢集的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="dc453-161">hello nodes listed in Service Fabric Explorer are a reflection of what hello Service Fabric system services (FM specifically) knows about hello number of nodes hello cluster had/has.</span></span> <span data-ttu-id="dc453-162">當您調整 hello 虛擬機器擴展集時，hello VM 已刪除，但是 FM 系統服務仍然會認為該 hello 節點 （也就是對應的 toohello 已刪除的 VM） 將回來。</span><span class="sxs-lookup"><span data-stu-id="dc453-162">When you scale hello Virtual Machine scale set down, hello VM was deleted but FM system service still thinks that hello node (that was mapped toohello VM that was deleted) will come back.</span></span> <span data-ttu-id="dc453-163">因此 Service Fabric 總管會繼續 toodisplay 該節點 （雖然 hello 健全狀況狀態可能是錯誤或不明）。</span><span class="sxs-lookup"><span data-stu-id="dc453-163">So Service Fabric Explorer continues toodisplay that node (though hello health state may be error or unknown).</span></span>

<span data-ttu-id="dc453-164">在訂單 toomake 確定節點已移除的 VM 時，您會有兩個選項：</span><span class="sxs-lookup"><span data-stu-id="dc453-164">In order toomake sure that a node is removed when a VM is removed, you have two options:</span></span>

1) <span data-ttu-id="dc453-165">選擇金級 」 或 「 銀級持久性層級 (可立即) 的 hello 叢集中的節點型別，可讓您 hello 基礎結構整合。</span><span class="sxs-lookup"><span data-stu-id="dc453-165">Choose a durability level of Gold or Silver (available soon) for hello node types in your cluster, which gives you hello infrastructure integration.</span></span> <span data-ttu-id="dc453-166">這將會自動 hello 節點從我們的系統服務 (FM) 狀態時移除您向下調整。</span><span class="sxs-lookup"><span data-stu-id="dc453-166">Which will then automatically remove hello nodes from our system services (FM) state when you scale down.</span></span>
<span data-ttu-id="dc453-167">請參閱太[hello 持久性層級的詳細資訊](service-fabric-cluster-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="dc453-167">Refer too[hello details on durability levels here](service-fabric-cluster-capacity.md)</span></span>

2) <span data-ttu-id="dc453-168">一旦已縮小 hello VM 執行個體，您需要 toocall hello[移除 ServiceFabricNodeState cmdlet](https://msdn.microsoft.com/library/mt125993.aspx)。</span><span class="sxs-lookup"><span data-stu-id="dc453-168">Once hello VM instance has been scaled down, you need toocall hello [Remove-ServiceFabricNodeState cmdlet](https://msdn.microsoft.com/library/mt125993.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="dc453-169">服務網狀架構叢集節點 toobe 數目向上在需要所有 hello 時間順序 toomaintain 可用性和保留狀態-參照 tooas 「 維持仲裁 」。</span><span class="sxs-lookup"><span data-stu-id="dc453-169">Service Fabric clusters require a certain number of nodes toobe up at all hello time in order toomaintain availability and preserve state - referred tooas "maintaining quorum."</span></span> <span data-ttu-id="dc453-170">因此，它是向 hello 叢集中的所有 hello 機器通常不安全 tooshut 除非您先執行[狀態的完整備份](service-fabric-reliable-services-backup-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="dc453-170">So, it is typically unsafe tooshut down all hello machines in hello cluster unless you have first performed a [full backup of your state](service-fabric-reliable-services-backup-restore.md).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="dc453-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dc453-171">Next steps</span></span>
<span data-ttu-id="dc453-172">讀取 hello 遵循 tooalso 深入了解規劃叢集的容量、 升級叢集，以及資料分割服務：</span><span class="sxs-lookup"><span data-stu-id="dc453-172">Read hello following tooalso learn about planning cluster capacity, upgrading a cluster, and partitioning services:</span></span>

* [<span data-ttu-id="dc453-173">規劃叢集容量</span><span class="sxs-lookup"><span data-stu-id="dc453-173">Plan your cluster capacity</span></span>](service-fabric-cluster-capacity.md)
* [<span data-ttu-id="dc453-174">叢集升級</span><span class="sxs-lookup"><span data-stu-id="dc453-174">Cluster upgrades</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="dc453-175">分割具狀態服務以達最大規模</span><span class="sxs-lookup"><span data-stu-id="dc453-175">Partition stateful services for maximum scale</span></span>](service-fabric-concepts-partitioning.md)

<!--Image references-->
[BrowseServiceFabricClusterResource]: ./media/service-fabric-cluster-scale-up-down/BrowseServiceFabricClusterResource.png
[ClusterResources]: ./media/service-fabric-cluster-scale-up-down/ClusterResources.png
