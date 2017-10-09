---
title: "aaaService 網狀架構節點型別與 VM 規模集 |Microsoft 文件"
description: "說明 Service Fabric 節點型別與 tooVM 規模集的關聯，以及 tooremote 連線 tooa 虛擬機器擴展集的執行個體或叢集節點的方式。"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 5441e7e0-d842-4398-b060-8c9d34b07c48
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: chackdan
ms.openlocfilehash: 830ea2816f5864de146a77483c85de26f91c2425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="hello-relationship-between-service-fabric-node-types-and-virtual-machine-scale-sets"></a><span data-ttu-id="2d0e5-103">hello Service Fabric 節點型別和虛擬機器擴展集之間的關聯性</span><span class="sxs-lookup"><span data-stu-id="2d0e5-103">hello relationship between Service Fabric node types and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="2d0e5-104">虛擬機器擴展集是您可以使用 toodeploy 和管理虛擬機器的集合做為一組 Azure 計算資源。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-104">Virtual Machine Scale Sets are an Azure Compute resource you can use toodeploy and manage a collection of virtual machines as a set.</span></span> <span data-ttu-id="2d0e5-105">在 Service Fabric 叢集中定義的每個節點類型都會安裝為不同的 VM 擴展集。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-105">Every node type that is defined in a Service Fabric cluster is set up as a separate VM Scale Set.</span></span> <span data-ttu-id="2d0e5-106">然後每個節點類型可以獨立相應增加或相應減少，可以開啟不同組的連接埠，並可以有不同的容量度量。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-106">Each node type can then be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span></span>

<span data-ttu-id="2d0e5-107">下列螢幕擷取畫面的 hello 示範具有兩個節點類型的叢集： 前端及後端。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-107">hello following screen shot shows a cluster that has two node types: FrontEnd and BackEnd.</span></span>  <span data-ttu-id="2d0e5-108">每個節點類型各有五個節點。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-108">Each node type has five nodes each.</span></span>

![有兩個節點類型的叢集螢幕擷取畫面][NodeTypes]

## <a name="mapping-vm-scale-set-instances-toonodes"></a><span data-ttu-id="2d0e5-110">對應虛擬機器擴展集的執行個體 toonodes</span><span class="sxs-lookup"><span data-stu-id="2d0e5-110">Mapping VM Scale Set instances toonodes</span></span>
<span data-ttu-id="2d0e5-111">您可以看到上方，hello 虛擬機器擴展集的執行個體從執行個體 0 開始，然後向上。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-111">As you can see above, hello VM Scale Set instances start from instance 0 and then goes up.</span></span> <span data-ttu-id="2d0e5-112">hello 編號會反映在 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-112">hello numbering is reflected in hello names.</span></span> <span data-ttu-id="2d0e5-113">例如，BackEnd_0 是 hello 後端虛擬機器擴展集的執行個體 0。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-113">For example, BackEnd_0 is instance 0 of hello BackEnd VM Scale Set.</span></span> <span data-ttu-id="2d0e5-114">這個特定的 VM 調整集有五個執行個體，名稱分別是 BackEnd_0、BackEnd_1、BackEnd_2、BackEnd_3、BackEnd_4。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-114">This particular VM Scale Set has five instances, named BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 and BackEnd_4.</span></span>

<span data-ttu-id="2d0e5-115">當您相應增加 VM 調整集，就會建立的新執行個體。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-115">When you scale up a VM Scale Set a new instance is created.</span></span> <span data-ttu-id="2d0e5-116">hello VM 規模調整集合名稱 + hello 下一個執行個體數字，通常會是 hello 新虛擬機器擴展集執行個體名稱。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-116">hello new VM Scale Set instance name will typically be hello VM Scale Set name + hello next instance number.</span></span> <span data-ttu-id="2d0e5-117">在我們的範例中是 BackEnd_5。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-117">In our example, it is BackEnd_5.</span></span>

## <a name="mapping-vm-scale-set-load-balancers-tooeach-node-typevm-scale-set"></a><span data-ttu-id="2d0e5-118">對應 VM 規模集負載平衡器 tooeach 節點型別/VM 規模集</span><span class="sxs-lookup"><span data-stu-id="2d0e5-118">Mapping VM scale set load balancers tooeach node type/VM Scale Set</span></span>
<span data-ttu-id="2d0e5-119">如果您已部署您的叢集，從 hello 入口網站，或使用我們提供，然後當您取得一份資源群組下所有資源的 hello 範例資源管理員範本，您會看到每個虛擬機器擴展集或節點類型的 hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-119">If you have deployed your cluster from hello portal or have used hello sample Resource Manager template that we provided, then when you get a list of all resources under a Resource Group then you will see hello load balancers for each VM Scale Set or node type.</span></span>

