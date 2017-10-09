---
title: "aaaManage Azure 保留的 IP 位址 （傳統）-PowerShell |Microsoft 文件"
description: "了解保留的 IP 位址 （傳統） 以及 toomanage 它們使用 PowerShell。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 34652a55-3ab8-4c2d-8fb2-43684033b191
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: c0a77b2ab8b1ab9bef6015c903eb735ea4358a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="reserved-ip-addresses-classic"></a><span data-ttu-id="23673-103">保留的 IP 位址 (傳統)</span><span class="sxs-lookup"><span data-stu-id="23673-103">Reserved IP addresses (Classic)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="23673-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="23673-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="23673-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="23673-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="23673-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="23673-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="23673-107">範本</span><span class="sxs-lookup"><span data-stu-id="23673-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="23673-108">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="23673-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

<span data-ttu-id="23673-109">Azure 中的 IP 位址分為兩個類別：動態和保留。</span><span class="sxs-lookup"><span data-stu-id="23673-109">IP addresses in Azure fall into two categories: dynamic and reserved.</span></span> <span data-ttu-id="23673-110">依預設由 Azure 管理的公用 IP 位址是動態的。</span><span class="sxs-lookup"><span data-stu-id="23673-110">Public IP addresses managed by Azure are dynamic by default.</span></span> <span data-ttu-id="23673-111">該 hello 用於給定的雲端服務 (VIP) 的 IP 位址的方式或 tooaccess 資源遭到關閉或停止 （取消配置） 時，VM 或角色執行個體直接 (ILPIP) 可以從時間 tootime 變更。</span><span class="sxs-lookup"><span data-stu-id="23673-111">That means that hello IP address used for a given cloud service (VIP) or tooaccess a VM or role instance directly (ILPIP) can change from time tootime, when resources are shut down or stopped (deallocated).</span></span>

