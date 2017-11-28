---
title: "Service Fabric 節點類型與 VM 調整集 |Microsoft Docs"
description: "說明 Service Fabric 節點類型如何與 VM 調整集產生關聯，以及如何遠端連線到 VM 調整集執行個體或叢集節點。"
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
ms.openlocfilehash: 3b1a22bb3653abb68fc73645ad2cb623fabc7736
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="the-relationship-between-service-fabric-node-types-and-virtual-machine-scale-sets"></a><span data-ttu-id="59d3a-103">Service Fabric 節點類型與虛擬機器調整集之間的關聯性</span><span class="sxs-lookup"><span data-stu-id="59d3a-103">The relationship between Service Fabric node types and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="59d3a-104">虛擬機器調整集是一個 Azure 計算資源，可以用來將一組 VM 當做一個集合加以部署和管理。</span><span class="sxs-lookup"><span data-stu-id="59d3a-104">Virtual Machine Scale Sets are an Azure Compute resource you can use to deploy and manage a collection of virtual machines as a set.</span></span> <span data-ttu-id="59d3a-105">在 Service Fabric 叢集中定義的每個節點類型都會安裝為不同的 VM 擴展集。</span><span class="sxs-lookup"><span data-stu-id="59d3a-105">Every node type that is defined in a Service Fabric cluster is set up as a separate VM Scale Set.</span></span> <span data-ttu-id="59d3a-106">然後每個節點類型可以獨立相應增加或相應減少，可以開啟不同組的連接埠，並可以有不同的容量度量。</span><span class="sxs-lookup"><span data-stu-id="59d3a-106">Each node type can then be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span></span>

<span data-ttu-id="59d3a-107">下列螢幕擷取畫面顯示具有 FrontEnd 和 BackEnd 兩個節點類型的叢集。</span><span class="sxs-lookup"><span data-stu-id="59d3a-107">The following screen shot shows a cluster that has two node types: FrontEnd and BackEnd.</span></span>  <span data-ttu-id="59d3a-108">每個節點類型各有五個節點。</span><span class="sxs-lookup"><span data-stu-id="59d3a-108">Each node type has five nodes each.</span></span>

![有兩個節點類型的叢集螢幕擷取畫面][NodeTypes]

## <a name="mapping-vm-scale-set-instances-to-nodes"></a><span data-ttu-id="59d3a-110">將 VM 調整集執行個體對應至節點</span><span class="sxs-lookup"><span data-stu-id="59d3a-110">Mapping VM Scale Set instances to nodes</span></span>
<span data-ttu-id="59d3a-111">如您在上面看到的，VM 調整集執行個體是從執行個體 0 開始，然後漸漸增加。</span><span class="sxs-lookup"><span data-stu-id="59d3a-111">As you can see above, the VM Scale Set instances start from instance 0 and then goes up.</span></span> <span data-ttu-id="59d3a-112">編號反映在名稱中。</span><span class="sxs-lookup"><span data-stu-id="59d3a-112">The numbering is reflected in the names.</span></span> <span data-ttu-id="59d3a-113">例如，BackEnd_0 是 BackEnd VM 調整集的執行個體 0。</span><span class="sxs-lookup"><span data-stu-id="59d3a-113">For example, BackEnd_0 is instance 0 of the BackEnd VM Scale Set.</span></span> <span data-ttu-id="59d3a-114">這個特定的 VM 調整集有五個執行個體，名稱分別是 BackEnd_0、BackEnd_1、BackEnd_2、BackEnd_3、BackEnd_4。</span><span class="sxs-lookup"><span data-stu-id="59d3a-114">This particular VM Scale Set has five instances, named BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 and BackEnd_4.</span></span>

