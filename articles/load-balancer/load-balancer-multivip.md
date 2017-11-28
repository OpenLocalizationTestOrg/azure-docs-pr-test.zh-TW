---
title: "aaaMutiple Vip 的雲端服務"
description: "多個 Vip 的概觀以及如何 tooset 雲端服務上的多個 Vip"
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
ms.openlocfilehash: b3e0f2b24968cb75a7064484a09ffe94505bb70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multiple-vips-for-a-cloud-service"></a><span data-ttu-id="48a25-103">為單一雲端服務設定多個 VIP</span><span class="sxs-lookup"><span data-stu-id="48a25-103">Configure multiple VIPs for a cloud service</span></span>

<span data-ttu-id="48a25-104">您可以透過公用網際網路所使用的 IP 位址提供的 azure 的 hello 存取 Azure 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="48a25-104">You can access Azure cloud services over hello public Internet by using an IP address provided by Azure.</span></span> <span data-ttu-id="48a25-105">這個公用 IP 位址是參照的 tooas VIP (虛擬 IP)，因為它連結 toohello Azure 負載平衡器，並不 hello hello 雲端服務內的虛擬機器 (VM) 執行個體。</span><span class="sxs-lookup"><span data-stu-id="48a25-105">This public IP address is referred tooas a VIP (virtual IP) since it is linked toohello Azure load balancer, and not hello Virtual Machine (VM) instances within hello cloud service.</span></span> <span data-ttu-id="48a25-106">您可以使用單一 VIP 來存取雲端服務中的任何 VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="48a25-106">You can access any VM instance within a cloud service by using a single VIP.</span></span>

<span data-ttu-id="48a25-107">不過，有可能需要多個 VIP 案例做為進入點 toohello 相同雲端服務。</span><span class="sxs-lookup"><span data-stu-id="48a25-107">However, there are scenarios in which you may need more than one VIP as an entry point toohello same cloud service.</span></span> <span data-ttu-id="48a25-108">比方說，您的雲端服務可以裝載多個不同的客戶裝載每個站台需要 SSL 連線使用 hello 預設連接埠 443，或租用戶的網站。</span><span class="sxs-lookup"><span data-stu-id="48a25-108">For instance, your cloud service may host multiple websites that require SSL connectivity using hello default port of 443, as each site is hosted for a different customer, or tenant.</span></span> <span data-ttu-id="48a25-109">在此案例中，您會為每個網站需要 toohave 不同的公用對外 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="48a25-109">In this scenario, you need toohave a different public facing IP address for each website.</span></span> <span data-ttu-id="48a25-110">hello 圖說明典型的多租用戶 web 裝載的具有需要多個 SSL 憑證上 hello 相同公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="48a25-110">hello diagram below illustrates a typical multi-tenant web hosting with a need for multiple SSL certificates on hello same public port.</span></span>

![多重 VIP SSL 案例](./media/load-balancer-multivip/Figure1.png)

<span data-ttu-id="48a25-112">在上述所有 Vip 使用 hello hello 範例相同的公用連接埠 (443) 和流量會重新導向的 tooone 或多個負載平衡的 Vm hello 內部 IP 位址的 hello 雲端服務裝載 hello 的所有網站的唯一私用連接埠。</span><span class="sxs-lookup"><span data-stu-id="48a25-112">In hello example above, all VIPs use hello same public port (443) and traffic is redirected tooone or more load balanced VMs on a unique private port for hello internal IP address of hello cloud service hosting all hello websites.</span></span>

> [!NOTE]
> <span data-ttu-id="48a25-113">另一種情況需要 hello 使用 hello 多個 Vip 裝載多個 SQL AlwaysOn 可用性群組接聽程式 hello 相同設定的虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="48a25-113">Another situation requiring hello use hello multiple VIPs is hosting multiple SQL AlwaysOn availability group listeners on hello same set of Virtual Machines.</span></span>