<span data-ttu-id="2d0e5-120">hello 名稱會像這樣： **LB 集&lt;NodeType 名稱&gt;**。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-120">hello name would something like: **LB-&lt;NodeType name&gt;**.</span></span> <span data-ttu-id="2d0e5-121">例如，以下螢幕擷取畫面中的 LB-sfcluster4doc-0：</span><span class="sxs-lookup"><span data-stu-id="2d0e5-121">For example, LB-sfcluster4doc-0, as shown in this screenshot:</span></span>

![資源][Resources]

## <a name="remote-connect-tooa-vm-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="2d0e5-123">遠端連接 tooa 虛擬機器擴展集的執行個體或叢集節點</span><span class="sxs-lookup"><span data-stu-id="2d0e5-123">Remote connect tooa VM Scale Set instance or a cluster node</span></span>
<span data-ttu-id="2d0e5-124">在叢集中定義的每個節點類型都會安裝為不同的 VM 擴展集。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-124">Every Node type that is defined in a cluster is set up as a separate VM Scale Set.</span></span>  <span data-ttu-id="2d0e5-125">表示 hello 節點型別可以縮放向上或向下獨立和可由不同的 VM Sku。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-125">That means hello node types can be scaled up or down independently and can be made of different VM SKUs.</span></span> <span data-ttu-id="2d0e5-126">不同於單一執行個體的 Vm，hello 虛擬機器擴展集的執行個體不會收到自己的虛擬 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-126">Unlike single instance VMs, hello VM Scale Set instances do not get a virtual IP address of their own.</span></span> <span data-ttu-id="2d0e5-127">因此，它可以是位元挑戰時您所需的 IP 位址和連接埠，您可以使用 tooremote 連接 tooa 特定執行個體。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-127">So it can be a bit challenging when you are looking for an IP address and port that you can use tooremote connect tooa specific instance.</span></span>

<span data-ttu-id="2d0e5-128">以下是您可以依照 toodiscover hello 步驟它們。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-128">Here are hello steps you can follow toodiscover them.</span></span>

### <a name="step-1-find-out-hello-virtual-ip-address-for-hello-node-type-and-then-inbound-nat-rules-for-rdp"></a><span data-ttu-id="2d0e5-129">步驟 1： 了解 hello 節點型別 hello 虛擬 IP 位址，然後 RDP 的輸入 NAT 規則</span><span class="sxs-lookup"><span data-stu-id="2d0e5-129">Step 1: Find out hello virtual IP address for hello node type and then Inbound NAT rules for RDP</span></span>
<span data-ttu-id="2d0e5-130">中，您需要 tooget hello 順序 tooget 連入的 NAT 規則值所定義的 hello 資源定義的一部分**Microsoft.Network/loadBalancers**。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-130">In order tooget that, you need tooget hello inbound NAT rules values that were defined as a part of hello resource definition for **Microsoft.Network/loadBalancers**.</span></span>

<span data-ttu-id="2d0e5-131">在 hello 入口網站中，瀏覽 toohello 負載平衡器刀鋒視窗，然後**設定**。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-131">In hello portal, navigate toohello Load balancer blade and then **Settings**.</span></span>

![LBBlade][LBBlade]

<span data-ttu-id="2d0e5-133">在 [設定] 中，按一下 [輸入 NAT 規則]。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-133">In **Settings**, click on **Inbound NAT rules**.</span></span> <span data-ttu-id="2d0e5-134">這可讓您 hello IP 位址和連接埠，您可以使用 tooremote 連接 toohello 第一個虛擬機器擴展集的執行個體。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-134">This now gives you hello IP address and port that you can use tooremote connect toohello first VM Scale Set instance.</span></span> <span data-ttu-id="2d0e5-135">在 hello 以下螢幕擷取畫面，它是**104.42.106.156**和**3389**</span><span class="sxs-lookup"><span data-stu-id="2d0e5-135">In hello screenshot below, it is **104.42.106.156** and **3389**</span></span>

![NATRules][NATRules]

### <a name="step-2-find-out-hello-port-that-you-can-use-tooremote-connect-toohello-specific-vm-scale-set-instancenode"></a><span data-ttu-id="2d0e5-137">步驟 2： 了解 hello 連接埠，您可以使用 tooremote toohello 特定虛擬機器擴展集執行個體/節點連接</span><span class="sxs-lookup"><span data-stu-id="2d0e5-137">Step 2: Find out hello port that you can use tooremote connect toohello specific VM Scale Set instance/node</span></span>
<span data-ttu-id="2d0e5-138">本文件稍早我討論 hello 虛擬機器擴展集的執行個體將 toohello 節點的對應。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-138">Earlier in this document, I talked about how hello VM Scale Set instances map toohello nodes.</span></span> <span data-ttu-id="2d0e5-139">我們將使用該 toofigure 出 hello 確切的通訊埠。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-139">We will use that toofigure out hello exact port.</span></span>