<span data-ttu-id="23673-112">tooprevent 變更 IP 位址，您可以保留的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="23673-112">tooprevent IP addresses from changing, you can reserve an IP address.</span></span> <span data-ttu-id="23673-113">保留的 Ip 僅做 VIP，確保 hello 雲端服務會維持為 hello 相同，因為即使資源都已關閉或停止 （取消配置） 該 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="23673-113">Reserved IPs can be used only as a VIP, ensuring that hello IP address for hello cloud service remains hello same, even as resources are shut down or stopped (deallocated).</span></span> <span data-ttu-id="23673-114">此外，您可以轉換現有的動態 Ip 做 VIP tooa 保留 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="23673-114">Furthermore, you can convert existing dynamic IPs used as a VIP tooa reserved IP address.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="23673-115">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="23673-115">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="23673-116">本文說明如何使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="23673-116">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="23673-117">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="23673-117">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="23673-118">了解如何 tooreserve 靜態公用 IP 位址使用 hello [Resource Manager 部署模型](virtual-network-ip-addresses-overview-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="23673-118">Learn how tooreserve a static public IP address using hello [Resource Manager deployment model](virtual-network-ip-addresses-overview-arm.md).</span></span>

<span data-ttu-id="23673-119">在 Azure 中的 toolearn 進一步了解 IP 位址，請閱讀 hello [IP 位址](virtual-network-ip-addresses-overview-classic.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="23673-119">toolearn more about IP addresses in Azure, read hello [IP addresses](virtual-network-ip-addresses-overview-classic.md) article.</span></span>

## <a name="when-do-i-need-a-reserved-ip"></a><span data-ttu-id="23673-120">何時需要保留的 IP？</span><span class="sxs-lookup"><span data-stu-id="23673-120">When do I need a reserved IP?</span></span>
* <span data-ttu-id="23673-121">**您想要訂用帳戶中保留的 hello IP 的 tooensure**。</span><span class="sxs-lookup"><span data-stu-id="23673-121">**You want tooensure that hello IP is reserved in your subscription**.</span></span> <span data-ttu-id="23673-122">如果您想 tooreserve 的 IP 位址，才會釋放，從您的訂用帳戶，在任何情況下，您應該使用保留公用 IP。</span><span class="sxs-lookup"><span data-stu-id="23673-122">If you want tooreserve an IP address that is not released from your subscription under any circumstance, you should use a reserved public IP.</span></span>  
* <span data-ttu-id="23673-123">**您想要您與雲端服務的 IP toostay 即使透過停止或取消配置狀態 (Vm)**。</span><span class="sxs-lookup"><span data-stu-id="23673-123">**You want your IP toostay with your cloud service even across stopped or deallocated state (VMs)**.</span></span> <span data-ttu-id="23673-124">如果您想使用的 IP 位址不會變更，來存取您服務 toobe，即使 hello 中的 Vm 雲端服務都已關閉或停止 （取消配置）。</span><span class="sxs-lookup"><span data-stu-id="23673-124">If you want your service toobe accessed by using an IP address that doesn't change, even when VMs in hello cloud service are shut down or stop (deallocated).</span></span>
* <span data-ttu-id="23673-125">**您想要從 Azure 的輸出流量使用可預期的 IP 位址的 tooensure**。</span><span class="sxs-lookup"><span data-stu-id="23673-125">**You want tooensure that outbound traffic from Azure uses a predictable IP address**.</span></span> <span data-ttu-id="23673-126">您可能需要您在內部部署防火牆設定 tooallow 唯一流量來自特定 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="23673-126">You may have your on-premises firewall configured tooallow only traffic from specific IP addresses.</span></span> <span data-ttu-id="23673-127">您可以藉由保留 IP，知道 hello 來源 IP 位址，而不需要您的防火牆規則，因為 tooan IP 變更 tooupdate。</span><span class="sxs-lookup"><span data-stu-id="23673-127">By reserving an IP, you know hello source IP address, and don't need tooupdate your firewall rules due tooan IP change.</span></span>

## <a name="faq"></a><span data-ttu-id="23673-128">常見問題集</span><span class="sxs-lookup"><span data-stu-id="23673-128">FAQ</span></span>
1. <span data-ttu-id="23673-129">我是否可以針對所有 Azure 服務都使用保留的 IP？</span><span class="sxs-lookup"><span data-stu-id="23673-129">Can I use a reserved IP for all Azure services?</span></span> <br>
    <span data-ttu-id="23673-130">否。</span><span class="sxs-lookup"><span data-stu-id="23673-130">No.</span></span> <span data-ttu-id="23673-131">保留的 IP 僅可用於 VM 和雲端服務透過 VIP 公開的執行個體角色。</span><span class="sxs-lookup"><span data-stu-id="23673-131">Reserved IPs can only be used for VMs and cloud service instance roles exposed through a VIP.</span></span>
2. <span data-ttu-id="23673-132">我可以有多少保留的 IP？</span><span class="sxs-lookup"><span data-stu-id="23673-132">How many reserved IPs can I have?</span></span> <br>
    <span data-ttu-id="23673-133">如需詳細資訊，請參閱 hello [Azure 限制](../azure-subscription-service-limits.md#networking-limits)發行項。</span><span class="sxs-lookup"><span data-stu-id="23673-133">For details, see hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
3. <span data-ttu-id="23673-134">保留的 IP 是否會收取費用？</span><span class="sxs-lookup"><span data-stu-id="23673-134">Is there a charge for reserved IPs?</span></span> <br>
    <span data-ttu-id="23673-135">有時是。</span><span class="sxs-lookup"><span data-stu-id="23673-135">Sometimes.</span></span> <span data-ttu-id="23673-136">如需定價詳細資料，請參閱 hello[保留 IP 位址定價詳細資料](http://go.microsoft.com/fwlink/?LinkID=398482)頁面。</span><span class="sxs-lookup"><span data-stu-id="23673-136">For pricing details, see hello [Reserved IP Address Pricing Details](http://go.microsoft.com/fwlink/?LinkID=398482) page.</span></span>
4. <span data-ttu-id="23673-137">我該如何保留 IP 位址？</span><span class="sxs-lookup"><span data-stu-id="23673-137">How do I reserve an IP address?</span></span> <br>
    <span data-ttu-id="23673-138">您可以使用 PowerShell，hello [Azure 管理 REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx)，或使用 hello [Azure 入口網站](https://portal.azure.com)tooreserve Azure 地區內的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="23673-138">You can use PowerShell, hello [Azure Management REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx), or hello [Azure portal](https://portal.azure.com) tooreserve an IP address in an Azure region.</span></span> <span data-ttu-id="23673-139">保留的 IP 位址是相關聯的 tooyour 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="23673-139">A reserved IP address is associated tooyour subscription.</span></span>
5. <span data-ttu-id="23673-140">我是否可以將保留的 IP 位址與同質群組型 VNet 搭配使用？</span><span class="sxs-lookup"><span data-stu-id="23673-140">Can I use a reserved IP with affinity group-based VNets?</span></span> <br>
    <span data-ttu-id="23673-141">否。</span><span class="sxs-lookup"><span data-stu-id="23673-141">No.</span></span> <span data-ttu-id="23673-142">保留的 IP 僅在區域 VNet 才受支援。</span><span class="sxs-lookup"><span data-stu-id="23673-142">Reserved IPs are only supported in regional VNets.</span></span> <span data-ttu-id="23673-143">與同質群組關聯的 VNet 不支援保留的 IP。</span><span class="sxs-lookup"><span data-stu-id="23673-143">Reserved IPs are not supported for VNets that are associated with affinity groups.</span></span> <span data-ttu-id="23673-144">如需有關如何將 VNet 與區域或同質群組產生關聯的詳細資訊，請參閱 hello[關於區域 Vnet 和同質群組](virtual-networks-migrate-to-regional-vnet.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="23673-144">For more information about associating a VNet with a region or affinity group, see hello [About Regional VNets and Affinity Groups](virtual-networks-migrate-to-regional-vnet.md) article.</span></span>

## <a name="manage-reserved-vips"></a><span data-ttu-id="23673-145">管理保留的 VIP</span><span class="sxs-lookup"><span data-stu-id="23673-145">Manage reserved VIPs</span></span>

<span data-ttu-id="23673-146">請確定您已安裝並設定 PowerShell hello hello 中的步驟，以[安裝和設定 PowerShell](/powershell/azure/overview)發行項。</span><span class="sxs-lookup"><span data-stu-id="23673-146">Ensure you have installed and configured PowerShell by completing hello steps in hello [Install and configure PowerShell](/powershell/azure/overview) article.</span></span> 

<span data-ttu-id="23673-147">您可以使用保留的 Ip，您必須先新增它 tooyour 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="23673-147">Before you can use reserved IPs, you must add it tooyour subscription.</span></span> <span data-ttu-id="23673-148">toocreate hello 公用 IP 集區的保留 IP 位址用於 hello*美國中部*位置，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="23673-148">toocreate a reserved IP from hello pool of public IP addresses available in hello *Central US* location, run hello following command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"
```

<span data-ttu-id="23673-149">但是請注意，您無法指定正在保留的 IP。</span><span class="sxs-lookup"><span data-stu-id="23673-149">Notice, however, that you cannot specify what IP is being reserved.</span></span> <span data-ttu-id="23673-150">tooview 哪些 IP 位址會保留在您訂用帳戶，執行下列 PowerShell 命令的 hello，並注意 hello 值*ReservedIPName*和*位址*:</span><span class="sxs-lookup"><span data-stu-id="23673-150">tooview what IP addresses are reserved in your subscription, run hello following PowerShell command, and notice hello values for *ReservedIPName* and *Address*:</span></span>

```powershell
Get-AzureReservedIP
```

<span data-ttu-id="23673-151">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="23673-151">Expected output:</span></span>

    ReservedIPName       : MyReservedIP
    Address              : 23.101.114.211
    Id                   : d73be9dd-db12-4b5e-98c8-bc62e7c42041
    Label                :
    Location             : Central US
    State                : Created
    InUse                : False
    ServiceName          :
    DeploymentName       :
    OperationDescription : Get-AzureReservedIP
    OperationId          : 55e4f245-82e4-9c66-9bd8-273e815ce30a
    OperationStatus      : Succeeded

>[!NOTE]
><span data-ttu-id="23673-152">當您使用 PowerShell 建立保留的 IP 位址時，您無法指定在資源群組 toocreate hello 保留 IP。</span><span class="sxs-lookup"><span data-stu-id="23673-152">When you create a reserved IP address with PowerShell, you cannot specify a resource group toocreate hello reserved IP in.</span></span> <span data-ttu-id="23673-153">Azure 會自動將它放在名為 *Default-Networking* 的資源群組中。</span><span class="sxs-lookup"><span data-stu-id="23673-153">Azure places it into a resource group named *Default-Networking* automatically.</span></span> <span data-ttu-id="23673-154">如果您建立使用 hello hello 保留 IP [Azure 入口網站](http://portal.azure.com)，您可以指定您選擇的任何資源群組。</span><span class="sxs-lookup"><span data-stu-id="23673-154">If you create hello reserved IP using hello [Azure portal](http://portal.azure.com), you can specify any resource group you choose.</span></span> <span data-ttu-id="23673-155">如果您建立 hello 保留 IP 的資源群組中非*預設網路*不過，每當您參考 hello 保留 IP 與命令例如`Get-AzureReservedIP`和`Remove-AzureReservedIP`，您必須參考 hello 名稱*群組資源群組名稱保留 ip 名稱*。</span><span class="sxs-lookup"><span data-stu-id="23673-155">If you create hello reserved IP in a resource group other than *Default-Networking* however, whenever you reference hello reserved IP with commands such as `Get-AzureReservedIP` and `Remove-AzureReservedIP`, you must reference hello name *Group resource-group-name reserved-ip-name*.</span></span>  <span data-ttu-id="23673-156">例如，如果您建立名為保留的 IP *myreservedip 產生*資源群組中名為*myResourceGroup*，您必須參考 hello hello 保留 IP，當做名稱*群組 myResourceGroupmyreservedip 產生*。</span><span class="sxs-lookup"><span data-stu-id="23673-156">For example, if you create a reserved IP named *myReservedIP* in a resource group named *myResourceGroup*, you must reference hello name of hello reserved IP as *Group myResourceGroup myReservedIP*.</span></span>   

<span data-ttu-id="23673-157">一旦 IP 已保留，直到刪除為止會維持相關聯的 tooyour 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="23673-157">Once an IP is reserved, it remains associated tooyour subscription until you delete it.</span></span> <span data-ttu-id="23673-158">toodelete 保留 IP，執行下列 PowerShell 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="23673-158">toodelete a reserved IP, run hello following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIP -ReservedIPName "MyReservedIP"
```

## <a name="reserve-hello-ip-address-of-an-existing-cloud-service"></a><span data-ttu-id="23673-159">保留現有的雲端服務的 hello IP 位址</span><span class="sxs-lookup"><span data-stu-id="23673-159">Reserve hello IP address of an existing cloud service</span></span>
<span data-ttu-id="23673-160">您可以保留現有的雲端服務的 hello IP 位址加入 hello`-ServiceName`參數。</span><span class="sxs-lookup"><span data-stu-id="23673-160">You can reserve hello IP address of an existing cloud service by adding hello `-ServiceName` parameter.</span></span> <span data-ttu-id="23673-161">雲端服務 tooreserve hello IP 位址*TestService*在 hello*美國中部*位置，執行下列 PowerShell 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="23673-161">tooreserve hello IP address of a cloud service *TestService* in hello *Central US* location, run hello following PowerShell command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US" -ServiceName TestService
```

## <a name="associate-a-reserved-ip-tooa-new-cloud-service"></a><span data-ttu-id="23673-162">關聯保留的 IP tooa 新的雲端服務</span><span class="sxs-lookup"><span data-stu-id="23673-162">Associate a reserved IP tooa new cloud service</span></span>
<span data-ttu-id="23673-163">hello 下列指令碼會建立新的保留 IP，然後將其相關聯 tooa 新的雲端服務名稱為*TestService*。</span><span class="sxs-lookup"><span data-stu-id="23673-163">hello following script creates a new reserved IP, then associates it tooa new cloud service named *TestService*.</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService -ReservedIPName MyReservedIP -Location "Central US"
```

> [!NOTE]
> <span data-ttu-id="23673-164">當您建立保留的 IP toouse 與雲端服務時，您仍然 toohello VM 使用參照*VIP:&lt;連接埠號碼 >*以輸入通訊。</span><span class="sxs-lookup"><span data-stu-id="23673-164">When you create a reserved IP toouse with a cloud service, you still refer toohello VM by using *VIP:&lt;port number>* for inbound communication.</span></span> <span data-ttu-id="23673-165">保留 IP，並不表示您可以直接連接 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="23673-165">Reserving an IP does not mean you can connect toohello VM directly.</span></span> <span data-ttu-id="23673-166">hello 保留的 IP 會被指派 toohello 雲端服務 VM 已部署至該 hello。</span><span class="sxs-lookup"><span data-stu-id="23673-166">hello reserved IP is assigned toohello cloud service that hello VM has been deployed to.</span></span> <span data-ttu-id="23673-167">若要直接 tooconnect tooa VM 的 IP，您有 tooconfigure 執行個體層級公用 IP。</span><span class="sxs-lookup"><span data-stu-id="23673-167">If you want tooconnect tooa VM by IP directly, you have tooconfigure an instance-level public IP.</span></span> <span data-ttu-id="23673-168">執行個體層級公用 IP 是一種公用 IP （稱為 ILPIP），會直接指派 tooyour VM。</span><span class="sxs-lookup"><span data-stu-id="23673-168">An instance-level public IP is a type of public IP (called an ILPIP) that is assigned directly tooyour VM.</span></span> <span data-ttu-id="23673-169">此類型 IP 無法保留。</span><span class="sxs-lookup"><span data-stu-id="23673-169">It cannot be reserved.</span></span> <span data-ttu-id="23673-170">如需詳細資訊，請閱讀 hello[執行個體層級公用 IP (ILPIP)](virtual-networks-instance-level-public-ip.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="23673-170">For more information, read hello [Instance-level Public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) article.</span></span>
> 

## <a name="remove-a-reserved-ip-from-a-running-deployment"></a><span data-ttu-id="23673-171">從執行中部署移除保留的 IP</span><span class="sxs-lookup"><span data-stu-id="23673-171">Remove a reserved IP from a running deployment</span></span>
<span data-ttu-id="23673-172">保留 IP tooremove 加入 tooa 新雲端服務，請執行下列 PowerShell 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="23673-172">tooremove a reserved IP added tooa new cloud service, run hello following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService
```

> [!NOTE]
> <span data-ttu-id="23673-173">從執行中部署移除保留的 IP 並不會從您的訂用帳戶移除 hello 保留項目。</span><span class="sxs-lookup"><span data-stu-id="23673-173">Removing a reserved IP from a running deployment does not remove hello reservation from your subscription.</span></span> <span data-ttu-id="23673-174">它會釋出 hello IP toobe 您訂用帳戶中的另一個資源所使用。</span><span class="sxs-lookup"><span data-stu-id="23673-174">It simply frees hello IP toobe used by another resource in your subscription.</span></span>
> 

## <a name="associate-a-reserved-ip-tooa-running-deployment"></a><span data-ttu-id="23673-175">執行部署的保留的 IP tooa 產生關聯</span><span class="sxs-lookup"><span data-stu-id="23673-175">Associate a reserved IP tooa running deployment</span></span>
<span data-ttu-id="23673-176">hello 下列命令會建立名為雲端服務*TestService2*與名為的新 VM *TestVM2*。</span><span class="sxs-lookup"><span data-stu-id="23673-176">hello following commands create a cloud service named *TestService2* with a new VM named *TestVM2*.</span></span> <span data-ttu-id="23673-177">現有的 hello 保留的 IP 名為*myreservedip 產生*則相關聯的 toohello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="23673-177">hello existing reserved IP named *MyReservedIP* is then associated toohello cloud service.</span></span>

```powershell
$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM2 -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService2 -Location "Central US"

Set-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService2
```

## <a name="associate-a-reserved-ip-tooa-cloud-service-by-using-a-service-configuration-file"></a><span data-ttu-id="23673-178">使用服務組態檔相關聯的保留的 IP tooa 雲端服務</span><span class="sxs-lookup"><span data-stu-id="23673-178">Associate a reserved IP tooa cloud service by using a service configuration file</span></span>
<span data-ttu-id="23673-179">您也可以使用服務組態檔 (CSCFG) 關聯保留的 IP tooa 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="23673-179">You can also associate a reserved IP tooa cloud service by using a service configuration (CSCFG) file.</span></span> <span data-ttu-id="23673-180">hello 下列範例 xml 會說明如何 tooconfigure 保留 VIP 的雲端服務 toouse 命名*myreservedip 產生*:</span><span class="sxs-lookup"><span data-stu-id="23673-180">hello following sample xml shows how tooconfigure a cloud service toouse a reserved VIP named *MyReservedIP*:</span></span>

    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ReservedIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
        <ConfigurationSettings>
          <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
        </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <ReservedIPs>
           <ReservedIP name="MyReservedIP"/>
          </ReservedIPs>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>

## <a name="next-steps"></a><span data-ttu-id="23673-181">後續步驟</span><span class="sxs-lookup"><span data-stu-id="23673-181">Next steps</span></span>
* <span data-ttu-id="23673-182">了解如何[IP 定址](virtual-network-ip-addresses-overview-classic.md)hello 傳統部署模型中的運作方式。</span><span class="sxs-lookup"><span data-stu-id="23673-182">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in hello classic deployment model.</span></span>
* <span data-ttu-id="23673-183">深入了解 [保留的私人 IP 位址](virtual-networks-reserved-private-ip.md)。</span><span class="sxs-lookup"><span data-stu-id="23673-183">Learn about [reserved private IP addresses](virtual-networks-reserved-private-ip.md).</span></span>
* <span data-ttu-id="23673-184">深入了解 [執行個體層級公用 IP (ILPIP) 位址](virtual-networks-instance-level-public-ip.md)。</span><span class="sxs-lookup"><span data-stu-id="23673-184">Learn about [Instance Level Public IP (ILPIP) addresses](virtual-networks-instance-level-public-ip.md).</span></span>