<span data-ttu-id="59d3a-115">當您相應增加 VM 調整集，就會建立的新執行個體。</span><span class="sxs-lookup"><span data-stu-id="59d3a-115">When you scale up a VM Scale Set a new instance is created.</span></span> <span data-ttu-id="59d3a-116">VM 調整集的名稱通常是 VM 調整集名稱 + 下一個執行個體編號。</span><span class="sxs-lookup"><span data-stu-id="59d3a-116">The new VM Scale Set instance name will typically be the VM Scale Set name + the next instance number.</span></span> <span data-ttu-id="59d3a-117">在我們的範例中是 BackEnd_5。</span><span class="sxs-lookup"><span data-stu-id="59d3a-117">In our example, it is BackEnd_5.</span></span>

## <a name="mapping-vm-scale-set-load-balancers-to-each-node-typevm-scale-set"></a><span data-ttu-id="59d3a-118">將 VM 調整集負載平衡器對應至每個節點類型/VM 調整集</span><span class="sxs-lookup"><span data-stu-id="59d3a-118">Mapping VM scale set load balancers to each node type/VM Scale Set</span></span>
<span data-ttu-id="59d3a-119">如果您已從入口網站或使用我們提供的範例 Resource Manager 範本部署您的叢集，您會得到一張資源群組下所有資源的清單，而且您會看到每個 VM 擴展集或節點類型的負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="59d3a-119">If you have deployed your cluster from the portal or have used the sample Resource Manager template that we provided, then when you get a list of all resources under a Resource Group then you will see the load balancers for each VM Scale Set or node type.</span></span>

<span data-ttu-id="59d3a-120">名稱類似 **LB-&lt;NodeType name&gt;**。</span><span class="sxs-lookup"><span data-stu-id="59d3a-120">The name would something like: **LB-&lt;NodeType name&gt;**.</span></span> <span data-ttu-id="59d3a-121">例如，以下螢幕擷取畫面中的 LB-sfcluster4doc-0：</span><span class="sxs-lookup"><span data-stu-id="59d3a-121">For example, LB-sfcluster4doc-0, as shown in this screenshot:</span></span>

![資源][Resources]

## <a name="remote-connect-to-a-vm-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="59d3a-123">遠端連線到 VM 調整集執行個體或叢集節點</span><span class="sxs-lookup"><span data-stu-id="59d3a-123">Remote connect to a VM Scale Set instance or a cluster node</span></span>
<span data-ttu-id="59d3a-124">在叢集中定義的每個節點類型都會安裝為不同的 VM 擴展集。</span><span class="sxs-lookup"><span data-stu-id="59d3a-124">Every Node type that is defined in a cluster is set up as a separate VM Scale Set.</span></span>  <span data-ttu-id="59d3a-125">這表示節點類型可以獨立相應增加或相應減少，且可由不同 VM SKU 組成。</span><span class="sxs-lookup"><span data-stu-id="59d3a-125">That means the node types can be scaled up or down independently and can be made of different VM SKUs.</span></span> <span data-ttu-id="59d3a-126">不同於單一執行個體的 VM，VM 調整集的執行個體不會收到自己的虛擬 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="59d3a-126">Unlike single instance VMs, the VM Scale Set instances do not get a virtual IP address of their own.</span></span> <span data-ttu-id="59d3a-127">所以當您要尋找可用來遠端連線至特定執行個體的 IP 位址和連接埠時，可能有點困難。</span><span class="sxs-lookup"><span data-stu-id="59d3a-127">So it can be a bit challenging when you are looking for an IP address and port that you can use to remote connect to a specific instance.</span></span>

<span data-ttu-id="59d3a-128">您可以依照以下步驟來找出它們。</span><span class="sxs-lookup"><span data-stu-id="59d3a-128">Here are the steps you can follow to discover them.</span></span>

