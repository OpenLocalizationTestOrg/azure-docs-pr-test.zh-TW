---
title: "單一雲端服務有多重 VIP"
description: "MultiVIP 的概觀以及如何在雲端服務上設定多重 VIP"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 85f6d26a-3df5-4b8e-96a1-92b2793b5284
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: f40e0501eed8d5f296e7c79d8a35705a695ae6fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-multiple-vips-for-a-cloud-service"></a><span data-ttu-id="b7ba3-103">為單一雲端服務設定多個 VIP</span><span class="sxs-lookup"><span data-stu-id="b7ba3-103">Configure multiple VIPs for a cloud service</span></span>

<span data-ttu-id="b7ba3-104">您可以使用 Azure 所提供的 IP 位址，透過公用網際網路存取 Azure 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="b7ba3-104">You can access Azure cloud services over the public Internet by using an IP address provided by Azure.</span></span> <span data-ttu-id="b7ba3-105">此公用 IP 位址也稱為 VIP (虛擬 IP)，因為它會連結至 Azure Load Balancer，而且不是雲端服務中的虛擬機器 (VM) 執行個體。</span><span class="sxs-lookup"><span data-stu-id="b7ba3-105">This public IP address is referred to as a VIP (virtual IP) since it is linked to the Azure load balancer, and not the Virtual Machine (VM) instances within the cloud service.</span></span> <span data-ttu-id="b7ba3-106">您可以使用單一 VIP 來存取雲端服務中的任何 VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="b7ba3-106">You can access any VM instance within a cloud service by using a single VIP.</span></span>

<span data-ttu-id="b7ba3-107">不過，在某些情況下，您可能需要一個以上的 VIP 作為相同雲端服務的進入點。</span><span class="sxs-lookup"><span data-stu-id="b7ba3-107">However, there are scenarios in which you may need more than one VIP as an entry point to the same cloud service.</span></span> <span data-ttu-id="b7ba3-108">比方說，您的雲端服務可以裝載多個需要使用預設連接埠 443 進行 SSL 連線的網站，因為每個網站是針對不同的客戶或租用戶進行裝載。</span><span class="sxs-lookup"><span data-stu-id="b7ba3-108">For instance, your cloud service may host multiple websites that require SSL connectivity using the default port of 443, as each site is hosted for a different customer, or tenant.</span></span> <span data-ttu-id="b7ba3-109">在此情況下，每個網站都需要有不同的公開 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b7ba3-109">In this scenario, you need to have a different public facing IP address for each website.</span></span> <span data-ttu-id="b7ba3-110">下圖說明典型的多租用戶 Web 裝載，它在相同的公用連接埠上需要有多個 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="b7ba3-110">The diagram below illustrates a typical multi-tenant web hosting with a need for multiple SSL certificates on the same public port.</span></span>

![多重 VIP SSL 案例](./media/load-balancer-multivip/Figure1.png)

<span data-ttu-id="b7ba3-112">在上面的範例中，所有 VIP 都使用相同的公用連接埠 (443)，而流量會重新導向至裝載所有網站之雲端服務的內部 IP 位址中唯一私人連接埠上的一或多個負載平衡 VM。</span><span class="sxs-lookup"><span data-stu-id="b7ba3-112">In the example above, all VIPs use the same public port (443) and traffic is redirected to one or more load balanced VMs on a unique private port for the internal IP address of the cloud service hosting all the websites.</span></span>

> [!NOTE]
> <span data-ttu-id="b7ba3-113">需要使用多重 VIP 的另一個狀況，是在同一組虛擬機器上裝載多個 SQL AlwaysOn 可用性群組接聽程式。</span><span class="sxs-lookup"><span data-stu-id="b7ba3-113">Another situation requiring the use the multiple VIPs is hosting multiple SQL AlwaysOn availability group listeners on the same set of Virtual Machines.</span></span>