<span data-ttu-id="2d0e5-140">hello 連接埠配置以遞增順序 hello 虛擬機器擴展集的執行個體。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-140">hello ports are allocated in ascending order of hello VM Scale Set instance.</span></span> <span data-ttu-id="2d0e5-141">因此在 hello 前端節點類型的範例中，每個 hello 五個執行個體的 hello 連接埠是 hello 下列。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-141">so in my example for hello FrontEnd node type, hello ports for each of hello five instances are hello following.</span></span> <span data-ttu-id="2d0e5-142">您 toodo 現在需要 hello 相同的對應虛擬機器擴展集執行個體。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-142">you now need toodo hello same mapping for your VM Scale Set instance.</span></span>

| <span data-ttu-id="2d0e5-143">**VM 擴展集執行個體**</span><span class="sxs-lookup"><span data-stu-id="2d0e5-143">**VM Scale Set Instance**</span></span> | <span data-ttu-id="2d0e5-144">**連接埠**</span><span class="sxs-lookup"><span data-stu-id="2d0e5-144">**Port**</span></span> |
| --- | --- |
| <span data-ttu-id="2d0e5-145">FrontEnd_0</span><span class="sxs-lookup"><span data-stu-id="2d0e5-145">FrontEnd_0</span></span> |<span data-ttu-id="2d0e5-146">3389</span><span class="sxs-lookup"><span data-stu-id="2d0e5-146">3389</span></span> |
| <span data-ttu-id="2d0e5-147">FrontEnd_1</span><span class="sxs-lookup"><span data-stu-id="2d0e5-147">FrontEnd_1</span></span> |<span data-ttu-id="2d0e5-148">3390</span><span class="sxs-lookup"><span data-stu-id="2d0e5-148">3390</span></span> |
| <span data-ttu-id="2d0e5-149">FrontEnd_2</span><span class="sxs-lookup"><span data-stu-id="2d0e5-149">FrontEnd_2</span></span> |<span data-ttu-id="2d0e5-150">3391</span><span class="sxs-lookup"><span data-stu-id="2d0e5-150">3391</span></span> |
| <span data-ttu-id="2d0e5-151">FrontEnd_3</span><span class="sxs-lookup"><span data-stu-id="2d0e5-151">FrontEnd_3</span></span> |<span data-ttu-id="2d0e5-152">3392</span><span class="sxs-lookup"><span data-stu-id="2d0e5-152">3392</span></span> |
| <span data-ttu-id="2d0e5-153">FrontEnd_4</span><span class="sxs-lookup"><span data-stu-id="2d0e5-153">FrontEnd_4</span></span> |<span data-ttu-id="2d0e5-154">3393</span><span class="sxs-lookup"><span data-stu-id="2d0e5-154">3393</span></span> |
| <span data-ttu-id="2d0e5-155">FrontEnd_5</span><span class="sxs-lookup"><span data-stu-id="2d0e5-155">FrontEnd_5</span></span> |<span data-ttu-id="2d0e5-156">3394</span><span class="sxs-lookup"><span data-stu-id="2d0e5-156">3394</span></span> |

### <a name="step-3-remote-connect-toohello-specific-vm-scale-set-instance"></a><span data-ttu-id="2d0e5-157">步驟 3： 遠端連線 toohello 特定虛擬機器擴展集執行個體</span><span class="sxs-lookup"><span data-stu-id="2d0e5-157">Step 3: Remote connect toohello specific VM Scale Set instance</span></span>
<span data-ttu-id="2d0e5-158">Hello 以下螢幕擷取畫面中使用遠端桌面連線 tooconnect toohello FrontEnd_1:</span><span class="sxs-lookup"><span data-stu-id="2d0e5-158">In hello screenshot below I use Remote Desktop Connection tooconnect toohello FrontEnd_1:</span></span>

![RDP][RDP]

## <a name="how-toochange-hello-rdp-port-range-values"></a><span data-ttu-id="2d0e5-160">Toochange hello RDP 連接埠值的範圍</span><span class="sxs-lookup"><span data-stu-id="2d0e5-160">How toochange hello RDP port range values</span></span>
### <a name="before-cluster-deployment"></a><span data-ttu-id="2d0e5-161">叢集部署之前</span><span class="sxs-lookup"><span data-stu-id="2d0e5-161">Before cluster deployment</span></span>
<span data-ttu-id="2d0e5-162">當您設定 hello 叢集使用的資源管理員範本時，您可以指定 hello 範圍 hello **inboundNatPools**。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-162">When you are setting up hello cluster using an Resource Manager template, you can specify hello range in hello **inboundNatPools**.</span></span>