### <a name="step-1-find-out-the-virtual-ip-address-for-the-node-type-and-then-inbound-nat-rules-for-rdp"></a><span data-ttu-id="59d3a-129">步驟 1：找出該節點類型的虛擬 IP 位址，然後找出 RDP 的輸入 NAT 規則</span><span class="sxs-lookup"><span data-stu-id="59d3a-129">Step 1: Find out the virtual IP address for the node type and then Inbound NAT rules for RDP</span></span>
<span data-ttu-id="59d3a-130">若要獲得這項資訊，您必須取得 **Microsoft.Network/loadBalancers**的資源定義中定義的輸入 NAT 規則值。</span><span class="sxs-lookup"><span data-stu-id="59d3a-130">In order to get that, you need to get the inbound NAT rules values that were defined as a part of the resource definition for **Microsoft.Network/loadBalancers**.</span></span>

<span data-ttu-id="59d3a-131">在入口網站中，瀏覽至 [負載平衡器] 刀鋒視窗的 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="59d3a-131">In the portal, navigate to the Load balancer blade and then **Settings**.</span></span>

![LBBlade][LBBlade]

<span data-ttu-id="59d3a-133">在 [設定] 中，按一下 [輸入 NAT 規則]。</span><span class="sxs-lookup"><span data-stu-id="59d3a-133">In **Settings**, click on **Inbound NAT rules**.</span></span> <span data-ttu-id="59d3a-134">這會給您可用來遠端連線至第一個 VM 調整集執行個體的 IP 位址和連接埠。</span><span class="sxs-lookup"><span data-stu-id="59d3a-134">This now gives you the IP address and port that you can use to remote connect to the first VM Scale Set instance.</span></span> <span data-ttu-id="59d3a-135">在以下的螢幕擷取畫面中是 **104.42.106.156** 和 **3389**</span><span class="sxs-lookup"><span data-stu-id="59d3a-135">In the screenshot below, it is **104.42.106.156** and **3389**</span></span>

![NATRules][NATRules]

### <a name="step-2-find-out-the-port-that-you-can-use-to-remote-connect-to-the-specific-vm-scale-set-instancenode"></a><span data-ttu-id="59d3a-137">步驟 2：找到可用來遠端連線至特定 VM 調整集執行個體/節點的連接埠</span><span class="sxs-lookup"><span data-stu-id="59d3a-137">Step 2: Find out the port that you can use to remote connect to the specific VM Scale Set instance/node</span></span>
<span data-ttu-id="59d3a-138">本文稍早討論了如何將 VM 調整集執行個體對應至節點。</span><span class="sxs-lookup"><span data-stu-id="59d3a-138">Earlier in this document, I talked about how the VM Scale Set instances map to the nodes.</span></span> <span data-ttu-id="59d3a-139">我們將使用它來找出確切的連接埠。</span><span class="sxs-lookup"><span data-stu-id="59d3a-139">We will use that to figure out the exact port.</span></span>

<span data-ttu-id="59d3a-140">連接埠是以 VM 擴展集執行個體的遞增順序配置。</span><span class="sxs-lookup"><span data-stu-id="59d3a-140">The ports are allocated in ascending order of the VM Scale Set instance.</span></span> <span data-ttu-id="59d3a-141">因此，在 FrontEnd 節點類型的範例中，五個執行個體的每個連接埠分別如下。</span><span class="sxs-lookup"><span data-stu-id="59d3a-141">so in my example for the FrontEnd node type, the ports for each of the five instances are the following.</span></span> <span data-ttu-id="59d3a-142">您現在需要對您的 VM 擴展集執行個體進行相同的對應。</span><span class="sxs-lookup"><span data-stu-id="59d3a-142">you now need to do the same mapping for your VM Scale Set instance.</span></span>