<span data-ttu-id="b7ba3-114">VIP 預設是動態的，這表示指派給雲端服務的實際 IP 位址會隨著時間改變。</span><span class="sxs-lookup"><span data-stu-id="b7ba3-114">VIPs are dynamic by default, which means that the actual IP address assigned to the cloud service may change over time.</span></span> <span data-ttu-id="b7ba3-115">若要防止發生該狀況，您可以為您的服務保留 VIP。</span><span class="sxs-lookup"><span data-stu-id="b7ba3-115">To prevent that from happening, you can reserve a VIP for your service.</span></span> <span data-ttu-id="b7ba3-116">若要深入了解保留的 VIP，請參閱 [保留的公用 IP](../virtual-network/virtual-networks-reserved-public-ip.md)。</span><span class="sxs-lookup"><span data-stu-id="b7ba3-116">To learn more about reserved VIPs, see [Reserved Public IP](../virtual-network/virtual-networks-reserved-public-ip.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b7ba3-117">如需有關 VIP 和保留的 IP 的定價資訊，請參閱 [IP 位址定價](https://azure.microsoft.com/pricing/details/ip-addresses/) 。</span><span class="sxs-lookup"><span data-stu-id="b7ba3-117">Please see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/) for information on pricing on VIPs and reserved IPs.</span></span>

<span data-ttu-id="b7ba3-118">您可以使用 PowerShell 來驗證雲端服務所使用的 VIP，以及新增和移除 VIP、將 VIP 關聯到端點，以及在特定 VIP 上設定負載平衡。</span><span class="sxs-lookup"><span data-stu-id="b7ba3-118">You can use PowerShell to verify the VIPs used by your cloud services, as well as add and remove VIPs, associate a VIP to an endpoint, and configure load balancing on a specific VIP.</span></span>

## <a name="limitations"></a><span data-ttu-id="b7ba3-119">限制</span><span class="sxs-lookup"><span data-stu-id="b7ba3-119">Limitations</span></span>

<span data-ttu-id="b7ba3-120">目前，多重 VIP 功能僅適用於下列案例：</span><span class="sxs-lookup"><span data-stu-id="b7ba3-120">At this time, Multi VIP functionality is limited to the following scenarios:</span></span>

* <span data-ttu-id="b7ba3-121">**僅限 IaaS**。</span><span class="sxs-lookup"><span data-stu-id="b7ba3-121">**IaaS only**.</span></span> <span data-ttu-id="b7ba3-122">您只能針對包含 VM 的雲端服務啟用多重 VIP。</span><span class="sxs-lookup"><span data-stu-id="b7ba3-122">You can only enable Multi VIP for cloud services that contain VMs.</span></span> <span data-ttu-id="b7ba3-123">您無法在具有角色執行個體的 PaaS 案例中使用多重 VIP。</span><span class="sxs-lookup"><span data-stu-id="b7ba3-123">You cannot use Multi VIP in PaaS scenarios with role instances.</span></span>
* <span data-ttu-id="b7ba3-124">**僅限 PowerShell**。</span><span class="sxs-lookup"><span data-stu-id="b7ba3-124">**PowerShell only**.</span></span> <span data-ttu-id="b7ba3-125">您只能使用 PowerShell 來管理多重 VIP。</span><span class="sxs-lookup"><span data-stu-id="b7ba3-125">You can only manage Multi VIP by using PowerShell.</span></span>

<span data-ttu-id="b7ba3-126">這些限制都是暫時的，隨時可能變更。</span><span class="sxs-lookup"><span data-stu-id="b7ba3-126">These limitations are temporary, and may change at any time.</span></span> <span data-ttu-id="b7ba3-127">請務必再次瀏覽此頁面，以確認未來變更。</span><span class="sxs-lookup"><span data-stu-id="b7ba3-127">Make sure to revisit this page to verify future changes.</span></span>

## <a name="how-to-add-a-vip-to-a-cloud-service"></a><span data-ttu-id="b7ba3-128">如何將 VIP 新增至雲端服務</span><span class="sxs-lookup"><span data-stu-id="b7ba3-128">How to add a VIP to a cloud service</span></span>
<span data-ttu-id="b7ba3-129">若要將 VIP 新增至您的服務，請執行下列 PowerShell 命令：</span><span class="sxs-lookup"><span data-stu-id="b7ba3-129">To add a VIP to your service, run the following PowerShell command:</span></span>

```powershell
Add-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

<span data-ttu-id="b7ba3-130">此命令會顯示類似下列範例的結果：</span><span class="sxs-lookup"><span data-stu-id="b7ba3-130">This command displays a result similar to the following sample:</span></span>

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Add-AzureVirtualIP   4bd7b638-d2e7-216f-ba38-5221233d70ce Succeeded

## <a name="how-to-remove-a-vip-from-a-cloud-service"></a><span data-ttu-id="b7ba3-131">如何從雲端服務移除 VIP</span><span class="sxs-lookup"><span data-stu-id="b7ba3-131">How to remove a VIP from a cloud service</span></span>
<span data-ttu-id="b7ba3-132">若要移除在上述範例中新增您的服務的 VIP，請執行下列 PowerShell 命令：</span><span class="sxs-lookup"><span data-stu-id="b7ba3-132">To remove the VIP added to your service in the example above, run the following PowerShell command:</span></span>

```powershell
Remove-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

> [!IMPORTANT]
> <span data-ttu-id="b7ba3-133">您只能移除沒有任何相關端點的 VIP。</span><span class="sxs-lookup"><span data-stu-id="b7ba3-133">You can only remove a VIP if it has no endpoints associated to it.</span></span>


## <a name="how-to-retrieve-vip-information-from-a-cloud-service"></a><span data-ttu-id="b7ba3-134">如何從雲端服務擷取 VIP 資訊</span><span class="sxs-lookup"><span data-stu-id="b7ba3-134">How to retrieve VIP information from a Cloud Service</span></span>
<span data-ttu-id="b7ba3-135">若要擷取與雲端服務相關聯的 VIP，請執行下列 PowerShell 指令碼：</span><span class="sxs-lookup"><span data-stu-id="b7ba3-135">To retrieve the VIPs associated with a cloud service, run the following PowerShell script:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="b7ba3-136">該指令碼會顯示類似下列範例的結果：</span><span class="sxs-lookup"><span data-stu-id="b7ba3-136">The script displays a result similar to the following sample:</span></span>

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

<span data-ttu-id="b7ba3-137">在此範例中，雲端服務有 3 個 VIP：</span><span class="sxs-lookup"><span data-stu-id="b7ba3-137">In this example, the cloud service has 3 VIPs:</span></span>

* <span data-ttu-id="b7ba3-138">**Vip1** 是預設 VIP，您知道因為 IsDnsProgrammedName 的值已設定為 true。</span><span class="sxs-lookup"><span data-stu-id="b7ba3-138">**Vip1** is the default VIP, you know that because the value for IsDnsProgrammedName is set to true.</span></span>
* <span data-ttu-id="b7ba3-139">**Vip2** 和 **Vip3** 因為沒有任何 IP 位址而不會予以使用。</span><span class="sxs-lookup"><span data-stu-id="b7ba3-139">**Vip2** and **Vip3** are not used as they do not have any IP addresses.</span></span> <span data-ttu-id="b7ba3-140">唯有將端點關聯到 VIP，才會予以使用。</span><span class="sxs-lookup"><span data-stu-id="b7ba3-140">They will only be used if you associate an endpoint to the VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="b7ba3-141">有額外的 VIP 與端點相關聯時，才會向您的訂用帳戶收費。</span><span class="sxs-lookup"><span data-stu-id="b7ba3-141">Your subscription will only be charged for extra VIPs once they are associated with an endpoint.</span></span> <span data-ttu-id="b7ba3-142">如需定價的詳細資訊，請參閱 [IP 位址定價](https://azure.microsoft.com/pricing/details/ip-addresses/)。</span><span class="sxs-lookup"><span data-stu-id="b7ba3-142">For more information on pricing, see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/).</span></span>

## <a name="how-to-associate-a-vip-to-an-endpoint"></a><span data-ttu-id="b7ba3-143">如何將 VIP 關聯至端點</span><span class="sxs-lookup"><span data-stu-id="b7ba3-143">How to associate a VIP to an endpoint</span></span>

<span data-ttu-id="b7ba3-144">若要將雲端服務上的 VIP 關聯至端點，請執行下列 PowerShell 命令：</span><span class="sxs-lookup"><span data-stu-id="b7ba3-144">To associate a VIP on a cloud service to an endpoint, run the following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -Protocol tcp -LocalPort 8080 -PublicPort 80 -VirtualIPName Vip2 |
    Update-AzureVM
```

<span data-ttu-id="b7ba3-145">該命令會建立一個連結至連接埠 *80* 上名為 *Vip2* 之 VIP 的端點，並使用連接埠 *8080* 上的 *TCP* 將它連結至名為 *myService* 的雲端服務中名為 *myVM1* 的 VM。</span><span class="sxs-lookup"><span data-stu-id="b7ba3-145">The command creates an endpoint linked to the VIP called *Vip2* on port *80*, and links it to the VM named *myVM1* in a cloud service named *myService* using *TCP* on port *8080*.</span></span>

<span data-ttu-id="b7ba3-146">若要驗證組態，請執行下列 PowerShell 命令：</span><span class="sxs-lookup"><span data-stu-id="b7ba3-146">To verify the configuration, run the following PowerShell command:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="b7ba3-147">輸出大致如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="b7ba3-147">The output looks similar to the following example:</span></span>

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         : 191.238.74.13
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

## <a name="how-to-enable-load-balancing-on-a-specific-vip"></a><span data-ttu-id="b7ba3-148">如何在特定 VIP 上啟用負載平衡</span><span class="sxs-lookup"><span data-stu-id="b7ba3-148">How to enable load balancing on a specific VIP</span></span>

<span data-ttu-id="b7ba3-149">您可以將單一 VIP 與多部虛擬機器產生關聯，以達到負載平衡。</span><span class="sxs-lookup"><span data-stu-id="b7ba3-149">You can associate a single VIP with multiple virtual machines for load balancing purposes.</span></span> <span data-ttu-id="b7ba3-150">例如，假設您有名為 *myService* 的雲端服務，以及名為 *myVM1* 和 *myVM2* 的兩部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b7ba3-150">For example, you have a cloud service named *myService*, and two virtual machines named *myVM1* and *myVM2*.</span></span> <span data-ttu-id="b7ba3-151">而您的雲端服務有多重 VIP，其中一個名為 *Vip2*。</span><span class="sxs-lookup"><span data-stu-id="b7ba3-151">And your cloud service has multiple VIPs, one of them named *Vip2*.</span></span> <span data-ttu-id="b7ba3-152">如果您想確保對 *Vip2* 上連接埠 *81* 的所有流量會在連接埠 *8181* 上的 *myVM1* 與 *myVM2* 之間達到平衡，請執行下列 PowerShell 指令碼：</span><span class="sxs-lookup"><span data-stu-id="b7ba3-152">If you want to ensure that all traffic to port *81* on *Vip2* is balanced between *myVM1* and *myVM2* on port *8181*, run the following PowerShell script:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2 -DefaultProbe |
    Update-AzureVM

Get-AzureVM -ServiceName myService -Name myVM2 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2  -DefaultProbe |
    Update-AzureVM
```

<span data-ttu-id="b7ba3-153">您也可以更新您的負載平衡器，以使用不同的 VIP。</span><span class="sxs-lookup"><span data-stu-id="b7ba3-153">You can also update your load balancer to use a different VIP.</span></span> <span data-ttu-id="b7ba3-154">比方說，如果您執行下列 PowerShell 命令，您將將負載平衡集變更為使用名為 Vip1 的 VIP：</span><span class="sxs-lookup"><span data-stu-id="b7ba3-154">For example, if you run the PowerShell command below, you will change the load balancing set to use a VIP named Vip1:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName myService -LBSetName myLBSet -VirtualIPName Vip1
```

## <a name="next-steps"></a><span data-ttu-id="b7ba3-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b7ba3-155">Next Steps</span></span>

[<span data-ttu-id="b7ba3-156">Azure 負載平衡器的 Log Analytics</span><span class="sxs-lookup"><span data-stu-id="b7ba3-156">Log analytics for Azure Load Balance</span></span>](load-balancer-monitor-log.md)

[<span data-ttu-id="b7ba3-157">網際網路面向的負載平衡器概觀</span><span class="sxs-lookup"><span data-stu-id="b7ba3-157">Internet facing load balancer overview</span></span>](load-balancer-internet-overview.md)

[<span data-ttu-id="b7ba3-158">開始使用網際網路面向的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="b7ba3-158">Get started on Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="b7ba3-159">虛擬網路概觀</span><span class="sxs-lookup"><span data-stu-id="b7ba3-159">Virtual Network Overview</span></span>](../virtual-network/virtual-networks-overview.md)

[<span data-ttu-id="b7ba3-160">保留的 IP REST API</span><span class="sxs-lookup"><span data-stu-id="b7ba3-160">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)