<span data-ttu-id="48a25-114">Vip 是動態的根據預設，這表示 hello 實際的 IP 位址指派 toohello 雲端服務會隨著時間變更。</span><span class="sxs-lookup"><span data-stu-id="48a25-114">VIPs are dynamic by default, which means that hello actual IP address assigned toohello cloud service may change over time.</span></span> <span data-ttu-id="48a25-115">tooprevent，種情況，您可以保留 VIP 為您的服務。</span><span class="sxs-lookup"><span data-stu-id="48a25-115">tooprevent that from happening, you can reserve a VIP for your service.</span></span> <span data-ttu-id="48a25-116">toolearn 深入了解保留 Vip，請參閱[保留公用 IP](../virtual-network/virtual-networks-reserved-public-ip.md)。</span><span class="sxs-lookup"><span data-stu-id="48a25-116">toolearn more about reserved VIPs, see [Reserved Public IP](../virtual-network/virtual-networks-reserved-public-ip.md).</span></span>

> [!NOTE]
> <span data-ttu-id="48a25-117">如需有關 VIP 和保留的 IP 的定價資訊，請參閱 [IP 位址定價](https://azure.microsoft.com/pricing/details/ip-addresses/) 。</span><span class="sxs-lookup"><span data-stu-id="48a25-117">Please see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/) for information on pricing on VIPs and reserved IPs.</span></span>

<span data-ttu-id="48a25-118">您可以使用 PowerShell tooverify hello 您的雲端服務所使用的 Vip，以及新增和移除 Vip、 建立關聯的 VIP tooan 端點，並設定負載平衡的特定 VIP 上。</span><span class="sxs-lookup"><span data-stu-id="48a25-118">You can use PowerShell tooverify hello VIPs used by your cloud services, as well as add and remove VIPs, associate a VIP tooan endpoint, and configure load balancing on a specific VIP.</span></span>

## <a name="limitations"></a><span data-ttu-id="48a25-119">限制</span><span class="sxs-lookup"><span data-stu-id="48a25-119">Limitations</span></span>

<span data-ttu-id="48a25-120">此時，多重 VIP 功能是限制的 toohello 下列案例：</span><span class="sxs-lookup"><span data-stu-id="48a25-120">At this time, Multi VIP functionality is limited toohello following scenarios:</span></span>

* <span data-ttu-id="48a25-121">**僅限 IaaS**。</span><span class="sxs-lookup"><span data-stu-id="48a25-121">**IaaS only**.</span></span> <span data-ttu-id="48a25-122">您只能針對包含 VM 的雲端服務啟用多重 VIP。</span><span class="sxs-lookup"><span data-stu-id="48a25-122">You can only enable Multi VIP for cloud services that contain VMs.</span></span> <span data-ttu-id="48a25-123">您無法在具有角色執行個體的 PaaS 案例中使用多重 VIP。</span><span class="sxs-lookup"><span data-stu-id="48a25-123">You cannot use Multi VIP in PaaS scenarios with role instances.</span></span>
* <span data-ttu-id="48a25-124">**僅限 PowerShell**。</span><span class="sxs-lookup"><span data-stu-id="48a25-124">**PowerShell only**.</span></span> <span data-ttu-id="48a25-125">您只能使用 PowerShell 來管理多重 VIP。</span><span class="sxs-lookup"><span data-stu-id="48a25-125">You can only manage Multi VIP by using PowerShell.</span></span>

<span data-ttu-id="48a25-126">這些限制都是暫時的，隨時可能變更。</span><span class="sxs-lookup"><span data-stu-id="48a25-126">These limitations are temporary, and may change at any time.</span></span> <span data-ttu-id="48a25-127">請確定 toorevisit 此頁面 tooverify 未來變更。</span><span class="sxs-lookup"><span data-stu-id="48a25-127">Make sure toorevisit this page tooverify future changes.</span></span>

## <a name="how-tooadd-a-vip-tooa-cloud-service"></a><span data-ttu-id="48a25-128">Tooadd VIP tooa 雲端服務的方式</span><span class="sxs-lookup"><span data-stu-id="48a25-128">How tooadd a VIP tooa cloud service</span></span>
<span data-ttu-id="48a25-129">tooadd VIP tooyour 服務，執行下列 PowerShell 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="48a25-129">tooadd a VIP tooyour service, run hello following PowerShell command:</span></span>

```powershell
Add-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

<span data-ttu-id="48a25-130">此命令會顯示結果類似 toohello，下列範例：</span><span class="sxs-lookup"><span data-stu-id="48a25-130">This command displays a result similar toohello following sample:</span></span>

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Add-AzureVirtualIP   4bd7b638-d2e7-216f-ba38-5221233d70ce Succeeded

## <a name="how-tooremove-a-vip-from-a-cloud-service"></a><span data-ttu-id="48a25-131">如何從雲端服務的 VIP tooremove</span><span class="sxs-lookup"><span data-stu-id="48a25-131">How tooremove a VIP from a cloud service</span></span>
<span data-ttu-id="48a25-132">tooremove hello VIP 加入 tooyour 服務在上面，執行下列 PowerShell 命令的 hello 的 hello 範例：</span><span class="sxs-lookup"><span data-stu-id="48a25-132">tooremove hello VIP added tooyour service in hello example above, run hello following PowerShell command:</span></span>

```powershell
Remove-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

> [!IMPORTANT]
> <span data-ttu-id="48a25-133">如果不有任何相關聯的端點 tooit，您只可以移除 VIP。</span><span class="sxs-lookup"><span data-stu-id="48a25-133">You can only remove a VIP if it has no endpoints associated tooit.</span></span>


## <a name="how-tooretrieve-vip-information-from-a-cloud-service"></a><span data-ttu-id="48a25-134">如何從雲端服務的 tooretrieve VIP 資訊</span><span class="sxs-lookup"><span data-stu-id="48a25-134">How tooretrieve VIP information from a Cloud Service</span></span>
<span data-ttu-id="48a25-135">tooretrieve hello Vip 相關聯的雲端服務，執行下列 PowerShell 指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="48a25-135">tooretrieve hello VIPs associated with a cloud service, run hello following PowerShell script:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="48a25-136">hello 指令碼會顯示結果類似 toohello，下列範例：</span><span class="sxs-lookup"><span data-stu-id="48a25-136">hello script displays a result similar toohello following sample:</span></span>

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

<span data-ttu-id="48a25-137">在此範例中，hello 雲端服務都有 3 Vip:</span><span class="sxs-lookup"><span data-stu-id="48a25-137">In this example, hello cloud service has 3 VIPs:</span></span>

* <span data-ttu-id="48a25-138">**Vip1**是 hello 預設 VIP，但您知道，因為設定 tootrue IsDnsProgrammedName hello 值。</span><span class="sxs-lookup"><span data-stu-id="48a25-138">**Vip1** is hello default VIP, you know that because hello value for IsDnsProgrammedName is set tootrue.</span></span>
* <span data-ttu-id="48a25-139">**Vip2** 和 **Vip3** 因為沒有任何 IP 位址而不會予以使用。</span><span class="sxs-lookup"><span data-stu-id="48a25-139">**Vip2** and **Vip3** are not used as they do not have any IP addresses.</span></span> <span data-ttu-id="48a25-140">此外，它們只能將使用如果您將端點 toohello VIP 產生關聯。</span><span class="sxs-lookup"><span data-stu-id="48a25-140">They will only be used if you associate an endpoint toohello VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="48a25-141">有額外的 VIP 與端點相關聯時，才會向您的訂用帳戶收費。</span><span class="sxs-lookup"><span data-stu-id="48a25-141">Your subscription will only be charged for extra VIPs once they are associated with an endpoint.</span></span> <span data-ttu-id="48a25-142">如需定價的詳細資訊，請參閱 [IP 位址定價](https://azure.microsoft.com/pricing/details/ip-addresses/)。</span><span class="sxs-lookup"><span data-stu-id="48a25-142">For more information on pricing, see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/).</span></span>

## <a name="how-tooassociate-a-vip-tooan-endpoint"></a><span data-ttu-id="48a25-143">如何 tooassociate VIP tooan 端點</span><span class="sxs-lookup"><span data-stu-id="48a25-143">How tooassociate a VIP tooan endpoint</span></span>

<span data-ttu-id="48a25-144">在雲端服務 tooan 端點上，執行下列 PowerShell 命令的 hello tooassociate VIP:</span><span class="sxs-lookup"><span data-stu-id="48a25-144">tooassociate a VIP on a cloud service tooan endpoint, run hello following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -Protocol tcp -LocalPort 8080 -PublicPort 80 -VirtualIPName Vip2 |
    Update-AzureVM
```

<span data-ttu-id="48a25-145">hello 命令會建立稱為 「 連結的 toohello VIP 端點*Vip2*連接埠上*80*，並將它連結 toohello 名為 VM *myVM1*雲端服務中名為*myService*使用*TCP*連接埠上*8080*。</span><span class="sxs-lookup"><span data-stu-id="48a25-145">hello command creates an endpoint linked toohello VIP called *Vip2* on port *80*, and links it toohello VM named *myVM1* in a cloud service named *myService* using *TCP* on port *8080*.</span></span>

<span data-ttu-id="48a25-146">tooverify hello 組態，執行下列 PowerShell 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="48a25-146">tooverify hello configuration, run hello following PowerShell command:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="48a25-147">hello 輸出看起來類似下列範例的 toohello:</span><span class="sxs-lookup"><span data-stu-id="48a25-147">hello output looks similar toohello following example:</span></span>

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

## <a name="how-tooenable-load-balancing-on-a-specific-vip"></a><span data-ttu-id="48a25-148">如何 tooenable 上的負載平衡的特定 VIP</span><span class="sxs-lookup"><span data-stu-id="48a25-148">How tooenable load balancing on a specific VIP</span></span>

<span data-ttu-id="48a25-149">您可以將單一 VIP 與多部虛擬機器產生關聯，以達到負載平衡。</span><span class="sxs-lookup"><span data-stu-id="48a25-149">You can associate a single VIP with multiple virtual machines for load balancing purposes.</span></span> <span data-ttu-id="48a25-150">例如，假設您有名為 *myService* 的雲端服務，以及名為 *myVM1* 和 *myVM2* 的兩部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="48a25-150">For example, you have a cloud service named *myService*, and two virtual machines named *myVM1* and *myVM2*.</span></span> <span data-ttu-id="48a25-151">而您的雲端服務有多重 VIP，其中一個名為 *Vip2*。</span><span class="sxs-lookup"><span data-stu-id="48a25-151">And your cloud service has multiple VIPs, one of them named *Vip2*.</span></span> <span data-ttu-id="48a25-152">如果您想要的所有流量 tooport tooensure *81*上*Vip2*之間平均*myVM1*和*myVM2*連接埠上*8181*，請執行 hello 下列 PowerShell 指令碼：</span><span class="sxs-lookup"><span data-stu-id="48a25-152">If you want tooensure that all traffic tooport *81* on *Vip2* is balanced between *myVM1* and *myVM2* on port *8181*, run hello following PowerShell script:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2 -DefaultProbe |
    Update-AzureVM

Get-AzureVM -ServiceName myService -Name myVM2 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2  -DefaultProbe |
    Update-AzureVM
```

<span data-ttu-id="48a25-153">您也可以更新您的負載平衡器 toouse 不同的 VIP。</span><span class="sxs-lookup"><span data-stu-id="48a25-153">You can also update your load balancer toouse a different VIP.</span></span> <span data-ttu-id="48a25-154">例如，如果您要執行 hello 下列 PowerShell 命令，將變更 hello 負載平衡集 toouse 名為 Vip1 VIP:</span><span class="sxs-lookup"><span data-stu-id="48a25-154">For example, if you run hello PowerShell command below, you will change hello load balancing set toouse a VIP named Vip1:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName myService -LBSetName myLBSet -VirtualIPName Vip1
```

## <a name="next-steps"></a><span data-ttu-id="48a25-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="48a25-155">Next Steps</span></span>

[<span data-ttu-id="48a25-156">Azure 負載平衡器的 Log Analytics</span><span class="sxs-lookup"><span data-stu-id="48a25-156">Log analytics for Azure Load Balance</span></span>](load-balancer-monitor-log.md)

[<span data-ttu-id="48a25-157">網際網路面向的負載平衡器概觀</span><span class="sxs-lookup"><span data-stu-id="48a25-157">Internet facing load balancer overview</span></span>](load-balancer-internet-overview.md)

[<span data-ttu-id="48a25-158">開始使用網際網路面向的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="48a25-158">Get started on Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="48a25-159">虛擬網路概觀</span><span class="sxs-lookup"><span data-stu-id="48a25-159">Virtual Network Overview</span></span>](../virtual-network/virtual-networks-overview.md)

[<span data-ttu-id="48a25-160">保留的 IP REST API</span><span class="sxs-lookup"><span data-stu-id="48a25-160">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)