| <span data-ttu-id="59d3a-143">**VM 擴展集執行個體**</span><span class="sxs-lookup"><span data-stu-id="59d3a-143">**VM Scale Set Instance**</span></span> | <span data-ttu-id="59d3a-144">**連接埠**</span><span class="sxs-lookup"><span data-stu-id="59d3a-144">**Port**</span></span> |
| --- | --- |
| <span data-ttu-id="59d3a-145">FrontEnd_0</span><span class="sxs-lookup"><span data-stu-id="59d3a-145">FrontEnd_0</span></span> |<span data-ttu-id="59d3a-146">3389</span><span class="sxs-lookup"><span data-stu-id="59d3a-146">3389</span></span> |
| <span data-ttu-id="59d3a-147">FrontEnd_1</span><span class="sxs-lookup"><span data-stu-id="59d3a-147">FrontEnd_1</span></span> |<span data-ttu-id="59d3a-148">3390</span><span class="sxs-lookup"><span data-stu-id="59d3a-148">3390</span></span> |
| <span data-ttu-id="59d3a-149">FrontEnd_2</span><span class="sxs-lookup"><span data-stu-id="59d3a-149">FrontEnd_2</span></span> |<span data-ttu-id="59d3a-150">3391</span><span class="sxs-lookup"><span data-stu-id="59d3a-150">3391</span></span> |
| <span data-ttu-id="59d3a-151">FrontEnd_3</span><span class="sxs-lookup"><span data-stu-id="59d3a-151">FrontEnd_3</span></span> |<span data-ttu-id="59d3a-152">3392</span><span class="sxs-lookup"><span data-stu-id="59d3a-152">3392</span></span> |
| <span data-ttu-id="59d3a-153">FrontEnd_4</span><span class="sxs-lookup"><span data-stu-id="59d3a-153">FrontEnd_4</span></span> |<span data-ttu-id="59d3a-154">3393</span><span class="sxs-lookup"><span data-stu-id="59d3a-154">3393</span></span> |
| <span data-ttu-id="59d3a-155">FrontEnd_5</span><span class="sxs-lookup"><span data-stu-id="59d3a-155">FrontEnd_5</span></span> |<span data-ttu-id="59d3a-156">3394</span><span class="sxs-lookup"><span data-stu-id="59d3a-156">3394</span></span> |

### <a name="step-3-remote-connect-to-the-specific-vm-scale-set-instance"></a><span data-ttu-id="59d3a-157">步驟 3：遠端連線到特定 VM 調整集執行個體</span><span class="sxs-lookup"><span data-stu-id="59d3a-157">Step 3: Remote connect to the specific VM Scale Set instance</span></span>
<span data-ttu-id="59d3a-158">在以下螢幕擷取畫面中，使用「遠端桌面連接」來連線到 FrontEnd_1：</span><span class="sxs-lookup"><span data-stu-id="59d3a-158">In the screenshot below I use Remote Desktop Connection to connect to the FrontEnd_1:</span></span>

![RDP][RDP]

## <a name="how-to-change-the-rdp-port-range-values"></a><span data-ttu-id="59d3a-160">如何變更 RDP 連接埠範圍值</span><span class="sxs-lookup"><span data-stu-id="59d3a-160">How to change the RDP port range values</span></span>
### <a name="before-cluster-deployment"></a><span data-ttu-id="59d3a-161">叢集部署之前</span><span class="sxs-lookup"><span data-stu-id="59d3a-161">Before cluster deployment</span></span>
<span data-ttu-id="59d3a-162">當您使用 Resource Manager 範本設定叢集時，可以在 **inboundNatPools**指定範圍。</span><span class="sxs-lookup"><span data-stu-id="59d3a-162">When you are setting up the cluster using an Resource Manager template, you can specify the range in the **inboundNatPools**.</span></span>

<span data-ttu-id="59d3a-163">移至 **Microsoft.Network/loadBalancers**的資源定義。</span><span class="sxs-lookup"><span data-stu-id="59d3a-163">Go to the resource definition for **Microsoft.Network/loadBalancers**.</span></span> <span data-ttu-id="59d3a-164">您會在下面找到 **inboundNatPools**的描述。</span><span class="sxs-lookup"><span data-stu-id="59d3a-164">Under that you find the description for **inboundNatPools**.</span></span>  <span data-ttu-id="59d3a-165">取代 *frontendPortRangeStart* 和 *frontendPortRangeEnd* 值。</span><span class="sxs-lookup"><span data-stu-id="59d3a-165">Replace the *frontendPortRangeStart* and *frontendPortRangeEnd* values.</span></span>