<span data-ttu-id="2d0e5-163">移 toohello 資源定義**Microsoft.Network/loadBalancers**。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-163">Go toohello resource definition for **Microsoft.Network/loadBalancers**.</span></span> <span data-ttu-id="2d0e5-164">下，您會發現 hello 描述**inboundNatPools**。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-164">Under that you find hello description for **inboundNatPools**.</span></span>  <span data-ttu-id="2d0e5-165">取代 hello *frontendPortRangeStart*和*frontendPortRangeEnd*值。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-165">Replace hello *frontendPortRangeStart* and *frontendPortRangeEnd* values.</span></span>

![inboundNatPools][InboundNatPools]

### <a name="after-cluster-deployment"></a><span data-ttu-id="2d0e5-167">叢集部署之後</span><span class="sxs-lookup"><span data-stu-id="2d0e5-167">After cluster deployment</span></span>
<span data-ttu-id="2d0e5-168">這是稍微複雜，而且可能會導致 hello Vm 被回收。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-168">This is a bit more involved and may result in hello VMs getting recycled.</span></span> <span data-ttu-id="2d0e5-169">您現在就必須使用 Azure PowerShell tooset 新值。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-169">You will now have tooset new values using Azure PowerShell.</span></span> <span data-ttu-id="2d0e5-170">請確定您的電腦已安裝 Azure PowerShell 1.0+ 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-170">Make sure that Azure PowerShell 1.0 or later is installed on your machine.</span></span> <span data-ttu-id="2d0e5-171">如果您有不這麼做之前，我們強烈建議您遵循所述的 hello 步驟[如何 tooinstall 和設定 Azure PowerShell。](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="2d0e5-171">If you have not done this before, I strongly suggest that you follow hello steps outlined in [How tooinstall and configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="2d0e5-172">Azure 帳戶登入 tooyour。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-172">Sign in tooyour Azure account.</span></span> <span data-ttu-id="2d0e5-173">如果這個 PowerShell 命令因為某些原因無法運作，您應該檢查 Azure PowerShell 是否已正確安裝。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-173">If this PowerShell command fails for some reason, you should check whether you have Azure PowerShell installed correctly.</span></span>

```
Login-AzureRmAccount
```

<span data-ttu-id="2d0e5-174">執行下列 tooget 詳細資料，您的負載平衡器上的 hello 和您看到的 hello 描述的 hello 值**inboundNatPools**:</span><span class="sxs-lookup"><span data-stu-id="2d0e5-174">Run hello following tooget details on your load balancer and you see hello values for hello description for **inboundNatPools**:</span></span>

```
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load balancer name>
```

<span data-ttu-id="2d0e5-175">現在設定*frontendPortRangeEnd*和*frontendPortRangeStart* toohello 您想要的值。</span><span class="sxs-lookup"><span data-stu-id="2d0e5-175">Now set *frontendPortRangeEnd* and *frontendPortRangeStart* toohello values you want.</span></span>

```
$PropertiesObject = @{
    #Property = value;
}
Set-AzureRmResource -PropertyObject $PropertiesObject -ResourceGroupName <RG name> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load Balancer name> -ApiVersion <use hello API version that get returned> -Force
```


## <a name="next-steps"></a><span data-ttu-id="2d0e5-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2d0e5-176">Next steps</span></span>
* [<span data-ttu-id="2d0e5-177">Hello 「 任何位置部署 」 功能與使用 Azure 管理叢集的比較概觀</span><span class="sxs-lookup"><span data-stu-id="2d0e5-177">Overview of hello "Deploy anywhere" feature and a comparison with Azure-managed clusters</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="2d0e5-178">叢集安全性</span><span class="sxs-lookup"><span data-stu-id="2d0e5-178">Cluster security</span></span>](service-fabric-cluster-security.md)
* [<span data-ttu-id="2d0e5-179"> Service Fabric SDK 和開始使用</span><span class="sxs-lookup"><span data-stu-id="2d0e5-179"> Service Fabric SDK and getting started</span></span>](service-fabric-get-started.md)

<!--Image references-->
[NodeTypes]: ./media/service-fabric-cluster-nodetypes/NodeTypes.png
[Resources]: ./media/service-fabric-cluster-nodetypes/Resources.png
[InboundNatPools]: ./media/service-fabric-cluster-nodetypes/InboundNatPools.png
[LBBlade]: ./media/service-fabric-cluster-nodetypes/LBBlade.png
[NATRules]: ./media/service-fabric-cluster-nodetypes/NATRules.png
[RDP]: ./media/service-fabric-cluster-nodetypes/RDP.png