![inboundNatPools][InboundNatPools]

### <a name="after-cluster-deployment"></a><span data-ttu-id="59d3a-167">叢集部署之後</span><span class="sxs-lookup"><span data-stu-id="59d3a-167">After cluster deployment</span></span>
<span data-ttu-id="59d3a-168">這稍微複雜一點，而且可能會導致 VM 設定被回收。</span><span class="sxs-lookup"><span data-stu-id="59d3a-168">This is a bit more involved and may result in the VMs getting recycled.</span></span> <span data-ttu-id="59d3a-169">您現在必須使用 Azure PowerShell 設定新的值。</span><span class="sxs-lookup"><span data-stu-id="59d3a-169">You will now have to set new values using Azure PowerShell.</span></span> <span data-ttu-id="59d3a-170">請確定您的電腦已安裝 Azure PowerShell 1.0+ 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="59d3a-170">Make sure that Azure PowerShell 1.0 or later is installed on your machine.</span></span> <span data-ttu-id="59d3a-171">如果您還沒安裝，強烈建議您依照 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="59d3a-171">If you have not done this before, I strongly suggest that you follow the steps outlined in [How to install and configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="59d3a-172">登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="59d3a-172">Sign in to your Azure account.</span></span> <span data-ttu-id="59d3a-173">如果這個 PowerShell 命令因為某些原因無法運作，您應該檢查 Azure PowerShell 是否已正確安裝。</span><span class="sxs-lookup"><span data-stu-id="59d3a-173">If this PowerShell command fails for some reason, you should check whether you have Azure PowerShell installed correctly.</span></span>

```
Login-AzureRmAccount
```

<span data-ttu-id="59d3a-174">執行下列命令取得負載平衡器的詳細資料，您會看到 **inboundNatPools**的值以及描述：</span><span class="sxs-lookup"><span data-stu-id="59d3a-174">Run the following to get details on your load balancer and you see the values for the description for **inboundNatPools**:</span></span>

```
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load balancer name>
```

<span data-ttu-id="59d3a-175">現在將 *frontendPortRangeStart* 和 *frontendPortRangeEnd* 設為您要的值。</span><span class="sxs-lookup"><span data-stu-id="59d3a-175">Now set *frontendPortRangeEnd* and *frontendPortRangeStart* to the values you want.</span></span>

```
$PropertiesObject = @{
    #Property = value;
}
Set-AzureRmResource -PropertyObject $PropertiesObject -ResourceGroupName <RG name> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load Balancer name> -ApiVersion <use the API version that get returned> -Force
```


## <a name="next-steps"></a><span data-ttu-id="59d3a-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="59d3a-176">Next steps</span></span>
* [<span data-ttu-id="59d3a-177">「到處部署」功能和與 Azure 受管理叢集比較的概觀</span><span class="sxs-lookup"><span data-stu-id="59d3a-177">Overview of the "Deploy anywhere" feature and a comparison with Azure-managed clusters</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="59d3a-178">叢集安全性</span><span class="sxs-lookup"><span data-stu-id="59d3a-178">Cluster security</span></span>](service-fabric-cluster-security.md)
* [<span data-ttu-id="59d3a-179"> Service Fabric SDK 和開始使用</span><span class="sxs-lookup"><span data-stu-id="59d3a-179"> Service Fabric SDK and getting started</span></span>](service-fabric-get-started.md)

<!--Image references-->
[NodeTypes]: ./media/service-fabric-cluster-nodetypes/NodeTypes.png
[Resources]: ./media/service-fabric-cluster-nodetypes/Resources.png
[InboundNatPools]: ./media/service-fabric-cluster-nodetypes/InboundNatPools.png
[LBBlade]: ./media/service-fabric-cluster-nodetypes/LBBlade.png
[NATRules]: ./media/service-fabric-cluster-nodetypes/NATRules.png
[RDP]: ./media/service-fabric-cluster-nodetypes/RDP.png
